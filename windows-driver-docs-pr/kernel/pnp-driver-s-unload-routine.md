---
title: PnP 驱动程序的 Unload 例程
description: PnP 驱动程序的 Unload 例程
ms.assetid: 71b30a84-d3c7-4674-94a6-b99f83567183
keywords:
- 卸载例程 WDK 内核、 PnP 驱动程序
- PnP 卸载例程 WDK 内核
- 即插即用卸载例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcc8430d2035ba3320e72a69a31738e8d8997782
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369728"
---
# <a name="pnp-drivers-unload-routine"></a>PnP 驱动程序的 Unload 例程





即插即用驱动程序必须具有[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)删除任何特定于驱动程序的资源，例如内存、 线程和事件，创建的例程[ **DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 如果没有要删除的特定于驱动程序的资源，该驱动程序仍然必须具有*Unload*例程，但它可以只返回。

驱动程序的*Unload*后已删除的驱动程序的所有设备随时可以调用例程。 PnP 管理器中调用的驱动程序*Unload*例程的 IRQL 在系统线程上下文中 = 被动\_级别。

即插即用驱动程序释放特定于设备的资源和 PnP 设备删除 Irp 响应中的设备对象。 PnP 管理器将发送这些 Irp 代表每个使用它枚举以及任何根枚举旧设备驱动程序的即插即用设备报告[ **IoReportDetectedDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioreportdetecteddevice)。

因此， *Unload*例程的即插即用驱动程序是通常简单，通常只包含**返回**语句。 但是，如果驱动程序分配中的任何驱动程序范围资源及其**DriverEntry**例程，必须释放这些资源在其*卸载*例程，除非它还执行该操作。 一般情况下，卸载即插即用驱动程序的过程是一项同步操作。

I/O 管理器释放驱动程序对象和使用该驱动程序分配任何驱动程序对象扩展[ **IoAllocateDriverObjectExtension**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatedriverobjectextension)。

 

 




