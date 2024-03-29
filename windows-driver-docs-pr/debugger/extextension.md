---
title: ExtExtension
description: ExtExtension 类是基类C++类表示 EngExtCpp 扩展库。
ms.assetid: 9c6c4633-df49-4f49-8116-d680bb20c3f5
keywords:
- ExtExtension Windows 调试
topic_type:
- apiref
api_name:
- ExtExtension
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d24605444c5472ee2638e23928ce46a5bc9d34da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366829"
---
# <a name="extextension"></a>ExtExtension


**ExtExtension**类是类的基类C++表示 EngExtCpp 扩展库的类。

**ExtExtension**类包括以下方法，可由子类：

[**初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))

[**取消初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff558961(v=vs.85))

[**OnSessionActive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552312(v=vs.85))

[**OnSessionInactive**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552318(v=vs.85))

[**OnSessionAccessible**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552310(v=vs.85))

[**OnSessionInaccessible**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff552315(v=vs.85))

**IsUserMode**

**IsKernelMode**

**IsLiveLocalUser**

**IsMachine32**

**IsCurMachine32**

**IsMachine64**

**IsCurMachine64**

**Is32On64**

**CanQueryVirtual**

**HasFullMemBasic**

**IsExtensionRemote**

**AreOutputCallbacksDmlAware**

**RequireUserMode**

**RequireKernelMode**

[**GetNumUnnamedArgs**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548001(v=vs.85))

[**GetUnnamedArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549464(v=vs.85))

[**GetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549465(v=vs.85))

[**HasUnnamedArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549733(v=vs.85))

[**GetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545586(v=vs.85))

[**GetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff545596(v=vs.85))

[**HasArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549721(v=vs.85))

[**HasCharArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff549727(v=vs.85))

[**SetUnnamedArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556876(v=vs.85))

[**SetUnnamedArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556878(v=vs.85))

[**SetUnnamedArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556879(v=vs.85))

[**SetArg**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556614(v=vs.85))

[**SetArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556618(v=vs.85))

[**SetArgU64**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556622(v=vs.85))

[**GetRawArgStr**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff548226(v=vs.85))

**GetRawArgCopy**

**Out**

**则发出警告**

**Err**

**Verb**

**Dml**

**DmlWarn**

**DmlErr**

**DmlVerb**

**DmlCmdLink**

**DmlCmdExec**

**RefreshOutputCallbackFlags**

**WrapLine**

**OutWrapStr**

**OutWrapVa**

**OutWrap**

**DemandWrap**

**AllowWrap**

**TestWrap**

**RequestCircleString**

**CopyCircleString**

**PrintCircleStringVa**

**PrintCircleString**

**SetAppendBuffer**

**AppendBufferString**

**AppendStringVa**

**AppendString**

**IsAppendStart**

**SetCallStatus**

**GetCachedSymbolTypeId**

**GetCachedFieldOffset**

**GetCachedFieldOffset**

**AddCachedSymbolInfo**

**GetExpr64**

**GetExprU64**

**GetExprS64**

**ThrowCommandHelp**

**ThrowInterrupt**

**ThrowOutOfMemory**

**ThrowContinueSearch**

**ThrowReloadExtension**

**ThrowInvalidArg**

**ThrowRemote**

**ThrowStatus**

**ThrowLastError**

**ExtExtension**类还包含可由子类的以下字段：

