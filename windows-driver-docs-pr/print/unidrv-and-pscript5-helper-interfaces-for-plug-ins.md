---
title: 插件的 Unidrv 和 Pscript5 帮助程序接口
description: 插件的 Unidrv 和 Pscript5 帮助程序接口
ms.assetid: 043a38f7-200c-4f1d-b937-4ddd6e2045dd
keywords:
- IPrintCoreHelperPS
- IPrintCoreHelperUni
- IPrintCoreHelper
- 帮助器接口 WDK 打印机接口 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68ebf1d245e9d043e14293091c517e9b4843c941
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378591"
---
# <a name="unidrv-and-pscript5-helper-interfaces-for-plug-ins"></a>插件的 Unidrv 和 Pscript5 帮助程序接口


因为[IPrintCoreHelperPS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperps)并[IPrintCoreHelperUni](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelperuni)接口继承[IPrintCoreHelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper)接口，所有三个接口共享一组公共的方法。 下表列出了中的帮助程序接口和说明中所有三个接口的方法有并且只有一个接口中的方法有的方法。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>包含在</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConvertStringToPTFormat</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>ConvertDefaultGDLSnapshot</strong></p></td>
<td><p><strong>IPrintCoreHelperUni</strong>仅接口</p></td>
</tr>
<tr class="odd">
<td><p><strong>ConvertGDLSnapshot</strong></p></td>
<td><p><strong>IPrintCoreHelperUni</strong>仅接口</p></td>
</tr>
<tr class="even">
<td><p><strong>CreateInstanceOfMSXMLObject</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumConstrainedOptions</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>EnumFeatures</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnumOptions</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>GetFeatureAttribute</strong></p></td>
<td><p><strong>IPrintCoreHelperPS</strong>仅接口</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetGlobalAttribute</strong></p></td>
<td><p><strong>IPrintCoreHelperPS</strong>仅接口</p></td>
</tr>
<tr class="even">
<td><p><strong>GetOptionAttribute</strong></p></td>
<td><p><strong>IPrintCoreHelperPS</strong>仅接口</p></td>
</tr>
<tr class="odd">
<td><p><strong>GetOption</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="even">
<td><p><strong>SetOptions</strong></p></td>
<td><p>全部</p></td>
</tr>
<tr class="odd">
<td><p><strong>WhyConstrained</strong></p></td>
<td><p>全部</p></td>
</tr>
</tbody>
</table>

 

 

 




