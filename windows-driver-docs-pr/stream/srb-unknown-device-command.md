---
title: SRB\_未知\_设备\_命令
description: SRB\_未知\_设备\_命令
ms.assetid: 89bc2176-e384-48bf-82d8-4a8ab2bd5159
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcd4836553f8e1bf0b2b1f3f6f14c4bdb17328dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377837"
---
# <a name="srbunknowndevicecommand"></a>SRB\_未知\_设备\_命令


## <span id="ddk_srb_unknown_device_command_ks"></span><span id="DDK_SRB_UNKNOWN_DEVICE_COMMAND_KS"></span>


在类驱动程序发送此请求将不知道如何微型驱动程序的句柄的 Irp 传递。 *pSrb*-&gt;**Irp**指向未处理 IRP。 请参阅[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)。

此请求可以用作流类并不了解，但微型驱动程序可能的 Irp 的 IRP 传递机制。 例如，有几个插即用 (PnP) Irp 的流类不会处理，但该 1394年照相机驱动程序执行。

如果微型驱动程序不支持 SRB\_未知\_设备\_命令，或者在不处理 IRP，但它应设置 pSRB-&gt;状态设置为状态\_不\_实现。

 

 





