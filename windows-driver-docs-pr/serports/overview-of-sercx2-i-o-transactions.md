---
title: SerCx2 I/O 事务概述
description: SerCx2 通过向串行控制器驱动程序发出一个或多个 I/O 事务处理读取或写入请求从客户端。
ms.assetid: 04DDFE53-4855-4029-BE1E-9D184B02A998
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6bd5e6d9af2272690d25642ad100f0c668fbf34
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354903"
---
# <a name="overview-of-sercx2-io-transactions"></a>SerCx2 I/O 事务概述


SerCx2 通过向串行控制器驱动程序发出一个或多个 I/O 事务处理读取或写入请求从客户端。 此驱动程序将每个事务视为串行控制器与请求中的数据缓冲区之间传输数据的自包含 I/O 操作。

芯片 (SoC) 集成线路上的系统通常包括串行控制器 （或 UARTs） 以启用与焊接到相同的印刷电路板其他集成线路的高速串行通信。 在这些 Soc 处理器可以使用通过编程方式设置 I/O (PIO) 可以直接传输数据到或从这些串行控制器中的内存映射数据寄存器。 此外，这些 Soc 通常提供高级的 DMA 硬件串行控制器和内存之间移动数据。

PIO 可能足以满足短数据传输，但使用 PIO 适用于较长的传输速率较高的数据过大带来了沉重负担处理器上。 DMA 需要卸载此类传输从处理器。

## <a name="types-of-io-transactions"></a>类型的 I/O 事务


SerCx2 定义以下三种常规类型的 I/O 事务：

-   PIO
-   系统 DMA
-   自定义

串行控制器的所有驱动程序必须支持使用 PIO 将数据传输的 I/O 事务。 串行控制器驱动程序可能还支持使用系统 DMA 或自定义数据传输机制，具体取决于串行控制器和相关联的硬件的功能的 I/O 事务。 该驱动程序可以支持系统 DMA 事务或自定义的事务，但不可同时使用两者。

对于每个类型的 I/O 事务串行控制器硬件支持，串行控制器驱动程序注册 SerCx2 的支持包。 此包描述相关的硬件功能，并包含 SerCx2 调用来启动和控制这种类型的 I/O 事务的一组的驱动程序实现事件回调函数。

如果串行控制器可以使用系统 DMA 控制器，这可能与其他设备共享，串行控制器驱动程序可能会支持系统 DMA 事务。 对于这些事务，SerCx2 设置系统 DMA 控制器并启动 DMA 传输。 串行控制器驱动程序在系统 DMA 事务期间执行较少的工作。

如果串行控制器具有某些自定义硬件机制，用于将数据传输，串行控制器驱动程序可能支持使用此机制的自定义事务。 例如，如果串行控制器硬件具有内置的总线 master DMA 功能，串行控制器驱动程序可以支持自定义事务以使此功能可供 SerCx2。

自定义的事务是灵活的数据传输机制，它们可以支持的类型。 但是，这些事务是实现都比 PIO 事务或系统 DMA 事务的难度。 若要支持自定义的事务，串行控制器驱动程序必须通常设置并初始化用于将数据传输的硬件。 此外，如果挂起的读取或写入请求在关联 custom-receive 之前取消或自定义传输的事务完成，该驱动程序必须终止该事务并完成该请求。

每个 I/O 事务是一个相对较简单的操作。 I/O 事务要么从串行控制器读取数据或将数据写入到控制器，并读取和写入永远不会混合使用。 I/O 事务使用单个传输模式 — PIO，系统 DMA，或自定义，并组合永远不会将传输模式。

SerCx2 以智能方式可以决定是否使用 PIO 或 DMA 来满足读取或写入请求。 例如，SerCx2 可以选择提供很短的读取或写入串行控制器驱动程序，因为 PIO 事务请求。 或者，SerCx2 可能提供更长的读取或写入串行控制器作为 DMA 事务请求。

## <a name="breaking-a-read-or-write-request-into-multiple-transactions"></a>分解为多个事务的读取或写入请求


某些系统 DMA 控制器可能需要 SerCx2 中断更长的读取或写入请求到两个或多个 I/O 事务的限制。 例如，如果系统 DMA 控制器需要 DMA 传输开始和结束字节边界甚至在内存中，但数据缓冲区中读取请求开始和结束奇数字节边界上，SerCx2 可能使用 PIO 将传输到缓冲区的第一个和最后一个字节并使用系统 DMA 的第一个和最后一个字节之间传输所有数据。 对于此示例，SerCx2 串行控制器驱动程序中所示的顺序将发出以下三个 I/O 事务：

1.  第一个字节 PIO 接收事务。
2.  系统 DMA 接收事务之间的字节数。
3.  最后一个字节 PIO 接收事务。

同样，如果自定义的数据传输机制可以开始和结束自定义传输在内存中，任意字节边界上的事务，但在写入请求的缓冲区大小超出最大传输长度的自定义传输的事务，SerCx2 分区为两个 （或多个） 的写入请求自定义传输的事务，其中每个不超过最大传输长度。

如果 SerCx2 需要拆分读取或写入到两个或多个 I/O 事务的请求，串行控制器驱动程序可以放心地忽略这些事务相互和请求的关系。 SerCx2 序列化事务以确保数据是接收或传输正确的顺序。

当串行控制器驱动程序注册的回调函数来支持系统 DMA 事务或自定义事务集时，驱动程序提供参数值，用于描述要执行这些事务的硬件的功能。 例如，对于系统 DMA 事务，参数包括对齐要求和 DMA 控制器的系统支持的最小值和最大传输长度。 SerCx2 使用这些参数来决定是否处理读取或写入请求为 PIO 事务或系统 DMA 事务，以及是否将拆分为两个或多个 I/O 事务的请求。

但是，串行控制器可能无法充分描述由串行控制器驱动程序提供给 SerCx2 参数的特殊的硬件功能。 因此，该驱动程序可能有权访问依赖于硬件的信息，使驱动程序来更好地决定比 SerCx2 有关如何进行分区读取或写入到一个或多个 I/O 事务请求。 作为一个选项，可以实现这样的驱动程序[ *EvtSerCx2SelectNextReceiveTransactionType* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_select_next_receive_transaction_type)并[ *EvtSerCx2SelectNextTransmitTransactionType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_select_next_transmit_transaction_type)事件回调函数。 SerCx2 调用这些函数中，如果它们实现，以便决定要用来满足读取或写入的 I/O 事务请求的驱动程序。

 

 




