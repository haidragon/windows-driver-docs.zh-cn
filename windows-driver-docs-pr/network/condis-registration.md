---
title: CoNDIS 注册
description: CoNDIS 注册
ms.assetid: 6db5a4a2-f090-4688-99fa-9d22ca7077ed
keywords:
- CoNDIS WDK 网络、 注册
- 注册的 CoNDIS 驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c02d91031d87c33fe723027f893af0cd745cfc54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385100"
---
# <a name="condis-registration"></a>CoNDIS 注册





若要支持的 CoNDIS，NDIS 驱动程序必须注册可选的 CoNDIS 函数入口点。 NDIS 驱动程序调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数以注册可选服务。

本部分包括以下主题：

[CoNDIS 微型端口驱动程序注册](condis-miniport-driver-registration.md)

[CoNDIS 客户端注册](condis-client-registration.md)

[CoNDIS 调用管理器注册](condis-call-manager-registration.md)

[CoNDIS MCM 注册](condis-mcm-registration.md)

 

 





