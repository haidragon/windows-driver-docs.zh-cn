---
title: 视频微型端口驱动程序的设备扩展 (XDDM)
description: 视频微型端口驱动程序的设备扩展（Windows 2000 模型）
ms.assetid: 4d7841d1-39e2-4bdf-b79b-3feb363a0fe5
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，设备扩展
- 设备扩展 WDK 微型端口
- 扩展 WDK 视频微型端口
- 适配器状态 WDK 微型端口
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 7a21b78fafd8d6f79f6c29937aaa086d453e0714
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716897"
---
# <a name="video-miniport-drivers-device-extension-windows-2000-model"></a>视频微型端口驱动程序的设备扩展（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_s_device_extension_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_S_DEVICE_EXTENSION_WINDOWS_2000_MODEL__GG"></span>


设备扩展是特定于适配器的状态信息的每个微型端口驱动程序的主要和只有全局存储区域。

每个微型端口驱动程序定义的大小、 内部结构和其设备扩展的内容。 视频端口驱动程序传递一个指针，除每个系统定义的微型端口驱动程序函数的输入参数作为设备扩展**DriverEntry**和实现，如果[ *HwVidSynchronizeExecutionCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pminiport_synchronize_routine)并*SvgaHwIoPortXxx*函数。 许多**视频端口**_Xxx_函数作为自变量也需要此指针。

微型端口驱动程序还必须使用设备扩展来维护单个适配器的状态信息。 系统检测到每个适配器都有单独的状态信息保留在单独的设备扩展。 微型端口驱动程序必须使用全局变量来存储每个适配器的任何状态。 这一点尤为重要，以便提供无缝的多个监视的支持。

 

 





