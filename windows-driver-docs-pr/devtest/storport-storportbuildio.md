---
title: StorPortBuildIo 规则 (storport)
description: 此规则验证，是否 StorPort 微型端口 StorPortBuildIo 例程将返回 FALSE，相关 SRB 未传递给 StartIo。
ms.assetid: C35954F9-9C59-408B-BF80-2B8DCD328F9C
ms.date: 05/21/2018
keywords:
- StorPortBuildIo 规则 (storport)
topic_type:
- apiref
api_name:
- StorPortBuildIo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3934008c94c3735536930c29564f45d1d34b4873
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67391857"
---
# <a name="storportbuildio-rule-storport"></a>StorPortBuildIo 规则 (storport)


此规则验证，如果 StorPort 微型端口**StorPortBuildIo**例程返回**FALSE**，相关 SRB 未传递给**StartIo**。 (在这种情况下，微型端口驱动程序必须通过调用完成 SRB [ **StorPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportnotification)通知类型为**RequestComplete**从**StorPortBuildIo**或其他某个)。

> [!NOTE]
> 此规则测试 StorPort 的正确操作，不微型端口的。

 

|              |          |
|--------------|----------|
| 驱动程序模型 | Storport |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">Static Driver Verifier</a>并指定<strong>StorPortBuildIo</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>

 

 





