---
title: DPC 对象简介
description: DPC 对象简介
ms.assetid: ae8758f5-0e23-4db2-9eac-aab31d98247b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ad5796d121b085cd806c29894045608509c148d1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369770"
---
# <a name="introduction-to-dpc-objects"></a>DPC 对象简介





因为 Isr 必须尽可能快地执行，驱动程序通常必须推迟后 ISR 返回服务中断之前完成。 因此，系统提供的支持*延迟过程调用*(Dpc)，可以从 Isr 对其进行排队和执行的应用在更高版本时和比 ISR 降低 IRQL

每个 DPC 是与系统定义相关联*DPC 对象*。 系统提供每个设备对象的一个 DPC 的对象。 在系统初始化此 DPC 对象时驱动程序注册为已知的 DPC 例程[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)例程。 如果需要多个 DPC，驱动程序可以创建其他 DPC 对象。 这些额外 Dpc 被称为[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)例程。

DPC 对象内容不应直接引用由驱动程序中。 未记录的对象的结构。 驱动程序没有访问该系统提供的 DPC 对象分配给每个设备对象。 驱动程序将存储分配的额外 dpc 进行标记，但这些 DPC 对象的内容应仅引用由系统例程。

DPC 对象和 dpc 进行标记还可以使用计时器。 有关详细信息，请参阅[计时器对象和 dpc 进行标记](timer-objects-and-dpcs.md)。

 

 




