---
title: MPIO\_控制器\_信息 WMI 类
description: MPIO\_控制器\_信息 WMI 类
ms.assetid: 0448e056-2bbe-4e4f-a729-a872393222e5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 61f3df09cb9d28a4f13a6e99cd8709c2090203d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386173"
---
# <a name="mpiocontrollerinfo-wmi-class"></a>MPIO\_控制器\_信息 WMI 类


MPIO 驱动程序使用 MPIO\_控制器\_信息 WMI 类，以标识存储控制器和其关联的 DSM。

```cpp
class MPIO_CONTROLLER_INFO
{

    //
    // Devices behind this controller will have a matching
    // ControllerId in the PDO_INFORMATION class.
    //
    [WmiDataId(1)] uint32 IdentifierType;
    [WmiDataId(2)] uint32 IdentifierLength;
    [WmiDataId(3)] uint8 Identifier[32];
    [WmiDataId(4)] uint32 ControllerState;
    [WmiDataId(5)] uint32 Pad;
    [WmiDataId(6), MaxLen(63)] string AssociatedDsm;
};
```

此类定义编译时通过 WMI 工具套件，它会生成[ **MPIO\_控制器\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mpiowmi/ns-mpiowmi-_mpio_controller_info)数据结构。 没有与此 WMI 类相关联的方法。

 

 





