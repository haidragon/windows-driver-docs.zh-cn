---
title: 指定 DMA 缓冲区的段
description: 指定 DMA 缓冲区的段
ms.assetid: 7cd51f22-bf9b-4c45-98f0-e9e0d41dab96
keywords:
- 内存段 WDK 显示，DMA 缓冲区
- DMA 缓冲区 WDK 显示，内存段
- 缓冲 WDK 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f432e4b6f4032d7e3c6cf718fbfe439bb4d5cea7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376077"
---
# <a name="specifying-segments-for-dma-buffers"></a>指定 DMA 缓冲区的段


## <span id="ddk_specifying_segments_for_dma_buffers_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_DMA_BUFFERS_GG"></span>


显示微型端口驱动程序可以指定 aperture 段可以从哪些 DMA 分配缓冲区。 此外可以作为连续的锁定的系统内存中分配 DMA 缓冲区。

视频内存管理器分配并销毁 DMA 缓冲区，当应用程序需要它们时。 因此，视频内存管理器需要一段，它可以从其分配 DMA 缓冲区。 请注意，段集可能包含一个段。

当 Microsoft DirectX 图形内核子系统调用显示微型端口驱动程序[ **DxgkDdiCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)函数创建图形上下文设备，可以指定显示微型端口驱动程序视频内存管理器可以从其分配 DMA 缓冲区一段组。 如果显示微型端口驱动程序设置**DmaBufferSegmentSet**的成员[ **DXGK\_DEVICEINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo)然后视频内存管理器将为 0，结构DMA 缓冲区; 为分配连续非分页的内存在这种情况下，显示微型端口驱动程序必须通过使用 PCI 周期内，访问内存，并通过 DMA，必须在发送数据直接从内存的物理地址。 如果显示微型端口驱动程序设置**DmaBufferSegmentSet**不为零，然后视频内存管理器将分配可分页内存，并将映射到指定的 aperture 细分的页。 Aperture 段中的页泄露给显示微型端口驱动程序中调用其[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)函数。

请注意，在基本的视频内存管理器模型不支持 DMA 缓冲区在本地的视频内存中。

 

 





