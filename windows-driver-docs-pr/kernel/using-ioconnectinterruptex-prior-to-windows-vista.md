---
title: 使用 Windows Vista 以前的 IoConnectInterruptEx
description: 使用 Windows Vista 以前的 IoConnectInterruptEx
ms.assetid: a08b2869-93f8-440b-9fbe-068604c6007d
keywords:
- IoConnectInterruptEx
- iointex.h
- 基于行的中断 WDK 内核
- 消息信号中断 WDK 内核
- CONNECT_LINE_BASED
- CONNECT_MESSAGE_BASED
- CONNECT_FULLY_SPECIFIED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21f8ef9078271bf00db99b62aabc2f8ca61586f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381618"
---
# <a name="using-ioconnectinterruptex-prior-to-windows-vista"></a>使用 Windows Vista 以前的 IoConnectInterruptEx


用于 Windows 2000、 Windows XP 或 Windows Server 2003 的驱动程序可以链接到要使用的 Iointex.lib 库[ **IoConnectInterruptEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterruptex)在这些版本的操作系统上。

若要使用**IoConnectInterruptEx**中此类驱动程序，包括 Iointex.h 为您的驱动程序，紧跟 wdm.h 中或 Ntddk.h 源代码中。 Iointex.h 标头声明该例程的原型。 生成您的驱动程序时，请确保它以静态方式链接到 Iointex.lib。

对于 Windows Vista，版本之前的操作系统**IoConnectInterruptEx** Iointex.lib 仅支持由提供连接\_完全\_例程的指定版本。 如果指定任何其他版本，该例程返回 NTSTATUS 错误代码，并设置*参数*-&gt;**版本**连接到\_完全\_指定。

使用此行为，您可以编写您的驱动程序，使其使用 CONNECT\_行\_基于或 CONNECT\_消息\_基于 Windows Vista 和连接\_完全\_前面指定上操作系统。 第一次调用**IoConnectInterruptEx**与*参数*-&gt;**版本**等于 CONNECT\_行\_基于或连接\_消息\_基于。 如果返回值是一个错误代码和*参数*-&gt;**版本**！ = CONNECT\_完全\_指定，然后重试该操作与*参数*-&gt;**版本**设置为连接\_完全\_指定。

下面的代码示例说明了该技术：

```cpp
IO_CONNECT_INTERRUPT_PARAMETERS params;

// deviceExtension is a pointer to the driver's device extension. 
//     deviceExtension->MessageUsed is a BOOLEAN.

RtlZeroMemory( &params, sizeof(IO_CONNECT_INTERRUPT_PARAMETERS) );
params.Version = CONNECT_MESSAGE_BASED;

// Set members of params.MessageBased here.

status = IoConnectInterruptEx(&params);

if ( NT_SUCCESS(status) ) {
    // Operation succeeded. We are running on Windows Vista.
    devExt->MessageUsed = TRUE; // We save this for posterity.
} else {
    // Check to see if we are running on an operating system prior to Windows Vista.
    if (params.Version == CONNECT_FULLY_SPECIFIED) {
        devExt->MessageUsed = FALSE;  // We're not using message-signaled interrupts.
 
        // Set members of params.FullySpecified here.
 
        status = IoConnectInterruptEx(&params);
    } else {
        // Other error.
    }
}
```

 

 




