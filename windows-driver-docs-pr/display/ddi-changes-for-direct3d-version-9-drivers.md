---
title: Direct3D 版本 9 驱动程序的 DDI 更改
description: Direct3D 版本 9 驱动程序的 DDI 更改
ms.assetid: b702c02d-3be6-46e8-9e53-5d33e5e3fc70
keywords:
- Direct3D 版本 10.1 WDK Windows 7 显示，DDI 的变化情况的 Direct3D 版本 9 的驱动程序
- Direct3D 9 版本的驱动程序 WDK Windows 7 显示
- Direct3D 版本 9 驱动程序 WDK Windows 7 显示，DDI 更改
- XR_BIAS WDK Windows 7 显示、 Direct3D 版本 9 DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad4249404fbdb6131b87a3f4640280695094014
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365100"
---
# <a name="ddi-changes-for-direct3d-version-9-drivers"></a>Direct3D 版本 9 驱动程序的 DDI 更改


本部分仅适用于 Windows 7 和更高版本的操作系统。

XR\_偏移是唯一的新扩展格式功能的 Windows 7 使其可供用户模式显示驱动程序只支持 Direct3D 版本 9 DDI。

此类用户模式下显示的驱动程序可以指示它支持 D3DDDIFMT\_A2B10G10R10\_XR\_偏置格式值从[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举。 该驱动程序通过创建一个条目的数组中指示这种支持填充[ **FORMATOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_formatop)中结构**pData**隶属[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)驱动程序将返回到调用的结构及其[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数和 D3DDDICAPS\_在中设置 GETFORMATDATA 值**类型**D3DDDIARG 成员\_GETCAPS。 此条目应指示，在**Operations**的成员**FORMATOP**，运行时可以执行与 D3DDDIFMT 图面的典型操作的所有\_A2B10G10R10\_XR\_偏差格式。 例如，驱动程序应将 FORMATOP\_\*\_中的位将呈现器目标**操作**。 该驱动程序还必须设置 FORMATOP\_DISPLAYMODE 和 FORMATOP\_中的位将 3DACCELERATION **Operations**。

如果驱动程序将返回[ **FORMATOP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_formatop) D3DDDIFMT 条目\_A2B10G10R10\_XR\_偏差格式，驱动程序可以随后接收对其的调用[**CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数来创建的资源 D3DDDIFMT\_A2B10G10R10\_XR\_偏差格式设置**格式**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构。

该驱动程序仅接收请求，以创建资源 D3DDDIFMT\_A2B10G10R10\_XR\_偏差格式为全屏显示翻转链。 桌面 Windows 管理器 (DWM) 处理窗口化表示法的 XR\_偏差着色器代码中。 该驱动程序应将 D3DDDIFMT\_A2B10G10R10\_XR\_偏置格式资源作为 D3DDDIFMT\_A2B10G10R10 格式中除了出扫描之外的所有操作，例如，可以将驱动程序视为 D3DDDIFMT\_A2B10G10R10\_XR\_偏置格式资源作为 D3DDDIFMT\_值混合处理、 筛选和格式转换操作的 A2B10G10R10 格式。 唯一的区别是如何 XR\_偏差会影响扫描扩展。有关扫描扩展的详细信息，请参阅[BGRA 扫描扩展支持](bgra-scan-out-support.md)。

 

 





