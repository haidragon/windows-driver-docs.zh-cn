---
title: WDI_TLV_INDICATION_STOP_AP
description: WDI_TLV_INDICATION_STOP_AP 是 TLV 包含为停止亚太可能的原因。
ms.assetid: 49FA6AF6-68BE-437B-9715-5090F52F0109
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7087e406b044010d4ebf48c3838c7720140d347f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380776"
---
# <a name="wditlvindicationstopap"></a>WDI\_TLV\_指示\_停止\_亚太


WDI\_TLV\_指示\_停止\_AP 是 TLV 包含为停止亚太可能的原因。

## <a name="tlv-type"></a>TLV 类型


0xE6

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------|
| UINT32 | 停止 AP 原因。 请参阅[ **WDI\_停止\_AP\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_stop_ap_reason)可能的原因值。 |

 

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

## <a name="see-also"></a>请参阅


[NDIS\_状态\_WDI\_指示\_停止\_亚太](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-stop-ap)

 

 




