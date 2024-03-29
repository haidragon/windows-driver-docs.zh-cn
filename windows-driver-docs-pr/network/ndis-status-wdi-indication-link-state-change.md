---
title: NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 指示以下情况下的任何
ms.assetid: 5a8fbe41-d063-4d34-beb8-92ceeb1d97a2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2151af5c3ec4ff9df9713b111a6bb4896dcd0db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384218"
---
# <a name="ndisstatuswdiindicationlinkstatechange"></a>NDIS\_状态\_WDI\_指示\_链接\_状态\_更改


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_链接\_状态\_更改以指示任何以下情况：

-   更改链接速度。
-   链接质量更改者超过阈值的值。 阈值为 1，如果连接质量提示设置为 WDI\_连接\_质量\_低\_延迟 (在中定义[ **WDI\_连接\_质量\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint))。 否则，阈值是 5。

| Object |
|--------|
| Port   |

 

主机使用来自此指示此信息来跟踪有关的当前链接的元数据，它可能会传播到用户。

在工作站和 P2P 客户端的情况下，对等的 MAC 地址设置为 bssid 时的连接的网络。 亚太/P2P 转的情况下，在对等的 MAC 地址设置为给定连接的设备的 MAC 地址。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                           | 允许多个 TLV 实例 | 可选 | 描述                       |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_链接\_状态\_更改\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-link-state-change-parameters) |                                |          | 链接状态更改参数。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>Header</p></td>
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




