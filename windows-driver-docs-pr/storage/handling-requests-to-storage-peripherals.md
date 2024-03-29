---
title: 处理对存储外设的请求
description: 处理对存储外设的请求
ms.assetid: 3859588e-fc39-4323-a901-8771874e64d2
keywords:
- 存储类驱动程序 WDK、 外围设备
- 类驱动程序 WDK 存储外围设备
- 外围设备 WDK 存储
- 存储外围设备 WDK
- 外围设备 WDK 存储有关存储外围设备
- 有关存储外围设备存储外围设备 WDK，
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb243e6885b877bd7f77a2b3f217c16760e78a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378470"
---
# <a name="handling-requests-to-storage-peripherals"></a>处理对存储外设的请求


## <span id="ddk_handling_requests_to_storage_peripherals_kg"></span><span id="DDK_HANDLING_REQUESTS_TO_STORAGE_PERIPHERALS_KG"></span>


对于需要通过基础总线执行请求的存储端口驱动程序的所有请求，在类驱动程序必须设置包含 SCSI 请求块 (SRB) 包含 SCSI 命令描述符块 (CDB) IRP。 因此，大多数存储类驱动程序有一个或多内部*BuildRequest*例程，从而生成 Srb。 有关此类例程的详细信息，请参阅[存储类驱动程序 BuildRequest 例程](storage-class-driver-s-buildrequest-routine.md)。

存储类驱动程序还通过上 IRP\_MJ\_SCSI 请求到基础存储端口驱动程序。 此类请求可源于[存储筛选器驱动程序](storage-filter-drivers.md)。

有关[ **IOCTL\_SCSI\_传递\_THROUGH** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_scsi_pass_through)中所述的请求[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)，类驱动程序负责设置**MinorFunction** IRP 的代码\_MJ\_设备\_控件在端口驱动程序的 I/O 堆栈位置，然后再将传递 IRPIRP\_MJ\_设备\_到端口驱动程序和控件请求[ **IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)。

每个存储类驱动程序负责拆分传输请求 (IRP\_MJ\_读取和/或 IRP\_MJ\_编写)，超出基础 HBA 的功能。 因此，大多数类驱动程序还调用内部*SplitTransferRequest*例程中所述[存储类驱动程序 SplitTransferRequest 例程](storage-class-driver-s-splittransferrequest-routine.md)，或实现中的相同功能为其调度例程读取和写入请求。

有关处理与存储外围设备的请求的其他信息，请参阅以下主题：

[处理 SCSI 传递请求](handling-scsi-pass-through-requests.md)

[处理与存储外围设备的即插即用请求](handling-pnp-requests-to-storage-peripherals.md)

[处理与存储外围设备的 Power 请求](handling-power-requests-to-storage-peripherals.md)

[队列存储请求](queuing-storage-requests.md)

 

 




