---
title: 扩展的相机控制
description: 扩展控件使用 KSPROPERTY 机制向应用程序公开相机控件。
ms.assetid: B480C007-7DCA-4CFB-9169-BE2D0B2D2137
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41705876d0bcd6f910a54f9f1cd7443a40dbab7
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565599"
---
# <a name="extended-camera-controls"></a>扩展的相机控制

扩展控件使用**KSPROPERTY**机制向应用程序公开相机控件。

以下标准化扩展控件列表 (由媒体基础定义) 启用其他 Windows 相机功能:

- [新元](#metadata)
- [焦点优先级](#focus-priority)
- [焦点状态](#focus-state)
- [感兴趣的扩展区域 (ROI)](#extended-region-of-interest-roi)
- [照片确认](#photo-confirmation)
- [照片序列 submode](#photo-sequence-submode)
- [EXIF 和 HW JPEG 编码器](#exif-and-hw-jpeg-encoder)
- [整数 ISO](#integer-iso)
- [高级焦点](#advanced-focus)
- [写](#flash)
- [Zoom](#zoom)
- [场景模式](#scene-mode)

某些控件作为异步控件向应用程序公开, 其他控件作为同步控件公开。

## <a name="synchronous-controls"></a>同步控件

对于这些控件, 捕获管道发出**KSPROPERTY**相机控制结构, 并期望驱动程序以同步方式返回请求。

## <a name="asynchronous-controls"></a>异步控件

对于这些控件, 捕获管道会发出**KSPROPERTY**, 使**KSEVENT**与该属性相关联, 并等待事件发出信号。 驱动程序必须同步完成**KSPROPERTY** , 并使用它作为触发器来启动异步操作。 异步操作完成后, 驱动程序必须向关联的**KSEVENT** (捕获管道正在等待) 发出信号。 捕获管道在收到信号时通知应用程序完成操作。

如果异步控件可以取消, 则必须在控件中指定**KSCAMERA\_EXTENDEDPROP\_标志\_CANCELOPERATION**标志。 如果无法取消控件, 则控件的操作不得超过5毫秒。

这些扩展控件是 ksmedia 中定义的以下 KS 属性集的一部分:

```cpp
#define STATIC_KSPROPERTYSETID_ExtendedCameraControl \
     0x1CB79112, 0xC0D2, 0x4213, 0x9C, 0xA6, 0xCD, 0x4F, 0xDB, 0x92, 0x79, 0x72
DEFINE_GUIDSTRUCT("1CB79112-C0D2-4213-9CA6-CD4FDB927972", KSPROPERTYSETID_ExtendedCameraControl);
#define KSPROPERTYSETID_ExtendedCameraControl DEFINE_GUIDNAMED(KSPROPERTYSETID_ExtendedCameraControl);
```

## <a name="metadata"></a>元数据

若要检索元数据, 用户模式组件 (DevProxy) 必须查询驱动程序的元数据缓冲要求。 用户模式组件提供此信息后, 它将为驱动程序分配适当的元数据缓冲区, 以填充并返回到用户模式组件。

[ **\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-metadata) [**KSPROPERTYCAMERACONTROL\_扩展属性中定义的 KSPROPERTY CAMERACONTROL 扩展元数据属性ID\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_cameracontrol_extended_property)客户端使用枚举来查询元数据缓冲区要求, 例如所需的元数据大小、内存对齐要求和所需的内存分配类型。

用户模式组件从驱动程序获取了元数据缓冲区要求后, 它会分配适当大小的元数据缓冲区, 并将所需的内存与所需的内存池对齐。 此元数据缓冲区与实际框架缓冲区一起发送到驱动程序以完成, 然后在填充时返回给用户模式组件。 对于 multishot 方案, 会为每个分配的帧缓冲区分配相应的元数据缓冲区, 并将其传递给照相机驱动程序。

[**KSSTREAM\_元数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_metadata_info)结构与以下标志一起用于将元数据缓冲区发送给驱动程序。

```cpp
#define KSSTREAM_HEADER_OPTIONSF_METADATA           0x00001000
```

一旦将缓冲区 (元数据 + 帧) 排队给驱动程序, DevProxy 就会发送一个标准[ **\_KSSTREAM 标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构, 后跟一个[**KS\_帧\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagks_frame_info)结构, 然后接**KSSTREAM\_元数据\_信息**结构。 DevProxy 将进一步屏蔽**KSSTREAM\_标头。** 在将缓冲区向下传递到驱动程序之前, OptionFlags 具有**KSSTREAM\_标头\_\_OPTIONSF 元数据**。

如果该驱动程序不支持元数据, 或者未实现 **\_KSPROPERTY\_CAMERACONTROL\_扩展元数据**, 则**KSPROPERTY\_CAMERACONTROL\_扩展\_METADATA**属性控件将失败。 在这种情况下, DevProxy 将不会分配元数据缓冲区, 并且从 DevProxy 向下传递到驱动程序的负载将**不\_包含\_KSSTREAM 元数据信息**结构。

如果驱动程序支持元数据, 且客户端不需要任何元数据, 则在将缓冲区发送到驱动程序时, DevProxy 将不会分配元数据缓冲区, 也不会传递**KSSTREAM\_元数据\_信息**。 如果应用程序不希望在给定的 pin 上使用元数据, 则此行为会减少不必要的元数据内存分配。

下面的结构描述了要由照相机驱动程序在元数据缓冲区中填充的元数据项的布局。

- [**KSCAMERA\_MetadataId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-kscamera_metadataid)
- [**KSCAMERA\_元\_数据 ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- [**KSCAMERA\_元\_数据 PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

下面的列表包含元数据项的布局。 这必须是8字节对齐的。

- [**KSCAMERA\_元\_数据 ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)
- 元数据

照片确认元数据由**MetadataId\_PhotoConfirmation**标识。 如果存在, 则表示与照片确认框架相关联。 照片确认元数据由 DevProxy 进行分析。

自定义元数据由**MetadataId\_自\_定义开始**的**MetadataId**标识。 自定义元数据项可以包含元数据的 blob, 这些元数据可以是针对预览 pin、EXIF 和/或图像 pin 的 OEM 元数据检测到的焦点状态和/或面部。 自定义 blob 的准确格式由实施驱动程序和 MFT0 的 OEM 决定。 MFT0 负责分析自定义 blob 并将每个元数据项附加为按**MFSampleExtension\_CaptureMetadata**特性包分组的属性, 该属性可由 MF 捕获管道和/或 WinRT 读取。

以下 IMFAttributes 是在**mfapi**中定义的。 它们是 MF 捕获管道和/或 WinRT 所必需的。 请注意, MFT0 不会为照片确认设置任何 IMFAttributes, 因为照片确认框架不会流过 DevProxy。

| Attribute (GUID)                            | 数据类型 |
|---------------------------------------------|-----------|
| **MF\_捕获\_元数据\_FOCUSSTATE**       | UINT32    |
| **MF\_捕获\_元数据\_FACEROIS**         | Blob      |
| **MF\_捕获\_元数据\_帧RAWSTREAM\_** | IUnknown  |

**MF\_捕获元\_数据\_帧RAWSTREAMIMFAttributes创建并附加到DevProxy的MFSampleExtensionCaptureMetadata,其中包含\_** **\_** 指向与原始元数据缓冲区 (**KSSTREAM\_元数据\_信息) 关联的 IMFMediaBuffer 接口的指针。数据**)。

当 MFT0 收到 IMFSample 时, 它将从**MF\_捕获\_\_元数据帧\_** 获取原始元数据缓冲区 RAWSTREAM 并分析任何其他自定义元数据项 (如焦点状态) 和将它们转换为上面定义的相应 IMFAttributes, 并将其附加到**MFSampleExtension\_CaptureMetadata**特性包。
以下 IMFAttributes 必须由 MF 管道和任何第三方提供的 MFTs 执行:

| 名称                                           | 类型                          |
|------------------------------------------------|-------------------------------|
| **MFSampleExtension\_CaptureMetadata**         | **IUnknown**(IMFAttributes)  |
| **MFSampleExtension\_EOS**                     | **UINT32**变量          |
| **MFSampleExtension\_PhotoThumbnail**          | **IUnknown**(IMFMediaBuffer) |
| **MFSampleExtension\_PhotoThumbnailMediaType** | **IUnknown**(IMFMediaType)   |

若要访问原始元数据缓冲区, MFT0 执行以下操作:

1. 从 IMFSample 接口**调用\_MFSampleExtension CaptureMetadata**上的**GetUnknown** , 以获取特性包的 IMFAttributes 接口。
2. 从上一步获取的 IMFAttributes 接口调用**MF\_捕获\_元数据\_\_帧 RAWSTREAM**上的**GetUnknown** , 以获取 IMFMediaBuffer 接口。
3. 调用锁定以获取与 IMFMediaBuffer 关联的原始元数据缓冲区。

若要将所需的 IMFAttributes 添加到**MFSampleExtension\_CaptureMetadata**特性包, MFT0 执行以下操作:

1. 从 IMFSample 接口**调用\_MFSampleExtension CaptureMetadata**上的**GetUnknown** , 以获取特性包的 IMFAttributes 接口。
2. 在MF **\_\_上调用 SetUINT32、SetBlob 或 SetUnknown 基于指定的 GUID 和数据类型从上一步获取的 IMFAttributes 接口捕获元数据\_** 在上表中。

### <a name="mandatory-metadata-attributes"></a>必需的元数据属性

可用的元数据属性的完整列表可在[捕获统计信息元数据属性](mf-capture-metadata.md)

## <a name="focus-priority"></a>焦点优先级

[**KSPROPERTY\_CAMERACONTROL\_EXTENDEDFOCUSPRIORITY属性ID是与焦点优先级DDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focuspriority)

## <a name="focus-state"></a>焦点状态

[**KSPROPERTY\_CAMERACONTROL\_扩展FOCUSSTATE属性ID是与焦点状态DDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusstate)

## <a name="extended-region-of-interest-roi"></a>扩展的兴趣投资回报区域

以下属性 Id 是与 ROI DDI 关联的控件:

- [**KSPROPERTY\_CAMERACONTROL\_扩展投资\_回报CONFIGCAPS\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-configcaps)

- [**KSPROPERTY\_CAMERACONTROL\_扩展投资\_回报ISPCONTROL\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-roi-ispcontrol)

## <a name="photo-confirmation"></a>照片确认

[**KSPROPERTY\_CAMERACONTROL\_扩展PHOTOCONFIRMATION属性ID是与照片确认DDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photoconfirmation)

## <a name="photo-sequence-submode"></a>照片序列 submode

[**KSPROPERTY\_CAMERACONTROL\_EXTENDEDPHOTOMODE属性ID是与照片序列DDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-photomode)

## <a name="exif-and-hw-jpeg-encoder"></a>EXIF 和 HW JPEG 编码器

管道不需要处理或弯曲 HW JPEG 编码器的任何 EXIF 数据;因此, EXIF 数据格式由驱动程序、MFT0 和 OEM 硬件 JPEG 编码器提供。 Oem 合作伙伴可以为 EXIF 属性定义任何自定义属性 GUID 和变体类型, 并将其附加到**MFSampleExtension\_CaptureMetaData**属性包, 供 OEM 组件使用。 如果 HW jpeg 编码器可用, 管道照片接收器组件将加载 hw jpeg 编码器, 并将**MFSampleExtension\_CaptureMetaData**属性包中包含的 exif 数据设置为使用的 exif 编码器选项[IPropertyBag2:: Write](https://go.microsoft.com/fwlink/?LinkId=331589)方法。

编码器选项属性包包含指定可用编码选项属性的 PROPBAG2 结构的数组。 设置到 HW JPEG 编码器的 EXIF 编码器选项由编码器选项属性包中的以下属性标识:

| 属性名      | VARTYPE         | ReplTest1                                                                                                                                                       | 适用的编解码器 |
|--------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|
| **SampleMetaData** | **VT\_未知** | 指向**MFSampleExtension\_CaptureMetaData**特性包的 IMFAttributes 接口的指针, 该接口包含包含 EXIF 数据的 OEM 子属性。 | JPEG              |

**MFSampleExtension\_CaptureMetaData**属性包只能包含任何 OEM 定义的 EXIF 子属性, MFT0 和 HW JPEG 编码器都可以读取它来容纳 EXIF 数据。 若要将 EXIF 数据从驱动程序传递到 HW JPEG 编码器, 驱动程序和 MFT0 必须执行以下操作:

1. 驱动程序在管道提供的元数据缓冲区中提供自定义 EXIF 元数据。 当示例返回到**MFSampleExtension\_** 时, 它**作为\_MF\_捕获\_元\_数据帧 RAWSTREAM** IMFAttribute 附加到 CaptureMetadataDevProxy.

2. 当 MFT0 收到 IMFSample 时, 它将从**MF\_捕获\_元\_数据帧\_** 获取原始元数据缓冲区 RAWSTREAM 并分析自定义 EXIF 元数据项, 并将其转换为 OEM 定义的IMFAttribute 并将其附加到**MFSampleExtension\_CaptureMetadata**特性包。

若要将 EXIF 数据从 MFT0 传递到 HW JPEG 编码器, 管道照片接收器会执行以下操作:

1. 从 IMFSample 调用**MFSampleExtension\_CaptureMetadata**上的**GetUnknown** , 以获取 IMFAttributes 接收时属性包的 IMFSample 接口。

2. 调用[IPropertyBag2:: Write](https://go.microsoft.com/fwlink/?LinkId=331589)将编码器选项属性 (由 SampleMetadata 标识) 设置为 HW JPEG 编码器。 编码器选项属性包含从上一步获得的 IMFAttributes 接口。 此接口包含所有自定义子属性, 包括 OEM EXIF 子属性, 以及本主题前面讨论的**元数据**部分中的标准化子属性。

若要检索用于进一步处理的 EXIF 数据, HW JPEG 编码器执行以下操作:

1. 调用**IPropertyBag2:: Read**以检索由 SampleMetadata 属性名称和 **\_VT 未知**类型标识的属性的属性值。 返回后, **punkVal**将接收**MFSampleExtension\_CaptureMetadata**的 IMFAttributes 接口。

2. 从上一步获取的接口调用 OEM EXIF 子属性上的**GetBlob**或**GetUnknown** , 以根据 OEM EXIF 子属性的 GUID 和数据类型获取 EXIF 数据 blob。

## <a name="thumbnail"></a>缩略图

MFT0 不需要为相机驱动程序生成任何缩略图。 照相机应用程序应生成其自己的缩略图。 可以通过照片确认图像、HW JPEG 编码器或调整大小大小的图像来生成缩略图。 这取决于应用程序开发人员。 为了保持 API 和应用与 Windows 8.1 应用的兼容性, 照相机驱动程序不得实现**KSPROPERTY\_CAMERACONTROL\_扩展\_PHOTOTHUMBNAIL**控件。

## <a name="integer-iso"></a>整数 ISO

[**KSPROPERTY\_CAMERACONTROLEXTENDED\_iso高级\_属性 ID 是与整数 ISO DDI 关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-iso-advanced)

## <a name="advanced-focus"></a>高级焦点

[**KSPROPERTY\_CAMERACONTROL\_EXTENDEDFOCUSMODE属性ID是与整数ISODDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-focusmode)

## <a name="flash"></a>Flash

[**KSPROPERTY\_CAMERACONTROL\_EXTENDEDFLASHMODE属性ID是与flashDDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-flashmode)

## <a name="zoom"></a>Zoom

[**KSPROPERTY\_CAMERACONTROL\_扩展缩放属性ID是与缩放DDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-zoom)

## <a name="scene-mode"></a>场景模式

[**KSPROPERTY\_CAMERACONTROL\_EXTENDEDSCENEMODE属性ID是与场景模式DDI关联的唯一控件。\_** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-cameracontrol-extended-scenemode)
