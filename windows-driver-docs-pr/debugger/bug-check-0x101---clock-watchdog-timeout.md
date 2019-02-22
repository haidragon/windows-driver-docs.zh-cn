---
title: Bug 检查 0x101 CLOCK_WATCHDOG_TIMEOUT
description: CLOCK_WATCHDOG_TIMEOUT bug 检查具有的值为 0x00000101，该值指示在已分配的时间间隔内未收到预期的时钟中断辅助处理器上。
ms.assetid: 2e35d8c5-00b3-4722-b596-a76f38eb5179
keywords:
- Bug 检查 0x101 CLOCK_WATCHDOG_TIMEOUT
- CLOCK_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CLOCK_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0ffc724a28bb6996f553e7f6af94eac21c513fd8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541835"
---
# <a name="bug-check-0x101-clockwatchdogtimeout"></a>Bug 检查 0x101:时钟\_监视器\_超时


时钟\_监视器\_超时错误检查的值为 0x00000101。 这表示在分配的时间间隔内未收到预期的时钟中断辅助处理器，在多处理器系统中上。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="clockwatchdogtimeout-parameters"></a>时钟\_监视器\_超时参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>时钟中断的超时间隔，在名义上的时钟计时周期</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>无响应的处理器的处理器控制块 (PRCB) 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

在指定的处理器不处理中断。 通常，当处理器无响应或发生死锁时出现此情况。

 

 



