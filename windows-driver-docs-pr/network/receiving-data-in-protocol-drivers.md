---
title: 在协议驱动程序中接收数据
description: 在协议驱动程序中接收数据
ms.assetid: 758c6a86-6704-410b-ba13-bf589b1e330f
keywords:
- 接收数据 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53bcdac651cbd2eddcd54977facfc7e1621e5ce7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373317"
---
# <a name="receiving-data-in-protocol-drivers"></a>在协议驱动程序中接收数据





下图说明了基本的接收操作，这涉及到协议驱动程序、 NDIS 和驱动程序堆栈中的基础驱动程序。

![说明一个简单的关系图的接收操作，这涉及到协议驱动程序、 ndis 和驱动程序堆栈中的基础驱动程序](images/protocolreceive.png)

NDIS 调用协议驱动程序[ *ProtocolReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)函数来处理接收来自基础驱动程序的迹象。 NDIS 调用*ProtocolReceiveNetBufferLists*基础驱动程序调用接收指示函数后 (例如， [ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)) 以指示接收的网络数据或循环后的数据。

如果**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ *ProtocolReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)未设置，协议驱动程序保留的所有权[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构之前它将调用[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)函数。 如果设置 NDIS **NDIS\_接收\_标志\_资源**标志，协议驱动程序不能保留**NET\_缓冲区\_列表**结构和关联的资源。 在集中**NDIS\_接收\_标志\_资源**标志指示基础驱动程序是否正在运行较低获得资源。 在这种情况下， *ProtocolReceiveNetBufferLists*函数应将接收到的数据复制到协议分配存储并尽可能快地返回。

**请注意**  NDIS 可以更改基础驱动程序表示的标志。 例如，如果微型端口驱动程序设置**NDIS\_接收\_标志\_资源**标志中*ReceiveFlags*参数[ **NdisMIndicateReceiveNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)函数，NDIS 可以复制所指示的数据并将复制到传递[ *ProtocolReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_receive_net_buffer_lists)与**NDIS\_接收\_标志\_资源**清除的标志。

 

**请注意**  如果**NDIS\_接收\_标志\_资源**设置标志，则协议驱动程序必须保留原来的一组[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)链接列表中的结构。 例如，设置此标志驱动程序可能处理结构并指示它们其中一个在堆栈中向上一次，但之前该函数将返回它，必须还原原始链接的列表。

 

协议驱动程序调用[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)函数，以释放所有权的一系列[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构，以及相关[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)结构和网络数据。

 

 





