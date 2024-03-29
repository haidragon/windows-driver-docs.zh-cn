---
title: 数据包合并概述
description: 数据包合并概述
ms.assetid: E406E89C-247B-4DCB-B309-B742BF0A27E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df260acc887b8681874ccc9631b169ec6556a97d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356096"
---
# <a name="overview-of-packet-coalescing"></a>数据包合并概述


某些 IP 版本 4 (IPv4) 和 IP 版本 6 (IPv6) 网络协议涉及到广播或多播的地址的数据包的传输。 IPv4/IPv6 子网中的多个主机接收这些数据包。 在大多数情况下，接收这些数据包的主机不会执行任何操作与这些数据包。 因此，这些不需要的多播或广播数据包接收会导致不必要的处理和电源消耗在接收主机内执行。

例如，主机 A 发送 IPv6 子网的多播链路本地多播名称解析 (LLMNR) 请求若要解决主机 B 的名称。 除了主机 A 上，在子网上的所有主机接收该 LLMNR 请求。 除了主机 B，在其他主机运行的 TCP/IP 协议堆栈检查该数据包，并确定数据包不适合它。 因此，协议堆栈会拒绝该数据包并调用[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)以返回到微型端口驱动程序的数据包。

从 NDIS 6.30，网络适配器可以支持 NDIS 数据包合并。 通过随机广播或多播的数据包数、 处理开销和电源的合并接收中断的数量，从而大大减少消耗了系统上。

数据包合并涉及以下步骤：

1.  过量驱动程序，如 TCP/IP 协议堆栈中，定义 NDIS 接收用于屏幕广播和多播数据包的筛选器。 基础驱动程序下载到基础微型端口驱动程序支持数据包合并这些筛选器。 微型端口驱动程序下载完成后，将网络适配器配置合并接收数据包与筛选器。

    有关这些筛选器的详细信息，请参阅[数据包合并接收筛选器](packet-coalescing-receive-filters.md)。

2.  接收到的数据包与匹配的接收筛选器进行缓存，或*合并*，网络适配器上。 适配器不会生成合并的数据包的接收中断。 相反，适配器会在主机硬件的另一个事件发生时中断。

    当生成此中断时，适配器必须指示中断的接收事件。 这样，要处理合并的数据包的网络适配器接收到的网络适配器。

    例如，支持数据包合并的网络适配器可以生成接收中断时可能出现以下事件之一：

    -   其过期时间设置为匹配的接收筛选器的最大的合并延迟值硬件计时器的过期日期。

    -   硬件合并缓冲区中的可用空间达到适配器指定低水位。

    -   接收数据包时与合并筛选器不匹配。

    -   另一个中断事件，例如已发送的完成事件，发生。

    有关此过程的详细信息，请参阅[处理数据包合并接收筛选器](handling-packet-coalescing-receive-filters.md)。

以下几点适用于通过 NDIS 合并的数据包的支持：

-   NDIS 支持合并的数据包分配给物理网络适配器的默认 NDIS 端口 （端口 0） 上收到的数据包。 NDIS 不支持数据包分配给虚拟网络适配器的 NDIS 端口上合并。 有关详细信息，请参阅[NDIS 端口](ndis-ports.md)。

-   NDIS 支持数据包的默认值上接收的数据包合并接收的网络适配器的队列。 此接收队列具有的 NDIS 标识符\_默认\_接收\_队列\_id。
