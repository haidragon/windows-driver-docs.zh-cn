---
title: 用户插入设备
description: 用户插入设备
ms.assetid: 1968270b-ce57-4a8c-8b7a-bbd4a972435d
keywords:
- 电源管理方案 WDK UMDF，插入设备
- 插入设备方案 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd71fa2fa7c86ae87cbb8ea6cc0c6fc3d559993b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385337"
---
# <a name="a-user-plugs-in-a-device"></a>用户插入设备


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当用户插入设备时，框架将调用 UMDF 驱动程序的即插即用和电源管理中按以下顺序，从设备到达的回调方法将状态图的底部：

![umdf 驱动程序的设备枚举和启动序列](images/umdf-powerup-sequence.png)

首先调用驱动程序的框架[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)回调，以便该驱动程序可以创建设备回调对象和一个用于表示设备的 framework 设备对象。 框架将继续进行向上访问序列，直到该设备正常调用驱动程序的回调例程。

框架将继续通过此序列的每个支持使用驱动程序的最低驱动程序堆栈中启动一个时，驱动程序的设备的 UMDF 函数或筛选器驱动程序。

 

 





