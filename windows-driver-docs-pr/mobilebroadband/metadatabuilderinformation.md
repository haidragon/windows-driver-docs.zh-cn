---
title: MetadataBuilderInformation
description: MetadataBuilderInformation
ms.assetid: 94403994-2165-405e-bfa0-974af8e241fe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6e5f20a8fc4a03a74c32846298d0b4365af7827
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521895"
---
# <a name="metadatabuilderinformation"></a>MetadataBuilderInformation

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

MetadataBuilderInformation 元素指定有关创建设备元数据包的应用程序的信息。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<MetadataBuilderInformation>
  text
  child elements
</MetadataBuilderInformation>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


一个字符串，包含 1 到 256 可打印字符 （含） 之间。

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
<td><p><a href="application-service-schema.md" data-raw-source="[Application](application-service-schema.md)">应用程序</a></p></td>
<td><p><a href="application-service-schema.md" data-raw-source="[Application](application-service-schema.md)">应用程序</a>元素指定应用程序创建的软件的服务元数据包的名称。</p></td>
</tr>
<tr class="even">
<td><p><a href="version.md" data-raw-source="[Version](version.md)">版本</a></p></td>
<td><p><a href="version.md" data-raw-source="[Version](version.md)">版本</a>元素指定应用程序创建的软件的服务元数据包的版本。</p></td>
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
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a></p></td>
<td><p><a href="packageinfo.md" data-raw-source="[PackageInfo](packageinfo.md)">PackageInfo</a>元素是父元素<a href="packageinfo-xml-schema.md" data-raw-source="[PackageInfo XML schema](packageinfo-xml-schema.md)">PackageInfo XML 架构</a>。 PackageInfo 元素的子元素指定设备元数据包的属性。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="MetadataBuilderInformation" type="tns:MetadataBuilderInformationType" minOccurs="0" /> 

<xs:complexType name="MetadataBuilderInformationType">
  <xs:sequence>
  <xs:element name="Application" type="tns:ApplicationType" />
  <xs:element name="Version" type="tns:VersionType" />
  <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
</xs:complexType> 

<xs:simpleType name="ApplicationType">
  <xs:restriction base="xs:string">
  <xs:minLength value="1" />
  <xs:maxLength value="256" />
  </xs:restriction>
</xs:simpleType> 

<xs:simpleType name="VersionType">
   <xs:restriction base="xs:string">
     <xs:minLength value="1" />
     <xs:maxLength value="256" />
   </xs:restriction> 
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


不使用的操作系统的任何组件的 MetadataBuilderInformation 元素。 它被保留供 OEM、 IHV 和 ISV。

 

 





