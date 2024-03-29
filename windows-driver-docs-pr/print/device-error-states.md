---
title: 设备错误状态
description: 设备错误状态
ms.assetid: 7d0fee11-0fdf-4490-88d0-fb074cbf4082
keywords:
- 错误状态 WDK 打印机
- 打印机错误状态 WDK
- 状态 WDK 打印机
- 脱机状态 WDK 打印机
- 热插拔总线 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5a8b44b2bde697dd3befcdd375aac08626ec5ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385400"
---
# <a name="device-error-states"></a>设备错误状态


打印设备和其驱动程序从用户可能会遇到任何错误状态应正常恢复。 它是所有设备的可能的错误状态的测试相关。 请确保设备通知的每个错误状态，用户和设备取消操作，将恢复，并从每个错误状态重新启动。 首次设置错误状态，并验证正确的错误状态的通知用户。

常见的打印机的错误状态包括：

-   **缺纸**

-   **打印门打开**

-   **墨粉不足**

-   **卡纸**

-   **Offline**

-   **热插拔总线错误**

测试每一种错误状态之前, 以及在打印作业期间，使用以下过程：

1.  设置错误状态，然后发送打印作业。

2.  验证可以取消、 恢复，并且重新启动该作业。

3.  设置以在打印作业期间发生的错误状态，然后再次验证，可以取消、 恢复，并重新启动该作业。

您还应为离线和热插拔的错误状态执行以下其他测试过程：

-   **Offline**
    -   打印机时将进入脱机状态，请验证打印作业保留在作业队列中，直到准备好进行试打印设备。 然后，作业应成功完成。
    -   期间和打印作业之前，请拔下从打印机的功能。 确认打印机重新获取作业队列，并开始试打印。 请参阅中的更多详细信息[电源管理](power-management.md)。
-   **热插拔总线错误**
    -   设备连接后，卸载和加载设备堆栈 (例如， [USB 驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index))。 发送打印作业之前、 期间和之后卸载堆栈。 例如，使用 USB 连接设备，卸载设备连接到 USB 根集线器或主机控制器。
    -   卸载和加载设备堆栈具有和没有正在进行中的打印作业进行测试。 验证可以取消、 恢复，并且重新启动该作业。
    -   重新加载设备堆栈，以允许恢复的打印作业。

 

 




