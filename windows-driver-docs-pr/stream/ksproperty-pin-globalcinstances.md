---
title: KSPROPERTY\_PIN\_GLOBALCINSTANCES
description: 客户端使用 KSPROPERTY\_PIN\_GLOBALCINSTANCES 来确定当前的 pin 数的 pin 的最大数目以及 pin 工厂中，此 pin 工厂实例化可以实例化。 此属性为可选项。
ms.assetid: 888b8ddf-aa36-4e2f-a74c-ab4ee693bb36
keywords:
- KSPROPERTY_PIN_GLOBALCINSTANCES 流式处理媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_GLOBALCINSTANCES
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f23ee0e85078b007897d5925dcf73829efd08be9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361095"
---
# <a name="kspropertypinglobalcinstances"></a>KSPROPERTY\_PIN\_GLOBALCINSTANCES


客户端使用 KSPROPERTY\_PIN\_GLOBALCINSTANCES 来确定当前的 pin 数的 pin 的最大数目以及 pin 工厂中，此 pin 工厂实例化可以实例化。 此属性为可选项。

## <span id="ddk_ksproperty_pin_globalcinstances_ks"></span><span id="DDK_KSPROPERTY_PIN_GLOBALCINSTANCES_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_CINSTANCES</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

指定此属性使用 KSP\_PIN，其中**PinId**成员指定 pin 工厂。

KSPIN\_CINSTANCES 是窗体的数据结构：

```cpp
typedef struct {
    ULONG PossibleCount;
    ULONG CurrentCount;
} KSPIN_CINSTANCES;
```

下面是描述每个成员的 KSPIN\_CINSTANCES 结构。

<span id="PossibleCount"></span><span id="possiblecount"></span><span id="POSSIBLECOUNT"></span>**PossibleCount**  
指定的 pin 的 pin 工厂可以实例化的最大数目上的驱动程序或 KSINTANCE\_不确定是否存在无最大值。

<span id="CurrentCount"></span><span id="currentcount"></span><span id="CURRENTCOUNT"></span>**CurrentCount**  
该驱动程序指定 pin 的 pin 工厂已实例化的当前的数目。

在类驱动程序不处理此属性;流微型驱动程序必须提供自己的处理。

KSPROPERTY\_PIN\_GLOBALCINSTANCES 指定绝对当前和最大实例数，通过筛选器的所有实例。 若要确定每个筛选器值，请使用[ **KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)。

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
<td>Ks.h （包括 Ks.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSP\_PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

 

 






