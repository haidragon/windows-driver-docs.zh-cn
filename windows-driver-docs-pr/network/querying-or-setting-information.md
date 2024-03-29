---
title: 查询或设置信息
description: 查询或设置信息
ms.assetid: 39bd9846-7c7e-4b93-8060-4da9c66ac591
keywords:
- 查询的面向连接的信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff3ccd33913d00dab3a910a6c487ca2ac63aa073
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381185"
---
# <a name="querying-or-setting-information"></a>查询或设置信息





CoNDIS 协议驱动程序和 NDIS 可以 OID 请求发送至基础驱动程序。 CoNDIS 协议驱动程序和微型端口调用管理器 (MCMs) 还可以发送 OID 请求为其他协议驱动程序。

面向连接的客户端或调用管理器会调用[ **NdisCoOidRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscooidrequest)查询或设置在绑定上的另一个协议驱动程序或基础微型端口驱动程序维护的信息。

在调用之前**NdisCoOidRequest**，一个客户端或调用管理器为其请求分配缓冲区，并初始化[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构。 此结构指定的请求 （查询或设置），类型标识的信息 (OID)，在查询或设置，并指向用于传递 OID 数据的缓冲区。

如果面向连接的客户端或调用 manager 传递有效*NdisAfHandle* (请参阅[地址系列](address-families.md))，NDIS 调用[ **ProtocolCoOidRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_co_oid_request)函数在绑定上每个协议驱动程序。

NDIS 定义用于标识适配器参数，包括操作参数，如设备特征、 可配置设置和统计信息的对象标识符 (OID) 值。 有关 Oid 的详细信息，请参阅[NDIS Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。

本部分包括以下主题：

[CoNDIS 微型端口驱动程序 OID 请求](condis-miniport-driver-oid-requests.md)

[CoNDIS 协议驱动程序 OID 请求](condis-protocol-driver-oid-requests.md)

[CoNDIS MCM OID 请求](condis-mcm-oid-requests.md)

 

 





