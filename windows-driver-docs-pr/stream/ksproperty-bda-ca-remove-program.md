---
title: KSPROPERTY\_BDA\_CA\_REMOVE\_PROGRAM
description: 客户端使用 KSPROPERTY\_BDA\_CA\_删除\_程序以防止对特定程序的访问。
ms.assetid: 07792113-6d47-4836-8db2-6960fb14ab87
keywords:
- KSPROPERTY_BDA_CA_REMOVE_PROGRAM 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_CA_REMOVE_PROGRAM
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0441cb12b47f35e92e78ab7d25e2c2e9e85e1fbf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364885"
---
# <a name="kspropertybdacaremoveprogram"></a>KSPROPERTY\_BDA\_CA\_REMOVE\_PROGRAM


客户端使用 KSPROPERTY\_BDA\_CA\_删除\_程序以防止对特定程序的访问。

## <span id="ddk_ksproperty_bda_ca_remove_program_ks"></span><span id="DDK_KSPROPERTY_BDA_CA_REMOVE_PROGRAM_KS"></span>


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

属性值指定的程序，导致无法访问。

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


[**KSEVENT\_BDA\_程序\_流\_状态\_已更改**](ksevent-bda-program-flow-status-changed.md)

[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






