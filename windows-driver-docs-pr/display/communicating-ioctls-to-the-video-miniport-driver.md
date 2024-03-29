---
title: 将 IOCTL 传送到视频微型端口驱动程序
description: 将 IOCTL 传送到视频微型端口驱动程序
ms.assetid: 9f9ad20e-d8cf-485d-adad-c04eeb40b705
keywords:
- 微型端口驱动程序 WDK Windows 2000 Ioctl
- Ioctl WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0f4f95a39ff6d1f470a74a75fac5a763f827a6d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370657"
---
# <a name="communicating-ioctls-to-the-video-miniport-driver"></a>将 IOCTL 传送到视频微型端口驱动程序


## <span id="ddk_communicating_ioctls_to_the_video_miniport_driver_gg"></span><span id="DDK_COMMUNICATING_IOCTLS_TO_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


下图显示了显示器驱动程序与使用 Ioctl 的微型端口驱动程序的通信方式。

![说明显示驱动程序/视频微型端口驱动程序通信的关系图](images/dpy2.png)

显示驱动程序调用[ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)使用 IOCTL 将同步请求发送到的微型端口驱动程序。 GDI 使用输入和输出的单独缓冲区以将请求传递到 I/O 子系统。 I/O 子系统将请求路由到处理请求的微型端口驱动程序的视频端口。

某些 IOCTL 请求需要访问视频寄存器的微型端口驱动程序和其他存储或从微型端口驱动程序的数据结构中检索信息。 通常情况下，没有请求需要的微型端口驱动程序来执行实际的绘制操作。

一般情况下，和显示器驱动程序，除非模块化另外规定，否则处理绘制和其他严格要求时间的操作。 将 IOCTL 发送到微型端口驱动程序，若要执行的时间关键函数可能会降低系统性能。

请参阅[视频的微型端口驱动程序 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)有关的系统定义视频 Ioctl 说明。 可以通过添加扩展显示驱动程序和视频的微型端口驱动程序之间的接口*专用 IOCTL*，如中所述，必须格式化该[定义的 I/O 控制代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/defining-i-o-control-codes)。 如果您需要编写新 IOCTL，应首先联系 Microsoft 技术支持。

 

 





