---
title: 常规 WIA 实用程序函数
description: 常规 WIA 实用程序函数
ms.assetid: 235c07a1-4903-4df6-b29f-0ecc342782b4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17d0ee16270e306db6abfb9e4bf92b73254f88dc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370599"
---
# <a name="general-wia-utility-functions"></a>常规 WIA 实用程序函数





可以使用以下函数可检索驱动程序项上下文中，从系统注册表中检索信息并将一个字符串。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>函数</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetdrvitemcontext" data-raw-source="[&lt;strong&gt;wiauGetDrvItemContext&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetdrvitemcontext)"><strong>wiauGetDrvItemContext</strong></a></p></td>
<td><p>获取驱动程序项上下文和驱动程序项，（可选）。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetresourcestring" data-raw-source="[&lt;strong&gt;wiauGetResourceString&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetresourcestring)"><strong>wiauGetResourceString</strong></a></p></td>
<td><p>获取资源字符串，将其作为存储<strong>BSTR</strong>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetvalidformats" data-raw-source="[&lt;strong&gt;wiauGetValidFormats&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaugetvalidformats)"><strong>wiauGetValidFormats</strong></a></p></td>
<td><p>调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo" data-raw-source="[&lt;strong&gt;IWiaMiniDrv::drvGetWiaFormatInfo&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetwiaformatinfo)"> <strong>IWiaMiniDrv::drvGetWiaFormatInfo</strong> </a>方法，并使有效格式，使用指定的 TYMED 值的列表。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropinpropspec" data-raw-source="[&lt;strong&gt;wiauPropInPropSpec&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropinpropspec)"><strong>wiauPropInPropSpec</strong></a></p></td>
<td><p>确定此类值的数组中是否包含指定的属性规范标识符 (ID)。 该函数根据需要获取的索引在其中发现的属性规范 ID。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropsinpropspec" data-raw-source="[&lt;strong&gt;wiauPropsInPropSpec&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaupropsinpropspec)"><strong>wiauPropsInPropSpec</strong></a></p></td>
<td><p>确定是否任何属性规范 Id 的列表是否包含在此类值的数组。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetdwordw" data-raw-source="[&lt;strong&gt;wiauRegGetDword&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetdwordw)"><strong>wiauRegGetDword</strong></a></p></td>
<td><p>获取<strong>DWORD</strong>值从<strong>DeviceData</strong>注册表部分。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetstrw" data-raw-source="[&lt;strong&gt;wiauRegGetStr&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaureggetstrw)"><strong>wiauRegGetStr</strong></a></p></td>
<td><p>获取一个字符串值从<strong>DeviceData</strong>注册表部分。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiauregopendataw" data-raw-source="[&lt;strong&gt;wiauRegOpenData&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiauregopendataw)"><strong>wiauRegOpenData</strong></a></p></td>
<td><p>此时将打开<strong>DeviceData</strong>注册表项。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiausetimageitemsize" data-raw-source="[&lt;strong&gt;wiauSetImageItemSize&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiausetimageitemsize)"><strong>wiauSetImageItemSize</strong></a></p></td>
<td><p>计算大小和宽度，以字节为单位的映像，根据当前 WIA_IPA_FORMAT 设置 （在 Microsoft Windows SDK 文档中定义），并将新值写入到相应的属性。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2c" data-raw-source="[&lt;strong&gt;wiauStrC2C&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2c)"><strong>wiauStrC2C</strong></a></p></td>
<td><p>将 ANSI 字符到另一个 ANSI 字符字符串的字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2w" data-raw-source="[&lt;strong&gt;wiauStrC2W&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrc2w)"><strong>wiauStrC2W</strong></a></p></td>
<td><p>将 ANSI 字符串转换为 Unicode 字符串。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2c" data-raw-source="[&lt;strong&gt;wiauStrW2C&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2c)"><strong>wiauStrW2C</strong></a></p></td>
<td><p>将 Unicode 字符串转换为 ANSI 字符串。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2w" data-raw-source="[&lt;strong&gt;wiauStrW2W&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiautil/nf-wiautil-wiaustrw2w)"><strong>wiauStrW2W</strong></a></p></td>
<td><p>将 Unicode 字符串到另一个 Unicode 字符串。</p></td>
</tr>
</tbody>
</table>

 

 

 




