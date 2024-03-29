---
title: 访问用户空间内存
description: 访问用户空间内存
ms.assetid: db0b6ba2-4cec-46c1-b13f-aba4c10a2d8c
keywords:
- 内存管理 WDK 内核，用户空间内存
- 用户空间内存 WDK 内核
- 虚拟用户空间内存 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc2706374d83158d506457b768d0c452dcd34f44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363456"
---
# <a name="accessing-user-space-memory"></a>访问用户空间内存





驱动程序无法通过用户模式虚拟地址直接访问内存，除非导致驱动程序的当前的 I/O 操作的用户模式线程的上下文中运行，并且它使用该线程的虚拟地址。

仅最高级别的驱动程序，例如 FSDs，可以确保将此类用户模式线程的上下文中调用其调度例程。 最高级别的驱动程序可以调用[ **MmProbeAndLockPages** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)锁定在较低的驱动程序的 IRP 设置之前，在用户缓冲区。

设置其设备对象的最低级别和中间驱动程序[缓冲 I/O](methods-for-accessing-data-buffers.md)或[直接 I/O](methods-for-accessing-data-buffers.md)可以依赖于 I/O 管理器或最高级别的驱动程序，要传递到锁定的用户的有效的访问缓冲或到系统空间缓冲 Irp 中。

 

 




