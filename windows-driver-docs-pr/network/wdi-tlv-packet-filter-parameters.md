---
title: WDI_TLV_PACKET_FILTER_PARAMETERS
description: WDI_TLV_PACKET_FILTER_PARAMETERS 是 TLV OID_WDI_SET_RECEIVE_PACKET_FILTER 包含数据包筛选器参数。
ms.assetid: 5B26DA60-BC5D-4CC5-A620-C076CECF22C0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_PACKET_FILTER_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fefe392f204db6abb985054e2658573e2cf8886d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385409"
---
# <a name="wditlvpacketfilterparameters"></a>WDI\_TLV\_PACKET\_FILTER\_PARAMETERS


WDI\_TLV\_数据包\_筛选器\_参数是包含数据包筛选器参数 TLV [OID\_WDI\_设置\_接收\_数据包\_筛选器](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-receive-packet-filter)。

## <a name="tlv-type"></a>TLV 类型


0x47

## <a name="length"></a>长度


UINT32 大小 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                      | 描述                                |
|---------------------------------------------------------------------------|--------------------------------------------|
| [**WDI\_PACKET\_FILTER\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_packet_filter_type) (UINT32) | 指定所需的 Wi-fi 数据包筛选器。 |

 

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

 

 




