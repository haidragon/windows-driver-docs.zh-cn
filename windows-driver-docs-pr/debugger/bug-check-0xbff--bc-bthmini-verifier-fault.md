---
title: Bug 检查 0xBFF BC_BTHMINI_VERIFIER_FAULT
description: BC_BTHMINI_VERIFIER_FAULT bug 检查具有 0x00000BFF 值。 这指示蓝牙微型端口可扩展驱动程序验证程序已捕获了冲突。
ms.assetid: 4BB54209-89EA-455D-B850-CC2A96A43C87
keywords:
- Bug 检查 0xBFF BC_BTHMINI_VERIFIER_FAULT
- BC_BTHMINI_VERIFIER_FAULT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BC_BTHMINI_VERIFIER_FAULT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c41bc7ecb9b1f81bbcaf3486d40e3a3804907727
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518971"
---
# <a name="bug-check-0xbff-bcbthminiverifierfault"></a>Bug 检查 0xBFF：业务连续性\_BTHMINI\_VERIFIER\_容错


业务连续性\_BTHMINI\_VERIFIER\_故障错误检查的值为 0x00000BFF。 这指示蓝牙微型端口可扩展驱动程序验证程序已捕获了冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="bcbthminiverifierfault-parameters"></a>业务连续性\_BTHMINI\_VERIFIER\_错误参数


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
<td align="left">1</td>
<td align="left"><p>蓝牙验证程序错误的子类型。</p>
<div class="code">
<code>0x1 : An attempt was made to return a packet with type that mis-matched its original request.
                  2 - Returned packet type
                  3 - Expected packet type
                  4 - Reserved
            0x2 : An attempt was made to return an unexpected status code and caused the packet to be discarded.
                  2 - Unexpected return status
                  3 - Reserved
                  4 - Reserved
            0x3 : Incorrect output buffer size was returned to indicate number of bytes written by the lower transport driver.
                  2 - Unexpected buffer size
                  3 - Expected buffer size
                  4 - Reserved</code>
</div></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>



<a name="resolution"></a>分辨率
----------

参数 1 描述冲突的类型。 查看调用堆栈，以确定表现不正常的驱动程序。








