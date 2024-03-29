---
title: 确定连接卸载功能
description: 确定连接卸载功能
ms.assetid: 9a7c40dd-7151-462f-b30b-0444a4177ff9
keywords:
- 连接将卸载 WDK TCP/IP 传输，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1764ed2d0d8453aaa602055e6158ad786b24bf4c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381431"
---
# <a name="determining-connection-offload-capabilities"></a>确定连接卸载功能





NDIS 支持两种类别的卸载服务：TCP/IP 卸载增强窗体的 NDIS 5.1 及更早的任务卸载服务的服务以及连接卸载服务。

NDIS 提供卸载硬件功能和基础微型端口适配器添加到协议中的驱动程序的当前配置[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构。 NDIS 提供任务卸载硬件功能和当前配置中的筛选器驱动程序为基础的微型端口适配器[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)结构。

管理应用程序使用对象标识符 (OID) 查询来获取 TCP/IP 的微型端口适配器卸载功能。 但是，过量驱动程序应避免使用 OID 的查询。 协议驱动程序必须处理该基础驱动程序报表中的 TCP/IP 卸载功能的更改。 微型端口驱动程序可以报告任务中的更改将卸载状态指示中的功能。 状态指示的列表，请参阅[NDIS TCP/IP 卸载状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-tcp-ip-offload-status-indications)。

管理应用程序 （或基础驱动程序） 可以通过查询来确定当前的连接卸载配置的 nic [OID\_TCP\_连接\_卸载\_当前\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-connection-offload-current-config)OID。 [ **NDIS\_TCP\_连接\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_tcp_connection_offload) OID 与相关联的结构\_TCP\_连接\_卸载\_当前\_配置指定微型端口适配器的当前连接卸载配置。

 

 





