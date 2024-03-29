---
title: 中断服务例程简介
description: 中断服务例程简介
ms.assetid: e83eb873-7cdf-4faf-9a6e-cc5954ebf1d6
keywords:
- 中断服务例程 WDK 内核，有关 Isr
- Isr WDK 内核，有关中断服务例程
- InterruptService
- 基于行的中断 WDK 内核
- 中断行 WDK 内核
- 消息信号中断 WDK 内核
- InterruptMessageService
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9abcb3032a9003aa774e3b764f77fbce850b713
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369730"
---
# <a name="introduction-to-interrupt-service-routines"></a>中断服务例程简介


接收中断的物理设备的驱动程序将注册一个或多个中断服务例程 (ISR) 服务中断。 系统调用 ISR 每次收到中断。

有关端口和低于 PCI 2.2 总线的设备生成*基于行的中断*。 设备通过称为对专用 pin 发送电气信号生成中断*中断行*。 在 Windows Vista 之前的 Microsoft Windows 版本仅支持基于行的中断。

从 PCI 2.2 开始，可以生成 PCI 设备*消息信号中断*。 设备的数据值写入到特定地址生成的消息信号中断。 Windows Vista 和更高版本操作系统支持基于行和消息信号中断。

系统支持两种不同类型的 Isr:

-   该驱动程序可以注册[ *InterruptService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kservice_routine)例程来处理基于行或消息信号中断。 （这是唯一可用在 Windows Vista 之前的类型）。系统通过驱动程序提供的上下文值。

-   该驱动程序可以注册[ *InterruptMessageService* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kmessage_service_routine)例程来处理消息信号中断。 系统将驱动程序提供的上下文值和中断消息的消息 ID 传递。

有关注册设备的中断提供服务的 InterruptService 或 InterruptMessageService 例程的详细信息，请参阅[简介 Message-Signaled 中断](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-message-signaled-interrupts)。
 

 




