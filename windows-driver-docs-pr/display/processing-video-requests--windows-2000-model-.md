---
title: 处理视频请求（Windows 2000 模型）
description: 处理视频请求（Windows 2000 模型）
ms.assetid: 86b3037e-2d18-46b0-8b02-c66be65a4001
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，处理请求
- 请求处理 WDK 微型端口
- I/O WDK 微型端口
- HwVidStartIO
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 375947591df95ffe9ef003b8009b9e2af8e146c5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363688"
---
# <a name="processing-video-requests-windows-2000-model"></a>处理视频请求（Windows 2000 模型）


## <span id="ddk_processing_video_requests_windows_2000_model__gg"></span><span id="DDK_PROCESSING_VIDEO_REQUESTS_WINDOWS_2000_MODEL__GG"></span>


对显示驱动程序的调用中发出的所有 I/O 请求**EngDeviceIoControl**视频端口驱动程序。 视频端口驱动程序，然后调用相应微型端口驱动程序[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)用一个指针指向每个函数[**视频\_请求\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)结构，它只是设置。 发送到的所有 VRPs *HwVidStartIO*有**IoControlCode**成员设置为 IOCTL\_视频\_*XXX*。

视频端口驱动程序还通过发送每个微型端口驱动程序管理的所有视频的微型端口驱动程序传入的请求的同步*HwVidStartIO*例程处理一次只有一个 VRP。 *HwVidStartIO*拥有每个输入的 VRP 微型端口驱动程序完成请求的操作并返回控件之前。 微型端口驱动程序完成当前 VRP 之前, 的视频端口驱动程序与 I/O 管理器对后续调用响应中发送任何未完成 IRP 代码保存[ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)通过相应的显示器驱动程序。

在视频的请求，接收[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)必须检查 VRP、 处理在适配器上的进行视频请求、 VRP 中设置相应的状态和其他信息和返回 **，则返回 TRUE**.

 

 





