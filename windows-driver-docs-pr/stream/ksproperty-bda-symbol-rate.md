---
title: KSPROPERTY\_BDA\_SYMBOL\_RATE
description: 客户端使用 KSPROPERTY\_BDA\_符号\_速率以控制解调器节点的符号速率。
ms.assetid: 11e2e020-3037-4a68-a8d6-c68efd86a518
keywords:
- KSPROPERTY_BDA_SYMBOL_RATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_SYMBOL_RATE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8aa8f863db66b371c3a6ad54fa24448bfa4d6286
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355420"
---
# <a name="kspropertybdasymbolrate"></a>KSPROPERTY\_BDA\_SYMBOL\_RATE


客户端使用 KSPROPERTY\_BDA\_符号\_速率以控制解调器节点的符号速率。

## <span id="ddk_ksproperty_bda_symbol_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_SYMBOL_RATE_KS"></span>


### <a name="usage-summary-table"></a>使用率摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>Get</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>Filter</p></td>
<td><p>KSP_NODE</p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

返回的值指定的符号速度。

**NodeId** KSP 成员\_节点指定解调器节点的标识符。

## <a name="see-also"></a>请参阅


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






