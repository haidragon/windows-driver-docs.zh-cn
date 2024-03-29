---
title: I/O 队列的电源管理
description: I/O 队列的电源管理
ms.assetid: 2e1bf9d2-615b-49b0-b677-f41b23c42eda
keywords:
- 电源管理 WDK KMDF，I/O 队列
- I/O 队列 WDK KMDF，电源管理
- I/O 请求 WDK KMDF，电源管理
- 电源管理的 I/O 队列 WDK KMDF
- 工作状态 WDK KMDF
- PowerManaged 设置 WDK KMDF
- 低功耗状态 WDK KMDF
- 睡眠电源管理 WDK KMDF
- 电源状态 WDK KMDF
- 设备电源状态 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b5a40b4e989d41036002b67f3c02131eec8decb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379619"
---
# <a name="power-management-for-io-queues"></a>I/O 队列的电源管理


当框架收到定向到一个驱动程序的设备的 I/O 请求时，框架会将该请求放在 I/O 队列中。 通过提供请求处理程序或通过轮询队列，该驱动程序可以从 I/O 队列获取 I/O 请求。 有关 I/O 队列的详细信息，请参阅[Framework 队列对象](framework-queue-objects.md)。

可以在设计您的驱动程序，应 I/O 请求您的驱动程序将接收为两个类别进行分组：

1.  要求设备在其工作 (D0) 状态下，获得的请求包括：
    -   读取或写入请求需要设备的功能驱动程序从中读取数据，或将数据写入到设备。
    -   设备控制请求的函数或总线驱动程序无法服务而无需访问设备。

2.  请求不需要设备以在其工作 (D0) 状态，包括：
    -   设备控制请求的函数或总线驱动程序可以服务而无需访问设备。
    -   可能的所有请求的筛选器驱动程序接收。
    -   驱动程序堆栈中的所有驱动程序，如果收到的堆栈支持不与任何硬件进行通信的仅限软件的设备的所有请求。

除非你正在编写筛选器驱动程序，或不与硬件通信堆栈的驱动程序，很可能您的驱动程序将收到不这样做要求设备在其工作状态，以及一些的某些请求。

若要支持这两种请求类型，该框架提供两种类型的 I/O 队列： 的那些*电源管理*和那些不是。 当您的驱动程序创建每个其 I/O 队列时，它会设置**PowerManaged**在队列中的成员[ **WDF\_IO\_队列\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/ns-wdfio-_wdf_io_queue_config)为结构**WdfTrue**或**WdfFalse**以指示以下值之一：

-   如果您的驱动程序设置**PowerManaged**到**WdfTrue**，队列是电源管理。

    电源管理队列中可用的 I/O 请求时，框架提供给驱动程序请求的仅当设备处于其工作 (D0) 状态。 因此，只要您的驱动程序收到请求时从电源管理的队列，可保证在 framework 即用设备。 如果设备不处于工作状态，框架存储在队列中的请求，直到设备变得可用。

    如果设备处于低功耗状态，因为它处于空闲状态，并且如果框架将 I/O 请求放入一个驱动程序的电源管理队列，框架会要求驱动程序堆栈，以将设备还原到其工作状态之前它将请求传递到您的驱动程序。

    如果设备是在低功耗状态，因为系统不是在其工作 (S0) 状态，并且如果该框架将 I/O 请求的一个驱动程序的电源管理队列中，框架将等待，直至设备返回到其工作 (D0) 状态，然后提供请求uest 到您的驱动程序。

    因为框架不会提供 I/O 请求从电源管理队列向驱动程序设备不处于工作状态，如果*驱动程序位于上面*[电源策略所有者](power-policy-ownership.md) *在驱动程序堆栈不能使用电源管理的 I/O 队列*。 如果位于上方的电源策略所有者的驱动程序使用电源管理的队列，并且设备处于低功耗状态，该驱动程序不会接收请求并不能将它传递给 power 策略所有者。 因此电源策略所有者，它控制设备的电源状态，不会不会唤醒设备。

-   如果您的驱动程序设置**PowerManaged**到**WdfFalse**，队列不是电源管理。

    不是电源管理队列中可用的 I/O 请求时，框架会将请求传递给无论设备是否在其工作 (D0) 状态的驱动程序。 如果你已设置您的队列，以便它仅接收请求，不需要访问设备，您的驱动程序可以提供服务每个请求，即使该设备不可用。

有关电源管理 I/O 队列的详细信息，请参阅[Using Power-Managed I/O 队列](using-power-managed-i-o-queues.md)。

几个的驱动程序需要某些直接插即用 (PnP) 控制和电源管理操作。 可以使用这些驱动程序*自行管理 I/O*。 有关详细信息，请参阅[使用自我管理 I/O](using-self-managed-i-o.md)。

 

 





