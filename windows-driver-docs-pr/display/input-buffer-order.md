---
title: 输入缓冲区顺序
description: 输入缓冲区顺序
ms.assetid: 99110b1a-1511-44f5-a4bb-a5e38fd41fff
keywords:
- 输入缓冲区 WDK DirectX VA
- 取消隔行扫描 WDK DirectX va，因此输入的缓冲区顺序
- 缓冲 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f35699f8c5c4ceebcabf9273fb7c5329bc957a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379913"
---
# <a name="input-buffer-order"></a>输入缓冲区顺序


## <span id="ddk_input_buffer_order_gg"></span><span id="DDK_INPUT_BUFFER_ORDER_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。**

对于每个组合去隔行和子流组合的情况下操作，启动到的驱动程序提供的调用时 VMR [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)回调函数。 在中*DdMoCompRender*调用，请**lpBufferInfo**的成员[ **DD\_RENDERMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构指向缓冲区的数组，描述目标面和每个输入视频源示例的图面。 *DdMoCompRender*函数反过来调用驱动程序的[ **DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/display/dxva-deinterlacebobdeviceclass-deinterlacebltex)函数。 有关详细信息，请参阅[从用户模式组件调用取消隔行扫描 DDI](calling-the-deinterlace-ddi-from-a-user-mode-component.md)。

数组中元素的顺序[ **DXVA\_VideoSample2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videosample2)中结构**源**隶属[ **DXVA\_DeinterlaceBltEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_deinterlacebltex)结构匹配**lpBufferInfo**数组与目标表面不存在的异常。

下面的主题介绍用于排列图面中的规则**lpBufferInfo**数组并提供一些示例来解释的图面序列顺序：

[输入的缓冲区顺序规则](input-buffer-order-rules.md)

[输入的缓冲区顺序示例 1](input-buffer-order-example-1.md)

[输入的缓冲区顺序示例 2](input-buffer-order-example-2.md)

[输入的缓冲区顺序示例 3](input-buffer-order-example-3.md)

[输入的缓冲区顺序示例 4](input-buffer-order-example-4.md)

[输入的缓冲区顺序示例 5](input-buffer-order-example-5.md)

[输入的缓冲区顺序示例 6](input-buffer-order-example-6.md)

 

 





