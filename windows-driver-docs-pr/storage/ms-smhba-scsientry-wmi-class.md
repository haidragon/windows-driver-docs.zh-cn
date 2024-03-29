---
title: MS\_SMHBA\_SCSIENTRY WMI 类
description: MS\_SMHBA\_SCSIENTRY WMI 类
ms.assetid: 8ac7a979-b3fe-4da6-a8e7-301c64b27e46
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e1e2d9bb44b382e421905625b8450c09282f4ba6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386122"
---
# <a name="mssmhbascsientry-wmi-class"></a>MS\_SMHBA\_SCSIENTRY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS\_SMHBA\_SCSIENTRY 类来存储生成的唯一标识 SCSI 逻辑单元和其适配器的操作系统的信息。 此类用于构造为逻辑单元的操作系统信息和 SSP 标识符之间的绑定。

MS\_SMHBA\_SCSIENTRY 类定义，如下所示在*Hbaapi.mof*:

```cpp
class MS_SMHBA_SCSIENTRY
{
    [HBAType("MS_SMHBA_PORTLUN"), WmiDataId(1)]
    MS_SMHBA_PORTLUN PortLun;

    [HBAType("HBA_LUID"), WmiDataId(2)]
    uint8  LUID[256];

    [HBAType("HBA_SCSIID"), WmiDataId(3)]
    HBAScsiID ScsiId;
};
```

此类定义编译时通过 WMI 工具套件，它会生成以下数据结构：

[**MS\_SMHBA\_SCSIENTRY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hbapiwmi/ns-hbapiwmi-_ms_smhba_scsientry)

没有与此 WMI 类相关联的方法。

 

 





