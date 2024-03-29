---
title: 电池微型类驱动程序功能
description: 电池微型类驱动程序功能
ms.assetid: f8da63fd-0bf9-4085-88c2-022c4ddc7caa
keywords:
- 电池 miniclass 驱动程序 WDK，功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f19d8871482119ef066459b91bf353f3ae87ca26
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354089"
---
# <a name="battery-miniclass-driver-functionality"></a>电池微型类驱动程序功能


## <span id="ddk_battery_miniclass_driver_functionality_dg"></span><span id="DDK_BATTERY_MINICLASS_DRIVER_FUNCTIONALITY_DG"></span>


电池 miniclass 驱动程序负责以下：

-   创建适用于其设备 FDO 并将特定于设备的信息存储在关联的设备扩展

-   分配和维护当前的电池的电池标记

-   跟踪的电池电量、 充电和电源状态

-   响应来自电池的状态信息的类驱动程序的请求

-   电池的电源状态更改时通知电池类驱动程序

-   在充电还是放电特定电池请求时

电池 miniclass 驱动程序的其他操作，如中所述处理 Ioctl，调用电池类驱动程序支持例程[电池类驱动程序的功能](battery-class-driver-functionality.md)。

每个电池 miniclass 驱动程序提供了一套[BatteryMini*Xxx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_battery/)例程。 电池类驱动程序调用这些例程以请求 miniclass 驱动程序执行特定于设备的任务。 此外，miniclass 驱动程序必须具有其他例程，如中所述[提供所需电池 Miniclass 驱动程序的功能](supplying-required-battery-miniclass-driver-functionality.md)。

 

 




