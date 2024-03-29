---
title: IPrintOemUI2 COM 接口
description: IPrintOemUI2 COM 接口
ms.assetid: 9aee61af-e8e2-4bc4-a17b-783242d1ac1f
keywords:
- IPrintOemUI2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67cad985aaefdcd113809dec7952a9426d60da9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371761"
---
# <a name="iprintoemui2-com-interface"></a>IPrintOemUI2 COM 接口





`IPrintOemUI2` COM 接口扩展[IPrintOemUI COM 接口](iprintoemui-com-interface.md)。 中的所有方法除了**IPrintOemUI**接口，`IPrintOemUI2`接口提供了以下方法。

**请注意**  如果使用的 Windows Vista 版本的 Unidrv 和 Pscript Dll，您可以实现以下方法 Unidrv 或 Pscript5 插件中的 Windows XP 和更高版本的 Windows 操作系统上运行。 Dll 的早期版本支持**IPrintOEM2::HideStandardUI** Pscript5 插件仅中的方法。

 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-documentevent" data-raw-source="[&lt;strong&gt;IPrintOemUI2::DocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-documentevent)"><strong>IPrintOemUI2::DocumentEvent</strong></a></p></td>
<td><p>允许插件的 UI 的核心驱动程序用户界面模块的默认实现替换<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent" data-raw-source="[&lt;strong&gt;DrvDocumentEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentevent)"> <strong>DrvDocumentEvent</strong> </a> DDI。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui" data-raw-source="[&lt;strong&gt;IPrintOemUI2::HideStandardUI&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-hidestandardui)"><strong>IPrintOemUI2::HideStandardUI</strong></a></p></td>
<td><p>允许插件 UI 以指定是否应显示或隐藏标准属性表。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes" data-raw-source="[&lt;strong&gt;IPrintOemUI2::QueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemui2-queryjobattributes)"><strong>IPrintOemUI2::QueryJobAttributes</strong></a></p></td>
<td><p>允许插件的 UI 进行后处理核心驱动程序的结果是在调用后<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes" data-raw-source="[&lt;strong&gt;DrvQueryJobAttributes&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes)"> <strong>DrvQueryJobAttributes</strong> </a> DDI。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅[实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

 

 




