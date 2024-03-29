---
title: 编写 Unload 例程
description: 编写 Unload 例程
ms.assetid: 578f3499-28fc-412b-bbb7-75f8023fa7c1
keywords:
- 标准驱动程序例程 WDK 内核，卸载例程
- 驱动程序例程 WDK 内核，卸载例程
- 例程 WDK 内核，卸载例程
- 卸载例程 WDK 内核
- 卸载例程 WDK 内核，有关卸载例程
- 将驱动程序
- 驱动程序替换 WDK 内核
- 正在卸载驱动程序
- 重新加载驱动程序 WDK 内核
- 驱动程序卸载 WDK 内核
- 驱动程序重新加载 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a595acf53b68821110913161b7dee2997803d63c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374128"
---
# <a name="writing-an-unload-routine"></a>编写 Unload 例程





任何驱动程序，它可以替换，或卸载并重新加载，在系统运行时必须具有[ *Unload* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_unload)例程。 所有 WDM 驱动程序必须都具有*Unload*例程。

尽管*Unload*例程都是可选的非 WDM 驱动程序[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)将失败，不提供任何驱动程序*卸载*例程。

本部分包含以下主题：

[卸载日常环境](unload-routine-environment.md)

[卸载例程的功能](unload-routine-functionality.md)

 

 




