---
title: Hyper-V 可扩展交换机发送和接收标志
description: Hyper-V 可扩展交换机发送和接收标志
ms.assetid: FBA506EC-4E9F-4964-9C9C-FF4910DDA908
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23216bd95306e31cbe14d03e8217d82346cf52ea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386538"
---
# <a name="hyper-v-extensible-switch-send-and-receive-flags"></a>Hyper-V 可扩展交换机发送和接收标志


**请注意**  此页面假定您熟悉的信息和中的关系图[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)并[混合转发](hybrid-forwarding.md)。

 

移到 HYPER-V 可扩展交换机数据路径上的数据包流量被通过以下方式扩展：

-   扩展将从传入数据路径中获取一个数据包时其[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)调用函数。 该扩展将数据包转发到基础扩展的入口数据路径上通过调用[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)。 筛选和转发扩展还可以将数据包从删除的入口数据路径通过调用[ **NdisFSendNetBufferListsComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)。

-   扩展将从出口数据路径中获取一个数据包时其[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)调用函数。 该扩展将数据包转发到通过调用过量的出口数据路径上的扩展[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)。 筛选和转发扩展还可以将数据包从删除出口数据路径通过调用[ **NdisFReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)。

可能会在中设置以下标志*SendFlags*的参数[ *FilterSendNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)或者[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists):

<a href="" id="ndis-send-flags-switch-single-source"></a>**NDIS\_发送\_标志\_交换机\_单个\_源**  
如果设置此标志中的链接列表的所有数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构源自相同的 HYPER-V 可扩展交换机源端口。

当调用 NDIS [ *FilterSendNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_send_net_buffer_lists)，它将设置此标志，如果可扩展交换机可扩展接口已分组的多个数据包从同一源端口。 为了获得最佳性能，扩展应将此分组保存在位置和设置此标志时，它调用[ **NdisFSendNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlists)。 扩展还可以添加任何源自或克隆到的链接列表的数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)如果扩展使用相同的结构源的其他端口在列表中的数据包。

**请注意**  如果在链接列表中的每个数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构使用相同的源端口，该扩展应设置**NDIS\_发送\_完成\_标志\_开关\_单一\_源**标志中*SendCompleteFlags*的参数[ **NdisFSendNetBufferListsComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfsendnetbufferlistscomplete)完成后发送请求。

 

<a href="" id="ndis-send-flags-switch-destination-group"></a>**NDIS\_SEND\_FLAGS\_SWITCH\_DESTINATION\_GROUP**  
如果设置此标志中的链接列表的所有数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构是转发到同一可扩展交换机目标端口。

转发扩展可将此标志用于链接的列表[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)后它会确定每个数据包转发的入口数据路径的结构目标端口。 使用和之前它将向上出口数据路径数据包转发的可扩展交换机基础的微型端口边缘删除此标志。

捕获和筛选扩展不能使用此标志。

**请注意**  转发扩展仅确定为非 NVGRE 数据包的数据包的目标端口。 如果数据包，NVGRE 数据包的 HYPER-V 网络虚拟化 (HNV) 组件确定数据包的目标端口，并将数据包转发。 有关详细信息，请参阅[混合转发](hybrid-forwarding.md)。

 

为了获得最佳性能，转发扩展应设置此标志如果链接列表中的所有数据包转发到同一目标端口。 通过设置此标志，该扩展正在确认链接列表中的所有数据包可扩展交换机转发上下文中都具有相同的目标端口元素。

**请注意**  转发扩展必须不设置此标志为具有多个目标的链接列表的端口。

 

可能会在中设置以下标志*ReceiveFlags*的参数[ *FilterReceiveNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)或者[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists):

<a href="" id="ndis-receive-flags-switch-single-source"></a>**NDIS\_接收\_标志\_交换机\_单个\_源**  
如果设置此标志中的链接列表的所有数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构源自相同的 HYPER-V 可扩展交换机源端口。

当调用 NDIS [ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)，它将设置此标志，如果可扩展交换机已分组的多个数据包从同一源端口。 为了获得最佳性能，扩展应将此分组保存在位置和设置此标志时，它调用[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)。 扩展还应添加任何源自或克隆到的链接列表的数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构如果数据包的相同源的其他端口在列表中的数据包。

**请注意**  如果在链接列表中的每个数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构使用相同的源端口，该扩展应设置**NDIS\_返回\_标志\_交换机\_单一\_源**标志中*ReturnFlags* 参数[*FilterReturnNetBufferLists* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)接收请求完成时。 扩展必须设置此标志*ReturnFlags*参数，如果它调用[ **NdisFReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreturnnetbufferlists)到它不是返回数据包或克隆。

 

<a href="" id="ndis-receive-flags-switch-destination-group"></a>**NDIS\_RECEIVE\_FLAGS\_SWITCH\_DESTINATION\_GROUP**  
如果设置此标志中的链接列表的所有数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构是转发到同一可扩展交换机目标端口。

当调用 NDIS [ *FilterReceiveNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_receive_net_buffer_lists)，它将设置此标志如果可扩展交换机已分组具有相同目标的多个数据包的端口。 为了获得最佳性能，扩展应将此分组保存在位置和设置此标志时，它调用[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)。 扩展还应添加任何源自或克隆到的链接列表的数据包[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构数据包是否为相同的目标端口在列表中其他数据包。

**请注意**  当扩展调用[ **NdisFIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfindicatereceivenetbufferlists)，它必须设置**NDIS\_接收\_标志\_资源**中的标志*ReceiveFlags*参数。 可扩展交换机接口将忽略此标记并将通过调用来完成接收指示[ *FilterReturnNetBufferLists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_return_net_buffer_lists)。

 

 

 





