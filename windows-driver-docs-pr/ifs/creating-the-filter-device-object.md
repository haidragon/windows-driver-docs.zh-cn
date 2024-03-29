---
title: 创建筛选器设备对象
description: 创建筛选器设备对象
ms.assetid: aca9a2ba-8630-4eb3-9312-a0c6454c3e44
keywords:
- 筛选器驱动程序 WDK 文件系统，将附加筛选器
- 文件系统筛选器驱动程序 WDK，附加筛选器
- 附加到文件系统卷的筛选器
- WDK 卷文件系统，将附加筛选器
- IoCreateDevice
- 筛选器 DOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1bd6111b0c9f9b85f0573c8c233c78fd0c8d6f1d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366793"
---
# <a name="creating-the-filter-device-object"></a>创建筛选器设备对象


## <span id="ddk_creating_the_filter_device_object_if"></span><span id="DDK_CREATING_THE_FILTER_DEVICE_OBJECT_IF"></span>


调用[ **IoCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)创建筛选器设备对象附加到卷或文件系统堆栈，如以下示例所示：

```cpp
status = IoCreateDevice(
          gFileSpyDriverObject,                     //DriverObject
          sizeof(MYLEGACYFILTER_DEVICE_EXTENSION),  //DeviceExtensionSize
          NULL,                                     //DeviceName
          DeviceObject->DeviceType,                 //DeviceType
          0,                                        //DeviceCharacteristics
          FALSE,                                    //Exclusive
          &newDeviceObject);                        //DeviceObject
```

在上面的代码段*DeviceObject*是指向目标设备对象将附加筛选设备对象到;*newDeviceObject*是指向筛选设备对象本身。

设置*DeviceExtensionSize*参数**sizeof**(MYLEGACYFILTER\_设备\_扩展) 将导致 MYLEGACYFILTER\_设备\_扩展结构，并将其分配的筛选器设备对象。 新创建的筛选器设备对象的**DeviceExtension**成员设置为指向此结构。 文件系统筛选器驱动程序通常定义，并为每个筛选器设备对象的设备扩展分配内存。 结构和设备扩展的内容特定于驱动程序。 但是，Microsoft Windows XP 及更高版本，筛选器驱动程序应定义设备\_的筛选器驱动程序对象的扩展结构，它至少包含以下成员：

```cpp
PDEVICE_OBJECT AttachedToDeviceObject;
```

在上述调用到[ **IoCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocreatedevice)，并设置*DeviceName*参数**NULL**指定筛选设备对象将未命名。 筛选设备对象永远不会被命名为。 由于筛选设备对象附加到文件系统卷或卷驱动程序堆栈，为筛选设备对象分配名称会创建系统安全漏洞。

*DeviceType*参数必须始终设置为 （文件系统或筛选器） 的目标设备对象的筛选器设备对象附加到的设备类型相同。 请务必传播这样一来，设备类型，因为它用在 I/O 管理器，报告返回给应用程序。

**请注意**  的文件系统和文件系统筛选器驱动程序应永远不会设置*DeviceType*文件的参数\_设备\_文件\_系统。 这不是此参数的有效值。 (该文件\_设备\_文件\_系统常量仅供在定义 FSCTL 代码中使用。)

 

另一个原因为何*DeviceType*参数十分重要是多的筛选器附加到特定类型的文件系统。 例如，特定筛选器可能会附加到所有本地磁盘文件系统，但不适用于 CD-ROM 的文件系统或远程文件系统。 此类筛选器通过检查文件系统卷或卷驱动程序堆栈中的最顶层的设备对象的设备类型确定文件系统的类型。 在大多数情况下，堆栈中的最顶层的设备对象是筛选设备对象。 因此，它是基本附加的筛选器设备的所有对象都具有相同的设备类型的基础文件系统卷或卷设备对象。

 

 




