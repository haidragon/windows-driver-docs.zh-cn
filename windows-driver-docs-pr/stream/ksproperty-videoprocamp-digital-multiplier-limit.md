---
title: KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数\_限制
description: KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数\_限制属性指定数字可以应用于图像的缩放量的上限。
ms.assetid: 66cc1dd5-3e07-47d8-bb30-b64b90b07ad9
keywords:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7d919c9f04e93b41d97a26b56b219539095dc2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381954"
---
# <a name="kspropertyvideoprocampdigitalmultiplierlimit"></a>KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数\_限制


KSPROPERTY\_VIDEOPROCAMP\_数字\_乘数\_限制属性指定数字可以应用于图像的缩放量的上限。

## <span id="ddk_ksproperty_videoprocamp_digital_multiplier_limit_ks"></span><span id="DDK_KSPROPERTY_VIDEOPROCAMP_DIGITAL_MULTIPLIER_LIMIT_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)"><strong>KSPROPERTY_VIDEOPROCAMP_S</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEOPROCAMP_NODE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_node_s)"> <strong>KSPROPERTY_VIDEOPROCAMP_NODE_S</strong></a></p></td>
<td><p>长</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为指定照相机的上限的数字乘数限制长时间。 值指定设备可以将应用于光盘映像的数字乘数的最大值。

<a name="remarks"></a>备注
-------

在 set 请求时，客户端应提供中的数字的乘数值**值**KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S 结构。

客户端可能使用 set 请求建立数字缩放的用户定义上限限制。

在 get 请求时，客户端接收中的上述值之一**值**KSPROPERTY 成员\_VIDEOPROCAMP\_节点\_S 结构。

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
<td>Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

[**KSPROPERTY\_VIDEOPROCAMP\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_videoprocamp_s)

 

 






