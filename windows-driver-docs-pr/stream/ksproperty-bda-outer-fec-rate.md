---
title: KSPROPERTY\_BDA\_OUTER\_FEC\_RATE
description: 客户端使用 KSPROPERTY\_BDA\_OUTER\_FEC\_速率以控制的二进制卷积方案用于外部的前向纠错 (FEC) 解调器节点类型。
ms.assetid: 0bf1819d-5361-4ab2-b337-e0dd393f5b9b
keywords:
- KSPROPERTY_BDA_OUTER_FEC_RATE 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_OUTER_FEC_RATE
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d94f1e68a4f297b8dbeda993221daf6b35f61645
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368149"
---
# <a name="kspropertybdaouterfecrate"></a>KSPROPERTY\_BDA\_OUTER\_FEC\_RATE


客户端使用 KSPROPERTY\_BDA\_OUTER\_FEC\_速率以控制的二进制卷积方案用于外部的前向纠错 (FEC) 解调器节点类型。

## <span id="ddk_ksproperty_bda_outer_fec_rate_ks"></span><span id="DDK_KSPROPERTY_BDA_OUTER_FEC_RATE_KS"></span>


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
<td><p>BinaryConvolutionCodeRate</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

BinaryConvolutionCodeRate 枚举类型中的返回的值标识二进制卷积方案。

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


[**BinaryConvolutionCodeRate**](https://docs.microsoft.com/previous-versions/windows/desktop/mstv/binaryconvolutioncoderate)

[**KSP\_NODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_node)

 

 






