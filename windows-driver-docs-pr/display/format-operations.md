---
title: 格式操作
description: 格式操作
ms.assetid: 242e5b5a-4184-487a-aeda-19149caa941b
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示纹理格式的属性列
- 纹理格式列出了 WDK DirectX 8.0
- DPIXELFORMAT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7499aa4041c462ee53f9307a6b7abdca9cc120e0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566256"
---
# <a name="format-operations"></a>格式操作


## <span id="ddk_format_operations_gg"></span><span id="DDK_FORMAT_OPERATIONS_GG"></span>


报告支持图面上的格式时 DirectX 8.0 驱动程序还必须指示可以对该格式的图面中执行哪些操作。 通过报告是一种像素格式的受支持的操作**dwOperations**字段[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)结构。 驱动程序应将此字段设置为该格式表面的所有受支持操作的逻辑组合。

 

 




