---
title: 使用通过电源管理的 I/O 队列
description: 使用通过电源管理的 I/O 队列
ms.assetid: 271d55ef-d82e-4ffd-bf41-a602c42c3f0e
keywords:
- I/O 队列 WDK KMDF，电源管理
- 电源管理的 I/O 队列 WDK KMDF
- 重新排队参数 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98f39c2816bd8e50a77e6292ea8e7d0c4f162c66
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372223"
---
# <a name="using-power-managed-io-queues"></a>使用通过电源管理的 I/O 队列


当驱动程序创建的 I/O 队列时，可以指定队列是否*电源管理*。 电源管理队列中可用的 I/O 请求时，框架提供给驱动程序请求的仅当设备处于其工作 (D0) 状态。 框架不允许设备之前该框架已从电源管理队列传递到驱动程序的所有 I/O 请求已完成、 取消或推迟，将保留其工作状态。

有关电源管理 I/O 队列的详细信息，请参阅[I/O 队列的电源管理](power-management-for-i-o-queues.md)。

## <a name="callback-functions-for-power-managed-queues"></a>Power-Managed 队列的回调函数


如果您的驱动程序使用电源管理的 I/O 队列，它可以提供两个其他回调函数：

<a href="" id="---------evtiostop"></a>[*EvtIoStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)  
[ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)回调函数，将停止处理指定的 I/O 请求。 设备会使其工作 (D0) 状态或被删除，框架将调用的 I/O 队列*EvtIoStop*驱动程序不包含每个 I/O 请求一次回调函数[完成](completing-i-o-requests.md)，其中包括请求驱动程序[拥有](request-ownership.md)以及它有[转发](forwarding-i-o-requests.md)到 I/O 的目标。

<a href="" id="---------evtioresume"></a>[*EvtIoResume*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)  
[ *EvtIoResume* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_resume)回调函数恢复处理以前已停止的 I/O 请求。 框架将调用的 I/O 队列*EvtIoResume*回调函数时它会继续提供 I/O 请求到驱动程序从队列中后设备返回到其工作状态。

每次框架将调用的驱动程序[ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)回调函数，则该函数通常[完成](completing-i-o-requests.md)或者[取消](canceling-i-o-requests.md)I/O请求或调用[ **WdfRequestStopAcknowledge** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequeststopacknowledge)框架返回请求的所有权。

执行此操作是可选的虽然一般情况下应提供[ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)电源管理队列的回调函数。 通过提供*EvtIoStop*，您的驱动程序可以帮助缩短你的设备，并可能在系统中之前, 经历进入低功耗状态的时间。

如果未提供[ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)电源管理的队列，请在 framework 等待，直到从电源管理队列传递到驱动程序的所有请求都都完成后才将移动设备 （或系统）低功率状态或删除该设备。 可能的此延期可以防止系统进入休眠状态或另一个较短的系统电源状态。 在极端情况下，它会使用错误检查代码 9F 导致系统崩溃。

如果您的驱动程序不会不将请求转发到 I/O 目标，并且不确定的时间保存请求，可以安全地省略[ *EvtIoStop* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_stop)电源管理队列。

## <a name="waiting-for-dispatcher-objects"></a>调度程序对象正在等待


一般情况下，驱动程序只应使用调度程序对象，作为 nonarbitrary 线程上下文中的同步机制。

因为[请求处理程序](request-handlers.md)任意线程上下文中运行，电源管理队列的请求处理程序必须等待内核调度程序对象来设置。 执行此操作可能会导致死锁。

有关当驱动程序可以等待调度程序对象，以及所需时它不能执行的操作的详细信息，请参阅[内核调度程序对象简介](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-kernel-dispatcher-objects)。

 

 





