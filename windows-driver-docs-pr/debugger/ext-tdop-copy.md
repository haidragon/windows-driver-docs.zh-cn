---
title: EXT\_TDOP\_复制
description: EXT\_TDOP\_复制子操作的调试\_请求\_EXT\_类型化\_数据\_ANSI 请求操作生成的类型化的数据说明的副本。
ms.assetid: 2de920de-db93-408d-8e80-a29c4e2930a0
keywords:
- EXT_TDOP_COPY Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_COPY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c94215a29e8414bd2b4e0a6c7364d531e8fe6b04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361365"
---
# <a name="exttdopcopy"></a>EXT\_TDOP\_复制


EXT\_TDOP\_复制的子操作[**调试\_请求\_EXT\_类型化\_数据\_ANSI** ](debug-request-ext-typed-data-ansi.md)[**请求**](request.md)操作生成的类型化的数据说明的副本。

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**Operation**  
设置为 EXT\_TDOP\_复制此子操作。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定的原始实例[**调试\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_debug_typed_data)结构。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收的实例的副本[**调试\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_debug_typed_data)指定结构**InData**。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态**  
接收此子操作返回的状态代码。 这是与返回的值相同[**请求**](request.md)。

<a name="remarks"></a>备注
-------

EXT\_TDOP\_副本是中的值[ **EXT\_TDOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)枚举。

此子操作的参数属于[ **EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)结构。 EXT 隶属\_类型化\_前面的参数部分中未列出的数据不使用此子操作，应设置为零。 前面的 Parameters 节中的成员的说明指定使用的成员。 在成员更多详细信息，请参阅**EXT\_类型化\_数据**。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[**DEBUG\_REQUEST\_EXT\_TYPED\_DATA\_ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT\_TDOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT\_类型化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**请求**](request.md)

 

 






