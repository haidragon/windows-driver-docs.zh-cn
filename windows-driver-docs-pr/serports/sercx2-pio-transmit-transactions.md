---
title: SerCx2 PIO-Transmit 事务
description: SerCx2 需要所有串行控制器驱动程序，以实现对支持传输使用编程 I/O (PIO) 的事务。
ms.assetid: 3BEF9A3D-1FEF-4626-B07F-1670359062AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9127e5c30537d40ab31a955df68a6ce6a9a0112f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356770"
---
# <a name="sercx2-pio-transmit-transactions"></a>SerCx2 PIO-Transmit 事务

SerCx2 需要所有串行控制器驱动程序，以实现对支持传输使用编程 I/O (PIO) 的事务。 若要启动 PIO 传输的事务，SerCx2 调用驱动程序的[ *EvtSerCx2PioTransmitWriteBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)事件回叫函数并提供写入缓冲区作为参数。

在此调用期间*EvtSerCx2PioTransmitWriteBuffer*函数将数据从写入缓冲区传输到传输 FIFO 串行控制器硬件中。 此数据传输持续写入缓冲区为空或传输先进先出不能立即接受更多的数据。 传输结束时，该函数将返回到先进先出已成功从写入缓冲区传输的字节数。

## <a name="creating-the-pio-transmit-object"></a>创建 PIO 传输对象

SerCx2 可以调用任何串行控制器驱动程序之前*EvtSerCx2PioTransmit*Xxx * * 函数，该驱动程序必须调用[ **SerCx2PioTransmitCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcreate)方法这些函数注册到 SerCx2。 此方法接受，作为输入参数，一个指向[ **SERCX2\_PIO\_传输\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_pio_transmit_config)结构，其中包含指向在驱动程序*EvtSerCx2PioTransmit*Xxx * * 函数。

该驱动程序，则需要实现所有这三个以下函数：

- [*EvtSerCx2PioTransmitWriteBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)
- [*EvtSerCx2PioTransmitEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)
- [*EvtSerCx2PioTransmitCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)

作为一个选项，该驱动程序可以实现一个或两个以下函数：

- [*EvtSerCx2PioTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)
- [*EvtSerCx2PioTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)

作为一个选项，该驱动程序可以实现以下三个函数：

- [*EvtSerCx2PioTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)
- [*EvtSerCx2PioTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)
- [*EvtSerCx2PioTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_purge_fifo)

如果该驱动程序实现上述列表中的任何函数，它必须实现所有这三个。

**SerCx2PioTransmitCreate**方法创建 PIO 传输对象，并提供与调用驱动程序[ **SERCX2PIOTRANSMIT** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)此对象的句柄。 在驱动程序*EvtSerCx2PioTransmit*Xxx * * 函数所有采用该句柄作为其第一个参数。 以下 SerCx2 方法将此句柄作为其第一个参数：

- [**SerCx2PioTransmitReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitready)
- [**SerCx2PioTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)
- [**SerCx2PioTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)
- [**SerCx2PioTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)
- [**SerCx2PioTransmitPurgeFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitpurgefifocomplete)

## <a name="hardware-initialization-and-clean-up"></a>硬件初始化和清理

初始化一个 PIO 传输的事务，开始时的串行控制器硬件或清理该事务结束时的串行控制器的硬件状态，可能需要一些串行控制器驱动程序。

如果驱动程序实现[ *EvtSerCx2PioTransmitInitializeTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)事件回调函数，SerCx2 调用此函数可初始化串行控制器，然后*EvtSerCx2PioTransmitWriteBuffer*启动事务的调用。 如果实现，则*EvtSerCx2PioTransmitInitializeTransaction*函数必须调用[ **SerCx2PioTransmitInitializeTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)方法，从而通知SerCx2 初始化串行控制器驱动程序完成。

如果该驱动程序实现[ *EvtSerCx2PioTransmitCleanupTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)事件回调函数，SerCx2 调用此函数后进行清除的硬件状态最终*EvtSerCx2PioTransmitWriteBuffer*在事务中调用。 如果实现，则*EvtSerCx2PioTransmitInitializeTransaction*函数必须调用[ **SerCx2PioTransmitCleanupTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)方法，从而通知SerCx2 清理串行控制器驱动程序完成。

