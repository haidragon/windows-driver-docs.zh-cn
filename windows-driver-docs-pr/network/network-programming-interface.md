---
title: 网络编程接口
description: 网络编程接口
ms.assetid: 74d706e1-5398-4685-b3ab-7b4c4b6b5588
keywords:
- NPI WDK 网络模块注册机构
- 客户端特性结构，WDK 网络模块注册机构
- 提供程序特性结构，WDK 网络模块注册机构
- 客户端调度表 WDK 网络模块注册机构
- 调度表 WDK 网络模块注册机构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5961cceedbeb93a4dcbc77cbeba3c42181bc68c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364019"
---
# <a name="network-programming-interface"></a>网络编程接口


一个*网络编程接口*，或 NPI，定义之间的接口[网络模块](network-module.md)，可以附加到另一个。 一个[客户端模块](client-module.md)如特定 NPI 的客户端只能附加到注册[提供程序模块](provider-module.md)，均将注册为提供程序的相同 NPI。 同样，为特定 NPI 的提供程序注册的提供程序模块只能附加到作为相同 NPI 的客户端注册的客户端模块。

每个 NPI 定义了以下项：

-   *NPI 标识符*用于唯一标识 NPI。 网络模块指定一个 NPI 标识符，以指示它支持网络模块注册自身网络模块注册机构 (NMR) 与特定 NPI。 网络模块可以通过将自身注册与 NMR 多次，一次为它支持每个 NPI 支持多个 NPIs。 NMR 将启动客户端模块附加到提供程序模块，仅当它们都支持相同 NPI。

-   一个可选[*客户端特征*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_client_characteristics)结构，它指定每个客户端模块的特定于 NPI 的特征。 此类特定于 NPI 的特征可能包括诸如 NPI 客户端模块支持，或该地址系列或协议的客户端模块需要哪些版本 （或版本）。 提供程序模块可以使用客户端模块的客户端特性结构中包含的信息来确定它将附加到客户端模块。 如果 NPI 未定义任何特征，NPI 特定于客户端，则不需要此结构。

-   一个可选[*提供程序特征*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netioddk/ns-netioddk-_npi_provider_characteristics)结构，它指定提供程序的每个模块的特定于 NPI 的特征。 此类特定于 NPI 的特征可能包括诸如 NPI 提供程序模块支持，或提供程序模块的地址族或协议支持的版本 （或版本）。 客户端模块可以使用提供程序模块的客户端特性结构中包含的信息来确定它将附加到提供程序模块。 如果 NPI 未定义任何特征，NPI 特定于提供程序，则不需要此结构。

-   零个或多个客户端模块回调函数。 提供程序模块已成功附加到客户端模块后，提供程序模块可以通过调用模块的回调函数的客户端访问客户端模块的功能。

-   一个或多个提供程序模块函数。 客户端模块已成功附加到提供程序模块后，客户端模块可以通过调用模块的函数的提供程序访问提供程序模块的功能。

-   一个*客户端调度表*结构，其中包含指向每个客户端模块回调函数的函数指针。 如果 NPI 未定义任何客户端模块回调函数，则不需要此结构。

-   一个*提供程序调度表*结构，其中包含指向每个提供程序模块函数的函数指针。

支持特定 NPI 的客户端模块使用 NPI 所定义的项目来实现该接口的客户端。 同样，支持特定 NPI 的提供程序模块使用 NPI 所定义的项目来实现接口的提供商端。

所有 NPI 所定义的项目都是不透明的 NMR NPI 标识符除外。 NMR 使用 NPI 标识符来确定哪些客户端模块应附加到提供程序的哪些模块。

 

 





