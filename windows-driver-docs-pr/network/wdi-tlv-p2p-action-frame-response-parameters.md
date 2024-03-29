---
title: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS 是 TLV 包含 Wi-Fi Direct 操作帧响应参数。
ms.assetid: 2DFF00A6-FDE2-43EF-93C2-EEA3DBC00D52
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 15f3020b936482caee1460f05779d8c6d2e4abc4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385712"
---
# <a name="wditlvp2pactionframeresponseparameters"></a>WDI\_TLV\_P2P\_ACTION\_FRAME\_RESPONSE\_PARAMETERS


WDI\_TLV\_P2P\_操作\_帧\_响应\_参数是包含 Wi-Fi Direct 操作帧响应参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0xAD

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                    | 描述                                                                                                                          |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_P2P\_ACTION\_FRAME\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 要发送的响应框架的类型。                                                                                               |
| [**WDI\_MAC\_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 目标对等方 Wi-Fi Direct 设备的设备地址。                                                                           |
| UINT8                                                                   | Wi-Fi Direct 对话框标记，表示此事务。                                                                                  |
| UINT32                                                                  | 发送超时。 指定的最长时间，以毫秒为单位，将发送此操作帧。                                            |
| UINT32                                                                  | 开机自检 ACK 停留时间。 指定传入数据包被确认后保留在侦听通道，以毫秒为单位的时间。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




