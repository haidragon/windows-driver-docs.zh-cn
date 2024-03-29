---
title: 处理存储类驱动程序中的 PnP 启动
description: 处理存储类驱动程序中的 PnP 启动
ms.assetid: 8d4ccd09-c5d2-4c9b-b94d-e22c916f0043
keywords:
- 存储类驱动程序 WDK，即插即用
- 类驱动程序 WDK 存储，即插即用
- 即插即用 WDK 存储
- 插 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbaedafacfcdfe970cee4bf83554126327ee723f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378500"
---
# <a name="handling-pnp-start-in-a-storage-class-driver"></a>处理存储类驱动程序中的 PnP 启动


## <span id="ddk_handling_pnp_start_in_a_storage_class_driver_kg"></span><span id="DDK_HANDLING_PNP_START_IN_A_STORAGE_CLASS_DRIVER_KG"></span>


存储类驱动程序 PnP 管理器调用的类驱动程序时执行特定于设备的初始化[ **DispatchPnP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程替换一个开始请求 (IRP\_MJ\_PNP与[ **IRP\_MN\_启动\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device))。 存储类驱动程序*DispatchPnP*日常操作会调用内部*StartDevice*例程或实现相同功能内联。 因为开始请求发送到 FDO 必须首先由处理堆栈中的最低驱动程序存储类驱动程序*DispatchPnP*例程将请求转发到下一步低驱动程序和[ **IoCallDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)之前，调用*StartDevice*。 如果该请求发送到 PDO，驱动程序不需要将请求转发前请先。

存储类驱动程序的内部*StartDevice*例程将设置其 FDO 驱动程序确定数据的设备扩展来管理设备的 I/O 请求。 有关详细信息，请参阅[设置了存储类驱动程序的设备扩展](setting-up-a-storage-class-driver-s-device-extension.md)。

一个*StartDevice*例程应启用驱动程序中注册任何设备接口及其*AddDevice*例程。 (请参阅[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)。)它还可能会创建其设备对象的符号链接。

较低的设备启动完成后，该驱动程序可以假定设备正处于 D0 电源状态 （完全在和操作），在大多数情况。 如果设备未完全启动后，端口驱动程序将排队的请求，直到设备已准备就绪。 但是，如果驱动程序的*StartDevice*例程需要执行任何操作需要涌流-例如，可以加快磁盘驱动器-驱动程序之前必须发送 D0 power 请求到下一步低驱动程序执行操作。

文件类型的设备的驱动程序\_设备\_磁盘或文件\_设备\_批量\_存储可以注册空闲检测并通过指定的设备类使用标准的电源策略超时节省和性能超时值为-1 中其**PoRegisterDeviceforIdleDetection**调用。

有关存储类驱动程序的详细信息*DispatchPnP*例程，请参阅[处理与存储外围设备的即插即用请求](handling-pnp-requests-to-storage-peripherals.md)。 有关处理即插即用启动请求的详细信息，请参阅[启动设备](https://docs.microsoft.com/windows-hardware/drivers/kernel/starting-a-device)。

 

 




