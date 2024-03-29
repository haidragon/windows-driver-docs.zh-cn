---
title: 编写 AddDevice 例程
description: 编写 AddDevice 例程
ms.assetid: 93a272f4-888c-4cc8-b013-c6313c10a8d8
keywords:
- 标准驱动程序例程 WDK 内核，AddDevice 例程
- 驱动程序例程 WDK 内核，AddDevice 例程
- 例程 WDK 内核，AddDevice 例程
- AddDevice 例程 WDK 内核
- 系统空间内存分配 WDK 内核
- 系统资源存储 WDK 内核
- 存储系统资源
- 设备对象 WDK 内核，创建
- 设备初始化 WDK 内核
- 初始化设备
- AddDevice 例程 WDK 内核，有关 AddDevice 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59de0dc6a9d31c72fb6f509a2d9db4a671b254b2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374134"
---
# <a name="writing-an-adddevice-routine"></a>编写 AddDevice 例程





支持即插即用任何驱动程序必须具有[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。 *AddDevice*例程创建了一个或多个表示为其驱动程序执行输入/输出请求的物理、 逻辑，或虚拟设备的设备对象。 它还将附加的设备对象到设备堆栈，因此设备堆栈将包含每个驱动程序与设备关联的设备对象。

PnP 管理器中调用的驱动程序*AddDevice*例程的每个设备驱动程序控制。 *AddDevice*例程称为系统在初始化期间 （当第一次枚举了设备），并且只要新设备会枚举在系统运行时。

本部分包含以下主题：

[AddDevice 例程在函数或筛选器驱动程序](adddevice-routines-in-function-or-filter-drivers.md)

[AddDevice 总线驱动程序中的例程](adddevice-routines-in-bus-drivers.md)

[编写 AddDevice 例程准则](guidelines-for-writing-adddevice-routines.md)

 

 




