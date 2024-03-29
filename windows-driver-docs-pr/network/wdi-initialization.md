---
title: Wi-fi 设备初始化
description: 本主题介绍的 Wi-fi 设备初始化后开机。
ms.assetid: EDF04E40-C278-42CE-8E17-F5AB0C1651EF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 250ec8ee8a365ebb0cf002374f5d19f0cc3fd532
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374710"
---
# <a name="wi-fi-device-initialization"></a>Wi-fi 设备初始化


本主题介绍的 Wi-fi 设备初始化后开机。 接通电源时，大多数 Wi-fi 设备显示在未初始化的模式下。 Wi-fi 设备没有足够的 ROM 来保存固件，因此 IHV 组件/驱动程序一部分的设备启动程序的设备的固件。 下图显示互连总线/独立方式初始化序列。

![wdi 初始化序列](images/wdi-initialization-sequence.png)

1.  IHV 组件负责固件下载到该适配器，适配器已启动时。 若要下载固件的确切机制是依赖总线。 此操作完成的上下文中[ *MiniportWdiOpenAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)调用。 这是一个异步操作。 主机负责确保该适配器完全初始化并准备进一步将命令发送到它之前处理命令。 实际的机制是互连依赖。
2.  后初始化适配器时，主机查询就设置属性，用于各种 Wi-fi 属性、 适配器和的微型端口初始化过程中创建端口 (Mac)。
3.  创建和初始化端口后，适配器可以接收任务和属性命令。

 

 





