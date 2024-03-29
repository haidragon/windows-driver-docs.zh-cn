---
title: UMDF 对象和接口
description: UMDF 对象和接口
ms.assetid: da816fef-a24f-4456-9d4a-36f291afe8b5
keywords:
- 用户模式驱动程序框架 WDK 对象
- 用户模式驱动程序 WDK UMDF，对象
- 对象 WDK UMDF
- UMDF 对象 WDK
- 接口 WDK UMDF
- framework 对象 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c76875f357624d9bec20a861a2faa4bd6d7583c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372307"
---
# <a name="umdf-objects-and-interfaces"></a>UMDF 对象和接口


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

用户模式驱动程序框架 (UMDF) 组成一组协同对象。 UMDF 创建和管理一系列对象公开给用户模式设备驱动程序。 这些对象中的部分由应用程序触发的操作，如 I/O 请求，响应 UMDF 驱动程序调用 UMDF 接口方法时创建其他 UMDF 对象时创建。 例如，若要创建的 I/O 队列对象，该驱动程序调用[ **IWDFDevice::CreateIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createioqueue)方法。

以下主题介绍了核心 framework 对象，它们基于组件对象模型 (COM) 和 UMDF DDI 编程模型的子集：

-   [Framework 对象](framework-objects.md)
-   [Framework 对象层次结构](framework-object-hierarchy.md)
-   [基于 COM 子集的 UMDF](umdf-based-on-com-subset.md)
-   [UMDF DDI 编程模型](umdf-ddi-programming-model.md)
-   [管理对象的生存期](managing-the-lifetime-of-objects.md)

 

 





