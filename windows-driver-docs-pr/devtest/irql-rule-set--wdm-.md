---
title: Irql rule set (WDM)
description: 使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。
ms.assetid: 40C17906-58D5-4023-A549-0164C3A92A06
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: a11d34f4b17aea200258fce450aa8998ed26d8d2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373648"
---
# <a name="irql-rule-set-wdm"></a>Irql rule set (WDM)


使用这些规则来验证您的驱动程序所需的 IRQL 在进行 DDI 调用。

未遵循 IRQL 规则的驱动程序可以操作可能会导致死锁条件或计算机崩溃期间导致严重问题。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"><strong>ForwardedAtBadIrql</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirql.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrql&lt;/strong&gt;](wdm-forwardedatbadirql.md)"> <strong>ForwardedAtBadIrql</strong> </a>规则指定驱动程序应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>在 IRQL&lt;DISPATCH_LEVEL 转发的 IRP 主要函数代码，除非下列情况之一：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"><strong>ForwardedAtBadIrqlAllocate</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlallocate.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlAllocate&lt;/strong&gt;](wdm-forwardedatbadirqlallocate.md)"> <strong>ForwardedAtBadIrqlAllocate</strong> </a>规则指定驱动程序应调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a> IRQL 在&lt;DISPATCH_LEVEL，转发的 IRP 主要函数代码，除非下列情况之一：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"><strong>ForwardedAtBadIrqlFsdAsync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdasync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdAsync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdasync.md)"> <strong>ForwardedAtBadIrqlFsdAsync</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>在 IRQL&lt;DISPATCH_LEVEL，转发的 IRP 主要函数代码，除非下列情况之一：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"><strong>ForwardedAtBadIrqlFsdSync</strong></a></p></td>
<td align="left"><p><a href="wdm-forwardedatbadirqlfsdsync.md" data-raw-source="[&lt;strong&gt;ForwardedAtBadIrqlFsdSync&lt;/strong&gt;](wdm-forwardedatbadirqlfsdsync.md)"> <strong>ForwardedAtBadIrqlFsdSync</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver" data-raw-source="[&lt;strong&gt;IoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)"> <strong>IoCallDriver</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver" data-raw-source="[&lt;strong&gt;PoCallDriver&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pocalldriver)"> <strong>PoCallDriver</strong> </a>在 IRQL&lt;DISPATCH_LEVEL，转发的 IRP 主要函数代码，除非下列情况之一：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power" data-raw-source="[&lt;strong&gt;IRP_MJ_POWER&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)"><strong>IRP_MJ_POWER</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read" data-raw-source="[&lt;strong&gt;IRP_MJ_READ&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)"><strong>IRP_MJ_READ</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write" data-raw-source="[&lt;strong&gt;IRP_MJ_WRITE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)"><strong>IRP_MJ_WRITE</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)"><strong>IRP_MJ_DEVICE_CONTROL</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control" data-raw-source="[&lt;strong&gt;IRP_MJ_INTERNAL_DEVICE_CONTROL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)"><strong>IRP_MJ_INTERNAL_DEVICE_CONTROL</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"><strong>IrqlApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlapclte.md" data-raw-source="[&lt;strong&gt;IrqlApcLte&lt;/strong&gt;](wdm-irqlapclte.md)"> <strong>IrqlApcLte</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obgetobjectsecurity" data-raw-source="[&lt;strong&gt;ObGetObjectSecurity&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obgetobjectsecurity)"> <strong>ObGetObjectSecurity</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreleaseobjectsecurity" data-raw-source="[&lt;strong&gt;ObReleaseObjectSecurity&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreleaseobjectsecurity)"> <strong>ObReleaseObjectSecurity</strong> </a>仅当执行在 IRQL &lt;= APC_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"><strong>IrqlDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqldispatch.md" data-raw-source="[&lt;strong&gt;IrqlDispatch&lt;/strong&gt;](wdm-irqldispatch.md)"> <strong>IrqlDispatch</strong> </a>规则指定驱动程序调用以下 DDIs，仅当执行在 IRQL = DISPATCH_LEVEL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"><strong>IrqlExAllocatePool</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexallocatepool.md" data-raw-source="[&lt;strong&gt;IrqlExAllocatePool&lt;/strong&gt;](wdm-irqlexallocatepool.md)"> <strong>IrqlExAllocatePool</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)"> <strong>ExAllocatePoolWithTag</strong> </a>和<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtagpriority" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTagPriority&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtagpriority)"> <strong>ExAllocatePoolWithTagPriority</strong> </a>仅当执行在 IRQL&lt;= DISPATCH_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"><strong>IrqlExApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte1.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte1&lt;/strong&gt;](wdm-irqlexapclte1.md)"> <strong>IrqlExApcLte1</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85)" data-raw-source="[&lt;strong&gt;ExAcquireFastMutex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff544337(v=vs.85))"> <strong>ExAcquireFastMutex</strong> </a>并<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85)" data-raw-source="[&lt;strong&gt;ExTryToAcquireFastMutex&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff545647(v=vs.85))"> <strong>ExTryToAcquireFastMutex</strong> </a>仅在 IRQL &lt;= APC_LEVEL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"><strong>IrqlExApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte2.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte2&lt;/strong&gt;](wdm-irqlexapclte2.md)"> <strong>IrqlExApcLte2</strong> </a>规则指定驱动程序只能在 IRQL 调用以下例程&lt;= APC_LEVEL。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"><strong>IrqlExApcLte3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclte3.md" data-raw-source="[&lt;strong&gt;IrqlExApcLte3&lt;/strong&gt;](wdm-irqlexapclte3.md)"> <strong>IrqlExApcLte3</strong> </a>规则指定驱动程序只能在 IRQL 调用以下执行支持例程&lt;= APC_LEVEL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"><strong>IrqlExApcLteInline</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexapclteinline.md" data-raw-source="[&lt;strong&gt;IrqlExApcLteInline&lt;/strong&gt;](wdm-irqlexapclteinline.md)"> <strong>IrqlExApcLteInline</strong> </a>规则指定 DDIs 仅调用适当的 IRQL 级别</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"><strong>IrqlExFree1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree1.md" data-raw-source="[&lt;strong&gt;IrqlExFree1&lt;/strong&gt;](wdm-irqlexfree1.md)"> <strong>IrqlExFree1</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)"> <strong>ExFreePool</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag)"> <strong>ExFreePoolWithTag</strong></a>在适当的 IRQL 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"><strong>IrqlExFree2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree2.md" data-raw-source="[&lt;strong&gt;IrqlExFree2&lt;/strong&gt;](wdm-irqlexfree2.md)"> <strong>IrqlExFree2</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)"> <strong>ExFreePool</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag)"> <strong>ExFreePoolWithTag</strong></a>在适当的 IRQL 调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"><strong>IrqlExFree3</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexfree3.md" data-raw-source="[&lt;strong&gt;IrqlExFree3&lt;/strong&gt;](wdm-irqlexfree3.md)"> <strong>IrqlExFree3</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)"> <strong>ExFreePool</strong> </a>并<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag" data-raw-source="[&lt;strong&gt;ExFreePoolWithTag&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exfreepoolwithtag)"> <strong>ExFreePoolWithTag</strong></a>在适当的 IRQL 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"><strong>IrqlExPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"> <strong>IrqlExPassive</strong> </a>规则指定驱动程序，调用以下执行支持例程只能在 IRQL = passive_level 调用：</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback" data-raw-source="[&lt;strong&gt;ExCreateCallback&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-excreatecallback)"><strong>ExCreateCallback</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisprocessorfeaturepresent" data-raw-source="[&lt;strong&gt;ExIsProcessorFeaturePresent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exisprocessorfeaturepresent)"><strong>ExIsProcessorFeaturePresent</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraiseaccessviolation" data-raw-source="[&lt;strong&gt;ExRaiseAccessViolation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraiseaccessviolation)"><strong>ExRaiseAccessViolation</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraisedatatypemisalignment" data-raw-source="[&lt;strong&gt;ExRaiseDatatypeMisalignment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exraisedatatypemisalignment)"><strong>ExRaiseDatatypeMisalignment</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus)"><strong>ExRaiseStatus</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exuuidcreate" data-raw-source="[&lt;strong&gt;ExUuidCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exuuidcreate)"><strong>ExUuidCreate</strong></a></p></li>
</ul>
<p><a href="wdm-irqlexpassive.md" data-raw-source="[&lt;strong&gt;IrqlExPassive&lt;/strong&gt;](wdm-irqlexpassive.md)"> <strong>IrqlExPassive</strong> </a>规则还指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus" data-raw-source="[&lt;strong&gt;ExRaiseStatus&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exraisestatus)"> <strong>ExRaiseStatus</strong> </a>在 IRQL &lt;= APC_LEVEL</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"><strong>IrqlIoApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlioapclte.md" data-raw-source="[&lt;strong&gt;IrqlIoApcLte&lt;/strong&gt;](wdm-irqlioapclte.md)"> <strong>IrqlIoApcLte</strong> </a>规则指定驱动程序调用以下 I/O 管理器例程，仅当执行在 IRQL &lt;= APC_LEVEL:</p>
<ul>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice" data-raw-source="[&lt;strong&gt;IoDeleteDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iodeletedevice)"><strong>IoDeleteDevice</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetinitialstack" data-raw-source="[&lt;strong&gt;IoGetInitialStack&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetinitialstack)"><strong>IoGetInitialStack</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseharderror" data-raw-source="[&lt;strong&gt;IoRaiseHardError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseharderror)"><strong>IoRaiseHardError</strong></a></p></li>
<li><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseinformationalharderror" data-raw-source="[&lt;strong&gt;IoRaiseInformationalHardError&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioraiseinformationalharderror)"><strong>IoRaiseInformationalHardError</strong></a></p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"><strong>IrqlIoDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliodispatch.md" data-raw-source="[&lt;strong&gt;IrqlIoDispatch&lt;/strong&gt;](wdm-irqliodispatch.md)"> <strong>IrqlIoDispatch</strong> </a>规则指定驱动程序调用以下 I/O 管理器例程，仅当执行在 IRQL &lt;= DISPATCH_LEVEL:<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetdevicetoverify" data-raw-source="[&lt;strong&gt;IoGetDeviceToVerify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iogetdevicetoverify)"><strong>IoGetDeviceToVerify</strong></a>， <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetdevicetoverify" data-raw-source="[&lt;strong&gt;IoSetDeviceToVerify&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iosetdevicetoverify)"> <strong>IoSetDeviceToVerify</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"><strong>IrqlIoPassive1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive1.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive1&lt;/strong&gt;](wdm-irqliopassive1.md)"> <strong>IrqlIoPassive1</strong> </a>规则指定驱动程序调用以下例程，仅当执行在 IRQL = passive_level 调用：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"><strong>IrqlIoPassive2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive2.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive2&lt;/strong&gt;](wdm-irqliopassive2.md)"> <strong>IrqlIoPassive2</strong> </a>规则指定驱动程序，调用以下 I/O 管理器例程只能在 IRQL = passive_level 调用：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive3.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive3&lt;/strong&gt;](wdm-irqliopassive3.md)"><strong>IrqlIoPassive3</strong></a></p></td>
<td align="left"><p>IrqlIoPassive3 规则指定驱动程序调用以下例程，仅当执行在 IRQL = passive_level 调用：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"><strong>IrqlIoPassive4</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive4.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive4&lt;/strong&gt;](wdm-irqliopassive4.md)"> <strong>IrqlIoPassive4</strong> </a>规则指定驱动程序调用以下例程，仅当执行在 IRQL = passive_level 调用：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"><strong>IrqlIoPassive5</strong></a></p></td>
<td align="left"><p><a href="wdm-irqliopassive5.md" data-raw-source="[&lt;strong&gt;IrqlIoPassive5&lt;/strong&gt;](wdm-irqliopassive5.md)"> <strong>IrqlIoPassive5</strong> </a>规则指定驱动程序调用特定的 I/O 管理器例程，仅当执行在 IRQL = passive_level 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"><strong>IrqlKeApcLte1</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte1.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte1&lt;/strong&gt;](wdm-irqlkeapclte1.md)"> <strong>IrqlKeApcLte1</strong> </a>规则指定驱动程序调用以下内核例程，仅当执行在 IRQL &lt;= APC_LEVEL:</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"><strong>IrqlKeApcLte2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeapclte2.md" data-raw-source="[&lt;strong&gt;IrqlKeApcLte2&lt;/strong&gt;](wdm-irqlkeapclte2.md)"> <strong>IrqlKeApcLte2</strong> </a>规则指定驱动程序调用以下内核例程，仅当执行在 IRQL &lt;= APC_LEVEL:</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"><strong>IrqlKeDispatchLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkedispatchlte.md" data-raw-source="[&lt;strong&gt;IrqlKeDispatchLte&lt;/strong&gt;](wdm-irqlkedispatchlte.md)"> <strong>IrqlKeDispatchLte</strong> </a>规则指定驱动程序调用以下内核例程，仅当执行在 IRQL &lt;= DISPATCH_LEVEL:</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkeraiselower.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](wdm-irqlkeraiselower.md)"><strong>IrqlKeRaiseLower</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeraiselower" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdm-irqlkeraiselower)"> <strong>IrqlKeRaiseLower</strong> </a>规则指定驱动程序执行以下操作时提高和降低 IRQL:</p>
当驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)"> <strong>KeRaiseIrql</strong></a>，它是在低于 IRQL 正在执行或等于的值<em>NewIrql</em>参数。<br />
驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)"> <strong>KeLowerIrql</strong> </a>仅在调用<strong>KeRaiseIrql</strong>或者<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)"> <strong>KeRaiseIrqlToDpcLevel</strong> </a>.<br />
</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"><strong>IrqlKeRaiseLower2</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkeraiselower2.md" data-raw-source="[&lt;strong&gt;IrqlKeRaiseLower2&lt;/strong&gt;](wdm-irqlkeraiselower2.md)"> <strong>IrqlKeRaiseLower2</strong> </a>规则指定驱动程序使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql" data-raw-source="[&lt;strong&gt;KeLowerIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kelowerirql)"> <strong>KeLowerIrql</strong> </a>还原由前面的调用引发原始 IRQL向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql" data-raw-source="[&lt;strong&gt;KeRaiseIrql&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirql)"> <strong>KeRaiseIrql</strong> </a>或<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel" data-raw-source="[&lt;strong&gt;KeRaiseIrqlToDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keraiseirqltodpclevel)"> <strong>KeRaiseIrqlToDpcLevel</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"><strong>IrqlKeReleaseSpinLock</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkereleasespinlock.md" data-raw-source="[&lt;strong&gt;IrqlKeReleaseSpinLock&lt;/strong&gt;](wdm-irqlkereleasespinlock.md)"> <strong>IrqlKeReleaseSpinLock</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock" data-raw-source="[&lt;strong&gt;KeReleaseSpinLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)"> <strong>KeReleaseSpinLock</strong> </a>仅当执行在 IRQL =DISPATCH_LEVEL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"><strong>IrqlKeSetEvent</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkesetevent.md" data-raw-source="[&lt;strong&gt;IrqlKeSetEvent&lt;/strong&gt;](wdm-irqlkesetevent.md)"> <strong>IrqlKeSetEvent</strong> </a>规则指定<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesetevent)"> <strong>KeSetEvent</strong> </a> IRQL 在仅调用例程&lt;= DISPATCH_LEVEL当<em>等待</em>设置为<strong>FALSE</strong>，而是在 IRQL &lt;= APC_LEVEL 时<em>等待</em>设置为<strong>TRUE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"><strong>IrqlKeWaitForMutexObject</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformutexobject.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMutexObject&lt;/strong&gt;](wdm-irqlkewaitformutexobject.md)"> <strong>IrqlKeWaitForMutexObject</strong> </a>规则指定驱动程序来调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff553344" data-raw-source="[&lt;strong&gt;KeWaitForMutexObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553344)"> <strong>KeWaitForMutexObject</strong> </a>例程在适当的 IRQL值的基础<em>超时</em>参数：</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"><strong>IrqlKeWaitForMultipleObjects</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlkewaitformultipleobjects.md" data-raw-source="[&lt;strong&gt;IrqlKeWaitForMultipleObjects&lt;/strong&gt;](wdm-irqlkewaitformultipleobjects.md)"> <strong>IrqlKeWaitForMultipleObjects</strong> </a>规则指定的调用方<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)"> <strong>KeWaitForMultipleObjects</strong> </a>例程必须正在运行在基于正确 IRQL<em>超时</em>参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"><strong>IrqlMmApcLte</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmapclte.md" data-raw-source="[&lt;strong&gt;IrqlMmApcLte&lt;/strong&gt;](wdm-irqlmmapclte.md)"> <strong>IrqlMmApcLte</strong> </a>规则指定，该驱动程序调用以下内存管理器例程仅当执行在 IRQL &lt;= APC_LEVEL:</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"><strong>IrqlMmDispatch</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlmmdispatch.md" data-raw-source="[&lt;strong&gt;IrqlMmDispatch&lt;/strong&gt;](wdm-irqlmmdispatch.md)"> <strong>IrqlMmDispatch</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreecontiguousmemory" data-raw-source="[&lt;strong&gt;MmFreeContiguousMemory&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmfreecontiguousmemory)"> <strong>MmFreeContiguousMemory</strong> </a>仅当执行在<strong>IRQL &lt;= DISPATCH_LEVEL</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"><strong>IrqlObPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlobpassive.md" data-raw-source="[&lt;strong&gt;IrqlObPassive&lt;/strong&gt;](wdm-irqlobpassive.md)"> <strong>IrqlObPassive</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle" data-raw-source="[&lt;strong&gt;ObReferenceObjectByHandle&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)"> <strong>ObReferenceObjectByHandle</strong> </a>仅当执行在 IRQL =PASSIVE_LEVEL 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"><strong>IrqlPsPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlpspassive.md" data-raw-source="[&lt;strong&gt;IrqlPsPassive&lt;/strong&gt;](wdm-irqlpspassive.md)"> <strong>IrqlPsPassive</strong> </a>规则指定驱动程序调用以下<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index" data-raw-source="[&lt;strong&gt;Process Structure routines&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)"><strong>处理结构例程</strong></a>仅当正在执行它在 IRQL = passive_level 调用：</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"><strong>IrqlReturn</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlreturn.md" data-raw-source="[&lt;strong&gt;IrqlReturn&lt;/strong&gt;](wdm-irqlreturn.md)"> <strong>IrqlReturn</strong> </a>规则指定驱动程序的调度例程返回在相同的 IRQL 在其中调用它们。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="wdm-irqlrtlpassive.md" data-raw-source="[&lt;strong&gt;IrqlRtlPassive&lt;/strong&gt;](wdm-irqlrtlpassive.md)"><strong>IrqlRtlPassive</strong></a></p></td>
<td align="left"><p>IrqlRtlPassive 规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtldeleteregistryvalue" data-raw-source="[&lt;strong&gt;RtlDeleteRegistryValue&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtldeleteregistryvalue)"> <strong>RtlDeleteRegistryValue</strong> </a>仅当执行在 IRQL = passive_level 调用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"><strong>IrqlZwPassive</strong></a></p></td>
<td align="left"><p><a href="wdm-irqlzwpassive.md" data-raw-source="[&lt;strong&gt;IrqlZwPassive&lt;/strong&gt;](wdm-irqlzwpassive.md)"> <strong>IrqlZwPassive</strong> </a>规则指定驱动程序调用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose" data-raw-source="[&lt;strong&gt;ZwClose&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntclose)"> <strong>ZwClose</strong> </a>仅当执行在 IRQL = passive_level 调用。</p></td>
</tr>
</tbody>
</table>

 

**若要选择的 Irql 规则设置**

1.  Microsoft Visual Studio 中选择您的驱动程序项目 (.vcxProj)。 从**驱动程序**菜单上，单击**启动 Static Driver Verifier...** .

2.  单击**规则**选项卡。下**规则集**，选择**Irql**。

    若要选择的默认规则集从 Visual Studio 开发人员命令提示符窗口，请指定**Irql.sdv**与 **/check**选项。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Irql.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅[以找到缺陷驱动程序中使用 Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)并[Static Driver Verifier 命令 (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)。

 

 





