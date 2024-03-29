---
title: Hyper-V 可扩展交换机转发上下文数据类型
description: Hyper-V 可扩展交换机转发上下文数据类型
ms.assetid: B5377411-C6F0-47BE-BD45-534AC784ED76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fda88cb4e96296bb1105dcea0e450ea41e3c320b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383698"
---
# <a name="hyper-v-extensible-switch-forwarding-context-data-types"></a>Hyper-V 可扩展交换机转发上下文数据类型


[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构为每个数据包的传输的 HYPER-V 可扩展交换机数据路径包含带外 (OOB) 数据。 此数据指定从数据包源于何处，以及数据包传递的一个或多个目标端口的源端口。 此 OOB 数据被称为*可扩展交换机转发上下文*。

已声明以下数据类型来访问一个数据包中的可扩展交换机转发上下文[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)结构：

<a href="" id="ndis-switch-forwarding-detail-net-buffer-list-info"></a>[**NDIS\_交换机\_转发\_详细信息\_NET\_缓冲区\_列表\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
这是数据包的包含转发特征的 64 位联合。 此数据包括数据包的起源的源端口和网络适配器连接的标识符。 此数据还包括未使用所提供的目标端口数组的元素数。

可扩展的交换机扩展可以访问此数据通过使用[ **NET\_缓冲区\_列表\_切换\_转发\_详细**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-switch-forwarding-detail)宏。

<a href="" id="ndis-switch-forwarding-destination-array"></a>[**NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)  
此结构定义数据包的目标端口数组。 此数组中的每个元素的格式设置为[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)结构。

[ **NDIS\_交换机\_转发\_目标\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构包含成员指定当前的总计数元素，以及数组中的元素数数。

可扩展的交换机扩展可以通过调用来获取此数组[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)函数。 如果该驱动程序添加或修改多个目标端口的数据包的数组中的元素，它必须调用[ *UpdateNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_update_net_buffer_list_destinations)函数。 此函数将这些更改提交给目标端口数组中的数据包转发上下文。

**请注意**  只有一个目标端口与数据包中提交更改，是要调用的驱动程序更高效[ *AddNetBufferListDestination* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_add_net_buffer_list_destination)函数。

 

<a href="" id="ndis-switch-port-destination"></a>[**NDIS\_SWITCH\_PORT\_DESTINATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)  
此结构定义数据包的目标端口。 对于与单个目标端口的数据包，都只有一个[ **NDIS\_交换机\_端口\_目标**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_switch_port_destination)目标端口数组中的元素。 对于具有多个目标端口的数据包，有一个或多个数组中的这些元素。

扩展已调用后可扩展交换机[ *GetNetBufferListDestinations* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-ndis_switch_get_net_buffer_list_destinations)若要获取数据包的目标端口数组，它可以访问各个元素数组中的使用[ **NDIS\_交换机\_端口\_目标\_处\_数组\_索引**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-switch-port-destination-at-array-index)宏。

 

 





