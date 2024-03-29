---
title: AllowStandardUserPinUnlock
description: AllowStandardUserPinUnlock
ms.assetid: 3fb6de78-662b-46d0-bf0c-9efde15b0861
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60bc78d534ae988f8569a46bf3fa3ff6f6d2ff7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566249"
---
[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> 开始在 Windows 10 版本 1507年中此元素已被弃用，可能不支持 Windows 的未来版本中。

# <a name="allowstandarduserpinunlock"></a>AllowStandardUserPinUnlock


AllowStandardUserPinUnlock 元素指定是否允许执行标准用户 PIN 解锁操作。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


```syntax
<AllowStandardUserPinUnlock>
  text
</ AllowStandardUserPinUnlock >
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个布尔值的位置 **，则返回 true**允许标准用户执行 PIN 解锁操作并**false**却没有。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有子元素。

## <a name="span-idparentelementsspanspan-idparentelementsspanspan-idparentelementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="networkconfiguration.md" data-raw-source="[NetworkConfiguration](networkconfiguration.md)">NetworkConfiguration</a></p></td>
<td><p>指定的采购和 Internet 移动宽带的配置文件，以使用或标准用户是否可以执行 PIN 解锁操作。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="AllowStandardUserPinUnlock" type="xs:boolean" minOccurs="0" />
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


AllowStandardUserPinUnlock 元素是可选的。

 

 





