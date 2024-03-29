---
title: NDIS_STATUS_RECEIVE_QUEUE_STATE
description: NDIS_STATUS_RECEIVE_QUEUE_STATE 状态指示过量驱动程序的队列状态的虚拟机队列 (VMQ) 接收到队列已更改。
ms.assetid: 59b42de9-6aa5-445e-a39a-de2421c945ea
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RECEIVE_QUEUE_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 339a3b978c3ae8f1dfe718e64f0d1a7d7ab6bc69
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385078"
---
# <a name="ndisstatusreceivequeuestate"></a>NDIS\_状态\_接收\_队列\_状态


NDIS\_状态\_接收\_队列\_过量驱动程序的队列状态的虚拟机队列 (VMQ) 接收到指示状态队列已更改。

<a name="remarks"></a>备注
-------

NDIS 6.20 和更高版本支持的虚拟机队列接口的微型端口驱动程序将生成此状态指示。

微型端口驱动程序提供[ **NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_queue_state)结构**StatusBuffer**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。

更改为*DMA 停止*状态是必需的唯一队列状态更改指示。 微型端口驱动程序必须指示此状态，它接收后[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)集请求并停止 DMA。 在这种情况下，微型端口驱动程序设置**QueueState**的成员[ **NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_queue_state)结构向**NdisReceiveQueueOperationalStateDmaStopped**。

后微型端口驱动程序收到[OID\_接收\_筛选器\_免费\_队列](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)设置请求，它必须停止任何已分配给指定的队列的共享内存的 DMA。

如果微型端口驱动程序已停止的 DMA 出于其他某种原因 （例如，它释放队列上的最后一个筛选器），不应输入队列*DMA 停止*状态。 但是，在中停止 DMA*已暂停*或*运行*队列上设置的状态，如果没有筛选器。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_接收\_队列\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_receive_queue_state)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

[OID\_RECEIVE\_FILTER\_FREE\_QUEUE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-free-queue)

 

 




