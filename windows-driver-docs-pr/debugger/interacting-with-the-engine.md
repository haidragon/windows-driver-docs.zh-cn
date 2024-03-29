---
title: 与引擎交互
description: 与引擎交互
ms.assetid: 80f5320f-ed34-4839-a16e-b3ff5d8edbfe
keywords:
- 调试器引擎 API，请使用
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3bd91da45431dca72433f3b9b12c8f5f338d90e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361320"
---
# <a name="interacting-with-the-engine"></a>与引擎交互


### <a name="span-idcommandsandexpressionsspanspan-idcommandsandexpressionsspancommands-and-expressions"></a><span id="commands_and_expressions"></span><span id="COMMANDS_AND_EXPRESSIONS"></span>命令和表达式

调试器引擎 API 提供了执行命令和计算表达式，如键入到 WinDbg 的方法[调试器命令窗口](the-debugger-command-window.md)。 若要执行的调试器命令，使用[ **Execute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-execute)。 或者，若要执行的所有命令在文件中，使用[ **ExecuteCommandFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-executecommandfile)。

该方法[ **Evaluate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-evaluate)将计算表达式使用C++或 MASM 语法。 调试器引擎中要计算表达式-例如所使用的语法**Evaluate**方法--由给定[ **GetExpressionSyntax** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexpressionsyntax) ，可以使用更改[**SetExpressionSyntaxByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexpressionsyntaxbyname)并[ **SetExpressionSyntax**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexpressionsyntax)。 将返回不同的语法识别的调试器数[ **GetNumberExpressionSyntaxes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumberexpressionsyntaxes)，并返回其名称[ **GetExpressionSyntaxNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexpressionsyntaxnames)。

返回的值的类型**Evaluate**由符号和已计算的字符串中使用的常量。 值包含在[**调试\_值**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/ns-dbgeng-_debug_value)结构，并且可以强制转换为使用不同类型[ **CoerceValue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)并[ **CoerceValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-coercevalues)。

### <a name="span-idaliasesspanspan-idaliasesspanaliases"></a><span id="aliases"></span><span id="ALIASES"></span>别名

*别名*都是自动替换时调试器命令和表达式中使用其他字符字符串的字符字符串。 有关别名的概述，请参阅[Using 别名](using-aliases.md)。 调试器引擎具有别名的多个类。

*修复名称的别名*按数字编制索引，它们的名称**美元 u0**，**美元 u1**，...，**美元 u9**。 可以使用设置的值的这些别名[ **SetTextMacro** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-settextmacro)方法，可以使用检索[ **GetTextMacro** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-gettextmacro)方法。

*自动别名*并*名用户为别名*可以具有任何名称。 由调试器引擎定义自动别名，用户通过调试器命令或调试器引擎 API 定义名为用户的别名。 若要定义或删除用户命名的别名，请使用[ **SetTextReplacement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-settextreplacement)方法。 [ **GetTextReplacement** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-gettextreplacement)方法返回的名称和值的自动别名或用户命名的别名。 可以使用删除所有用户命名的别名[ **RemoveTextReplacements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removetextreplacements)方法。 [ **GetNumberTextReplacements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnumbertextreplacements)方法将返回的用户名称和自动别名数; 这可以用于**GetTextReplacement**来循环访问所有这些别名。 [ **OutputTextReplacements** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputtextreplacements)方法将打印的所有用户命名别名，包括其名称和值的列表。

**请注意**  名用户为别名如果用户命名别名未指定相同的名称自动别名，将隐藏自动别名，以便按名称检索值的别名值，将使用名为用户的别名。

 

### <a name="span-idengineoptionsspanspan-idengineoptionsspanengine-options"></a><span id="engine_options"></span><span id="ENGINE_OPTIONS"></span>引擎选项

引擎具有多种选项可控制其行为。 中列出了这些选项[**调试\_ENGOPT\_XXX**](https://docs.microsoft.com/previous-versions/ff541475(v=vs.85))。 返回的[ **GetEngineOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getengineoptions) ，可使用设置[ **SetEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setengineoptions)。 可以使用设置的各个选项[ **AddEngineOptions** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-addengineoptions)和取消设置使用[ **RemoveEngineOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-removeengineoptions)。

### <a name="span-idinterruptsspanspan-idinterruptsspaninterrupts"></a><span id="interrupts"></span><span id="INTERRUPTS"></span>中断

中断是一种方法来强制中断到调试器或指示引擎停止处理当前命令，例如，通过在 WinDbg 中按 Ctrl + Break。

若要请求中断到调试器，或中断调试器的当前任务，请使用[ **SetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setinterrupt)。 若要检查是否已中断，请使用[ **GetInterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getinterrupt)。

**请注意**  调试器扩展从较长的任务时，建议扩展，接下来请**GetInterrupt**定期并停止处理如果请求了中断。

 

请求时中断到调试器，引擎可能会超时，如果需要对目标执行被侵入的情形而言太长。 如果目标是无响应状态，或者被侵入的情形请求被阻止或延迟资源争用，则可以发生此问题。 返回引擎要等待的时间长度[ **GetInterruptTimeout** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getinterrupttimeout) ，可使用设置[ **SetInterruptTimeout**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setinterrupttimeout)。

 

 





