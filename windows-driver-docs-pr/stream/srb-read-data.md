---
title: SRB\_READ\_DATA
description: SRB\_READ\_DATA
ms.assetid: b59d705d-5215-42ee-85cf-369a2e69f99b
keywords:
- SRB_READ_DATA 流式处理媒体设备
topic_type:
- apiref
api_name:
- SRB_READ_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb81167225ba568a003db556f408f1264b095426
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377875"
---
# <a name="srbreaddata"></a>SRB\_READ\_DATA


## <span id="ddk_srb_read_data_ks"></span><span id="DDK_SRB_READ_DATA_KS"></span>


在类驱动程序收到的读取的请求的微型驱动程序。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序可以将以下项之一设置为 SRB 中的状态，或者它可以传递其他错误代码，以指示错误的情况下，例如内存错误和错误的参数。 在类驱动程序只检查状态\_成功。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态\_成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态\_不\_实现  
指示该函数不受微型驱动程序。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态\_IO\_设备\_错误  
指示发生了硬件故障。

### <a name="comments"></a>备注

值*pSrb*-&gt;**CommandData**。**DataBufferArray**指向的数组[ **KSSTREAM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_header)结构，一起描述了数据缓冲区。 *PSrb*指针指向[ **HW\_流\_请求\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)结构。 *pSrb*-&gt;**CommandData**。**NumberOfBuffers**指定数组的大小。

**当 SRB\_读取\_微型驱动程序收到数据命令时，响应的微型驱动程序例程应：**

1.  检查以确定当前的流状态。 微型驱动程序应仅接受读取的请求时在暂停或运行状态。 如果流已停止，它应立即完成并返回 SRB。

2.  SRB 放入队列。

 

 





