---
title: OID_RECEIVE_FILTER_SET_FILTER
description: 基础驱动程序发出 OID_RECEIVE_FILTER_SET_FILTER OID 方法的请求，网络适配器上设置筛选器。
ms.assetid: ec3e119e-662f-48a6-8c68-20da20590b24
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_SET_FILTER 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 04b63eb1e5d1d78fc9efef7fbc8a314418dc8737
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384918"
---
# <a name="oidreceivefiltersetfilter"></a>OID\_RECEIVE\_FILTER\_SET\_FILTER

基础驱动程序发出 OID 方法请求的 OID\_接收\_筛选器\_设置\_筛选器的网络适配器上设置筛选器。

**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含调用方分配的缓冲区的指针。 此缓冲区已格式化为包含以下信息：

-   [ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters) ndis 指定的参数的结构接收筛选器。

-   一个数组[ **NDIS\_接收\_筛选器\_字段\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_field_parameters)结构指定的筛选器测试条件中的字段网络数据包标头。

通过 OID 方法请求成功返回后**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。 如果基础驱动程序创建新的接收筛选器，NDIS 使用新的筛选器标识符更新此结构。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下的 NDIS 接口中使用：

-   [NDIS 数据包合并](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-packet-coalescing)。 详细了解如何使用此接口中接收的筛选器，请参阅[管理数据包合并接收筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/managing-packet-coalescing-receive-filters)。

