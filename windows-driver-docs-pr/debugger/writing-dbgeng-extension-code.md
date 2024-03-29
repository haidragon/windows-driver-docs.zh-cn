---
title: 编写 DbgEng 扩展代码
description: 本部分介绍了编写 DbgEng 扩展插件代码
ms.assetid: b1ee686b-986e-46eb-a4bf-93e2de6d1aeb
keywords:
- DbgEng 扩展编写
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41bbdea3bb3257b51ad5fc75edaa3a75b94b620a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369394"
---
# <a name="writing-dbgeng-extension-code"></a>编写 DbgEng 扩展代码


## <span id="ddk_writing_dbgeng_extension_code_dbx"></span><span id="DDK_WRITING_DBGENG_EXTENSION_CODE_DBX"></span>


[DbgEng 扩展](debugger-engine-and-extension-apis.md)命令可以包含的任何标准C++代码。 此外可以包括C++出现在 dbgeng.h 标头文件，此外在 wdbgexts.h 标头文件中出现 C 函数的接口。

如果你想要使用从 wdbgexts.h 函数，则需要定义 KDEXT\_wdbgexts.h 之前包含 64 位。 例如：

```cpp
#define KDEXT_64BIT 
#include wdbgexts.h 
#include dbgeng.h 
```

可以扩展命令中使用的 dbgeng.h 中接口的完整列表，请参阅[调试器引擎参考](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-engine-reference)。

可以扩展命令中使用的 wdbgexts.h 中的函数的完整列表，请参阅[WdbgExts 函数](https://docs.microsoft.com/windows-hardware/drivers/debugger/wdbgexts-functions)。 这些函数的数量显示在 32 位版本和 64 位版本。 通常情况下，64 位版本结束"64"版本和 32 位版本中的有任何数字结束-例如， **ReadIoSpace64**并**ReadIoSpace**。 在调用 wdbgexts.h 函数从 DbgEng 扩展时，应始终使用"64"结尾的函数名称。 这是因为[调试器引擎](introduction.md#debugger-engine)始终使用 64 位指针在内部，而不考虑目标平台。

如果包含 wdbgexts.h DbgEng 扩展中，应调用[ **GetWindbgExtensionApis64** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getwindbgextensionapis64)在你的扩展 DLL 的初始化过程中 (请参阅[ *调用 DebugExtensionInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nc-dbgeng-pdebug_extension_initialize))。

**请注意**  必须尝试从任何调试器扩展调用任何 DbgHelp 或了内部错误的例程。 调用这些例程不受支持，可能会导致各种问题。

 

 

 





