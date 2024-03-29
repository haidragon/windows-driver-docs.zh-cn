---
title: 功率表接口
description: 功率表接口
ms.assetid: be3ffb33-f1da-403d-b888-378ffd5cac8a
keywords:
- Power 计量和预算 WDK 接口
- 电源指示器接口 WDK
- PMI WDK 电源表
ms.date: 10/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 407b2b57697a8564ecf2e3202cba215128233363
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376969"
---
# <a name="power-meter-interface"></a>功率表接口


计量器接口 (PMI) 服务 I/O 请求数据包 (Irp) 的 WDM 驱动程序通过提供从[电源管理器](https://docs.microsoft.com/windows-hardware/drivers/kernel/power-manager)和 Power WMI 提供程序组件的[用户模式下 Power 服务](user-mode-power-service.md)(UMPS)。

PMI 为颁发的用户模式服务或应用程序的各种 I/O 控制 (IOCTL) 请求数据包提供支持。 此 IOCTL 接口提供了有关以下各项的信息：

-   电源计数功能和配置电源表。 这包括采样间隔和 power 阈值。

-   电源指示器电源预算配置。

-   资产的电表，供应商的名称和计量的序列号等信息。

-   当前电源级别和预算信息。

PMI 还提供支持计数事件，例如当达到或超过预算或 power 阈值的电源通知。

计数从 PMI 访问的信息的能力是通常是只读的。 但是，具体取决于电源表的功能，其预算方面的配置无法具有只读或读/写权限。

有关 PMI IOCTL 接口的详细信息，请参阅[PMI Ioctl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/pmi/index)。

 
**请注意**   PMB 基础结构支持 Windows 7、 Windows Server 2008 R2 和更高版本的 Windows 操作系统上。


 




