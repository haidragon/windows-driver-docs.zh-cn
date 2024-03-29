---
title: 有关日志中记录跟踪的即时跟踪记录器 (IFR)
description: 即时跟踪记录器 (IFR) 是一个新的跟踪功能，允许跟踪提供程序，如内核模式驱动程序，以获取最少的设置的跟踪日志并创建一组保留的最新的 WPP 日志消息的内存中缓冲区。
ms.assetid: D11FA28E-3B0C-4D9D-AEDA-8A80DE58091C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d3dafaf8fdff305a2feb503336051775f8fac53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363778"
---
# <a name="inflight-trace-recorder-ifr-for-logging-traces"></a>有关日志中记录跟踪的即时跟踪记录器 (IFR)


**摘要**

-   如何启用即时跟踪在 Visual Studio 中的录制器
-   如何将跟踪消息发送到 WPP 默认日志或自定义日志
-   如何在调试器中查看跟踪消息

**适用于：**

-   最低操作系统：对于 KMDF 和 WDM 驱动程序开发人员的 Windows 8
-   最低操作系统：(2.15) UMDF 驱动程序开发人员的 Windows 10

**重要的 API**

-   [**WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))
-   [**WppRecorderLogCreate （仅限内核模式驱动程序）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)
-   [**WppRecorderDumpLiveDriverData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderdumplivedriverdata)

*即时跟踪记录器 (IFR)* 是新的跟踪功能，允许跟踪提供程序，如内核模式驱动程序，以获取最少的设置的跟踪日志并创建一组保留的最新的 WPP 日志消息的内存中缓冲区。

Windows 提供多种机制让你可以帮助您诊断和调试在开发过程中您的驱动程序的问题的驱动程序添加跟踪消息。 一种机制是[WPP 软件跟踪](wpp-software-tracing.md)。 它包括[WPP 预处理器](wpp-preprocessor.md)允许跟踪提供程序将具有较小的内存需求量的 printf 样式跟踪消息。 但是，若要查看的跟踪消息的日志，提供程序必须为启用，跟踪控制器等[TraceView](traceview.md)或[Tracelog](tracelog.md)必须停止并启动跟踪会话才能创建日志，然后，使用者，如 TraceView 必须设置格式并显示日志。

Windows 10 引入了一项新功能：利用 WPP 基础结构的 IFR。 如果该驱动程序启用 WPP 跟踪和 IFR，跟踪日志记录会自动打开，并且你可以轻松地查看消息，而无需启动或停止跟踪会话。

IFR 从驱动程序，名为的非分页池分配的内存的一个页*默认日志*。 日志收集跟踪消息发送的驱动程序，并可以在内核调试器中查看缓冲区的输出，该驱动程序运行时。 发生故障时可以在转储获取最新的跟踪消息。 无需重新构造崩溃只是为了收集跟踪数据。

默认日志是有益的主要是因为该驱动程序可以获取具有最小配置的跟踪日志。 请务必注意，驱动程序已不能控制默认日志的大小。 因为所有跟踪消息都发送到一个循环缓冲区，最新消息覆盖更早的消息，而不考虑的信息的级别。 可能的可以错过一条错误消息，并只能看到信息性消息。

若要获取更好地控制日志代码，IFR 使驱动程序来创建和管理自定义的缓冲区。

**请注意**唯一内核模式驱动程序 （KMDF 和 WDM） 可以在此版本的 Windows 中，创建自定义的缓冲区。 UMDF 驱动程序不能创建自定义的缓冲区。



-   该驱动程序可以用于不同目的创建多个缓冲区，以便详细记录器填缓冲区未满。
-   该驱动程序可以控制的自定义的缓冲区，错误分区 （稍后讨论） 自定义的缓冲区的大小。
-   该驱动程序可以指定自定义日志的字符串标识符。 在查看跟踪消息，您可以区分从不同的缓冲区的消息。
-   由于 IFR 基于 WPP，即使使用 IFR 启用驱动程序，因此您可以查看在 WPP 消息[TraceView](traceview.md)。 但是，若要查看这些消息，必须启用跟踪提供程序并启动会话。

