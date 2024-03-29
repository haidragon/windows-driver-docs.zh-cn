---
title: DispatchSystemControl 例程
description: DispatchSystemControl 例程
ms.assetid: b885a4a3-a9b6-423c-83bb-ee502724b0d0
keywords:
- 调度例程 WDK 内核，DispatchSystemControl 例程
- 系统控制调度例程 WDK 内核
- IRP_MJ_SYSTEM_CONTROL I/O 函数代码
- DispatchSystemControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e59815ff2b921e6eb350415632549757b73561
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384972"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl 例程





驱动程序的[ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程处理的 Irp [ **IRP\_MJ\_系统\_控件** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control) I/O 函数代码。

所有驱动程序必须提供*DispatchSystemControl*例程。 此例程旨在提供支持 Windows Management Instrumentation (WMI)。 无论是否驱动程序支持 WMI，此例程必须将 IRP 传递给下一个较低驱动程序。

若要了解如何实现*DispatchSystemControl*例程，以及如何在一般情况下支持 WMI，请参阅[Windows Management Instrumentation](implementing-wmi.md)。

 

 




