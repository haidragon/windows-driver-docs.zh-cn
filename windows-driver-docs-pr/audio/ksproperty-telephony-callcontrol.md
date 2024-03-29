---
title: KSPROPERTY\_电话\_CALLCONTROL
description: KSPROPERTY\_电话\_CALLCONTROL 属性用于启动和终止电话呼叫。
ms.assetid: AAC2A218-9A2D-4EFE-B609-5078028B2426
keywords:
- KSPROPERTY_TELEPHONY_CALLCONTROL 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TELEPHONY_CALLCONTROL
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e92e6adca6755789f9cb7449eee50220d3df3731
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391595"
---
# <a name="kspropertytelephonycallcontrol"></a>KSPROPERTY\_电话\_CALLCONTROL


KSPROPERTY\_电话\_CALLCONTROL 属性用于启动和终止电话呼叫。

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
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>Filter</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol" data-raw-source="[&lt;strong&gt;KSTELEPHONY_CALLCONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_tagkstelephony_callcontrol)"><strong>KSTELEPHONY_CALLCONTROL</strong></a></p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY\_电话\_CALLCONTROL 属性请求将返回状态\_成功以指示已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

KSPROPERTY\_电话\_CALLCONTROL 包含 CallType 和 CallControlOp 有关的信息。

电话\_CALLCONTROLOP\_启用将开始从音频驱动程序角度来看的移动电话网络调用，更新 jack 状态关联到活动、 移动电话 bidi 终结点保存调用类型并将调用状态更新为已启用。

电话\_CALLCONTROLOP\_禁用将终止从音频驱动程序角度来看的移动电话网络调用，更新 jack 状态关联到的移动电话 bidi 终结点拔出并将调用状态更新为已禁用。 在这种情况下忽略调用类型。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>最低受支持的客户端</p></td>
<td align="left"><p>Windows 10</p></td>
</tr>
<tr class="even">
<td align="left"><p>最低受支持的服务器</p></td>
<td align="left"><p>无受支持的版本</p></td>
</tr>
<tr class="odd">
<td align="left"><p>客户端</p></td>
<td align="left"><p>Windows 10 移动版</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

 

 





