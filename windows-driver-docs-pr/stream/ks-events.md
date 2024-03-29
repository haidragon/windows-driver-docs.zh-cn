---
title: KS 事件
description: KS 事件
ms.assetid: 3eaa1d65-8417-4a07-b358-823394baec9b
keywords:
- 流式处理 WDK，事件的内核
- KS WDK 事件
- 流式处理事件 WDK 内核
- 事件设置 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7753843fe9ccabccb34978f279f23deb1864374
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382512"
---
# <a name="ks-events"></a>KS 事件





如果你正在编写 AVStream 微型驱动程序，请参阅[AVStream 中的事件处理](event-handling-in-avstream.md)。

事件集是相关的事件侦听器可以为其请求通知组。 例如，侦听器无法注册的设备状态更改或流的位置中的更改通知。 事件发生时，内核流式处理通知此事件注册任何客户端。

微型驱动程序描述如何通过提供支持事件，它们[ **KSEVENT\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_item)结构，其中包含指向处理例程的指针。

通过调用内核流式处理代理例程通知注册侦听器[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)与 IOCTL\_KS\_启用\_事件的控制代码和指针[ **KSEVENT** ](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))并[ **KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata).structures。

IOCTL\_KS\_禁用\_事件请求禁用指定的事件。 必须使用相同的指针，用于启用该事件，以禁用它。 此指针唯一地标识的事件。 （可选） 指定客户端可能**NULL**指针和长度为零，则客户端禁用所有活动事件。

所有事件集必须都支持 KSEVENT\_类型\_BASICSUPPORT 标志。 请参阅[ **KSEVENT** ](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))有关可用事件标志的列表。

某些事件类型需要其他参数来注册事件通知。 例如， [ **KSEVENT\_时钟\_位置\_标记**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)时钟到达特定时间戳时，会触发一个时钟上的事件。 因此，注册以接收此事件通知的客户端必须指定触发该事件的时间戳。

在这种情况下，微型驱动程序传递额外的数据参数中的数据缓冲区后[ **KSEVENTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)结构。 支持此类事件类型的微型驱动程序使用的扩展的数据结构，其中第一个成员是类型 KSEVENTDATA，保存通知数据。

 

 




