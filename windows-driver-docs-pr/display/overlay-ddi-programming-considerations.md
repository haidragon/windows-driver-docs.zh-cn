---
title: 覆盖 DDI 编程注意事项
description: 覆盖 DDI 编程注意事项
ms.assetid: 887624a7-0293-4add-94a7-d490ebd93205
keywords:
- 覆盖 DDI WDK Windows 7 显示，编程注意事项
- 覆盖 DDI WDK Server 2008 R2 显示，编程注意事项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1a8a74479524618050c25c870efe2d3387c440d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354708"
---
# <a name="overlay-ddi-programming-considerations"></a>覆盖 DDI 编程注意事项


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

当您实现[覆盖 DDI](overlay-ddi.md)在用户模式显示驱动程序，应考虑使用以下编程提示：

-   如果该驱动程序支持覆盖 DDI，它必须设置 D3DCAPS\_位覆盖**Caps**的成员[D3DCAPS9](https://go.microsoft.com/fwlink/p/?linkid=122122)结构。 D3DCAPS9 结构是 DirectX 9.0 SDK 文档中所述。 驱动程序设置 D3DCAPS\_覆盖位以响应对的调用其[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数在其中 D3DDDICAPS\_GETD3D9CAPS 值中设置**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构*pData*参数指向。

-   64 位而不是 32 位的显示格式时 (例如，当 DWM 使用 D3DDDIFMT\_A16B16G16R16F 取值[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)的显示模式的枚举)，则Direct3D 的运行时将覆盖颜色键中的低 32 位**DstColorKeyLow**的成员[ **D3DDDI\_OVERLAYINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddi_overlayinfo)结构和在高 32 位**DstColorKeyHigh**的成员**D3DDDI\_OVERLAYINFO**。

 

 





