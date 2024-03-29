---
title: 重启绑定
description: 重启绑定
ms.assetid: 5abec927-cb73-4b02-b977-c4f45bd37c42
keywords:
- 协议驱动程序 WDK 网络绑定重新启动
- NDIS 协议驱动程序 WDK，绑定重启
- 绑定重启 WDK 网络
- 绑定状态 WDK 网络
- 重新启动协议驱动程序的绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2ccb56fa55421fc27eaec1f6e7fb0b2cf39695
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384708"
---
# <a name="restarting-a-binding"></a>重启绑定





若要重新启动已暂停的绑定，NDIS 发送协议驱动程序即插即用的网络，并播放 (PnP) 重新启动事件通知。 协议驱动程序收到重新启动通知后，受影响的绑定将进入正在重新启动状态。

若要发送的重新启动通知，NDIS 调用协议驱动程序[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)函数。 [ **NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification) NDIS 将传递给结构*ProtocolNetPnPEvent*指定**NetEventRestart**中**NetEvent**成员并**缓冲区**成员包含一个指向[ **NDIS\_协议\_重新启动\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_restart_parameters)结构。 NDIS 提供一个指针指向[ **NDIS\_重新启动\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_restart_attributes)结构**RestartAttributes**的 NDIS成员\_协议\_重新启动\_参数结构。

**请注意**  绑定已暂停时，NDIS 可以重新配置驱动程序堆栈。 新堆栈配置为基础的适配器可以支持一组不同的功能。 这些新功能可能会影响协议驱动程序在对绑定进行通信的方式。

 

协议驱动程序应使用中的信息[ **NDIS\_协议\_重新启动\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_protocol_restart_parameters)结构，以避免不必要的 OID 请求。

在正在重新启动状态下，协议驱动程序可以：

-   使用查询驱动程序堆栈的 OID 请求。 例如，驱动程序可以找出有关支持的接收方缩放通过使用[OID\_代\_接收\_规模\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-receive-scale-capabilities)。

-   重新分配[ **NET\_缓冲区**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)并[ **NET\_缓冲区\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)池，如有必要。

-   枚举的基础的筛选器模块的列表。

-   使用 OID 请求，以显示适配器的新功能。

该驱动程序已准备好继续发送和接收操作的绑定后，该绑定将进入运行状态。

 

 





