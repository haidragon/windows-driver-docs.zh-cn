---
title: 编写 Bug 检查原因回调例程
description: 编写 Bug 检查回调例程
ms.assetid: 62aefe67-e197-4c45-b994-19bd7369dbc1
keywords:
- bug 检查回调例程 WDK 内核
- 回调例程 WDK bug 检查
- 注册回调例程
- KeRegisterBugCheckCallback
- BugCheckCallback
ms.date: 05/02/2019
ms.localizationpriority: medium
ms.openlocfilehash: 678f34a25c3a9ff04a6e13cb6b5bf1eb76aabdb4
ms.sourcegitcommit: cffd3bab903ac0a2412cc7df91584278e4fef179
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467823"
---
# <a name="writing-a-bug-check-reason-callback-routine"></a>编写 Bug 检查原因回调例程

可以根据需要提供一个驱动程序[ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)回调函数，该系统调用后的故障转储函数写入文件。

> [!NOTE]
> 本指南介绍了 bug 检查*原因*回调例程，而不[ *KBUGCHECK_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_callback_routine)回调函数。

在此回调中，该驱动程序可以：

* 将特定于驱动程序的数据添加到故障转储文件
* 将设备重置到已知状态

使用下面的例程来注册和删除回调：

* [**KeRegisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback)
* [**KeDeregisterBugCheckReasonCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback)

此回调类型负载过重，行为更改基于[ **KBUGCHECK_CALLBACK_REASON** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_kbugcheck_callback_reason)注册时提供的常量值。  本指南介绍了不同的使用方案。

有关 bug 检查数据的常规信息，请参阅[读取 Bug 检查回调数据](https://docs.microsoft.com/windows-hardware/drivers/debugger/reading-bug-check-callback-data)。

## <a name="bug-check-callback-routine-restrictions"></a>Bug 检查回调例程限制

Bug 检查回调例程执行在 IRQL = 高\_级别，这会强制执行强限制可以执行的操作。

Bug 检查回调例程不能：

* 分配内存
* 访问可分页内存
* 使用任何同步机制
* 调用在 IRQL 必须执行的任何例程 = 调度\_级别或更低

Bug 检查回调例程保证运行而不发生中断，因此不需要进行同步。 （如果 bug 检查例程使用的任何同步机制，系统将发生死锁。）

可以安全地使用驱动程序的 bug 检查回调例程**读取\_端口\_<em>XXX</em>** ，**读取\_注册\_<em>XXX</em>** ，**编写\_端口\_<em>XXX</em>** ，以及**编写\_注册\_ <em>XXX</em>** 例程与驱动程序的设备进行通信。 (有关这些例程的信息，请参阅[硬件抽象层例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))。)

## <a name="implementing-a-kbcallbackaddpages-callback-routine"></a>实现 KbCallbackAddPages 回调例程

内核模式驱动程序可以实现[ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)类型的回调函数<i>KbCallbackAddPages</i>若要添加的数据的一个或多个页崩溃转储文件时出现的 bug 检查。 若要向操作系统注册此例程，该驱动程序调用<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a> </b>例程。 该驱动程序卸载之前，必须调用<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a> </b>例程，以删除注册。

从已注册的 Windows 8 开始<i>KbCallbackAddPages</i>期间调用例程<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-memory-dump">内核内存转储</a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/complete-memory-dump">完全内存转储</a>。 在早期版本的 Windows 中，已注册<i>KbCallbackAddPages</i>在内核内存转储，但不是在完全内存转储期间调用例程。 默认情况下，内核内存转储包括仅使用由 Windows 内核进行错误检查时，而完全内存转储则包括所有 Windows 使用的物理内存的物理页。 完全内存转储不，默认情况下，包括平台固件使用的物理内存。

你<i>KbCallbackAddPages</i>例程可以提供特定于驱动程序的数据将添加到转储文件。 例如，对于内核内存转储，这些额外的数据可以包括物理页的未映射到虚拟内存中的系统地址范围，但已包含可帮助你调试您的驱动程序的信息。 <i>KbCallbackAddPages</i>例程可能会添加到转储文件 （任何驱动程序拥有物理页未映射或并将其映射到用户模式虚拟内存中的地址。

Bug 检查时，操作系统将调用所有已注册<i>KbCallbackAddPages</i>例程来轮询数据将添加到故障转储文件的驱动程序。 每次调用将的连续数据的一个或多个页添加到故障转储文件。 一个<i>KbCallbackAddPages</i>例程可以提供虚拟地址或起始页的物理地址。 如果在调用期间提供多个页，则页面是在虚拟或物理内存中，根据起始地址是虚拟还是物理连续的。 若要提供非连续页<i>KbCallbackAddPages</i>例程可以设置一个标志， <b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_add_pages">KBUGCHECK_ADD_PAGES</a> </b>结构，以指示它已附加数据，并具有若要再次调用。

与不同*KbCallbackSecondaryDumpData*例程，将数据追加到辅助崩溃转储区域， <i>KbCallbackAddPages</i>例程会向主崩溃转储区域中添加的数据页。 调试、 主崩溃期间转储数据比更容易访问辅助崩溃转储数据。

