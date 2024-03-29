---
title: 从 CoNDIS 驱动程序发送 NET_BUFFER 结构
description: 从 CoNDIS 驱动程序发送 NET_BUFFER 结构
ms.assetid: 63bca3f0-b598-4006-bfd0-6df32ab2cbe7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84521d3e0cf646a5720f6d3f2153592fed660708
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386844"
---
# <a name="sending-netbuffer-structures-from-condis-drivers"></a>发送 NET\_缓冲区结构的 CoNDIS 驱动程序





下图说明了基本的 CoNDIS 发送操作，这涉及到协议驱动程序、 NDIS 和微型端口驱动程序。

![说明基本 condis 的关系图发送操作，这涉及到协议驱动程序、 ndis 和微型端口驱动程序](images/netbuffercosend.png)

如前图所示，协议驱动程序调用[ **NdisCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscosendnetbufferlists)函数来发送[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)虚拟连接 (VC) 上的结构。 NDIS 然后调用微型端口驱动程序[ **MiniportCoSendNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_co_send_net_buffer_lists)函数将转发 NET\_缓冲区\_列表结构为基础的微型端口驱动程序。

所有的 NET\_基于缓冲区的发送操作是异步的。 因此，微型端口驱动程序始终调用[ **NdisMCoSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcosendnetbufferlistscomplete)函数，并提供相应的状态代码，在完成时发送数据。 微型端口驱动程序可以完成发送操作的每个 NET\_缓冲区\_列表结构独立于其他 NET\_缓冲区\_列表结构。 NDIS 调用协议驱动程序[ **ProtocolCoSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_send_net_buffer_lists_complete)函数每个时间微型端口驱动程序调用**NdisMCoSendNetBufferListsComplete**。

协议驱动程序可以回收的所有权[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构和所有关联的结构和数据立即 NDIS 调用协议驱动程序*ProtocolCoSendNetBufferListsComplete*函数。

微型端口驱动程序或 NDIS 可以返回 NET\_缓冲区\_按任意顺序的列表结构。 但，保证协议驱动程序的列表[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)附加到每个网络的结构\_缓冲区\_列表结构尚未修改。

协议驱动程序集**SourceHandle**中的成员[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构相同的值与*NdisVcHandle*的参数**NdisCoSendNetBufferLists**。 使用 NDIS **SourceHandle**要返回 NET 成员\_缓冲区\_给发送 NET 协议驱动程序的列表结构\_缓冲区\_列表结构。

中间驱动程序还设置**SourceHandle**成员在 NET\_缓冲区\_列表结构*NdisVcHandle*值。 如果中间驱动程序将转发发送请求，该驱动程序必须将保存**SourceHandle**过量的驱动程序提供之前它将写入到的值**SourceHandle**成员。 当 NDIS 返回转发的 NET\_缓冲区\_必须还原到中间驱动程序，中间驱动程序的列表结构**SourceHandle**保存它。

协议驱动程序可以通过使用相同的机制作为无连接驱动程序取消发送请求。 有关取消发送请求的详细信息，请参阅[取消发送操作](canceling-a-send-operation.md)。

 

 