## <a name="draining-and-purging-the-transmit-fifo"></a>排出和清除传输先进先出

串行控制器驱动程序应实现[ *EvtSerCx2PioTransmitDrainFifo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)事件回调函数，如果该驱动程序可以检测何时传输 FIFO 清空。 如果实现，SerCx2 后会立即调用此函数在 PIO 传输事务中的数据的最后一个字节写入传输先进先出。 在此调用期间*EvtSerCx2PioTransmitDrainFifo*函数通常情况下允许中断时传输 FIFO 清空，触发，然后返回而不等待。 当先进先出清空时，驱动程序会调用[ **SerCx2PioTransmitDrainFifoComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)方法以通知 SerCx2。 仅在收到此通知后不会 SerCx2 完成正在等待的写入 ([**IRP\_MJ\_编写**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 与 PIO 传输事务相关联的请求。

如果串行控制器驱动程序不实现*EvtSerCx2PioTransmitDrainFifo*函数，SerCx2 必须完成正在等待的写入请求，而没有首先验证传输 FIFO 已清空。 可以将被写入到先进先出的数据传输而无需较长的延迟不能保证。 可以传输之前，在写请求完成后，仍保持先进先出的任何数据可能会丢失。 已成功完成的写入请求中此意外的数据丢失可以创建将请求发送的外围设备驱动程序的可靠性问题。

实现一个驱动程序*EvtSerCx2PioTransmitDrainFifo*函数还必须实现[ *EvtSerCx2PioTransmitCancelDrainFifo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)和[ *EvtSerCx2PioTransmitPurgeFifo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)事件回调函数。

*EvtSerCx2PioTransmitCancelDrainFifo*函数使 SerCx2 完成之前取消正在进行的先进先出排出操作。 如果写入请求超时或被取消，SerCx2 可能会取消此操作。 如果*EvtSerCx2PioTransmitCancelDrainFifo*函数已成功取消 FIFO 排出操作，此函数将返回**TRUE**。 返回值 **，则返回 TRUE**串行控制器驱动程序不调用，但将不会调用的可保证**SerCx2PioTransmitDrainFifoComplete**。 返回值**FALSE**指示*EvtSerCx2PioTransmitDrainFifo*函数具有名为或将很快就会调用**SerCx2PioTransmitDrainFifoComplete**。

如果 PIO 传输的事务与关联的写入请求被取消或时间出完成之前，SerCx2 调用*EvtSerCx2PioTransmitPurgeFifo*函数，如果实现它后，若要放弃所有可能的未发送的数据保持传输先进先出。 SerCx2 使用它获取此函数告知外围设备驱动程序完全的数据的字节数已成功传输到外围设备的写入请求的信息。

## <a name="ready-notifications"></a>准备就绪通知

当*EvtSerCx2PioTransmitWriteBuffer*调用结束，因为传输先进先出不能立即接受更多的数据、 SerCx2 必须等待完成 PIO 接收事务，直到在一些更高版本时，FIFO 已准备好接受的详细信息数据。 在这种情况下，调用 SerCx2 [ *EvtSerCx2PioTransmitEnableReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)启用串行控制器驱动程序将发送就绪通知的事件回调函数。 如果启用了此通知，串行控制器驱动程序调用[ **SerCx2PioTransmitReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitready)方法以通知 SerCx2 时驱动程序检测到传输 FIFO 是准备好接受更多的数据。 在响应此通知时，调用 SerCx2 *EvtSerCx2PioTransmitWriteBuffer*函数来写入先进先出更多的数据。

如果就绪通知已启用写请求超时或被取消时，调用 SerCx2 [ *EvtSerCx2PioTransmitCancelReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)事件回调函数，若要取消挂起通知。 如果此函数已成功取消挂起通知，它将返回 **，则返回 TRUE**。 返回值 **，则返回 TRUE**串行控制器驱动程序将不会调用保证**SerCx2PioTransmitReady**。 返回值**FALSE**指示*EvtSerCx2PioTransmitDrainFifo*函数将调用，或已调用**SerCx2PioTransmitReady**。
