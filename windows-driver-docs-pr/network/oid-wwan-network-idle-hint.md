---
title: OID_WWAN_NETWORK_IDLE_HINT
description: OID_WWAN_NETWORK_IDLE_HINT 将提示发送到有关是否应数据的接口上为活动或空闲的网络接口。
ms.assetid: 1FE758C1-543A-45B4-A377-336A1307689F
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_NETWORK_IDLE_HINT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e2765c66ef4da9ffa395171c5c38a0dabdce77d7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360774"
---
# <a name="oidwwannetworkidlehint"></a>OID\_WWAN\_NETWORK\_IDLE\_HINT


OID\_WWAN\_网络\_空闲\_提示将提示发送到有关是否应数据的接口上为活动或空闲的网络接口。 网络服务使用试探法来确定何时将此请求发送到接口，通常，对于一段时间内将会有网络流量减少估计时或在系统即将进入空闲状态 （例如连接待机）。 网络接口可用于为其试探方法的输入实现过程如"快速休眠"。

不支持查询请求。

微型端口驱动程序必须处理集请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本完成与请求的必需[ **NDIS\_WWAN\_网络\_空闲\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)结构，指示网络空闲提示。

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
<td><p>在 Windows 10 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_NETWORK\_IDLE\_HINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_network_idle_hint)

 

 