操作系统会填写<b>BugCheckCode</b>的成员<b>KBUGCHECK_ADD_PAGES</b>结构的<i>ReasonSpecificData</i>指向。 <i>KbCallbackAddPages</i>例程必须设置的值<b>标志</b>，<b>地址</b>，以及<b>计数</b>此结构的成员。

首次调用前<i>KbCallbackAddPages</i>，操作系统初始化<b>上下文</b>到<b>NULL</b>。 如果<i>KbCallbackAddPages</i>不止一次调用例程，操作系统将保留回调例程已写入到的值<b>上下文</b>上一个调用中的成员。

一个<i>KbCallbackAddPages</i>例程受到严格限制在可执行的操作。 有关详细信息，请参阅[Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

## <a name="implementing-a-kbcallbackdumpio-callback-routine"></a>实现 KbCallbackDumpIo 回调例程

内核模式驱动程序可以实现[ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)类型的回调函数<i>KbCallbackDumpIo</i>执行每个时间数据写入到的工作故障转储文件。 系统通过<i>ReasonSpecificData</i>参数，指向[ **KBUGCHECK_DUMP_IO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_dump_io)结构。 <b>缓冲区</b>成员将指向当前数据，并<b>BufferLength</b>成员指定它的长度。 <b>类型</b>成员指示当前将要写入的数据，如转储文件标头信息、 内存状态或由驱动程序提供数据的类型。 有关的信息的可能类型的说明，请参阅<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_kbugcheck_dump_io_type">KBUGCHECK_DUMP_IO_TYPE</a> </b>枚举。

系统可以编写崩溃转储文件，按顺序，或不按顺序。 如果系统正在写入崩溃转储文件按顺序，则<b>偏移量</b>的成员<i>ReasonSpecificData</i>为-1; 否则为<b>偏移量</b>设置为当前偏移量，在故障转储文件中的字节。

当系统将按顺序写入该文件时，它会调用每个<i>KbCallbackDumpIo</i>例程一个或更多次时编写标头信息 (<b>类型</b> = <b>KbDumpIoHeader</b>)、 一个或多个时间时编写在发生崩溃的主要部分转储文件 (<b>类型</b> = <b>KbDumpIoBody</b>)，且一个或更多次时写入辅助转储数据(<b>类型</b> = <b>KbDumpIoSecondaryDumpData</b>)。 完成后写入崩溃转储文件的系统，它调用具有回调<b>缓冲区</b> = <b>NULL</b>， <b>BufferLength</b> = 0，和<b>类型</b>  =  <b>KbDumpIoComplete</b>。

主要目的<i>KbCallbackDumpIo</i>例程是允许系统崩溃转储数据写入到的磁盘设备。 例如，监视系统状态的设备可以使用回调，以报告系统已发出的 bug 检查，并提供用于分析故障转储。

使用<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a> </b>注册<i>KbCallbackDumpIo</i>例程。 驱动程序随后可通过删除回调<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a> </b>例程。 如果可以卸载该驱动程序，它必须删除任何已注册的回调中其<i> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload">DRIVER_UNLOAD</a> </i>回调函数。

一个<i>KbCallbackDumpIo</i>例程强限制了可执行的操作。 有关详细信息，请参阅[Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

## <a name="implementing-a-kbcallbacksecondarydumpdata-callback-routine"></a>实现 KbCallbackSecondaryDumpData 回调例程

内核模式驱动程序可以实现[ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)类型的回调函数<i>KbCallbackSecondaryDumpData</i>提供要追加到数据故障转储文件。

系统组<b>InBuffer</b>， <b>InBufferLength</b>， <b>OutBuffer</b>，以及<b>MaximumAllowed</b>成员<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a> </b>结构的<i>ReasonSpecificData</i>指向。 <b>MaximumAllowed</b>成员指定的最大转储例程可以提供的数据量。

值<b>OutBuffer</b>成员将确定系统是否正在请求的大小，驱动程序的转储数据或数据本身，按如下所示：

* 如果<b>OutBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA 成员是<b>NULL</b>，系统仅请求大小的信息。 <i>KbCallbackSecondaryDumpData</i>例程会填写<b>OutBuffer</b>并<b>OutBufferLength</b>成员。 
* 如果<b>OutBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA 等于成员<b>InBuffer</b>成员，系统正在请求驱动程序的辅助转储数据。 <i>KbCallbackSecondaryDumpData</i>例程会填写<b>OutBuffer</b>并<b>OutBufferLength</b>成员，并将事件写入到指定的缓冲区数据<b>OutBuffer</b>。

<b>InBuffer</b> KBUGCHECK_SECONDARY_DUMP_DATA 成员指向的例程使用一个较小缓冲区。 <b>InBufferLength</b>成员指定缓冲区的大小。 如果要写入的数据量小于<b>InBufferLength</b>，回调例程可以使用此缓冲区来提供对系统的崩溃转储数据。 然后设置回调例程<b>OutBuffer</b>到<b>InBuffer</b>并<b>OutBufferLength</b>到实际写入缓冲区的数据量。

必须编写的是比更大的数据量的驱动程序<b>InBufferLength</b>可以使用自己的缓冲区来提供的数据。 回调例程执行，并且必须驻留在驻留内存 （如非分页缓冲池） 之前，此缓冲区必须已分配。 然后设置回调例程<b>OutBuffer</b>指向驱动程序的缓冲区，并<b>OutBufferLength</b>缓冲区写入崩溃转储文件中的数据量。

要写入到崩溃转储文件的数据的每个块的标记的值为<b>Guid</b>的成员<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_secondary_dump_data">KBUGCHECK_SECONDARY_DUMP_DATA</a> </b>结构。 使用的 GUID 必须是唯一的驱动程序。 若要显示此 GUID 与对应的辅助转储数据，可以使用<b>.enumtag</b>命令或<b>IDebugDataSpaces3::ReadTagged</b>中调试器扩展的方法。 调试器和调试器扩展的信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/debugger/index">Windows 调试</a>。

驱动程序可以将具有相同 GUID 的多个块写入崩溃转储文件，但这是非常好的做法，因为只有第一个块可供调试器。 注册多个的驱动程序<i>KbCallbackSecondaryDumpData</i>例程应为每个回调分配一个唯一的 GUID。

使用<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keregisterbugcheckreasoncallback">KeRegisterBugCheckReasonCallback</a> </b>注册<i>KbCallbackSecondaryDumpData</i>例程。 驱动程序随后可通过删除回调例程<b> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kederegisterbugcheckreasoncallback">KeDeregisterBugCheckReasonCallback</a> </b>例程。 如果该驱动程序，可以卸载，则它必须删除任何已注册的回调例程中其<i> <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload">DRIVER_UNLOAD</a> </i>回调函数。

一个<i>KbCallbackSecondaryDumpData</i>例程受到严格限制在可执行的操作。 有关详细信息，请参阅[Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

## <a name="implementing-a-kbcallbacktriagedumpdata-callback-routine"></a>实现 KbCallbackTriageDumpData 回调例程

从 Windows 10，版本 1809年和 Windows Server 2019，内核模式驱动程序可以实现[ *KBUGCHECK_REASON_CALLBACK_ROUTINE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)类型的回调函数*KbCallbackTriageDumpData*将虚拟内存范围添加到划分的小型转储文件。 系统通过<i>ReasonSpecificData</i>参数，指向[ **KBUGCHECK_TRIAGE_DUMP_DATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_kbugcheck_triage_dump_data)描述转储数据的结构。

在以下示例中，该驱动程序配置会审转储数组，然后注册回调的最小实现：

```cpp
// Globals 
 
KBUGCHECK_REASON_CALLBACK_RECORD ExampleBugcheckCallbackRecord; 
PKTRIAGE_DUMP_DATA_ARRAY gTriageDumpDataArray; 
 
//  call this register function from DriverInit, etc.
 
VOID ExampleRegisterTriageDataCallbacks() 
{ 
 
    // 
    // Allocate a triage dump array in the non-paged pool. 
    // 
 
gTriageDumpDataArray = 
    (PKTRIAGE_DUMP_DATA_ARRAY)ExAllocatePoolWithTag(NonPagedPoolNx, 2*PAGE_SIZE, "Xmpl"); 
 
    // 
    // Initialize the dump data block array. 
    // 
 
    KeInitializeTriageDumpDataArray( gTriageDumpDataArray, 2*PAGE_SIZE, "Example"); 
 
    KeInitializeCallbackRecord( &ExampleBugcheckCallbackRecord ); 
 
    KeRegisterBugCheckReasonCallback( 
        &ExampleBugCheckCallbackRecord, 
        ExampleBugCheckCallbackRoutine, 
        KbCallbackTriageDumpData, 
        "Example" 
        ); 
} 
 
// Callback function 
 
VOID 
ExampleBugCheckCallbackRoutine( 
    KBUGCHECK_CALLBACK_REASON Reason, 
    PKBUGCHECK_REASON_CALLBACK_RECORD Record, 
    PVOID Data, 
    ULONG Length 
    ) 
{ 
    PKBUGCHECK_TRIAGE_DUMP_DATA DumpData; 
    NTSTATUS Status; 
 
    DumpData = (PKBUGCHECK_TRIAGE_DUMP_DATA) Data; 
 
    Status = KeAddTriageDumpDataBlock(gTriageDumpDataArray, gImportant, SizeofGImportant); 
 
    // Pass our arrays back 
 
    if (NT_SUCCESS(Status)) { 
        DumpData->RequiredDataArray = gTriageDumpDataArray; 
    } 
 
    return; 
}
```
一个<i>KbCallbackTriageDumpData</i>例程受到严格限制在可执行的操作。 有关详细信息，请参阅[Bug 检查回调例程限制](#bug-check-callback-routine-restrictions)。

