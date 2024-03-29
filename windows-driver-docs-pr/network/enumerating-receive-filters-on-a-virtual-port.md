---
title: 枚举虚拟端口上的接收筛选器
description: 枚举虚拟端口上的接收筛选器
ms.assetid: E809B7A3-256B-4351-8A60-D80D4A86EFDB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18d63f98b33e1e201b12dc0f98a1a014865dfc5c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354564"
---
# <a name="enumerating-receive-filters-on-a-virtual-port"></a>枚举虚拟端口上的接收筛选器





上创建虚拟端口 (VPort) 后 NIC 切换的网络适配器，基础驱动程序和用户应用程序可以执行以下操作：

-   枚举 VPort 的接收筛选器的参数。

    有关详细信息，请参阅[枚举接收筛选器](#enumerating-receive-filters)。

-   查询特定的接收筛选器的参数。

    有关详细信息，请参阅[查询一个特定的接收筛选器](#querying-a-specific-receive-filter)。

有关如何创建 VPort 的详细信息，请参阅[创建虚拟端口](creating-a-virtual-port.md)。

## <a name="enumerating-receive-filters"></a>枚举接收筛选器


若要获取的列表的 NIC 切换，请过量驱动程序的虚拟端口 (VPort) 设置的筛选器的所有接收和应用程序可以发出对象标识符 (OID) 的方法请求[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构最初包含一个指向[**NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构。

过量的驱动程序或用户应用程序会发出此 OID 方法请求之前，必须将格式化[ **NDIS\_接收\_筛选器\_信息\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)结构，并按以下方式设置此结构的成员：

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 基础驱动程序将获取通过以下方式之一的 VPort 标识符：

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。

    **请注意**  此成员才有效的驱动程序或应用程序设置 NDIS\_接收\_筛选器\_信息\_数组\_VPORT\_ID\_中的指定标志**标志**成员。 如果未设置此标志，接收返回在 NIC 交换机上的每个 VPort 上设置的筛选器。

     

从 OID 方法请求的成功返回后[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)，则**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含的指针的已更新[ **NDIS\_接收\_筛选器\_INFO\_数组**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info_array)后跟一个或多个结构[ **NDIS\_接收\_筛选器\_信息** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_info)结构。 每个**NDIS\_接收\_筛选器\_信息**结构指定的接收筛选器的指定 VPort 上设置的唯一标识符。

## <a name="querying-a-specific-receive-filter"></a>查询特定的接收筛选器


过量驱动程序或应用程序可以发出的 OID 方法请求[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)来获取 VPort 上的特定筛选器参数。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构最初包含一个指向[**NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。

过量的驱动程序或用户应用程序会发出此 OID 方法请求之前，必须将格式化[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，并按以下方式设置此结构的成员：

-   **FilterId**成员必须设置为其参数位于要返回的筛选器的非零值的标识符值。

    **请注意**  过量的驱动程序从较早的 OID 方法请求获取筛选器标识符[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)或[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)。 应用程序可以仅从较早的 OID OID 方法请求获取筛选器标识符\_接收\_筛选器\_枚举\_筛选器。

     

-   **QueueId**成员必须设置为 NDIS\_默认\_接收\_队列\_id。

-   **VPortId**成员必须设置为与 VPort 关联的标识符。 基础驱动程序将获取通过以下方式之一的 VPort 标识符：

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_创建\_VPORT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-create-vport)。

    -   从上一个 OID 方法请求的[OID\_NIC\_交换机\_枚举\_VPORTS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-nic-switch-enum-vports)。

NDIS 句柄[OID\_接收\_筛选器\_枚举\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-enum-filters)并[OID\_接收\_筛选器\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-parameters)方法 OID 请求微型端口驱动程序。 NDIS 从它来自数据的内部缓存中获取信息[OID\_接收\_筛选器\_设置\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-set-filter)OID 请求。

 

 





