---
title: ATA 微型端口驱动程序例程中的同步的访问
description: 未同步的 ATA 微型端口驱动程序例程中的同步的访问
ms.assetid: ed047579-9f22-4725-a4b0-3c44b8db89ef
keywords:
- ATA 端口驱动程序 WDK，同步
- 同步 WDK ATA 端口驱动程序
- 未同步的处理 WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b4835f91652cd490cd1a4f9291d1883fd0849e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368161"
---
# <a name="synchronized-access-within-ata-miniport-driver-routines"></a>ATA 微型端口驱动程序例程中的同步的访问


## <span id="ddk_synchronized_access_within_unsynchronized_ata_miniport_driver_rout"></span><span id="DDK_SYNCHRONIZED_ACCESS_WITHIN_UNSYNCHRONIZED_ATA_MINIPORT_DRIVER_ROUT"></span>


**请注意**ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能被修改或不可用在将来。 相反，我们建议使用[Storport 驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)并[Storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。


甚至当 ATA 微型端口驱动程序执行未同步的处理的 I/O 请求中时才及其[ **IdeHwBuildIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_buildio)例程，它可以同步对关键系统结构的访问通过调用[ **AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestsynchronizedroutine)。 此例程类似于[ **StorPortSynchronizeAccess** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nf-storport-storportsynchronizeaccess) Storport I/O 模型中提供的例程。 有关如何 Storport 微型端口驱动程序管理的详细信息的同步访问的关键数据结构，请参阅[内未同步的微型端口驱动程序例程的同步访问](synchronized-access-within-unsynchronized-miniport-driver-routines.md)。

当 ATA 微型端口驱动程序调用**AtaPortRequestSynchronizedRoutine**，它必须提供指向回调例程的指针。 回调例程处理 I/O 请求必须与中断处理程序同步的一部分。 为了提高性能，编写驱动程序以时间为可能要执行的回调例程。

 

 