**重要须知**  
IFR 中的消息没有与之关联的时间戳。

只能在 Windows 调试器中查看跟踪消息。



## <a name="span-idbeforeyoubeginspanspan-idbeforeyoubeginspanspan-idbeforeyoubeginspanbefore-you-begin"></a><span id="Before_you_begin..."></span><span id="before_you_begin..."></span><span id="BEFORE_YOU_BEGIN..."></span>开始之前...


-   自己应熟悉[WPP 软件跟踪](wpp-software-tracing.md)如[将 WPP 软件跟踪添加到您的驱动程序](adding-wpp-software-tracing-to-a-windows-driver.md)并[声明和调用 WPP 宏](adding-wpp-macros-to-a-trace-provider.md)。
-   阅读此博客文章[如何包括和驱动程序的公共 PDB 文件中查看 WPP 跟踪消息](https://techcommunity.microsoft.com/t5/Microsoft-USB-Blog/bg-p/MicrosoftUSBBlog/archive/2013/06/29/wpp-blog-post.aspx)。
-   研究 toaster 示例。 已修改它来演示如何启用 IFR 并使用它。 有关详细信息，请参阅[Toaster 示例驱动程序](https://go.microsoft.com/fwlink/p/?LinkId=617723)。

## <a name="span-idenablewppsoftwaretracingspanspan-idenablewppsoftwaretracingspanspan-idenablewppsoftwaretracingspanenable-wpp-software-tracing"></a><span id="Enable_WPP_software_tracing"></span><span id="enable_wpp_software_tracing"></span><span id="ENABLE_WPP_SOFTWARE_TRACING"></span>启用 WPP 软件跟踪


可以配置您的驱动程序以使用 IFR 之前，必须首先设置您的驱动程序作为 WPP[跟踪提供程序](trace-provider.md)。

-   如果使用 Visual Studio 中提供的 WDF 驱动程序模板创建您的驱动程序，则启用 WPP 跟踪。 在项目属性中查看与跟踪相关的设置。

    1.  在 Visual Studio 中，右键单击你想要启用的解决方案资源管理器中，单击该项目**属性。**
    2.  为你想要支持 （例如，所有配置和所有平台） 的生成目标设置的配置和平台。
    3.  在项目属性页中，选择**配置属性**然后单击**WPP 跟踪**。
    4.  下**常规**，单击**运行 Wpp 跟踪**，选择**是**从下拉列表菜单，然后单击**确定**。

        ![启用 visual studio 中的 wpp 软件跟踪](images/wpp-enable.png)

    5.  下**文件选项**，设置的值**扫描配置数据**到包含跟踪信息文件的名称调试跟踪相关的函数定义和宏。 在此示例中，定义位于 Trace.h。

        ![启用 visual studio 中的 wpp 软件跟踪](images/wpp-enable2.png)

-   如果不使用 WDF 驱动程序模板之一，设置 WPP 软件跟踪。 创建头文件 （类似于 trace.h WDF 模板附带）。 该标头文件包含 WPP 宏 ([WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))， [WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))) 和 WPP 控制标志和跟踪消息语句。 有关说明，请参阅[添加到 Windows 驱动程序 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)。

    请确保执行这些任务：

    -   为您的驱动程序将 GUID 定义为跟踪提供程序。

        **语法 WPP\_控制\_GUID**

        ```ManagedCPlusPlus
        #define WPP_CONTROL_GUIDS \
            WPP_DEFINE_CONTROL_GUID(GUIDFriendlyName, (ControlGUID),  \
                WPP_DEFINE_BIT(NameOfTraceFlag1)  \
                WPP_DEFINE_BIT(NameOfTraceFlag2)  \
                .............................   \
                .............................   \
                WPP_DEFINE_BIT(NameOfTraceFlag31) 
        ```

    -   将打印跟踪语句的源文件中包括跟踪标头文件 （在此示例中，Trace.h）。
    -   包括[跟踪消息格式](trace-message-format-file.md)源文件，与关联的文件 ( *&lt;源文件&gt;* .tmh) 包含要打印的跟踪消息的源代码文件中。
        ```ManagedCPlusPlus
        #include "trace.h"
        //
        // This tmh is generated by the WPP Preprocessor.
        //
        #include "MyDriver.tmh"
        ```

    -   初始化在 WPP [DriverEntry](28131-driverentry-saving-pointer-to-buffer.md)的您的驱动程序。
        ```ManagedCPlusPlus
        //
        // WPP Initialization
        //
        WPP_INIT_TRACING(DriverObject, RegistryPath);

        ```

    -   释放 WPP 驱动程序卸载方法中的资源。
        ```ManagedCPlusPlus
        //
        // WPP release resources
        //

        WPP_CLEANUP( DriverObject) );
        ```

