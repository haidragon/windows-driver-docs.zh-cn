---
title: 中间驱动程序中的动态绑定
description: 中间驱动程序中的动态绑定
ms.assetid: 0b825141-2a19-40c6-82cf-8e897a25b0aa
keywords:
- 中间驱动程序 WDK 网络、 绑定
- NDIS 中间驱动程序 WDK、 绑定
- 动态绑定 WDK 网络
- 绑定操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1948ccc8ebb8013a4e995fe7e21172c0d2fdb5e0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386543"
---
# <a name="dynamic-binding-in-an-intermediate-driver"></a>中间驱动程序中的动态绑定





中间的驱动程序必须通过提供同时支持动态绑定到基础微型端口适配器[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)和一个[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

当微型端口适配器可用时，会调用 NDIS *ProtocolBindAdapterEx*函数可以将绑定到该微型端口适配器任何中间驱动程序。 绑定操作的一部分，中间驱动程序应初始化与该微型端口适配器相关联的虚拟微型端口。 微型端口适配器中删除时，将调用 NDIS *ProtocolUnbindAdapterEx*函数绑定到该微型端口适配器任何中间驱动程序。

以下主题包含有关中间驱动程序中动态绑定操作的其他信息：

[中间驱动程序绑定操作](intermediate-driver-binding-operations.md)

[打开基础中间驱动程序的适配器](opening-an-adapter-underlying-an-intermediate-driver.md)

[初始化虚拟微型端口](initializing-virtual-miniports.md)

[取消绑定操作的中间驱动程序](intermediate-driver-unbinding-operations.md)

 

 





