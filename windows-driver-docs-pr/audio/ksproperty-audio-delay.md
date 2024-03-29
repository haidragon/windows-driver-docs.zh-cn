---
title: KSPROPERTY\_音频\_延迟
description: KSPROPERTY\_音频\_延迟属性指示滞后时间的延迟节点 (KSNODETYPE\_延迟) 引入到指定的通道。
ms.assetid: ac260b83-1d7c-49d7-b325-ea0f21646d39
keywords:
- KSPROPERTY_AUDIO_DELAY 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_DELAY
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b559208677814c3e1f04f66c22ac3098ce467365
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358948"
---
# <a name="kspropertyaudiodelay"></a>KSPROPERTY\_音频\_延迟


KSPROPERTY\_音频\_延迟属性指示滞后时间的延迟节点 ([**KSNODETYPE\_延迟**](ksnodetype-delay.md)) 引入到指定的通道。

## <span id="ddk_ksproperty_audio_delay_ks"></span><span id="DDK_KSPROPERTY_AUDIO_DELAY_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用率摘要表

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
<th align="left">Get</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstime" data-raw-source="[&lt;strong&gt;KSTIME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstime)"><strong>KSTIME</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 为类型 KSTIME 指定滞后时间的大量的结构。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_音频\_延迟属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h （包括 Ksmedia.h）</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSTIME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kstime)

[**KSNODETYPE\_延迟**](ksnodetype-delay.md)

 

 






