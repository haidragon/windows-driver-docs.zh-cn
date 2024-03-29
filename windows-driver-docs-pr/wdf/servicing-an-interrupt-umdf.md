---
title: 为中断提供服务
description: 为中断提供服务
ms.assetid: 79BA75B3-E10F-4AC1-A2C5-A502BF821188
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c5c2f702d0a2ce46f8ad5084976413dc048a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376193"
---
# <a name="servicing-an-interrupt"></a>为中断提供服务


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

服务中断包括两个步骤：

1.  以中断服务例程快速，保存易失性信息 （如寄存器内容）。
2.  处理工作项的例程中保存的易失性信息。

当设备生成的硬件中断时，框架将调用驱动程序的中断服务例程 (ISR) 作为实现的基于框架的驱动程序[ *OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数。

[ *OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数，在被动运行\_级别，必须快速保存中断的信息，如寄存器内容排队的工作项数据，处理并且返回 ISR 以允许其他中断的中断行共享服务。 因为在被动运行 UMDF 驱动程序的 ISR\_级别，处理 PCI 基于行的中断不建议。 多个设备，其中一些可能不接受 ISR 延迟之间通常共享这些中断。 但是，您可以处理 PCI MSI 中断 UMDF 驱动程序中。 这些中断具有边缘的语义，不能共享。

通常情况下， [ *OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数计划工作项，以处理更高版本的已保存的信息。 基于框架的驱动程序实现为工作项例程[ *OnInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)回调函数。

大多数驱动程序使用单个[ *OnInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)中断每种类型的回调函数。 若要计划的执行*OnInterruptWorkItem*驱动程序必须调用回调函数[ **IWDFInterrupt::QueueWorkItemForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfinterrupt-queueworkitemforisr)中[*OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数。

如果您的驱动程序创建多个框架为每个设备队列对象，则可以考虑使用单独的工作项对象和[ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)每个队列的回调函数。 若要计划的执行*OnWorkItem*回调函数，该驱动程序必须先创建一个或多个工作项对象通过调用[ **IWdfDevice3::CreateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-createworkitem)，通常是从驱动程序的[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调函数。 然后，驱动程序的[ *OnInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_isr)回调函数可以调用[ **IWDFWorkItem::Enqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfworkitem-enqueue)。

驱动程序通常完成 I/O 请求在其[ *OnInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfinterrupt/nc-wudfinterrupt-wudf_interrupt_workitem)或[ *OnWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfworkitem/nc-wudfworkitem-wudf_workitem_function)回调函数。

处理中断的 UMDF 驱动程序的示例，请参阅[SpbAccelerometer](https://go.microsoft.com/fwlink/p/?linkid=256189)示例驱动程序，可以开始于 Windows 8 WDK。

 

 





