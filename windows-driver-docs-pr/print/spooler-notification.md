---
title: 后台处理程序通知
description: 后台处理程序通知
ms.assetid: b5d9b909-f2e4-4773-903e-1dd73b0ca567
keywords:
- 后台处理程序通知 WDK 打印
- 打印后台处理程序通知 WDK
- 通知 WDK 打印后台处理程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9006653cc89ced0ce352ff7b8f2c81736c1294c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355087"
---
# <a name="spooler-notification"></a>后台处理程序通知





此功能是在 Windows Vista 及更高版本。

后台处理程序通知机制提供托管后台处理程序的组件 （如打印机驱动程序、 打印处理器和端口监视器） 和应用程序之间的双向通信路径。 所涉及的应用程序可以在不同的会话和安全上下文中运行。

后台处理程序通知机制解决了当打印后台处理程序进程中运行的组件需要在其中启动打印作业在会话中显示用户界面元素时发生的问题。 在 Windows 2000 及更早版本，始终显示由这些打印组件任何用户界面将出现在会话 0，后台处理程序服务运行的会话中。 若要帮助解决这个问题，两个后台处理程序函数已添加适用于 Windows XP [ **SplPromptUIInUsersSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-splpromptuiinuserssession)并[ **SplIsSessionZero** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-splissessionzero). 后台处理程序通知机制提供了更多的功能不是执行这些功能，仅限于显示对话框中的消息。

[后台处理程序通知的概述](overview-of-spooler-notification.md)

[后台处理程序通知术语](spooler-notification-terminology.md)

[公共接口](public-interfaces.md)

 

 




