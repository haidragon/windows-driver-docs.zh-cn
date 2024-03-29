---
title: 序列处理
description: 有关通过注册由 NFC CX 公开的特定驱动程序序列支持非标准 NCI 扩展的信息。
ms.assetid: D0BE9827-2A15-4AA5-ADB9-80071ED37583
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 970c46b7769b7c742430fdead9b686169684071f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386504"
---
# <a name="sequence-handling"></a>序列处理


最全面的非标准 NCI 功能和扩展由来自不同供应商的 NFCC 固件实现与芯片集配置、 固件下载和硬件优化。 通过注册由 NFC CX 公开的特定驱动程序序列，NFC 客户端驱动程序可以支持这些非标准扩展。 客户端驱动程序为特定的顺序处理程序通过注册[ **NfcCxRegisterSequenceHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxregistersequencehandler)函数。 它通常是在初始化期间，应在调用后[ **NfcCxDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxdeviceinitialize)。 这些处理程序通过调用注销[ **NfcCxUnRegisterSequenceHandler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxunregistersequencehandler)设备关闭期间。 客户端驱动程序的顺序处理程序回调调用后，NFC CX 驱动程序将不会发出任何 NCI 命令，直到 NFC 客户端驱动程序完成其处理。 这些序列处理程序回调旨在是异步的从而允许客户端通知其完成的 NFC CX 之前向控制器发出 I/O 请求的任何数量。 NFC CX 使用监视程序计时器机制来确定处于挂起的状态。 如果监视程序计时器过期的客户端的序列处理程序完成之前，触发的 bug 检查和 UMDF 主机进程将终止 UMDF 框架。

中的序列处理程序的一部分实现的任何其他逻辑的 NFC 客户端驱动程序的要求如下：

-   当处理这些序列 NFC 客户端发送任何 NCI 命令应确保不违反 NFC CX 由指定的当前状态的完整性。 因此，NFC 客户端必须处理此要求确保 NFC 设备的正常运行。 例如，处理初始化完成序列时，客户端驱动程序不应颁发 NCI 核心\_重置\_CMD 以重置芯片集。
-   NFC 客户端驱动程序所需确保 NCI 响应和向下发送到控制器的 NCI 命令生成的通知不发送到 NFC CX [ **NfcCxNciReadNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfccx/nf-nfccx-nfccxncireadnotification)函数。 这是必需的因为否则 NFC CX NCI 状态机将获取与它 NFCC 与交换的命令不同步。

## <a name="in-this-section"></a>本节内容


-   [序列](sequences.md)
-   [序列标志](sequence-flags.md)
-   [初始化序列](initialization-sequence.md)
-   [NFCEE 发现序列](nfcee-discovery-sequence.md)
-   [RF 发现序列](rf-discovery-sequence.md)
-   [标记 RF 数据交换序列](tag-rf-data-exchange-sequence.md)
-   [P2P RF 数据交换序列](p2p-rf-data-exchange-sequence.md)
-   [卡仿真 RF 序列](card-emulation-rf-sequence.md)

 

 
## <a name="related-topics"></a>相关主题
[NFC 设备驱动程序接口 (DDI) 概述](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[NFC 类扩展 (CX) 引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