```cpp
class ExtExtension
{
public:
    USHORT  m_ExtMajorVersion;
    USHORT  m_ExtMinorVersion;
    ULONG  m_ExtInitFlags;
    ExtKnownStruct *  m_KnownStructs;
    ExtProvidedValue *  m_ProvidedValues;
    ExtCheckedPointer<IDebugAdvanced>  m_Advanced;
    ExtCheckedPointer<IDebugClient>  m_Client;
    ExtCheckedPointer<IDebugControl>  m_Control;
    ExtCheckedPointer<IDebugDataSpaces>  m_Data;
    ExtCheckedPointer<IDebugRegisters>  m_Registers;
    ExtCheckedPointer<IDebugSymbols>  m_Symbols;
    ExtCheckedPointer<IDebugSystemObjects>  m_System;
    ExtCheckedPointer<IDebugAdvanced2>  m_Advanced2;
    ExtCheckedPointer<IDebugAdvanced3>  m_Advanced3;
    ExtCheckedPointer<IDebugClient2>  m_Client2;
    ExtCheckedPointer<IDebugClient3>  m_Client3;
    ExtCheckedPointer<IDebugClient4>  m_Client4;
    ExtCheckedPointer<IDebugClient5>  m_Client5;
    ExtCheckedPointer<IDebugControl2>  m_Control2;
    ExtCheckedPointer<IDebugControl3>  m_Control3;
    ExtCheckedPointer<IDebugControl4>  m_Control4;
    ExtCheckedPointer<IDebugDataSpaces2>  m_Data2;
    ExtCheckedPointer<IDebugDataSpaces3>  m_Data3;
    ExtCheckedPointer<IDebugDataSpaces4>  m_Data4;
    ExtCheckedPointer<IDebugRegisters2>  m_Registers2;
    ExtCheckedPointer<IDebugSymbols2>  m_Symbols2;
    ExtCheckedPointer<IDebugSymbols3>  m_Symbols3;
    ExtCheckedPointer<IDebugSystemObjects2>  m_System2;
    ExtCheckedPointer<IDebugSystemObjects3>  m_System3;
    ExtCheckedPointer<IDebugSystemObjects4>  m_System4;
    ULONG  m_OutputWidth;
    ULONG  m_ActualMachine;
    ULONG  m_Machine;
    ULONG  m_PageSize;
    ULONG  m_PtrSize;
    ULONG  m_NumProcessors;
    ULONG64  m_OffsetMask;
    ULONG  m_DebuggeeClass;
    ULONG  m_DebuggeeQual;
    ULONG  m_DumpFormatFlags;
    bool  m_IsRemote;
    bool  m_OutCallbacksDmlAware;
    ULONG  m_OutMask;
    ULONG  m_CurChar;
    ULONG  m_LeftIndent;
    bool  m_AllowWrap;
    bool  m_TestWrap;
    ULONG  m_TestWrapChars;
    PSTR  m_AppendBuffer;
    ULONG  m_AppendBufferChars;
    PSTR  m_AppendAt;
};
```

## <a name="span-idmembersspanspan-idmembersspanspan-idmembersspanmembers"></a><span id="Members"></span><span id="members"></span><span id="MEMBERS"></span>成员


<span id="m_ExtMajorVersion"></span><span id="m_extmajorversion"></span><span id="M_EXTMAJORVERSION"></span>**m\_ExtMajorVersion**  
扩展库的主版本号。 此属性应设置[**初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))方法。 如果未设置，则默认为**1**。

<span id="m_ExtMinorVersion"></span><span id="m_extminorversion"></span><span id="M_EXTMINORVERSION"></span>**m\_ExtMinorVersion**  
扩展库的次版本号。 此属性应设置[**初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))方法。 如果未设置，则默认为**0** （零）。

<span id="m_ExtInitFlags"></span><span id="m_extinitflags"></span><span id="M_EXTINITFLAGS"></span>**m\_ExtInitFlags**  
DbgEng 扩展初始化标志[*调用 DebugExtensionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_initialize)。

<span id="m_KnownStructs"></span><span id="m_knownstructs"></span><span id="M_KNOWNSTRUCTS"></span>**m\_KnownStructs**  
一个数组[ **ExtKnownStruct** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/engextcpp/ns-engextcpp-extknownstruct)扩展插件库是支持的输出格式设置的结构。 设置此成员[**初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))方法，此方法返回后不应更改。

如果**m\_KnownStructs**不是**NULL**，则**TypeName**的最后一个成员**ExtKnownStruct**数组中的结构必须是**NULL**。

设置格式的输出，目标的结构名称与该结构的类型的名称匹配时**TypeName**之一的成员**ExtKnownStruct**结构此数组中指定的回调函数在中**方法**成员调用来执行格式设置。

<span id="m_ProvidedValues"></span><span id="m_providedvalues"></span><span id="M_PROVIDEDVALUES"></span>**m\_ProvidedValues**  
一个数组**ExtProvidedValue**结构列出伪寄存器，扩展库可以提供的值。 设置此成员[**初始化**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff550945(v=vs.85))方法，此方法返回后不应更改。

如果**m\_ProvidedValues**不是**NULL**，则**ValueName**的最后一个成员**ExtProvidedValue**结构数组必须是**NULL**。

评估伪寄存器中，如果伪名称注册的匹配项时**ValueName**之一的成员**ExtProvidedValue** 中指定的回调函数中此数组结构**方法**成员调用来计算伪寄存器。

