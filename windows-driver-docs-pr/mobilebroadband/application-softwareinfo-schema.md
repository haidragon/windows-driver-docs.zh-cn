---
title: Application (SoftwareInfo)
description: Application (SoftwareInfo)
ms.assetid: 1f16a690-4453-4563-a4b1-44bbd5d02f47
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a95bae273f1e80f50d9b235a5aecf5282fced669
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547902"
---
# <a name="application-softwareinfo"></a>Application (SoftwareInfo)

[!include[MBAE deprecation warning](mbae-deprecation-warning.md)]

应用程序元素指定关联的设备通知处理程序。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Application Id=”tns:ApplicationIdType”>
  Child element
</Application>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>属性</th>
<th>在任务栏的搜索框中键入</th>
<th>必需</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ID</p></td>
<td><p>tns:ApplicationIdType</p></td>
<td><p>是</p></td>
<td><p>应用程序的 ID。</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><a href="devicenotificationhandlers.md" data-raw-source="[DeviceNotificationHandlers](devicenotificationhandlers.md)">DeviceNotificationHandlers</a></p></td>
<td><p>指定设备通知处理程序的列表。</p></td>
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
<td><p><a href="applications.md" data-raw-source="[Applications](applications.md)">Applications</a></p></td>
<td><p>指定在 PC 上检测到操作员的移动宽带硬件时将下载的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD


``` syntax
<xs:element name="Application" type="tns:ApplicationType"/>

<xs:complexType name="ApplicationType">
  <xs:sequence>
    <xs:element name="DeviceNotificationHandlers" type="tns:DeviceNotificationHandlersType" minOccurs="0" />
    <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
  </xs:sequence>
  <xs:attribute name="Id" type="tns:ApplicationIdType" use="required"/>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


应用程序元素是可选的。

 

 





