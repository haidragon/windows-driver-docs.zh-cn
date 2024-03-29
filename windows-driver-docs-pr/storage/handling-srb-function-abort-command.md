---
title: 处理 SRB_FUNCTION_ABORT_COMMAND
description: 处理 SRB_FUNCTION_ABORT_COMMAND
ms.assetid: 74d46df6-2e3e-45d8-bedb-a81a80a0aec1
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB_FUNCTION_ABORT_COMMAND
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61d4d49db615e763ddba21653fe9612e6aebeea3
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716937"
---
# <a name="handling-srbfunctionabortcommand"></a>处理 SRB\_函数\_中止\_命令


## <span id="ddk_handling_srb_function_abort_command_kg"></span><span id="DDK_HANDLING_SRB_FUNCTION_ABORT_COMMAND_KG"></span>


*HwScsiStartIo*例程还会负责处理与传入 Srb**函数**成员设置为 SRB\_函数\_中止\_命令。

中止请求，微型端口驱动程序的*HwScsiStartIo*例程应验证，给定的 SRB 不已中止已通过调用**ScsiPortGetSrb**目标逻辑单元并将进行比较指针返回到当前 SRB **NextSrb**值。 如果它们不相等，已中止当前 SRB，和微型端口驱动程序*HwScsiStartIo*例程应执行以下操作：

1.  设置输入 SRB 的**SrbStatus**到 SRB\_状态\_中止\_失败。

2.  调用[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)与_NotificationType_**RequestComplete**和 SRB 中的输入。

3.  调用**ScsiPortNotification**再次_NotificationType_**NextRequest**，或与**NextLuRequest**如果 HBA 支持有标记的队列或每个逻辑单元的多个请求。

否则为*HwScsiStartIo*例程执行以下操作：

1.  设置在其设备、 逻辑单元和/或 SRB 扩展请求上下文。

2.  程序 HBA 中止给定**NextSrb**请求。

 

 




