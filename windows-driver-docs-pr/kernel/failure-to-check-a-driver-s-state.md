---
title: 无法检查驱动程序的状态
description: 无法检查驱动程序的状态
ms.assetid: 963f79f6-2282-41bd-9cf4-bd5bc02a510e
keywords:
- 可靠性 WDK 内核驱动程序状态检查
- 检查驱动程序状态
- 驱动程序状态检查
- 验证驱动程序状态
- 正确的设备状态 WDK 内核
- 设备状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5abed19a2fc7f9095afbd5e0831460123496f494
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386616"
---
# <a name="failure-to-check-a-drivers-state"></a>无法检查驱动程序的状态





在以下示例中，驱动程序使用**ASSERT**宏，以检查正确的设备中的状态已检验版本，但不会检查设备状态免费生成中：

```cpp
   case IOCTL_WAIT_FOR_EVENT:

      ASSERT((!Extension->WaitEventIrp));
      Extension->WaitEventIrp = Irp;
      IoMarkIrpPending(Irp);
      status = STATUS_PENDING;
```

在调试内部版本，如果该驱动程序已持有 IRP 挂起状态，系统将断言。 在免费版本中，但是，该驱动程序不检查此错误。 两次调用相同的 IOCTL 原因驱动程序无法继续跟踪的 IRP。

在多处理器系统上，此代码片段可能会导致其他问题。 假设在条目上此例程具有 （操作的权限） 的所有权此 IRP。 当该例程将保存**Irp**中的全局结构指针**扩展-&gt;WaitEventIrp**，另一个线程可以从该全局结构获取 IRP 地址并对执行操作IRP。 若要避免此问题，该驱动程序应将标记挂起的 IRP 将保存 IRP 和应包括对这两个调用前[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)和联锁序列中的分配。 一个[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel) IRP 的例程也有必要。

 

 




