---
title: SRB\_关闭\_设备\_实例
description: SRB\_关闭\_设备\_实例
ms.assetid: 55a72f4f-45b3-427d-80b7-620aac870a8a
keywords:
- SRB_CLOSE_DEVICE_INSTANCE 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_CLOSE_DEVICE_INSTANCE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87bde33d8a9fbbe7486d18e225bace5157806659
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358408"
---
# <a name="srbclosedeviceinstance"></a>SRB\_关闭\_设备\_实例


## <span id="ddk_srb_close_device_instance_ks"></span><span id="DDK_SRB_CLOSE_DEVICE_INSTANCE_KS"></span>


在类驱动程序将发送此请求关闭以前打开的适配器实例。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序应设置以下项之一为 SRB 中的状态：

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

大多数适配器不支持多个实例，因此，在这种情况下**FilterInstanceExtensionSize**字段中[ **HW\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_initialization_data)结构应设置为 0，且应永远不会收到此命令。

 

 





