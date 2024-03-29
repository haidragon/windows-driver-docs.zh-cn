---
title: errlog
description: Errlog 扩展 I/O 系统错误日志中显示任何挂起的项的内容。
ms.assetid: 2ef6331e-fa83-4515-8d70-5094e40b8497
keywords:
- errlog Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- errlog
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4bb12ea9c8b93cc2bf6e5d3dbb054a0b04dfb24d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362499"
---
# <a name="errlog"></a>!errlog


**！ Errlog**扩展 I/O 系统错误日志中显示的任何挂起的项的内容。

```dbgcmd
!errlog 
```

## <span id="ddk__errlog_dbg"></span><span id="DDK__ERRLOG_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

璝惠[ **IoWriteErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)，请参阅 Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

此命令显示 I/O 系统错误日志中的任何挂起的事件有关的信息。 这些是事件通过调用排队[ **IoWriteErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)函数，以写入到系统的事件日志，以允许进行后续查看**事件查看器**。

已排队的条目[ **IoWriteErrorLogEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iowriteerrorlogentry)但尚未提交的错误，将显示日志。

此命令可作为帮助诊断在系统崩溃后由于它会显示挂起的错误信息，无法将其提交到之前暂停系统的错误日志。

 

 





