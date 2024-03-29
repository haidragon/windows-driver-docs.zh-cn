---
title: 编写 FilterUnloadCallback 例程
description: 编写 FilterUnloadCallback 例程
ms.assetid: 2f680770-38af-4dcb-93b8-7f770e0378b2
keywords:
- FilterUnloadCallback
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4f51a4030d43efaaa88bf76e3ba4c57e861666e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385653"
---
# <a name="writing-a-filterunloadcallback-routine"></a>编写 FilterUnloadCallback 例程


## <span id="ddk_writing_a_filterunloadcallback_routine_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


*FilterUnloadCallback*例程定义，如下所示：

```cpp
typedef NTSTATUS
(*PFLT_FILTER_UNLOAD_CALLBACK) (
    FLT_FILTER_UNLOAD_FLAGS Flags
    );
```

*FilterUnloadCallback*例程具有一个输入的参数*标志*，可以是**NULL**或 FLTFL\_筛选器\_卸载\_必需。 筛选器管理器将此参数设置为 FLTFL\_筛选器\_卸载\_强制性来指示卸载操作是必需。 有关此参数的详细信息，请参阅[ **PFLT\_筛选器\_卸载\_回调**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nc-fltkernel-pflt_filter_unload_callback)。

微筛选器驱动程序*FilterUnloadCallback*例程必须执行以下步骤：

-   关闭任何打开的内核模式下通信服务器端口句柄。

-   调用[ **FltUnregisterFilter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltunregisterfilter)注销微筛选器驱动程序。

-   执行任何所需的全局清除。

-   返回适当的 NTSTATUS 值。

本部分包括：

[关闭通信服务器端口](closing-the-communication-server-port.md)

[取消注册微筛选器](unregistering-the-minifilter.md)

[执行全局清理](performing-global-cleanup.md)

[从 FilterUnloadCallback 例程返回状态](returning-status-from-a-filterunloadcallback-routine.md)

 

 




