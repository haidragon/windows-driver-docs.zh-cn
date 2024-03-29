---
title: USB 视频类实现
description: USB 视频类实现
ms.assetid: b390d741-9ddc-4bac-bca2-73e32461c5ed
keywords:
- USB 视频类驱动程序 WDK AVStream 实现
- 视频类驱动程序 WDK USB、 实现
- UVC 驱动程序 WDK AVStream 实现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ff01a736deeb7459cec5a2527539e06835b7a17
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383140"
---
# <a name="usb-video-class-implementation"></a>USB 视频类实现


提供 Microsoft USB 视频类驱动程序 (usbvideo.sys) 是固定为中心的 AVStream 微型驱动程序。 它为每个 USB 视频类创建筛选器工厂？ 枚举由操作系统的兼容设备实例。 该驱动程序还会创建在设备上，每个输入或输出终端的 pin 工厂与**数据流**的成员[ **KSPIN\_描述符**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)结构设置为相关值。

USB 视频类驱动程序使用内部设备拓扑报告的设备描述符来构造流式处理 (KS) 组成的筛选器、 节点和连接的拓扑关系图的内核。

USB 视频类根据的数量和类型的设备支持的控件，动态报告筛选器、 pin 和通过 KS 自动化表 AVStream 筛选器和 pin 描述符中的节点属性集。

根据每个视频或仍在设备上的图像数据终结点支持的数据格式，USB 视频类报告支持 KS 数据范围和各自 AVStream pin 描述符中的数据交叉处理程序的相应的列表。 USB 视频类驱动程序将通过信息导出[内核流式处理代理](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)模块。

USB 视频类驱动程序还支持音频/视频流同步;usbvideo.sys 可以充当 KS 主时钟，并将时间戳添加到视频样本。 USB 视频类规范包括有关硬件应如何提供对类驱动程序的计时信息的详细信息。

若要与 USB 视频类进行通信，用户模式下客户端调用 DirectShow 或媒体基础接口。 这些接口是 COM 接口包装器内核流式处理代理定义为插件。请参阅的详细信息的 Microsoft Windows SDK 文档[Media Foundation](https://go.microsoft.com/fwlink/p/?linkid=144771)。

 

 




