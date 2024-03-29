---
title: NDIS 筛选器驱动程序开发路线图
description: NDIS 筛选器驱动程序开发路线图
ms.assetid: 346dae93-4cb7-4cb5-a2cf-41be9809fec2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03bf24b6974ebbf15fe1623e75302c12e0867eec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384532"
---
# <a name="roadmap-for-developing-ndis-filter-drivers"></a>NDIS 筛选器驱动程序开发路线图


若要创建的网络驱动程序接口规范 (NDIS) 筛选器驱动程序包，请执行以下步骤：

- 第 1 步：了解 Windows 体系结构和驱动程序。

  你必须了解驱动程序在 Windows 操作系统中的工作原理的基础知识。 了解基础知识将帮助你做出适当的设计决策，还可以简化开发过程。 有关驱动程序的基本原理的详细信息，请参阅[的所有驱动程序开发人员概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)。

- 步骤 2：了解有关 NDIS。

  有关常规信息有关 NDIS 和 NDIS 驱动程序，请参阅以下主题：

  [Windows 网络体系结构和 OSI 模型](windows-network-architecture-and-the-osi-model.md)

  [网络驱动程序的编程注意事项](network-driver-programming-considerations.md)

  [驱动程序堆栈管理](driver-stack-management.md)

  [NET\_缓冲体系结构](net-buffer-architecture.md)

- 步骤 3:确定其他 Windows 驱动程序的设计决策。

  详细了解如何使更多 Windows 设计决策，请参阅[创建可靠的内核模式驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/creating-reliable-kernel-mode-drivers)，[的 64 位驱动程序的编程问题](https://docs.microsoft.com/windows-hardware/drivers/kernel/programming-issues-for-64-bit-drivers)，和[创建国际 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/creating-international-inf-files)。

- 步骤 4：了解有关 Windows 驱动程序生成、 测试和调试的进程和工具。

  构建一个驱动程序不同于生成在用户模式应用程序。 Windows 驱动程序生成、 调试和测试过程，驱动程序签名，有关详细信息和[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)测试，请参阅[构建、 调试和测试驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 有关生成的详细信息，测试、 验证和调试工具，请参阅[驱动程序开发工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/index)。

- 步骤 5：读取[筛选器驱动程序简介主题](introduction-to-ndis-filter-drivers.md)。

- 步骤 6：读取[编写协议驱动程序部分](writing-ndis-miniport-drivers.md)。

  本部分提供的主要协议概述驱动程序接口。 这些接口包括协议驱动程序提供的函数 (*ProtocolXxx*函数) 和 NDIS 调用启动的操作。 提供了 NDIS **Ndis * Xxx*** 协议驱动程序调用以执行 NDIS 操作的函数。

- 步骤 7：审阅[NDIS 筛选器驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=617915)中[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库...

- 步骤 8：开发 （或端口），生成、 测试和调试您的 NDIS 驱动程序。

  如果要将迁移现有驱动程序移植指导，请参阅：

  -   [移植到 NDIS 6.0 的 NDIS 5.x 驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/network/porting-ndis-5-x-drivers-to-ndis-6-0)
  -   [移植到 NDIS 6.20 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-20.md)
  -   [移植到 NDIS 6.30 NDIS 6.x 驱动程序](porting-ndis-6-x-drivers-to-ndis-6-30.md)

  有关迭代构建、 测试和调试的详细信息，请参阅[概述的构建、 调试和测试过程](https://docs.microsoft.com/windows-hardware/drivers)。 此过程将有助于确保您构建适用的驱动程序。

- 步骤 9：创建您的驱动程序的驱动程序包。

  有关如何安装驱动程序的详细信息，请参阅[提供一个驱动程序包](https://docs.microsoft.com/windows-hardware/drivers)。 有关如何安装的 NDIS 驱动程序的详细信息，请参阅[安装和升级网络组件](installing-and-upgrading-network-components.md)。

- 步骤 10：签名和分发您的驱动程序。

  最后一步是登录 （可选） 和分发该驱动程序。 如果您的驱动程序符合质量标准，为定义[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)，可以将其分配通过 Microsoft Windows 更新计划。 有关如何将驱动程序分发的详细信息，请参阅[分发驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

这些是基本步骤。 其他步骤可能有必要在单独的驱动程序的需求。

 

 





