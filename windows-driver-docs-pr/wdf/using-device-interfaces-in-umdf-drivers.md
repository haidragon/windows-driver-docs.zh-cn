---
title: 在 UMDF 驱动程序中使用设备接口
description: 在 UMDF 驱动程序中使用设备接口
ms.assetid: acb6da80-bd04-48f0-b42a-96463f091b0a
keywords:
- 用户模式驱动程序 WDK UMDF，设备接口
- UMDF WDK、 设备接口
- 用户模式驱动程序框架 WDK，设备接口
- 设备接口 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6c8695e09c548b168af7bb8b2d084f5c6eb4995
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372280"
---
# <a name="using-device-interfaces-in-umdf-drivers"></a>在 UMDF 驱动程序中使用设备接口


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一个*设备接口*是符号链接 (PnP) 插到应用程序可用于访问设备的设备。 在用户模式应用程序可以将接口的符号链接名称传递给 API 元素，如 Microsoft Win32 [ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)函数。 若要获取设备接口的符号链接名称，用户模式应用程序可以调用**SetupDi**函数。 有关 SetupDi 函数的详细信息，请参阅 SetupDi 设备接口函数。

每个设备接口属于*设备接口类*。 例如，CD-ROM 设备驱动程序堆栈可能会提供一个接口，属于 GUID\_DEVINTERFACE\_CDROM 类。 其中一个光盘设备驱动程序将注册实例的 guid\_DEVINTERFACE\_CDROM 类，以通知系统和应用程序的 CD-ROM 设备已可用。 有关设备接口类的详细信息，请参阅[简介设备接口](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-device-interface-classes)。

### <a name="registering-a-device-interface"></a>注册设备接口

若要注册设备接口类的实例，基于 UMDF 驱动程序可以调用[ **IWDFDevice::CreateDeviceInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createdeviceinterface)中其[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数。 如果该驱动程序支持的接口的多个实例，它可以为每个实例分配的唯一引用字符串。

### <a name="enabling-and-disabling-a-device-interface"></a>启用和禁用设备接口

如果创建成功，则框架将自动启用和禁用基于设备的即插即用状态的接口。

此外，驱动程序可以禁用和重新启用一个根据需要在设备接口。 例如，如果驱动程序确定其设备已停止响应，该驱动程序可以调用[ **IWDFDevice::AssignDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-assigndeviceinterfacestate)禁用设备的接口和禁止获取对接口的新句柄的应用程序。 （不影响现有的句柄的接口。）如果设备更高版本可用时，该驱动程序可以调用**IWDFDevice::AssignDeviceInterfaceState**再次以重新启用接口。

### <a name="receiving-requests-to-access-a-device-interface"></a>接收的请求来访问设备接口

应用程序请求对驱动程序的设备接口的访问，框架将调用的驱动程序[ **IQueueCallbackCreate::OnCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)回调函数。 该驱动程序可以调用[ **IWDFFile::RetrieveFileName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdffile-retrievefilename)若要获取的设备或应用程序正在访问的文件的名称。 如果该驱动程序指定引用字符串，它注册的设备接口时，操作系统在文件中包含的引用字符串或设备名称**IWDFFile::RetrieveFileName**返回。

### <a name="creating-device-events"></a>创建设备事件

基于 UMDF 驱动程序可以创建特定于设备的自定义事件 (称为*设备事件*) 通过调用[ **IWDFDevice::PostEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-postevent)。 已注册为使用任何设备的接口的驱动程序可以接收通知的设备的自定义事件。 基于 UMDF 驱动程序通过提供接收此类通知[ **IRemoteInterfaceCallbackEvent::OnRemoteInterfaceEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)回调函数。

自定义事件是唯一的设备。 创建事件驱动程序的开发人员和接收事件的驱动程序的开发人员必须了解事件的含义。

### <a name="accessing-another-drivers-device-interface"></a>访问另一个驱动程序的设备接口

如果您希望基于 UMDF 驱动程序以将 I/O 请求发送到设备接口提供了该另一个驱动程序，可以创建[远程 I/O 目标](general-i-o-targets-in-umdf.md)，表示设备接口。

首先，必须注册您的驱动程序设备接口可用时接收通知。 请使用以下步骤：

1.  当您的驱动程序调用[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)，该驱动程序可以提供[IPnpCallbackRemoteInterfaceNotification](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackremoteinterfacenotification)接口。 [ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)设备接口不可用时，此接口的回调函数将通知您的驱动程序。

2.  后驱动程序调用[ **IWDFDriver::CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)，它可以调用[ **IWDFDevice2::RegisterRemoteInterfaceNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-registerremoteinterfacenotification)为驱动程序将使用每个设备接口。

随后，框架将调用的驱动程序[ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数指定的设备接口将成为每个时间可用。 回调函数可以调用[ **IWDFRemoteInterfaceInitialize::GetInterfaceGuid** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-getinterfaceguid)并[ **IWDFRemoteInterfaceInitialize::RetrieveSymbolicLink**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremoteinterfaceinitialize-retrievesymboliclink)来确定哪些设备接口已到达。

您的驱动程序[ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数通常应执行以下操作：

1.  调用[ **IWDFDevice2::CreateRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-createremoteinterface)来创建远程接口对象，（可选） 提供[IRemoteInterfaceCallbackEvent](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackevent)和[IRemoteInterfaceCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremoteinterfacecallbackremoval)接口。

2.  调用[ **IWDFDevice2::CreateRemoteTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)若要创建一个远程目标对象，（可选） 提供[IRemoteTargetCallbackRemoval](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iremotetargetcallbackremoval)接口。

3.  调用[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface)连接到远程目标的设备接口。

    如果一个 SWENUM 软件设备枚举器创建的设备接口，您的驱动程序必须调用**OpenRemoteInterface**从工作项。 (有关示例，请参阅**QueueUserWorkItem** Windows SDK 中的函数。)

现在该驱动程序可以设置的格式并将 I/O 请求发送到远程的 I/O 目标。

除了[ **IPnpCallbackRemoteInterfaceNotification::OnRemoteInterfaceArrival** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackremoteinterfacenotification-onremoteinterfacearrival)回调函数，基于 UMDF 驱动程序可提供两个其他回调函数来接收设备接口事件的通知：

-   [ **IRemoteInterfaceCallbackRemoval::OnRemoteInterfaceRemoval** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremoteinterfacecallbackremoval-onremoteinterfaceremoval)回调函数时删除设备接口通知驱动程序。

-   [ **IRemoteInterfaceCallbackEvent::OnRemoteInterfaceEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iremoteinterfacecallbackevent-onremoteinterfaceevent)设备的自定义事件到达时将回调函数通知驱动程序。

 

 





