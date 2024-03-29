---
title: ServiceIconFile
description: ServiceIconFile
ms.assetid: a35a121d-66a8-485e-ac12-adc653db3572
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 891e257bdac542c3eeee5bcbd6ee7d567db13db8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525323"
---
# <a name="serviceiconfile"></a>ServiceIconFile

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

> [!IMPORTANT]
> 在 Windows 10 版本 1709年及更高版本，此字段已替换为通过 COSA 品牌。 品牌 COSA 中的字段上的说明[规划你的桌面 COSA/APN 数据库提交](planning-your-desktop-cosa-apn-database-submission.md)。 如果你面向的 Windows 10，版本 1709 之前, 的 Windows 版本仍会创建元数据包在本部分中所述。 有关 COSA 详细信息，请参阅[COSA 概述](cosa-overview.md)。 

ServiceIconFile 元素在服务元数据包中指定服务图标文件的名称。 服务图标文件用于显示 Windows 连接管理器中的移动网络运营商 (MNO) 或移动虚拟网络运营商 (MVNO) 的徽标。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<ServiceProvider>
  text
</ServiceProvider>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


没有特性。

## <a name="span-idtextvaluespanspan-idtextvaluespanspan-idtextvaluespantext-value"></a><span id="Text_value"></span><span id="text_value"></span><span id="TEXT_VALUE"></span>文本值


使用图标文件的名称。ICO 扩展。

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
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a></p></td>
<td><p><a href="serviceinfo.md" data-raw-source="[ServiceInfo](serviceinfo.md)">ServiceInfo</a>元素是父元素<a href="serviceinfo-xml-schema.md" data-raw-source="[ServiceInfo XML schema](serviceinfo-xml-schema.md)">ServiceInfo XML 架构</a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="ServiceIconFile" type="tns:ServiceIconFileType" minOccurs="0"/>

<xs:simpleType name="ServiceIconFileType">
  <xs:restriction base="xs:string">
    <xs:pattern value=".+\.ico"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


所需的图标文件大小如下所示：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>256x256:32bit+Alpha（压缩）</p></td>
<td><p>24x24:32bit+Alpha</p></td>
</tr>
<tr class="even">
<td><p>48x48:32bit+Alpha</p></td>
<td><p>24x24:8bit256</p></td>
</tr>
<tr class="odd">
<td><p>48x48:8bit256</p></td>
<td><p>24x24:4bit16</p></td>
</tr>
<tr class="even">
<td><p>48x48:4bit16</p></td>
<td><p>16x16:32bit+Alpha</p></td>
</tr>
<tr class="odd">
<td><p>32x32:32bit+Alpha</p></td>
<td><p>16x16:8bit256</p></td>
</tr>
<tr class="even">
<td><p>32x32:8bit256</p></td>
<td><p>16x16:4bit16</p></td>
</tr>
<tr class="odd">
<td><p>32x32：4 位 16</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>

 

ServiceIconFile 元素标记为可选的架构中。 但是，提交到 Windows 开发人员中心仪表板不带 ServiceIconFile 元素的服务元数据包将被拒绝。

 

 





