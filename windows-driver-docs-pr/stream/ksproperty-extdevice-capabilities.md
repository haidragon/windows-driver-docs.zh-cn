---
title: KSPROPERTY\_EXTDEVICE\_功能
description: KSPROPERTY\_EXTDEVICE\_功能属性检索外部设备的功能。
ms.assetid: c408b4cf-2fd9-41b2-b182-47baa551fd93
keywords:
- KSPROPERTY_EXTDEVICE_CAPABILITIES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_EXTDEVICE_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7cccc26108d55c80269d596faf5cb549574999e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354884"
---
# <a name="kspropertyextdevicecapabilities"></a>KSPROPERTY\_EXTDEVICE\_功能


KSPROPERTY\_EXTDEVICE\_功能属性检索外部设备的功能。

## <span id="ddk_ksproperty_extdevice_capabilities_ks"></span><span id="DDK_KSPROPERTY_EXTDEVICE_CAPABILITIES_KS"></span>


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
<td><p>设备</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTDEVICE_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)"><strong>KSPROPERTY_EXTDEVICE_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagdevcaps" data-raw-source="[&lt;strong&gt;DEVCAPS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagdevcaps)"><strong>DEVCAPS</strong></a></p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是描述外部设备的功能的 DEVCAPS 结构。

<a name="remarks"></a>备注
-------

**功能**KSPROPERTY 成员\_EXTDEVICE\_S 结构指定外部设备的功能。

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

[**KSPROPERTY\_EXTDEVICE\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_extdevice_s)

[**DEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagdevcaps)

 

 






