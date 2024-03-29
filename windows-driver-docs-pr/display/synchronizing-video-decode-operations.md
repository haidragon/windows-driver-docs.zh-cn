---
title: 同步视频解码操作
description: 同步视频解码操作
ms.assetid: 4c88bf8f-0f10-4281-b856-a0e056d69d0e
keywords:
- 视频解码 WDK DirectX va，因此同步
- 解码视频 WDK DirectX va，因此同步
- 同步 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ed23ab0b98491230657003d2c37443fe1ef74cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372041"
---
# <a name="synchronizing-video-decode-operations"></a>同步视频解码操作


## <span id="ddk_synchronizing_video_decode_operations_gg"></span><span id="DDK_SYNCHRONIZING_VIDEO_DECODE_OPERATIONS_GG"></span>


DirectX VA 2.0 的同步机制已改进从 1.0 版和更类似于 Microsoft Direct3D 操作所用的同步机制。

在 DirectX VA 1.0 中，主要由解码器执行同步。 解码器可以使用压缩的缓冲区之前，它将调用[ *DdMoCompQueryStatus* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_querystatus)函数来确定缓冲区是否可供使用 （也就是说，硬件不访问缓冲区）。 如果缓冲区不可用，解码器必须进入睡眠状态、 轮询，或执行其他操作。

DirectX VA 2.0 使用顶点缓冲区和索引缓冲区已使用 Direct3D 的同步模型。 在 DirectX VA 2.0 中，锁定压缩的缓冲区解码器执行同步。 如果用户模式显示驱动程序将尝试锁定压缩的缓冲区和缓冲区正在使用中，该驱动程序可以失败锁定或重命名缓冲区。 用户模式显示驱动程序请求的视频内存管理器时重命名缓冲区驱动程序设置**放弃**的成员[ **D3DDDICB\_LOCKFLAGS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddicb_lockflags)对的调用中的结构[ **pfnLockCb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_lockcb)函数。 如果用户模式显示驱动程序重命名缓冲区，则该驱动程序返回一个指向备用缓冲区，以便该解码器可继续使用而不被阻止。

通常情况下，对于 DirectX VA 2.0 中，同步都是问题仅当硬件会占用更多的缓冲区副本不直接压缩的缓冲区。

 

 