## <a name="span-idstep2spanspan-idstep2spanenable-ifr"></a><span id="step_2"></span><span id="STEP_2"></span>启用 IFR


将 WPP 软件跟踪添加到您的驱动程序之后, IFR 基础结构已到位。 只需在项目属性中启用该功能。

1.  在 Visual Studio 中，右键单击你想要启用的解决方案资源管理器中，单击该项目**属性。**
2.  为你想要支持 （例如，所有配置和所有平台） 的生成目标设置的配置和平台。
3.  在项目属性页中，单击**配置属性**然后单击**WPP 跟踪**。
4.  下**函数和宏选项**，单击**启用 WPP 记录器**，选择**是**从下拉列表菜单，然后单击**确定**。

    这将定义**启用\_WPP\_记录器**编译器标志还将启用 DLL 宏 ( **-dll** UMDF 驱动程序和**公里**对于 KMDF驱动程序）。

    即使使用启用 IFR，WPP 消息仍可以记录而无需使用 IFR 使用 Traceview 包含在 Windows Driver Kit (WDK) 之类的工具。

    ![启用 visual studio 中的 wpp 记录器](images/wpp-enable3.png)

5.  链接具有 WppRecorder.lib 的驱动程序项目。

    1.  在项目属性中，单击**配置属性**然后单击**链接器**。
    2.  下**输入**，添加 **$(DDK\_LIB\_路径)\\wpprecorder.lib**到**附加依赖项**字段。

    ![启用 visual studio 中的 wpp 记录器](images/wpp-enable4.png)

6.  添加**Wpprecorder.h**调用 IFR Api，如每个源文件[ **WppRecorderLogCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)设置你自己 IFR 日志。 调用后的 Api [WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))中调用*DriverEntry* KMDF 或 UMDF 2.15 驱动程序的例程。

## <a name="span-idusethedefaultlogspanspan-idusethedefaultlogspanspan-idusethedefaultlogspanuse-the-default-log"></a><span id="Use__the_default_log"></span><span id="use__the_default_log"></span><span id="USE__THE_DEFAULT_LOG"></span>使用默认日志


为驱动程序项目启用 WPP 后，WPP 创建默认日志。 WPP 打印的默认日志的缓冲区大小为 4096 个字节。 对于调试版本，缓冲区是 24576 字节。

