---
title: KSPROPERTY\_ALLOCATOR\_控制\_捕获\_CAP
description: KSPROPERTY\_ALLOCATOR\_控制\_捕获\_CAPS 属性会通知的视频端口 （这是捕获支持是否可用） 的捕获功能覆盖 Mixer。
ms.assetid: 9e2947a3-ef5b-4a2a-a607-6c0c4be44b1c
keywords:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a5392c1809c2feaf09ef2858b1c539a76888c7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386929"
---
# <a name="kspropertyallocatorcontrolcapturecaps"></a>KSPROPERTY\_ALLOCATOR\_控制\_捕获\_CAP


KSPROPERTY\_ALLOCATOR\_控制\_捕获\_CAPS 属性会通知的视频端口 （这是捕获支持是否可用） 的捕获功能覆盖 Mixer。

## <span id="ddk_ksproperty_allocator_control_capture_caps_ks"></span><span id="DDK_KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_KS"></span>


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
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_caps_s)"><strong>KSPROPERTY_ALLOCATOR_CONTROL_CAPTURE_CAPS_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

属性值 （操作数据） 是一个 ulong 值，指定是否支持交错的捕获。

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

[**KSPROPERTY\_ALLOCATOR\_控制\_捕获\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksproperty_allocator_control_capture_caps_s)

 

 






