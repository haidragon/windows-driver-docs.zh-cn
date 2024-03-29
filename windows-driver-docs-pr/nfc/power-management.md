---
title: NFP 电源管理
description: NFP 电源管理
ms.assetid: A47F4B01-A912-410A-8CF8-656D2C125148
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8446945e110e8093bd3e790f2278049237f44979
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386524"
---
# <a name="nfp-power-management"></a>NFP 电源管理


NFP 设备运行三个电源模式之一。 这些模式才*active*，*空闲*，*备用*，以及*power 删除*。 禁用发布或订阅到设备时，NFP 设备可以进入低能耗模式。 NFP 驱动程序将转换为启用的响应中的电源模式之一的设备，或禁用从 Windows 通知。

NFP 驱动程序将收到[ **IOCTL\_NFP\_启用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_enable)或者[ **IOCTL\_NFP\_禁用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_disable)控制代码，以便启用或禁用订阅、 发布和是否存在事件。 这些控制代码也会触发设备电源模式更改。 [近场邻近 (NFP) 的连接的备用平台的电源管理](https://docs.microsoft.com/windows-hardware/design/device-experiences/near-field-promiximity--nfp--power-management-for-modern-standby-platforms)主题提供了适用于 NFP 设备的电源模式更改的详细的说明。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[邻近 DDI 引用附近](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

