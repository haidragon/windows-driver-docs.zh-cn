---
title: 提交命令缓冲区
description: 提交命令缓冲区
ms.assetid: 3622697a-3989-4756-89d4-c67c81815d49
keywords:
- 命令缓冲区 WDK 显示，请提交
- 将 WDK 显示的命令缓冲区提交
- 传递 WDK 显示的命令缓冲区
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f45a3349afd5c4a1362615f44719c07284266bdd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379868"
---
# <a name="submitting-a-command-buffer"></a>提交命令缓冲区


## <span id="ddk_submitting_a_command_buffer_gg"></span><span id="DDK_SUBMITTING_A_COMMAND_BUFFER_GG"></span>


为传递通过 Windows Vista 图形堆栈的命令缓冲区，必须执行以下一系列操作：

1.  用户模式显示驱动程序将启动命令缓冲区提交如果 Direct3D 运行时将调用以下的用户模式显示驱动程序函数，以执行指定的操作之一：

    -   [**存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_present)函数以显示图形。
    -   [**刷新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_flush)函数提交硬件命令。
    -   [**锁**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lock)函数来锁定在当前的命令批处理中使用的资源。

    请注意用户模式显示驱动程序也始终启动命令缓冲区提交，每当命令缓冲区已满。

2.  用户模式显示驱动程序调用 Direct3D 运行时[ **pfnRenderCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_rendercb)函数以提交到运行时的命令缓冲区。

3.  DirectX 图形内核子系统调用显示微型端口驱动程序[ **DxgkDdiRender** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或[ **DxgkDdiRenderKm** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)函数验证命令缓冲区、 编写 DMA 缓冲区中的硬件的格式，并生成一个分配列表，其中介绍了使用的图面。 请注意尚未修补 DMA 缓冲区 （分配物理地址）。
    **请注意**  如果在运行时通过调用用户模式显示驱动程序的启动命令缓冲区提交[**存在**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_present)函数中，图形子系统调用显示微型端口驱动程序[ **DxgkDdiPresent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_present)函数，而非[ **DxgkDdiRender** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_render)或[**DxgkDdiRenderKm**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_renderkm)。

     

4.  视频内存管理器会调用显示微型端口驱动程序[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数来创建特殊用途的 DMA 缓冲区，称为分页缓冲区，将指定的分配中附带的 DMA 缓冲区到和从 GPU 可访问的内存的分配列表。 有关详细信息，请参阅[分页视频内存资源](paging-video-memory-resources.md)。

5.  GPU 计划程序调用显示微型端口驱动程序[ **DxgkDdiPatch** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_patch)函数以将物理地址分配给 DMA 缓冲区中的资源。 但是，计划程序不需要调用**DxgkDdiPatch**将物理地址分配给分页缓冲区，因为分页缓冲区的实际地址已传入，并且分配期间[ *DxgkDdiBuildPagingBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)调用。

6.  GPU 计划程序调用显示微型端口驱动程序[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数请求该驱动程序队列到 GPU 执行单元的分页缓冲区。

7.  GPU 计划程序调用显示微型端口驱动程序[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数请求该驱动程序队列到 GPU 执行单元的 DMA 缓冲区。 每个提交至 GPU 的 DMA 缓冲区包含 fence 标识符。 GPU 完成处理的 DMA 缓冲区后，GPU 会产生中断。

8.  在中断的通知显示微型端口驱动程序及其[ **DxgkDdiInterruptRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_interrupt_routine)函数。 显示微型端口驱动程序应显示为从 GPU，刚刚完成的 DMA 缓冲区的 fence 标识符。

9.  显示微型端口驱动程序应调用[ **DxgkCbNotifyInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_notify_interrupt)函数，以通知 DMA 缓冲区已完成的 GPU 计划程序。

10. 显示微型端口驱动程序应调用[ **DxgkCbQueueDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkcb_queue_dpc)排队延缓的过程调用 (DPC) 的函数。

11. 通知显示微型端口驱动程序的 DPC 处理大部分 DMA 缓冲区处理。

 

 





