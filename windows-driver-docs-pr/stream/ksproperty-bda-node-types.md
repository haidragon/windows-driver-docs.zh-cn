---
title: KSPROPERTY\_BDA\_NODE\_TYPES
description: 客户端使用 KSPROPERTY\_BDA\_节点\_类型来检索节点类型的列表。
ms.assetid: 8fe72434-3635-4c2c-a72a-1fd398e488d8
keywords:
- KSPROPERTY_BDA_NODE_TYPES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_NODE_TYPES
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 590dbb0659bf11f36f85d3404d9c87175352bf70
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386916"
---
# <a name="kspropertybdanodetypes"></a>KSPROPERTY\_BDA\_NODE\_TYPES


客户端使用 KSPROPERTY\_BDA\_节点\_类型来检索节点类型的列表。

## <span id="ddk_ksproperty_bda_node_types_ks"></span><span id="DDK_KSPROPERTY_BDA_NODE_TYPES_KS"></span>


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
<td><p>否</p></td>
<td><p>Filter</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>KSNODE_DESCRIPTORs 的列表</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

在模板拓扑中每个节点类型可仅出现一次，但它可在实际的拓扑结构中出现多次。 此节点类型列表是一个数组 KSNODE\_描述符结构。 通常情况下，此数组中每个元素的索引用于标识每个特定节点类型。

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


[**BdaPropertyNodeTypes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertynodetypes)

[**KSNODE\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksnode_descriptor)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






