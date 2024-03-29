---
title: 将 WPP 宏添加到跟踪提供程序
description: 将 WPP 宏添加到跟踪提供程序
ms.assetid: fc6db47c-ef18-4454-a385-adee1858b9d4
keywords:
- Windows 软件跟踪预处理器 WDK，宏
- WPP 软件跟踪 WDK，宏
- WDK WPP 宏
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac55b640ebc38669e8754de2d192011356a216a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371463"
---
# <a name="adding-wpp-macros-to-a-trace-provider"></a>将 WPP 宏添加到跟踪提供程序


## <span id="ddk_adding_wpp_macros_to_a_driver_tools"></span><span id="DDK_ADDING_WPP_MACROS_TO_A_DRIVER_TOOLS"></span>


若要添加到 WPP 软件跟踪的默认窗体[跟踪提供程序](trace-provider.md)，如内核模式驱动程序或用户模式应用程序，添加以下 C 预处理器指令和 WPP 宏调用提供程序的源代码：

-   **\#包括**以下形式向每个源文件，其中包含任何 WPP 宏的指令。 此语句包含[跟踪消息标头文件](trace-message-header-file.md)创建的[WPP 预处理器](wpp-preprocessor.md)为每个源文件：

    ```
    #include <source-file-name.tmh>
    ```

    跟踪消息标头文件必须包含在源文件 WPP 宏的任何调用之前和之后定义[WPP\_控制\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))宏。

-   一个[WPP\_控制\_GUID](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556186(v=vs.85))定义每个源文件包含其他 WPP 宏指令。

    此定义指定驱动程序的控件 GUID 和驱动程序定义的跟踪标志名称。 定义必须添加到源代码文件之前 **\#包括** 语句包括文件的跟踪消息标头文件。

-   一个[WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))宏调用驱动程序的源代码。

    有关驱动程序，此宏将激活软件驱动程序中的跟踪。 此宏是通常驱动程序在初始化期间调用，例如[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。

    对于用户模式应用程序，调用此宏其中不跟踪以前尝试的源代码中的某个位置。

    初始化后，可以使用[TraceView](traceview.md)或[Tracelog](tracelog.md)启动软件跟踪会话，并显示跟踪消息。

-   一个[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))宏调用[跟踪提供程序的](trace-provider.md)源代码。 此宏将停用软件驱动程序中的跟踪。

    驱动程序，此宏调用通常添加到驱动程序的[ **Unload** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程。

    对于用户模式应用程序，此宏在源代码中的某个位置后调用的最后一个跟踪尝试进行。

-   [**DoTraceMessage** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff544918(v=vs.85))宏调用来记录跟踪消息。

 

 





