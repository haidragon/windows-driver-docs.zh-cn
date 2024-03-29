---
title: SerCx2 PIO-Receive 事务
description: SerCx2 需要所有串行控制器驱动程序，以实现对支持接收事务使用编程 I/O (PIO)。
ms.assetid: 00C43A55-ACAF-4AB6-BDFB-F3D9350C4536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a29de3836a96c4e0a5b9cbd2985bd00548664f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356773"
---
# <a name="sercx2-pio-receive-transactions"></a>SerCx2 PIO-Receive 事务

SerCx2 需要所有串行控制器驱动程序，以实现对支持接收事务使用编程 I/O (PIO)。 若要启动 PIO 接收事务，SerCx2 调用驱动程序的[ *EvtSerCx2PioReceiveReadBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)事件回叫函数并读取缓冲区作为参数提供。

在此调用期间*EvtSerCx2PioReceiveReadBuffer*函数将数据传输到读取缓冲区中接收 FIFO 串行控制器硬件中。 此数据传输持续读取的缓冲区已满或没有更多数据是从接收 FIFO 立即可用。 传输结束时，该函数将返回已成功传输到读取缓冲区从先进先出的字节数。 此函数永远不会等待接收更多的数据。

## <a name="creating-the-pio-receive-object"></a>创建 PIO 接收对象

SerCx2 可以调用任何串行控制器驱动程序之前*EvtSerCx2PioReceive*Xxx * * 函数，该驱动程序必须调用[ **SerCx2PioReceiveCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecreate)方法这些函数注册到 SerCx2。 此方法接受，作为输入参数，一个指向[ **SERCX2\_PIO\_接收\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_pio_receive_config)结构，其中包含指向在驱动程序*EvtSerCx2PioReceive*Xxx * * 函数。

该驱动程序，则需要实现所有这三个以下函数：

- [*EvtSerCx2PioReceiveReadBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)
- [*EvtSerCx2PioReceiveEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)
- [*EvtSerCx2PioReceiveCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)

作为一个选项，该驱动程序可以实现一个或两个以下函数：

- [*EvtSerCx2PioReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)
- [*EvtSerCx2PioReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)

**SerCx2PioReceiveCreate**方法创建 PIO 接收对象并提供与调用驱动程序[ **SERCX2PIORECEIVE** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)此对象的句柄。 在驱动程序*EvtSerCx2PioReceive*Xxx * * 函数所有采用该句柄作为其第一个参数。 以下 SerCx2 方法将此句柄作为其第一个参数：

- [**SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveready)
- [**SerCx2PioReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)
- [**SerCx2PioReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

初始化 PIO 接收事务开始时的串行控制器硬件或清理该事务结束时的串行控制器的硬件状态，可能需要一些串行控制器驱动程序。

如果驱动程序实现[ *EvtSerCx2PioReceiveInitializeTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)事件回调函数，SerCx2 调用此函数可初始化串行控制器，然后*EvtSerCx2PioReceiveReadBuffer*启动事务的调用。 如果实现，则*EvtSerCx2PioReceiveInitializeTransaction*函数必须调用[ **SerCx2PioReceiveInitializeTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)方法，从而通知SerCx2 初始化串行控制器驱动程序完成。

如果该驱动程序实现[ *EvtSerCx2PioReceiveCleanupTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)事件回调函数，SerCx2 调用此函数后进行清除的硬件状态最终*EvtSerCx2PioReceiveReadBuffer*在事务中调用。 如果实现，则*EvtSerCx2PioReceiveInitializeTransaction*函数必须调用[ **SerCx2PioReceiveCleanupTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete)方法，从而通知 SerCx2该驱动程序完成后清理串行控制器。

## <a name="ready-notifications"></a>准备就绪通知

当*EvtSerCx2PioReceiveReadBuffer*调用结束，因为没有更多数据可立即用于从接收 FIFO，读取 SerCx2 无法完成该 PIO 接收事务之前，在稍后的某个时间，串行控制器接收更多的数据。 在这种情况下，调用 SerCx2 [ *EvtSerCx2PioReceiveEnableReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)事件回调函数，以使就绪通知。 通常情况下，此函数允许中断可供读取从接收先进先出的数据的一个或多个字节时触发。 当且仅当启用了此通知，串行控制器驱动程序调用[ **SerCx2PioReceiveReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveready)方法以通知 SerCx2 时驱动程序检测到接收 FIFO 不再为空。 在响应此通知时，调用 SerCx2 *EvtSerCx2PioReceiveReadBuffer*函数来读取新收到的数据。

此外，SerCx2 使用就绪通知来有效地管理作为 PIO 接收事务处理读取请求的处理过程中的超时值。 有关这些超时值的详细信息，请参阅[**串行\_超时**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts)。

如果就绪通知已启用读取的请求超时或被取消时，调用 SerCx2 [ *EvtSerCx2PioReceiveCancelReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)事件回调函数，若要取消挂起通知。 如果此函数已成功取消挂起通知，它将返回 **，则返回 TRUE**。 返回值 **，则返回 TRUE**串行控制器驱动程序将不会调用保证[ **SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveready)。 返回值**FALSE**指示控制器驱动程序已调用，或将很快就会调用**SerCx2PioReceiveReady**。
