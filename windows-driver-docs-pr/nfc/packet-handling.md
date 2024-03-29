---
title: NCI 数据包处理
description: 在某些情况下，NFC CX 所定义的顺序可能不是足够的 NFC 客户端驱动程序以添加其自定义逻辑。
ms.assetid: 48BD5100-A1D4-4844-B53A-DAC73FDBB089
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c039455cd70cfbfa972f563fc4ef82ec5f7174c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373818"
---
# <a name="nci-packet-handling"></a>NCI 数据包处理


在某些情况下，NFC CX 所定义的顺序可能不是足够的 NFC 客户端驱动程序以添加其自定义逻辑。 在这些情况下，因为交换 NCI 的所有数据包通过 NFC CX 与 NFC 控制器通过 NFC 客户端驱动程序 （用于处理与传输层进行交互），这使 NFC 客户端驱动程序有机会注入之间的其他 NCI 数据包由 CX 和 NFCC 交换标准 NCI 数据包。 但是，NFC 客户端驱动程序必须确保以下要求是如果它利用除了要求此扩展性点满足 （1） 和 （2） 的序列可扩展性节中指定：

-   完成这些其他的 NCI 数据包交换后，NFC 客户端驱动程序必须发送的响应和通知与发送的 NFC CX 通过 NCI 命令相关联[ **NfcCxNciReadNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxncireadnotification)回调。

-   由于每个通道流控制执行 NFC CX 逻辑通道管理中，因此 NFC 客户端驱动程序不应执行的任何逻辑都将对此造成影响。 因此，建议 NFC 客户端驱动程序不会在其不知情的情况下打开的 CX 逻辑通道上发送的任何其他数据数据包。

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

