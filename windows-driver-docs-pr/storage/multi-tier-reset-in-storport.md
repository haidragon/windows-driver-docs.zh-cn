---
title: Storport 中的多层重置
description: Storport 中的多层重置
ms.assetid: 11c717b9-5154-43dd-b357-ff093cabec4b
keywords:
- Storport 驱动程序 WDK，错误
- 错误 WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 865a3e4e6c96ead2631fc55fe0218fe84466e62b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384662"
---
# <a name="multi-tier-reset-in-storport"></a>Storport 中的多层重置


## <span id="ddk_multi_tier_reset_in_storport_kg"></span><span id="DDK_MULTI_TIER_RESET_IN_STORPORT_KG"></span>


Storport 驱动程序实现更高级的重置方案比 SCSI 端口驱动程序。 重置整个总线的 SCSI 端口方法便代价高昂的操作，即使在 SCSI 总线上。 在高性能的总线上，如光纤通道总线，总线重置甚至不可行。

如果可能，Storport 驱动程序和相关的更高级别的驱动程序会尝试重置逻辑单元。 如果此操作失败，Storport 会尝试将设备重置。 最后，如果此方法也会失败，Storport 重置总线。 此序列生成显著减少总线重置操作。

若要解决高性能的总线的更复杂要求，Storport 实现允许重置选项的更多的多层重置操作。 有两种类型的重置 Srb 可以请求，而不是一个通过发送：

最后，总线重置操作会受影响的同步回调例程，通过[ **HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)。

 

 




