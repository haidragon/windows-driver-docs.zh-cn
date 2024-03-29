---
title: KSPROPERTY\_BDA\_MODULATION\_TYPE
description: 客户端使用 KSPROPERTY\_BDA\_调制\_类型以控制如 QPSK 或 8VSB 解调器类型。
ms.assetid: 7c7dd8a4-4aa2-4e62-9b08-05c202df957d
keywords:
- KSPROPERTY_BDA_MODULATION_TYPE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_MODULATION_TYPE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d35a1b8eefba0adeafd91531b8c639eae61575a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374623"
---
# <a name="kspropertybdamodulationtype"></a>KSPROPERTY\_BDA\_MODULATION\_TYPE


客户端使用 KSPROPERTY\_BDA\_调制\_类型以控制如 QPSK 或 8VSB 解调器类型。

## <span id="ddk_ksproperty_bda_modulation_type_ks"></span><span id="DDK_KSPROPERTY_BDA_MODULATION_TYPE_KS"></span>


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
<td><p>ModulationType</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

ModulationType 枚举类型中的返回的值标识解调器类型。

**NodeId** KSP 成员\_节点指定解调器节点的标识符。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h （包括 Bdamedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

[**ModulationType**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/modulationtype)

 

 






