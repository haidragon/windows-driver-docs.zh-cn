---
title: KSPROPERTY\_BDA\_传输\_模式
description: 客户端使用 KSPROPERTY\_BDA\_传输\_模式来控制如何广播信号进行传输的解调器节点上的设置。
ms.assetid: 8d49a45f-031f-445f-ae2e-d98223a7d524
keywords:
- KSPROPERTY_BDA_TRANSMISSION_MODE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TRANSMISSION_MODE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b65a0bce233dbf0a618d74fcc3efa60ca5303a8b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355415"
---
# <a name="kspropertybdatransmissionmode"></a>KSPROPERTY\_BDA\_传输\_模式


客户端使用 KSPROPERTY\_BDA\_传输\_模式来控制如何广播信号进行传输的解调器节点上的设置。

## <span id="ddk_ksproperty_bda_transmission_mode_ks"></span><span id="DDK_KSPROPERTY_BDA_TRANSMISSION_MODE_KS"></span>


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
<td><p>TransmissionMode</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

TransmissionMode 枚举类型中的返回的值标识为如何广播信号进行传输的设置。

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

[**TransmissionMode**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/transmissionmode)

 

 






