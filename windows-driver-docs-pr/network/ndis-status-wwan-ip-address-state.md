---
title: NDIS_STATUS_WWAN_IP_ADDRESS_STATE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 通知来告知附加 PDP 上下文的 IP 配置的更改 MB 服务。
ms.assetid: 98E4028D-AD75-4F12-ADA4-41725253166F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_IP_ADDRESS_STATE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b246b73cc066af436961799c972cdcc05a5a4eec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377632"
---
# <a name="ndisstatuswwanipaddressstate"></a>NDIS\_状态\_WWAN\_IP\_地址\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_IP\_地址\_状态通知来告知附加 PDP 上下文的 IP 配置的更改 MB 服务。

使用此通知[ **NDIS\_WWAN\_IP\_地址\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)结构。

<a name="remarks"></a>备注
-------

必须与其他 PDP 上下文会话相关联的 NDIS 端口上发送此通知。

微型端口驱动程序应发送此通知后附加 PDP 上下文已成功激活并已针对此上下文获取的 IP 配置。 如果设备将指示未经请求的 IP 配置更改后的上下文激活，微型端口驱动程序应发送未经请求的指示与此通知使用更新的 IP 配置。

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
<td><p>在 Windows 8.1 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_IP\_地址\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_ip_address_state)

 

 




