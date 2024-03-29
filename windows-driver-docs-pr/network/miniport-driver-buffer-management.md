---
title: 微型端口驱动程序缓冲区管理
description: 微型端口驱动程序缓冲区管理
ms.assetid: 3b8844e0-9b38-4030-9aec-b713643de523
keywords:
- 缓冲 WDK NDIS 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 769e83f5650b687262ecf47da8944de31c2eacdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373939"
---
# <a name="miniport-driver-buffer-management"></a>微型端口驱动程序缓冲区管理





通常情况下调用微型端口驱动程序[ **NdisAllocateNetBufferListPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferlistpool)从[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)创建池[**NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构。 微型端口驱动程序使用这些结构指示接收到的数据。

通常情况下，分配 NET 的微型端口驱动程序才能\_缓冲区\_列表结构将分配和队列之一[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer) 该网络上的结构\_缓冲区\_列表结构。 若要预分配 NET 效率更高\_缓冲区结构时的 NET 池分配\_缓冲区\_比以分配 NET 列表结构\_缓冲区\_列表结构和 NET\_结构的单独缓冲区。

微型端口驱动程序可以调用**NdisAllocateNetBufferListPool**并设置*AllocateNetBuffer*参数**TRUE**指示[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)预先分配结构。 在此情况下，NET\_缓冲区结构都已预分配以每个 NET\_缓冲区\_从池中分配驱动程序的列表结构。 此类驱动程序必须调用[ **NdisAllocateNetBufferAndNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocatenetbufferandnetbufferlist)无法从这个池分配结构。

通常，微型端口驱动程序会调用**NdisAllocateNetBufferAndNetBufferList**从*MiniportInitializeEx*来分配任意多个缓冲区，因为它会将用于后续接收操作。 在这种情况下，该驱动程序管理免费缓冲区的内部的列表。

[ *MiniportReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_return_net_buffer_lists)函数可以准备返回的 NET\_缓冲区\_列表结构以供重用在后面会收到指示。 尽管*MiniportReturnNetBufferLists*无法返回 NET\_缓冲区\_给池的列表结构 (例如，它可能会调用[ **NdisFreeNetBufferList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlist))，它可能更有效，而无需将它们返回到池重用结构。

微型端口驱动程序应释放所有 NET\_缓冲区\_列表结构和关联的数据时 NDIS 停止适配器。 驱动程序可以调用**NdisFreeNetBufferList**来释放结构并[ **NdisFreeNetBufferListPool** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreenetbufferlistpool)函数来释放 NET\_缓冲区\_列表池。

 

 





