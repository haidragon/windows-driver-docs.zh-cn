---
title: 默认时钟
description: 默认时钟
ms.assetid: 8c1a51e5-238b-446a-8f20-3fe1b82020b5
keywords:
- 默认时钟 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87c17ac3da20cde10ba78d63ec48670800d4ce7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376377"
---
# <a name="default-clocks"></a>默认时钟





可以调用流式处理微型驱动程序的内核[ **KsAllocateDefaultClockEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksallocatedefaultclockex)分配并初始化默认时钟结构。 或者，他们可以调用[ **KsAllocateDefaultClock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksallocatedefaultclock)，这是包装**KsAllocateDefaultClockEx**具有 nonclock 成员的默认参数。 调用[ **KsCreateDefaultClock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-kscreatedefaultclock)后使用**KsAllocateDefaultClockEx**初始化默认时钟。

支持默认时钟[KSPROPSETID\_时钟](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-clock)，并可能只是作为筛选器 pin 提供的任何其他时钟进行访问。 基础数据结构，但是，是创建的筛选器是固定的并且该 pin 和时钟的创建的任何实例共享。 时钟依赖于 pin 后，若要更新的当前状态和共享的数据结构中的其他元素。 默认时钟句柄通知请求和时钟的查询。

提供此时钟的筛选器上的 pin 是分配主时钟，pin 将拥有此时钟。 Pin 应引用时钟文件对象，就像它已分配某些其他时钟实现。 创建实例时，默认时钟不引用插针的文件对象。 相反，它会基于常见时钟结构的初始分配和时钟打开每个文件对象的内部引用计数。 即使时钟的所有者释放时钟结构，它始终位于，直到关闭的所有文件对象。 Pin 可以直接访问默认时钟对象，而不是通过标准时钟接口。

微型驱动程序可以支持[ **KSPROPERTY\_时钟\_FUNCTIONTABLE** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-clock-functiontable)属性来为用户模式下客户端提供一种机制以检查引用的时钟时间。 启用此选项，从而实现精确的速率匹配的函数指针具有的结构中填充此属性。

此外，微型驱动程序支持[ **KSPROPERTY\_流\_速率**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-stream-rate)如果指定的 pin 允许率更改的属性。

使用内核流式处理代理接口的应用程序中调用方法[IKsClockPropertySet](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-iksclockpropertyset)界面，用于获取和设置可能会用于其他地方速率匹配的物理时钟时间。

请参阅[质量管理](quality-management.md)有关相关信息。

 

 




