---
title: 计时器准确性
description: 系统计时器例程通常情况下允许调用方为计时器指定绝对或相对过期时间。
ms.assetid: CA29DC02-1AEA-4A13-B2D6-8C8052E21EDB
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 10ee2a2218d97986f86a70cc0551b5bdabf061dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382959"
---
# <a name="timer-accuracy"></a>计时器准确性


系统计时器例程通常情况下允许调用方为计时器指定绝对或相对过期时间。 有关示例，请参阅[ **KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)， [ **KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)，或[ **KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)。 系统时钟的粒度受限制使用的操作系统可以衡量的到期时间的准确性。

系统时间更新上的系统时钟，每个时钟周期，并且只精确到最新刻度线。 如果调用方指定一个绝对过期时间，计时器的过期过程中检测到的第一个在指定时间后发生的系统时钟周期的处理。 因此，计时器将过期晚于指定的绝对过期时间最多一个系统时钟时间。 如果改为指定的计时器间隔或相对过期时间，则过期可能会发生一段最早于或晚于指定的时间，具体取决于确切的开始和结束时间在此间隔位于系统时钟计时周期之间的位置句点。 无论是否指定绝对或相对时间时，计时器过期可能不会检测到甚至更高版本如果中断系统时钟的处理延迟的中断处理对于其他设备。

当调用方指定相对过期时间时，计时器例程会将当前系统时钟时间添加到指定的相对过期时间来计算绝对到期时间用于计时器。 系统时间只精确到系统时钟的最新刻度线，因为计算的过期时间可能长达系统时钟时间早于过期时间所需的调用方。 如果指定的相对过期时间接近或超过系统时钟的时间更小，可能会立即过期计时器，且没有任何延迟。

一种以更准确地支持更短的到期时间的可行方法是减少系统时钟计时周期数之间的时间，但这样做很可能会增加功率消耗。 此外，减少系统时钟时间可能无法可靠地实现更细的系统时钟粒度除非中断处理在平台中的其他设备可以保证不延迟的系统时钟中断处理。

从 Windows 8 开始[ **KeDelayExecutionThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)使用更精确的技术来计算绝对到期时间从调用方指定相对过期时间。 首先，若要获取当前系统时间的更精确地估计，例程使用系统性能计数器来测量时间过去的最后一个系统时钟计时周期。 接下来，该例程将系统时间此更精确地估计值添加到相对过期时间来计算绝对到期时间。 通过这种方法来计算绝对到期时间会精确到在微秒内。 因此，指定的相对过期时间到期之前，不会过期计时器。 计时器可能仍会过期最系统时钟时间晚于指定的时间，并可能甚至更高版本中，如果过期的系统时钟中断处理延迟的中断处理对于其他设备。

如果系统时间更改计时器过期前，相对计时器不会受到影响，但系统调整每个绝对计时器。 相对计时器始终过期后经过指定的时间单位数，而不考虑绝对系统时间。 绝对计时器到期特定系统时，因此绝对计时器的等待持续时间中的系统时间更改的更改。

 

 




