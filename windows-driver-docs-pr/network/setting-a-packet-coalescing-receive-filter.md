---
title: 设置数据包合并接收筛选器
description: 设置数据包合并接收筛选器
ms.assetid: 59BD092F-A530-446F-93E7-02E1F254E9A0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d3b15629976c392c4a87cb1535a2c5f2963830f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386829"
---
# <a name="setting-a-packet-coalescing-receive-filter"></a>设置数据包合并接收筛选器


若要下载和上支持数据包合并的微型端口驱动程序设置接收筛选器，基础驱动程序发出的 OID 方法请求[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter). **InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request) OID 请求包含指向的结构调用方分配的缓冲区。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) ndis 指定的参数的结构接收筛选器。

-   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构指定的筛选器测试条件中的字段网络数据包标头。

有关如何基础驱动程序指定的参数为接收数据包合并筛选器的详细信息，请参阅[指定一个数据包合并接收筛选器](specifying-a-packet-coalescing-receive-filter.md)。

当 NDIS 收到 OID 请求基础的网络适配器上设置接收筛选器时，它会验证接收筛选器参数。 如果基础驱动程序指定新的接收筛选器，NDIS 还会生成接收筛选器的唯一的筛选器标识符 (ID)。

NDIS 分配所需的资源和筛选器 ID 之后，它 OID 将请求转发到微型端口驱动程序。 微型端口驱动程序微型端口驱动程序能够成功地分配必要的软件和硬件资源的接收筛选器，如果完成 OID 请求状态为 NDIS\_状态\_成功。

从 OID 方法请求的成功返回后[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)，则**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。 此结构进行了更新的 NDIS 与新的筛选器 id。

 

 