如果默认日志缓冲区分配失败，跟踪消息发送到 WPP。 也就是说，通过 IFR，则不记录跟踪消息，但跟踪仍被视为实时 WPP 跟踪。 若要确定是否已创建的默认日志，该驱动程序必须调用[ **WppRecorderIsDefaultLogAvailable**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn914614(v=vs.85))。 如果默认的日志不存在，该驱动程序想要使用 IFR，驱动程序必须创建一个日志。 有关详细信息，请参阅[创建自定义日志](#create)。

1.  初始化[**记录器\_配置\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_configure_params)通过调用结构[**记录器\_配置\_PARAMS\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-recorder_configure_params_init)。 宏集**CreateDefaultLog**成员为 TRUE，指示该驱动程序想要使用的默认日志。
2.  调用[ **WppRecorderConfigure** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderconfigure)通过指定的地址初始化[**记录器\_配置\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_configure_params)结构。
3.  可以获取记录器\_日志不透明句柄通过调用的默认日志[ **WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))。
4.  通过调用 Trace.h 中声明的跟踪宏打印到默认日志的跟踪消息。 有关详细信息，请参阅[定义跟踪函数](#define)。
5.  查看跟踪在调试器中的消息。 有关详细信息，请参阅[中查看跟踪消息](#view)。

**请注意**若要禁用默认的日志，设置**CreateDefaultLog**的成员[**记录器\_配置\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_configure_params)到为 FALSE，然后调用[ **WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderconfigure)。



在此示例中，该驱动程序获取的句柄的默认日志。

```ManagedCPlusPlus

NTSTATUS
DriverEntry(
_In_ PDRIVER_OBJECT  DriverObject,
_In_ PUNICODE_STRING RegistryPath
)
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    RECORDER_CONFIGURE_PARAMS recorderConfig;

    RECORDER_LOG logHandle = NULL;

        // Initialize WPP Tracing.

    WPP_INIT_TRACING(DriverObject, RegistryPath);

    // If a default log is available, store the handle to the default log.

    if (WppRecorderIsDefaultLogAvailable())
    {
        RECORDER_CONFIGURE_PARAMS_INIT(&recorderConfig);

        WppRecorderConfigure(&recorderConfig);

        logHandle = WppRecorderLogGetDefault();

    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = KMDFWPPEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
        KMDFWPPEvtDeviceAdd
        );

    status = WdfDriverCreate(DriverObject,
        RegistryPath,
        &attributes,
        &config,
        WDF_NO_HANDLE
        );

    if (!NT_SUCCESS(status)) {
        PrintEvents(logHandle, TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

## <a name="span-idcreatespanspan-idcreatespancreate-a-custom-log-kernel-mode-drivers-only"></a><span id="create"></span><span id="CREATE"></span>创建自定义日志 （仅限内核模式驱动程序）


IFR 的默认日志使用 4096 非分页缓冲池内存块。 所有跟踪消息都写入一个循环缓冲区。 有时，最新的消息可以覆盖以前的消息。

例如，您的驱动程序有单独的数据流路径用来控制和数据传输请求。 如果从这两个活动记录到同一缓冲区，最有可能，控制跟踪消息将被覆盖的数据传输消息。 在这种情况下，你可以配置这些请求的单独缓冲区。

在另一个示例中，有两个设备，并将其一台设备发送多个其他的详细跟踪消息。 如果驱动程序使用的默认日志，设备可能会导致缓冲区，并从另一台设备的消息可被删除。 相反，驱动程序可以创建两个自定义日志，以便每个设备可以将消息发送到其缓冲区，并可以单独查看从每个设备的消息。

1.  初始化[**记录器\_日志\_创建\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_log_create_params)结构通过调用[**记录器\_日志\_创建\_PARAMS\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-recorder_log_create_params_init)。 WPP 使用的默认日志参数，除非修改结构的成员。
2.  可选。 设置**TotalBufferSize**成员添加到所需的大小。 默认情况下的大小设置为 1024 个字节 (请参阅记录器\_日志\_默认\_缓冲区\_Wpprecorder.h 大小)。
    **请注意**WPP 日志从非页面缓冲池分配缓冲区。 日志被划分为两个循环缓冲区调用分区： 常规和错误。 错误分区仅显示跟踪的消息\_级别\_错误。 与所有其他级别相关的消息发送到常规分区。 设计分区以防止详细跟踪提供程序覆盖低优先级的消息与自己的错误消息。 调用方指定的缓冲区大小**TotalBufferSize**，指示这些分区的总大小。 错误分区不能超过总缓冲区大小的一半。 在初始化之后修改的缓冲区大小。



3.  可选。 设置**LogIdentifier**为一个字符串，可帮助你识别此缓冲区中的跟踪消息。 字符串不得超过 16 个字符的长度。
4.  调用[ **WppRecorderLogCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)通过指定的地址填充[**记录器\_日志\_创建\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_log_create_params)结构。
5.  跟踪消息打印到此新的缓冲区通过调用跟踪宏并传递记录器\_接收的日志句柄[ **WppRecorderLogCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)调用。
6.  查看跟踪在调试器中的消息。 有关详细信息，请参阅[中查看跟踪消息](#view)。

在系统注册表中定义最大和最小缓冲区大小。 您可以相应地设置这些值以节省内存并配置日志记录功能。

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\<serviceName>\Parameters
   WppRecorder_PerBufferMinBytes
   Data type
   REG_DWORD
   Description
   The minimum number of bytes that can be allocated to a  log buffer.  The default is 256 bytes.

   WppRecorder_PerBufferMaxBytes
   Data type
   REG_DWORD
   Description
   The maximum number of bytes that can be allocated to a  log buffer.  The default is 8192 bytes.

   LogPages
   Data type
   REG_DWORD
   Description
   The number of pages to store the default log. The default is 1.

   VerboseOn
   Data type
   REG_DWORD
   Description
   By default (0), IFR only logs errors, warnings, and informational events. Setting this value to 1 adds the verbose output to get logged. 
```

如果在指定的大小[**记录器\_日志\_创建\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_log_create_params)的最小字节数少于[ **WppRecorderLogCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)分配**WppRecorder\_PerBufferMinBytes**字节。 同样，如果大小超过最大值**WppRecorderLogCreate**分配**WppRecorder\_PerBufferMaxBytes**字节。

若要删除自定义日志，请调用[ **WppRecorderLogDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogdelete)之前调用[WPP\_清理](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556179(v=vs.85))。 线程进入此函数后，所有线程必须不登录到此缓冲区不再。 您可以在调用此函数[ *EvtDriverUnload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_unload)驱动程序的实现。

此示例代码是驱动程序的驱动程序入口函数的代码段。 在此示例中，该驱动程序禁用默认日志、 创建自定义日志，并设置其缓冲区大小和标识符。

```ManagedCPlusPlus
ULONG MyDriverLogSize = 8 * 1024;

NTSTATUS
DriverEntry(
_In_ PDRIVER_OBJECT  DriverObject,
_In_ PUNICODE_STRING RegistryPath
)
{
    WDF_DRIVER_CONFIG config;
    NTSTATUS status;
    WDF_OBJECT_ATTRIBUTES attributes;

    RECORDER_CONFIGURE_PARAMS recorderConfig;

    RECORDER_LOG_CREATE_PARAMS recorderCreate;

    RECORDER_LOG logHandle = NULL;

    // Initialize WPP Tracing.

    WPP_INIT_TRACING(DriverObject, RegistryPath);
    // If a default log is available, then configure the size of the buffer.
    // Store the handle to the default log and use it to set the identifier name.

    RECORDER_CONFIGURE_PARAMS_INIT(&recorderConfig);

    recorderConfig.CreateDefaultLog = FALSE;

    RECORDER_LOG_CREATE_PARAMS_INIT(&recorderCreate, NULL);
    recorderCreate.TotalBufferSize = MyDriverLogSize;
    RtlStringCbPrintfA(recorderCreate.LogIdentifier,
        RECORDER_LOG_IDENTIFIER_MAX_CHARS,
        "KMDFWpp_Log");

    status = WppRecorderLogCreate(&recorderCreate, &logHandle);
    if (!NT_SUCCESS(status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DRIVER, "WppRecorderLogCreate failed %!STATUS!", status);
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Entry");

    //
    // Register a cleanup callback so that we can call WPP_CLEANUP when
    // the framework driver object is deleted during driver unload.
    //
    WDF_OBJECT_ATTRIBUTES_INIT(&attributes);
    attributes.EvtCleanupCallback = KMDFWPPEvtDriverContextCleanup;

    WDF_DRIVER_CONFIG_INIT(&config,
        KMDFWPPEvtDeviceAdd
        );

    status = WdfDriverCreate(DriverObject,
        RegistryPath,
        &attributes,
        &config,
        WDF_NO_HANDLE
        );

    if (!NT_SUCCESS(status)) {
        PrintEvents(logHandle, TRACE_LEVEL_ERROR, TRACE_DRIVER, "WdfDriverCreate failed %!STATUS!", status);
        WPP_CLEANUP(DriverObject);
        return status;
    }

    PrintEvents(logHandle, TRACE_LEVEL_INFORMATION, TRACE_DRIVER, "%!FUNC! Exit");

    return status;
}
```

## <a name="span-iddefinespanspan-iddefinespandefine-trace-functions"></a><span id="define"></span><span id="DEFINE"></span>定义跟踪函数


添加具有"IFRLOG"作为输入参数的跟踪函数 （在你 Trace.h)。 有关跟踪宏的信息，请参阅[对 Windows 驱动程序添加 WPP 软件跟踪](adding-wpp-software-tracing-to-a-windows-driver.md)。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define our
// Trace function.
//
// begin_wpp config
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC PrintEvents(IFRLOG, LEVEL, FLAGS, MSG, ...);
// end_wpp
//
```

在上述示例中，有两个跟踪函数，TraceEvents 和 PrintEvents。 WPP 与函数声明中指定的参数生成用于这些函数的宏。 在使用本主题中的示例，该驱动程序使用 TraceEvents 和 PrintEvents。 PrintEvents 需要"IFRLOG"作为参数。 该驱动程序调用此函数时，必须指定记录器\_日志句柄作为"IFRLOG"的参数值。 仅当你创建的自定义缓冲区添加 IFRLOG。 TraceEvents 将打印到默认日志。 这在功能提供了向后兼容现有的跟踪语句，而无需任何更改。

若要打印到默认日志的跟踪消息，该驱动程序或者调用 PrintEvents 使用收到的句柄[ **WppRecorderLogGetDefault** ](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))调用，或调用 TraceEvents，而该句柄。

若要打印到自定义日志，驱动程序通过对的调用中收到的句柄[ **WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)。

## <a name="span-idmaketracemessagesavailableinpublicsymbolsspanspan-idmaketracemessagesavailableinpublicsymbolsspanspan-idmaketracemessagesavailableinpublicsymbolsspanmake-trace-messages-available-in-public-symbols"></a><span id="Make__trace_messages_available_in_public_symbols"></span><span id="make__trace_messages_available_in_public_symbols"></span><span id="MAKE__TRACE_MESSAGES_AVAILABLE_IN_PUBLIC_SYMBOLS"></span>使跟踪消息可在公共符号


在 WPP，[跟踪消息格式](trace-message-format-file.md)查看实际 WPP 消息所需的信息。 该信息存储在私有符号文件 (Pdb)。 TMF 信息自动包含在私有 PDB，但不是公共的 PDB。 因此，你无法查看消息，而无需专用 PDB。 若要将跟踪消息添加到你的公共 PDB，

若要使公开，其中某些 WPP 跟踪消息，必须将特殊标记添加到每个消息中。 添加`// WPP_FLAGS(-public:<trace function name>)`后 Trace.h 文件中的定义。 由带标记 **– 公共**切换 WPP 命令行中。 开关添加到 WPP 预处理器，以便它可以保持&lt;funcName&gt;跟踪公共 PDB 文件中的批注。

```ManagedCPlusPlus
//
// This comment block is scanned by the trace preprocessor to define our
// Trace function.
//
// begin_wpp config
// FUNC Trace{FLAG=MYDRIVER_ALL_INFO}(LEVEL, MSG, ...);
// FUNC TraceEvents(LEVEL, FLAGS, MSG, ...);
// FUNC PrintEvents(IFRLOG, LEVEL, FLAGS, MSG, ...);
// WPP_FLAGS(-public:PrintEvents);
// end_wpp
//
```

## <a name="span-idviewspanspan-idviewspanview-the-trace-messages"></a><span id="view"></span><span id="VIEW"></span>查看跟踪消息


若要查看跟踪消息，请使用[Wdfkd 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)Windows 调试器中。 扩展命令是 Wdfkd.dll。

1.  加载 Wdfkd 命令中，输入`.load Wdfkd.dll`在调试器中。
2.  使用以下命令来查看跟踪消息。

    [ **!wdfkd.wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)

    [ **!wdfkd.wdfcrashdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfcrashdump)

内核模式驱动程序可以通过查看跟踪日志[RCDRKD 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)。 这些命令不可用到的用户模式驱动程序。

## <a name="span-idbestpracticesspanspan-idbestpracticesspanspan-idbestpracticesspanbest-practices"></a><span id="Best_practices"></span><span id="best_practices"></span><span id="BEST_PRACTICES"></span>最佳做法


-   调用后 IFR Api [WPP\_INIT\_跟踪](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/ff556191(v=vs.85))中调用*DriverEntry*例程的内核模式驱动程序或在*DLLMain*例程UMDF 2.15 驱动程序。 如果全局策略通过禁用日志记录，然后调用 WPP\_INIT\_跟踪不会启用日志记录。

-   如果[ **WppRecorderLogCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)失败，该调用将返回 NULL 句柄。 在这种情况下，您可以选择忽略的返回值**WppRecorderLogCreate** ，并使用 RECODER\_日志句柄来打印 WPP 消息。

-   不要删除返回的句柄[ **WppRecorderLogGetDefault**](https://docs.microsoft.com/previous-versions/windows/hardware/previsioning-framework/dn895240(v=vs.85))。 若要禁用默认的日志，请设置**CreateDefaultLog**的成员[**记录器\_配置\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/ns-wpprecorder-_recorder_configure_params)为 FALSE，然后调用[**WppRecorderConfigure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderconfigure)。

-   不要调用[ **WppRecorderLogSetIdentifier** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogsetidentifier)通过传递默认日志句柄。 不允许该操作。

-   从非页面缓冲池分配 IFR 缓冲区。 这些分配的累积影响可能会导致严重性能问题，特别是在较小的内存占用设备上。 请求中的较小缓冲区大小你[ **WppRecorderLogCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wpprecorder/nf-wpprecorder-wpprecorderlogcreate)。 此外，如果不需要日志记录功能，则禁用默认日志。

-   若要查看日志缓冲区的大小，请使用[ **！ wdfkd.wdflogdump** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)命令。 如果使用的[RCDRKD 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)，然后可以通过查看大小[ **！ rcdrkd.rcdrloglist**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-rcdrkd-rcdrloglist)

## <a name="span-idumdfandkmdfdifferencesspanspan-idumdfandkmdfdifferencesspanspan-idumdfandkmdfdifferencesspanumdf-and-kmdf-differences"></a><span id="UMDF_and_KMDF_differences"></span><span id="umdf_and_kmdf_differences"></span><span id="UMDF_AND_KMDF_DIFFERENCES"></span>UMDF 和 KMDF 差异


-   只将内核模式驱动程序可以创建自定义的缓冲区。 此功能不适用于用户模式驱动程序。
-   不能使用查看某个用户模式驱动程序的跟踪日志[RCDRKD 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/rcdrkd-extensions)。 必须使用[Wdfkd 扩展](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-extensions--wdfkd-dll-)。









