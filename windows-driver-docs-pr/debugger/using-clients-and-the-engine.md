---
title: 使用客户端和引擎
description: 使用客户端和引擎
ms.assetid: 899184f5-334b-4fd1-98ce-64475650ace5
keywords:
- DbgEng 扩展，引擎客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b704ed709cf8beeba05b3fafb19551138eb62601
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368617"
---
# <a name="using-clients-and-the-engine"></a>使用客户端和引擎


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


DbgEng 扩展与交互[调试器引擎](introduction.md#debugger-engine)通过客户端对象。

当调用扩展函数时，它被传递客户端。 扩展函数应使用的所有其交互使用调试器引擎时，此客户端，除非有特定原因要使用另一个客户端。

扩展库可能通过创建其自己的客户端对象时初始化[ **DebugCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugcreate)。 此客户端可用来注册从 DLL 的回调对象。

**请注意**  修改客户端传递到扩展函数时应小心。 具体而言，向此客户端注册回调可能会中断调试器的输入、 输出或事件处理。 建议创建新的客户端，以注册回调。

 

 

 





