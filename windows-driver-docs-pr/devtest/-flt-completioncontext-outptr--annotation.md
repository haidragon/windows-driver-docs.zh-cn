---
title: _Flt_CompletionContext_Outptr_ 注释
description: 使用_Flt_CompletionContext_Outptr_批注声明的文件系统微筛选器预操作回调函数 PFLT_PRE_OPERATION_CALLBACK 时。
ms.assetid: C3B285EA-0DAB-48D4-AE2F-CB4FBB30EF15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 956c70c6386e68c87b9a0b02da10485172c3b61b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364177"
---
# <a name="fltcompletioncontextoutptr-annotation"></a>\_Flt\_CompletionContext\_Outptr\_批注


使用 **\_Flt\_CompletionContext\_Outptr\_** 批注声明文件系统微筛选器预操作回调函数时[ **PFLT\_PRE\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)。 此批注置于*CompletionContext*参数。 此批注指示代码分析工具来检查是否*CompletionContext*适合于 FLT\_PREOP\_回调\_状态返回值。

如果预操作回调函数 ([**PFLT\_PRE\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)) 返回 FLT\_PREOP\_成功\_与\_回调或 FLT\_PREOP\_SYNCHRONIZE *CompletionContext*可能或可能不能为 NULL。 对于任何其他 FLT\_PREOP\_回调\_状态返回值*CompletionContext*必须为 NULL。 *CompletionContext*是从筛选器的预操作回调传递到相应的操作后回调函数的筛选器定义的状态 ([**PFLT\_POST\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback))。 如果筛选器返回 FLT 只调用操作后回调\_PREOP\_成功\_WITH\_回调或 FLT\_PREOP\_从其预操作回调进行同步函数。 如果筛选器未通过任何状态从其预操作的回调函数为其操作后的回调函数*CompletionContext*为 NULL，因此*CompletionContext*中其操作后的回调函数将为 NULL。 每个单独的筛选器决定是否要返回中的状态*CompletionContext*从预操作回调函数，因此，最多每个单独的筛选器知道是否不应看到在*CompletionContext*其操作后的回调函数中。

## <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>示例


下面的示例演示的函数原型[ **PFLT\_PRE\_操作\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)函数调用*SwapPreReadBuffers*. *CompletionContext*参数接收将传递给操作后的回调函数的上下文，并使用声明 **\_Flt\_CompletionContext\_Outptr\_** 批注。

```ManagedCPlusPlus
FLT_PREOP_CALLBACK_STATUS
SwapPreReadBuffers(
    _Inout_ PFLT_CALLBACK_DATA Data,
    _In_ PCFLT_RELATED_OBJECTS FltObjects,
    _Flt_CompletionContext_Outptr_ PVOID *CompletionContext
    );
```

**\_Flt\_CompletionContext\_Outptr\_** specstrings.h 中定义批注。 使用批注可以添加有价值的错误检查，而无需添加到你的代码的开销或复杂程度。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**PFLT\_PRE\_OPERATION\_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_pre_operation_callback)

[**PFLT\_POST\_OPERATION\_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_post_operation_callback)

[Windows 驱动程序的 SAL 2.0 注释](sal-2-annotations-for-windows-drivers.md)





