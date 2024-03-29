---
title: HardwareIdList (PackageInfo)
description: HardwareIdList (PackageInfo)
ms.assetid: 32bd11f8-767f-4082-b753-efa9debf23cc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15f45b60560676e26d7c7fcd12879058d1f44646
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554179"
---
# <a name="hardwareidlist-packageinfo"></a>HardwareIdList (PackageInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

HardwareIDList 元素指定服务元数据包的一个或多个硬件标识的字符串。 指定每个字符串[HardwareID](hardwareid.md)元素。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<HardwareIDList>
  child elements
</HardwareIDList>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


必须包含一个或多个[HardwareID](hardwareid.md)元素。

## <a name="span-idchildelementsspanspan-idchildelementsspanspan-idchildelementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


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
<td><p><a href="hardwareid.md" data-raw-source="[HardwareID](hardwareid.md)">HardwareID</a></p></td>
<td><p><a href="hardwareid.md" data-raw-source="[HardwareID](hardwareid.md)">HardwareID</a>元素表示移动网络运营商。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a></p></td>
<td><p><a href="metadatakey.md" data-raw-source="[MetadataKey](metadatakey.md)">MetadataKey</a>元素指定设备元数据包的特性。 例如：</p>
<ul>
<li><p>每个设备支持的硬件函数的标识符。</p></li>
<li><p>特定于语言的区域设置的包中的文本字符串。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="HardwareIDList" type="tns:HardwareIDListType" />

<xs:complexType name="HardwareIDListType">
  <xs:sequence>
    <xs:element name="HardwareID" type="tns:HardwareIDType" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


HardwareIDList 元素是必需的。

 

 





