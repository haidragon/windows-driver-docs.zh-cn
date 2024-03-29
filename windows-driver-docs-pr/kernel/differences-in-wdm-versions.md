---
title: WDM 版本的差异
description: WDM 版本的差异
ms.assetid: 735b01c4-4eff-4c8e-ab60-3813d1830112
keywords:
- WDM 驱动程序 WDK 内核版本
- 版本 WDK WDM
- WDK WDM 的兼容性
- 跨系统的兼容性 WDK WDM
- Plug and Play WDK WDM
- 驱动程序支持例程 WDK WDM
- 电源管理 WDK WDM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635e8d7ba624f981ac6c90004d1f3e03ccd28781
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384997"
---
# <a name="differences-in-wdm-versions"></a>WDM 版本的差异





若要确保跨系统的兼容性的最简单方法是编写使用仅限 WDM 编号最低的版本都支持的功能的驱动程序。 但是，这并不总是可能。 有时，驱动程序需要额外的代码以利用的 WDM，更高版本中提供的功能或补偿的 Windows 操作系统之间的差异。

### <a name="wdm-differences-in-driver-support-routines"></a>WDM 驱动程序支持例程的差异

每个 Windows Driver Kit (WDK) 参考页[驱动程序支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)指示如果例程限制为特定版本的 WDM，或其行为是在不同的操作系统版本不同。 在使用之前驱动程序支持的任何例程中的跨系统驱动程序，请务必了解任何特定于版本的限制或行为。

### <a name="wdm-differences-in-plug-and-play"></a>Plug and Play WDM 差异

仅在 Windows 2000 和更高版本的基于 NT 的操作系统 （WDM 版本 1.10 及更高版本） 支持以下插 I/O 请求数据包 (IRP):

[**IRP\_MN\_SURPRISE\_REMOVAL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-surprise-removal)

此外，以下 Irp 工作方式在 Windows 98 上 / 我如何从它们在基于 NT 的操作系统上工作：

[**IRP\_MN\_停止\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)并[ **IRP\_MN\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-remove-device)

[**IRP\_MN\_查询\_删除\_设备**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)

### <a name="wdm-differences-in-power-management"></a>中电源管理的 WDM 差异

以下的电源管理功能和输入/输出请求不同操作之间 Windows 98 中 / 我操作系统和基于 NT 的操作系统：

[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-porequestpowerirp)

[**PoRegisterDeviceForIdleDetection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregisterdeviceforidledetection)

[**IRP\_MN\_查询\_电源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power)

[**IRP\_MN\_SET\_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)

完成 power Irp，Windows 98 上的驱动程序时 / 我必须完成 power Irp 在 IRQL = 被动\_级别，而在基于 NT 的操作系统上的驱动程序可以完成此类 Irp 在 IRQL = 被动\_级别或 IRQL = 调度\_级别。

DO\_电源\_PAGABLE 标志中[**设备\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object) Windows 98 上以不同的方式使用结构 / 我比在基于 NT 的操作系统操作系统。

### <a name="wdm-differences-in-kernel-mode-driver-operation"></a>在内核模式驱动程序操作中的 WDM 差异

Windows 98 的内核模式 WDM 驱动程序 / 我必须遵循特定的准则使用浮点运算，MMX，3DNOW ！，或 Intel 的 SSE 扩展。 有关详细信息，请参阅[使用浮点或 WDM 驱动程序中的 MMX](using-floating-point-or-mmx-in-a-wdm-driver.md)。

Windows 98 / 我提供了固定的数量的可能不适合某些驱动程序的工作线程。

 

 




