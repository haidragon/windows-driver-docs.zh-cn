---
title: IWiaLog COM 接口
description: IWiaLog COM 接口
ms.assetid: e5d42b5d-796f-42f3-9c01-4234b8765ca6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80cda9b71779f3686c99dd1ca97c48e1cbff8231
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378895"
---
# <a name="iwialog-com-interface"></a>IWiaLog COM 接口





[ **IWiaLog 接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nn-wia_lh-iwialog)过时中 Microsoft Windows XP 及更高版本，并且不再受支持。 改为使用 WIA 的诊断日志宏。

用于向后兼容性。 此接口中的方法允许微型驱动程序错误、 跟踪和警告消息写入日志。 **IWiaLog**接口提供了以下方法。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-initializelog" data-raw-source="[&lt;strong&gt;IWiaLog::InitializeLog&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-initializelog)"><strong>IWiaLog::InitializeLog</strong></a></p></td>
<td><p>初始化日志记录实用程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-log" data-raw-source="[&lt;strong&gt;IWiaLog::Log&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-log)"><strong>IWiaLog::Log</strong></a></p></td>
<td><p>记录到文件或其他目标的一条消息。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-hresult" data-raw-source="[&lt;strong&gt;IWiaLog::hResult&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wia_lh/nf-wia_lh-iwialog-hresult)"><strong>IWiaLog::hResult</strong></a></p></td>
<td><p>将字符串转换为 HRESULT。</p></td>
</tr>
</tbody>
</table>

 

有关此接口的详细信息，请参阅[IWiaLog 界面和诊断日志宏](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)。

 

 




