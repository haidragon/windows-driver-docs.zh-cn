---
title: 处理系统电源的更改
description: 处理系统电源的更改
ms.assetid: 80e36a23-8a41-46f0-a7cb-0039c306a695
keywords:
- 电源更改 WDK 网络
- Nic WDK 网络、 电源源更改
- 网络接口卡 WDK 网络、 电源源更改
- 即插即用 WDK NDIS 微型端口，电源源更改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fec6724de9c670a1c0d7c8974091f7a1c6d31cf7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379829"
---
# <a name="handling-a-change-in-the-systems-power-source"></a>处理系统电源的更改





系统可以更改从电池电源到 AC 电源，反之亦然。

初始化微型端口驱动程序之后, NDIS 调用微型端口驱动程序[ *MiniportDevicePnPEventNotify* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_device_pnp_event_notify)函数，以通知系统的电源的微型端口驱动程序。 微型端口驱动程序可以使用此信息来调整 NIC 的功率消耗 例如，无线 LAN (WLAN) 设备的微型端口驱动程序无法降低功率消耗，如果系统正在使用电池电源或如果系统正在 AC 电源，请增加功率消耗。

 

 