-   [单根 I/O 虚拟化 (SR-IOV)](https://docs.microsoft.com/windows-hardware/drivers/network/single-root-i-o-virtualization--sr-iov-)。 详细了解如何使用此接口中接收的筛选器，请参阅[上虚拟端口设置接收的筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-a-receive-filter-on-a-virtual-port)。

-   [虚拟机队列 (VMQ)](https://docs.microsoft.com/windows-hardware/drivers/network/virtual-machine-queue--vmq--in-ndis-6-20)。 详细了解如何使用此接口中接收的筛选器，请参阅[设置和清除 VMQ 筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/setting-and-clearing-vmq-filters)。

OID 方法请求的 OID\_接收\_筛选器\_设置\_筛选器是必需的支持 NDIS 数据包合并、 SR-IOV 或 VMQ 接口的微型端口驱动程序。

基础驱动程序初始化[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构，其请求的筛选器配置。 NDIS 分配中的筛选器标识符**FilterId**成员的 NDIS\_接收\_筛选器\_参数结构，并将方法请求传递给基础的微型端口驱动程序。

在接收队列设置每个筛选器具有唯一的筛选器标识符为网络适配器。 也就是说，筛选器标识符未在不同的队列，用于管理网络适配器上复制。 当 NDIS 收到 OID 请求接收队列上设置筛选器时，它会验证筛选器参数。 NDIS 分配所需的资源和筛选器标识符后，它将提交到基础的网络适配器的 OID 请求。 如果网络适配器能够成功地分配必要的软件和硬件资源的筛选器，它完成 OID 请求返回状态为 NDIS\_状态\_成功。

**请注意**从 NDIS 6.30 开始，数据包合并接收筛选器仅支持在默认接收的网络适配器的队列。 此接收队列具有的 NDIS 标识符\_默认\_接收\_队列\_id。



微型端口驱动程序必须保留已分配的接收筛选器的筛选器标识符。 NDIS OID 请求更高版本中使用筛选器的标识符，若要更改接收筛选器参数或清除接收筛选器。

后微型端口驱动程序收到[OID\_接收\_筛选器\_队列\_分配\_完成](oid-receive-filter-queue-allocation-complete.md)请求和它已在队列中，队列设置的筛选器处于*运行*状态。 在此状态下，微型端口驱动程序可以通过调用开始的队列中的数据包迹象[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)。

### <a name="additional-guidelines-for-the-sr-iov-interface"></a>SR-IOV 接口的其他准则

以下几点适用于支持 SR-IOV 的接口的微型端口驱动程序：

-   对于 SR-IOV 接口中，默认值或非默认虚拟端口 (VPort) 上创建接收队列。

    **请注意**从 Windows Server 2012 中，SR-IOV 接口仅支持默认接收 VPort 队列。

    通过 OID 集请求的分配的 SR-IOV VPort 后[OID\_NIC\_交换机\_创建\_VPORT](oid-nic-switch-create-vport.md)，过量驱动程序上的 OID 的 OID 请求 VPort 可以设置筛选器\_接收\_筛选器\_设置\_筛选器。

    **请注意**仅分配 VPort 基础驱动程序可以在该 VPort 上设置筛选器。

-   由于默认 VPort 始终存在，因此过量驱动程序始终可以设置筛选器在默认 VPort。

-   创建 VPort 时，它设置没有接收筛选器。 在这种情况下，微型端口驱动程序必须指示任何微型端口驱动程序收到的 OID 的 OID 请求之前接收该 VPort 上的数据包\_接收\_筛选器\_设置\_VPort 进行筛选。 发出此 OID 请求后，微型端口驱动程序可以指示该 VPort 上的数据包。

    **请注意**如果微型端口驱动程序正在进行的 OID 的 OID 请求指示 VPort 上的数据包\_接收\_筛选器\_设置\_筛选器，它必须完成 OID 请求，并返回 NDIS\_状态\_成功状态代码。

### <a name="additional-guidelines-for-the-vmq-interface"></a>VMQ 接口的其他准则

以下几点适用于支持 VMQ 接口的微型端口驱动程序：

-   分配 VMQ 接收队列后，过量驱动程序可以设置筛选器的 OID 的 OID 请求的接收队列\_接收\_筛选器\_设置\_筛选器。

    **请注意**仅分配接收队列协议驱动程序可以在该队列上设置筛选器。

-   由于默认队列始终存在，因此过量驱动程序始终可以设置筛选器上的默认队列。 如果网络适配器支持删除队列，过量驱动程序可以设置筛选器删除队列。

    基础驱动程序并不拥有默认值或删除队列。 因此，绑定到的网络适配器的所有协议驱动程序使用默认值或删除队列。

-   创建接收队列时，它设置没有接收筛选器。 在这种情况下，微型端口驱动程序必须指示该接收队列上的任何接收数据包的微型端口驱动程序收到的 OID 的 OID 请求之前\_接收\_筛选器\_设置\_接收队列的筛选器。 发出此 OID 请求后，可以指示微型端口驱动程序上的数据包接收队列。

    **请注意**如果微型端口驱动程序正在进行的 OID 的 OID 请求指示队列上的数据包\_接收\_筛选器\_设置\_筛选器，它必须完成 OID 请求，并返回 NDIS\_状态\_成功状态代码。

### <a name="return-status-codes"></a>返回状态代码

微型端口驱动程序将返回一个 OID 的 OID 方法请求的以下状态代码\_接收\_筛选器\_设置\_筛选器：

<a href="" id="ndis-status-success"></a>NDIS\_状态\_成功  
已成功在队列上设置了筛选器。 包含已更新信息缓冲区[ **NDIS\_接收\_筛选器\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)结构。

<a href="" id="ndis-status-pending"></a>NDIS\_状态\_PENDING  
请求正在等待完成。 最终状态代码和结果将传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-parameter"></a>NDIS\_状态\_无效\_参数  
一个或多个基础驱动程序提供的参数无效。

<a href="" id="ndis-status-invalid-length"></a>NDIS\_状态\_无效\_长度  
信息缓冲区太短。 NDIS 集**数据。方法\_信息。BytesNeeded**中的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)是必需的最小缓冲区大小的结构。

<a href="" id="ndis-status-not-supported"></a>NDIS\_状态\_不\_支持  
微型端口驱动程序的 NDIS 版本是 6.20 之前的版本。

<a href="" id="ndis-status-failure"></a>NDIS\_状态\_失败  
请求由于其他原因而失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.20 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)

[**NDIS\_OID\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)

[**NDIS\_RECEIVE\_FILTER\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_parameters)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[**NET\_BUFFER\_LIST\_RECEIVE\_FILTER\_ID**](https://docs.microsoft.com/windows-hardware/drivers/network/net-buffer-list-receive-filter-id)

[OID\_NIC\_SWITCH\_CREATE\_VPORT](oid-nic-switch-create-vport.md)

[OID\_RECEIVE\_FILTER\_CLEAR\_FILTER](oid-receive-filter-clear-filter.md)

[OID\_接收\_筛选器\_队列\_分配\_完成](oid-receive-filter-queue-allocation-complete.md)