<span id="m_Advanced"></span><span id="m_advanced"></span><span id="M_ADVANCED"></span>**m\_高级**  
[ **IDebugAdvanced** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_Client"></span><span id="m_client"></span><span id="M_CLIENT"></span>**m\_客户端**  
[ **IDebugClient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_Control"></span><span id="m_control"></span><span id="M_CONTROL"></span>**m\_Control**  
[ **IDebugControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_Data"></span><span id="m_data"></span><span id="M_DATA"></span>**m\_数据**  
[ **IDebugDataSpaces** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugdataspaces)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_Registers"></span><span id="m_registers"></span><span id="M_REGISTERS"></span>**m\_注册**  
[ **IDebugRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugregisters)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_Symbols"></span><span id="m_symbols"></span><span id="M_SYMBOLS"></span>**m\_符号**  
[ **IDebugSymbols** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbols)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_System"></span><span id="m_system"></span><span id="M_SYSTEM"></span>**m\_系统**  
[ **IDebugSystemObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsystemobjects)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。

<span id="m_Advanced2"></span><span id="m_advanced2"></span><span id="M_ADVANCED2"></span>**m\_Advanced2**  
[ **IDebugAdvanced2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Advanced3"></span><span id="m_advanced3"></span><span id="M_ADVANCED3"></span>**m\_Advanced3**  
[ **IDebugAdvanced3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Client2"></span><span id="m_client2"></span><span id="M_CLIENT2"></span>**m\_Client2**  
[ **IDebugClient2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Client3"></span><span id="m_client3"></span><span id="M_CLIENT3"></span>**m\_Client3**  
[ **IDebugClient3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Client4"></span><span id="m_client4"></span><span id="M_CLIENT4"></span>**m\_Client4**  
[ **IDebugClient4** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Client5"></span><span id="m_client5"></span><span id="M_CLIENT5"></span>**m\_Client5**  
[ **IDebugClient5** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Control2"></span><span id="m_control2"></span><span id="M_CONTROL2"></span>**m\_Control2**  
[ **IDebugControl2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Control3"></span><span id="m_control3"></span><span id="M_CONTROL3"></span>**m\_Control3**  
[ **IDebugControl3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Control4"></span><span id="m_control4"></span><span id="M_CONTROL4"></span>**m\_Control4**  
[ **IDebugControl4** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Data2"></span><span id="m_data2"></span><span id="M_DATA2"></span>**m\_Data2**  
[ **IDebugDataSpaces2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugdataspaces)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Data3"></span><span id="m_data3"></span><span id="M_DATA3"></span>**m\_Data3**  
[ **IDebugDataSpaces3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugdataspaces)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Data4"></span><span id="m_data4"></span><span id="M_DATA4"></span>**m\_Data4**  
[IDebugDataSpaces4](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugdataspaces)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Registers2"></span><span id="m_registers2"></span><span id="M_REGISTERS2"></span>**m\_Registers2**  
[ **IDebugRegisters2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugregisters)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Symbols2"></span><span id="m_symbols2"></span><span id="M_SYMBOLS2"></span>**m\_Symbols2**  
[ **IDebugSymbols2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbols)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_Symbols3"></span><span id="m_symbols3"></span><span id="M_SYMBOLS3"></span>**m\_Symbols3**  
[ **IDebugSymbols3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbols)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_System2"></span><span id="m_system2"></span><span id="M_SYSTEM2"></span>**m\_System2**  
[ **IDebugSystemObjects2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsystemobjects)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_System3"></span><span id="m_system3"></span><span id="M_SYSTEM3"></span>**m\_System3**  
[ **IDebugSystemObjects3** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsystemobjects)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_System4"></span><span id="m_system4"></span><span id="M_SYSTEM4"></span>**m\_System4**  
[ **IDebugSystemObjects4** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsystemobjects)可以使用的扩展插件库在客户端对象的接口指针。 是从外部调用扩展方法的调用期间有效-例如，扩展执行命令时，调用[ *ExtKnownStructMethod* ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff543989(v=vs.85))和**ExtProvideValueMethod**。 此接口不可能的调试器引擎的所有版本中可用。

<span id="m_PtrSize"></span><span id="m_ptrsize"></span><span id="M_PTRSIZE"></span>**m\_PtrSize**  
当前目标上的指针的大小。 如果目标使用 32 位指针**m\_PtrSize**为 4。 如果目标使用 64 位指针**m\_PtrSize**为 8。

<span id="m_AppendBuffer"></span><span id="m_appendbuffer"></span><span id="M_APPENDBUFFER"></span>**m\_AppendBuffer**  
字符缓冲区，用于扩展库中的字符串返回到引擎。 此缓冲区的大小是**m\_AppendBufferChars**。 方法**AppendBufferString**， **AppendStringVa**，并**AppendString**可用于将字符串写入到此缓冲区。

<span id="m_AppendBufferChars"></span><span id="m_appendbufferchars"></span><span id="M_APPENDBUFFERCHARS"></span>**m\_AppendBufferChars**  
大小，以字符为单位的缓冲区**m\_AppendBuffer**。









