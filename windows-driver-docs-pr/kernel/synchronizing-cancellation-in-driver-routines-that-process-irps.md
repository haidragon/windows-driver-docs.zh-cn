---
title: 在处理 IRP 的驱动程序例程中同步取消
description: 在处理 IRP 的驱动程序例程中同步取消
ms.assetid: 0b252ebd-b9d5-4747-9a27-c1ecffdbae18
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3168dca81e35e5e423dda994ca1d6059a4a0f030
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355482"
---
# <a name="synchronizing-cancellation-in-driver-routines-that-process-irps"></a>在处理 IRP 的驱动程序例程中同步取消





任何驱动程序例程的取消排队或被调用，将保持为可取消状态，包括驱动程序的 IRP [ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)例程，必须执行以下操作：

1.  调用[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))。

2.  检查并确保**Irp**等于**DeviceObject-&gt;CurrentIrp**。 如果没有，请调用[ **IoReleaseCancelSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))并将控制权返回。

    如果两个不相同， **CurrentIrp**之间的时间可能已取消的[ **IoStartPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartpacket)发布取消自旋锁和此例程获取它。

3.  调用[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine)与**NULL** *CancelRoutine*用于从可取消状态中删除 IRP 的指针。

4.  检查**Irp-&gt;取消**字段，以确定是否要取消 IRP，或若要开始处理 I/O 请求。

    如果**Irp-&gt;取消**设置为**TRUE**，执行以下操作：

    -   调用**IoReleaseCancelSpinLock**。
    -   设置**Irp-&gt;IoStatus.Status**于状态\_已取消。
    -   设置**Irp-&gt;IoStatus.Information**为 0。
    -   调用[ **IoStartNextPacket** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket) (在*StartIo*例程) 启动的下一个数据包。
    -   调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)使用的 IO 优先级提升\_否\_完成 IRP 的增量。

    如果**Irp-&gt;取消**设置为**FALSE**，调用**IoReleaseCancelSpinLock**和开始请求处理 I/O 请求，或将 IRP 传递给下一步越低驱动程序，根据需要。

管理其自己的 Irp，而不是使用 I/O 管理器提供的设备队列，队列的驱动程序不需要调用时获取取消自旋锁**IoSetCancelRoutine**。 但是，这些驱动程序，应检查[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程的指针的**IoSetCancelRoutine**返回以确定是否已经启动了取消例程。

在处理可取消 Irp 任何驱动程序，每个处理 IRP，然后被请求的 I/O 操作的编程基础设备的驱动程序例程应检查所有传入 Irp 的可取消状态。 具体而言，最高级别的设备驱动程序同时使用*StartIo*并[ *ControllerControl* ](https://msdn.microsoft.com/library/windows/hardware/ff542049)例程应处理传入 Irp 中为这两个这些驱动程序例程已所述。

 

 




