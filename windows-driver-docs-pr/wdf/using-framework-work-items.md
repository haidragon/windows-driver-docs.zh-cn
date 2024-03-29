---
title: 使用框架工作项
description: 使用框架工作项
ms.assetid: d7e6d187-bed4-4071-a50b-90f32c4f0d5a
keywords:
- 工作项 WDK KMDF
- 队列 WDK KMDF，framework 工作项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e14f7db2a014d058ad081651d214b0209d02fa35
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372258"
---
# <a name="using-framework-work-items"></a>使用框架工作项





一个*工作项*是一个驱动程序中执行的任务[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)事件回调函数。 这些函数以异步方式运行在 IRQL = 被动\_级别，请在系统工作线程的上下文中。

基于框架的驱动程序通常使用工作项，如果[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)函数，运行在 IRQL =调度\_级别，必须执行其他处理在 IRQL = 被动\_级别。

换而言之，驱动程序可以使用工作项，如果在 IRQL 运行的函数 = 调度\_级别必须调用的函数，可以调用仅在 IRQL = 被动\_级别。

通常情况下，驱动程序的[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)或[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)回调函数创建一个工作项对象，并将其添加到系统的工作项队列。 随后，系统工作线程取消排队对象和调用的工作项[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数。

### <a name="sample-drivers-that-use-work-items"></a>使用工作项的示例驱动程序

[示例基于框架的驱动程序](sample-kmdf-drivers.md)使用工作项包括 1394 AMCC5933、 PCIDRV 和 Toaster。

### <a href="" id="ddk-setting-up-a-work-item-df"></a>设置工作项

若要设置的工作项，您的驱动程序必须：

1.  创建工作项。

    驱动程序调用[ **WdfWorkItemCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)若要创建工作项对象，并标识[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数将处理工作项。

2.  存储有关工作项的信息。

    通常情况下，驱动程序使用的工作项对象的上下文内存来存储有关任务的信息的[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)应执行的回调函数。 当*EvtWorkItem*调用回调函数，它可以通过访问此上下文内存中检索信息。 有关如何分配和访问上下文的内存的信息，请参阅[框架对象上下文空间](framework-object-context-space.md)。

3.  将工作项添加到系统的工作项队列。

    驱动程序调用[ **WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，这将驱动程序的工作项添加到工作项队列。

当您的驱动程序调用[ **WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)，它必须提供一个框架设备对象或 framework 队列对象的句柄。 当系统中删除该对象时，它还会删除与对象关联的任何现有工作项。 将释放工作项对象和其关联的工作项回调将先于父对象清理[ *EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)调用回调。

有关框架对象层次结构的清理规则的详细信息，请参阅[Framework 对象生命周期](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-life-cycle)。

### <a href="" id="ddk-using-the-work-item-callback-function-df"></a>使用工作项回调函数

工作项已添加到工作项队列后，它保留在队列中直到系统工作线程变为可用。 系统工作线程从队列中移除工作项，然后调用驱动程序的[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数，将工作项对象作为输入传递。

通常情况下， [ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数将执行以下步骤：

1.  通过访问工作项对象的上下文内存来获取有关工作项的驱动程序所提供的信息。

2.  执行指定的任务。 如果有必要，请回调函数可以调用[ **WdfWorkItemGetParentObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemgetparentobject)来确定工作项的父对象。

3.  调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)删除工作项对象或如果该驱动程序将重新排队工作项，指示工作项的句柄现已可供重复使用。

每个工作项的回调函数执行的任务必须是相对较短。 操作系统提供有限的数量的系统工作线程，因此如果它使用工作项回调函数来执行耗时的任务，您的驱动程序可能会降低系统性能。

### <a href="" id="ddk-creating-and-deleting-work-items-df"></a>创建和删除工作项

驱动程序可以使用以下两种方法之一来创建和删除工作项：

-   一次使用每个工作项： 创建工作项时需要它以及它所应用后立即将其删除。

    此方法很有用的驱动程序，需要很少使用 （通常少于每分钟一次） 的少量的工作项。

    例如，驱动程序的[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数可以调用[ **WdfWorkItemCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate) ，然后[ **WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，和工作项[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数可以调用[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete).

    如果您的驱动程序遵循此方案中，并且其[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数接收状态\_不足\_资源返回值从[ **WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)，驱动程序必须能推迟所需的工作，直到系统资源 （通常是内存） 变为可用。

-   创建您的驱动程序在必要时请求的一个或多个工作项。

    此方法很有用的驱动程序，使用经常用于工作项 （超过通常每分钟一次），或者，如果您的驱动程序[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数不能轻松地处理状态\_不足\_资源返回介于[ **WdfWorkItemCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)。

    系统驱动程序调用之前不会分配到工作项的工作线程[ **WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)。 因此，即使系统工作线程数是一种有限的资源，初始化设备时创建工作项小消耗的内存而不是会影响系统性能。

    以下步骤描述了可能的情况：

    1.  驱动程序的[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数调用[ **WdfWorkItemCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemcreate)获取工作项句柄。
    2.  在驱动程序[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)回调函数创建的一系列操作[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数必须执行，然后调用[ **WdfWorkItemEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，使用步骤 1 中的句柄。
    3.  在驱动程序[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数执行的操作的列表，并设置一个标志，指示已运行的回调函数。

    随后，每次在驱动程序[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)调用回调函数必须确定是否[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)回调函数已运行。 如果*EvtWorkItem*尚未进行回调函数， *EvtInterruptDpc*回调函数不会调用[ **WdfWorkItemEnqueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemenqueue)，因为工作项仍在排队。 在这种情况下， *EvtInterruptDpc*回调函数仅可更新的操作列表*EvtWorkItem*回调函数。

    每个工作项是与设备或队列相关联。 关联的设备或队列中删除时，framework 删除所有关联的工作项，因此如果使用此方法，该驱动程序不必调用[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)。

几个的驱动程序可能需要调用[ **WdfWorkItemFlush** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nf-wdfworkitem-wdfworkitemflush)若要刷新工作项队列中的各自的工作项。 有关的示例用法**WdfWorkItemFlush**，请参阅该方法的参考页。

如果该驱动程序调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)上未完成的工作项，结果取决于工作项的状态：

|工作项状态|结果|
|-|-|
|创建但未排入队列|立即清除工作项。|
|排入队列|调用到[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)等待，直到工作项完成执行，然后清理工作项|
|执行|如果该驱动程序调用[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)中[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem) （在同一个线程）， [ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)立即返回。 一次[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)完成之后，工作项将清理。  否则为[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)等待 EvtWorkItem 来完成。|

 





