---
title: 处理器数量的更改
description: 处理器数量的更改
ms.assetid: 9ced4b42-c83d-49da-8405-b95b0c0144fa
keywords:
- 动态硬件分区 WDK、 更改的处理器数
- 硬件分区 WDK 动态的更改的处理器数
- 分区 WDK 动态硬件，更改的处理器数
- 活动处理器 WDK 动态硬件分区
- 处理器计数 WDK 动态硬件分区
- 处理器关联 WDK 动态硬件分区
- 每个处理器的数据结构 WDK 动态硬件分区
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6d6e6821e2db99cedeede35a53869f1f45c5323
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383361"
---
# <a name="changes-to-the-number-of-processors"></a>处理器数量的更改


在动态可分区服务器上，可以在任何时间添加到硬件分区的处理器。 因此，不应造成硬件分区、 处理器关联值或分配给每个活动的处理器的处理器数中的任何假设 active 处理器数。 处理器关联值中设置的位表示每个硬件分区中当前处于活动状态的处理器。 如果将一个处理器添加到硬件分区，则会将更改设置的特定位。

如果任一以下语句是设备驱动程序，则返回 true，则必须更新驱动程序，以便它将正常工作的动态可分区服务器上处理器动态添加到硬件分区时：

-   设备驱动程序使用硬件分区中的活动的处理器数来确定的使用，如它在分配的内存量，它创建的线程数或它使用其他资源量的资源量。 在这种情况下，设备驱动程序的资源分配将不正确，如果一个处理器动态添加到硬件分区。 这会影响性能或驱动程序的行为。

-   设备驱动程序将指导处理器关联值的位。 在此情况下，设备驱动程序可能无法正常工作如果它不能处理对处理器关联值的动态更改或无法处理的设置的位序列中的空白。

-   设备驱动程序中的处理器关联值使用 bits，若要将驱动程序分配的资源分配给特定的处理器。 在这种情况下，设备驱动程序的资源分配将不正确，如果一个处理器动态添加到硬件分区。 这会影响性能或驱动程序的行为。

-   设备驱动程序为每个活动处理器硬件分区中分配数据结构。 在此情况下，不良行为、 数据损坏或如果它尝试访问这些数据结构的动态添加到硬件分区的处理器的 bug 检查可能导致设备驱动程序。

-   设备驱动程序的调度例程使用在其运行以访问数据结构或其他资源分配给该特定处理器的处理器的处理器数。 在这种情况下，设备驱动程序的调度例程会导致不良行为、 数据损坏或如果用户尝试访问这些资源以获取动态添加到硬件分区的处理器的 bug 检查。

-   设备驱动程序计划其中断服务例程 (Isr)、 延缓的过程调用 (Dpc) 或特定的处理器上的其他线程。 在此情况下，设备驱动程序可能会停止正常如果到硬件分区中，添加一个处理器，并且设备驱动程序将不能充分利用任何新的处理器。

-   设备驱动程序不支持资源重新平衡。 在此情况下，设备驱动程序将不能使用用于处理中断的硬件分区添加任何新处理器。

-   设备驱动程序使用负载平衡算法将分布到多个处理器的 I/O 请求的处理。 在此情况下，设备驱动程序可能会停止正常如果到硬件分区中，添加一个处理器，并且设备驱动程序将不能充分利用任何新的处理器。

如果设备驱动程序对活动的处理器数的更改的影响，它必须与操作系统将处理器添加到硬件分区时收到通知注册。 当通知的设备驱动程序时，它可以响应所需的安全和最佳操作。 有关设备驱动程序如何可以注册其自身与操作系统的详细信息，请参阅[驱动程序通知](driver-notification.md)。

若要检索当前活动中的处理器数硬件分区，设备驱动程序应调用[ **KeQueryActiveProcessorCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryactiveprocessorcount)函数。 若要检索当前的处理器关联值，设备驱动程序可以调用[ **KeQueryActiveProcessors** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryactiveprocessors)函数或**KeQueryActiveProcessorCount**函数。

**请注意**  如果设备驱动程序为每个活动处理器硬件分区中分配数据结构和设备驱动程序将失败，如果内存分配数据结构的新处理器失败，则设备驱动程序可能若要处理的最大操作系统支持的处理器数的驱动程序初始化期间分配足够的这些数据结构。 在此情况下，设备驱动程序不需要分配新的数据结构，在将新处理器添加到硬件分区。 但是，除非这些数据结构的大小是相当小，这可能是使用效率低下的内存资源。 设备驱动程序可以查询通过调用操作系统支持的处理器的最大数目[ **KeQueryMaximumProcessorCount** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequerymaximumprocessorcount)函数。

 

**重要**  通知到硬件分区中添加了处理器时，设备驱动程序始终应更新任何保存的值的活动的处理器和处理器关联的数目。

 

**重要**  设备驱动程序不应计算组中的处理器关联值，以确定硬件分区中的活动处理器数的比特数。 我们建议使用设备驱动程序调用**KeQueryActiveProcessorCount**函数实现此目的。 此函数返回的活动的处理器数和相关的处理器关联值。

 

**重要**  适用于 Windows Vista、 Windows Server 2008 和更高版本的 Windows 必须使用的设备驱动程序[ **KeNumberProcessors** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kequeryactiveprocessors)内核变量若要确定硬件分区中的活动处理器数。 **KeNumberProcessors**内核变量是 Windows Vista Service Pack 1 (SP1)、 Windows Server 2008 和更高版本的 Windows 中已过时。

 

 

 




