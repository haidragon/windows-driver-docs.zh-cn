---
title: 销毁与 Direct3D 上下文关联的对象
description: 销毁与 Direct3D 上下文关联的对象
ms.assetid: b464eb31-6062-4c0c-90a2-2de39b5a85ac
keywords:
- 内存泄漏 WDK DirectX 9.0
- 上下文 WDK Direct3D DirectX 9.0
- 销毁上下文 WDK DirectX 9.0 与关联的对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 361bf31541addd0034a9d46e6e016bd544d16cb3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384885"
---
# <a name="destroying-objects-associated-with-a-direct3d-context"></a>销毁与 Direct3D 上下文关联的对象


## <span id="ddk_destroying_objects_associated_with_a_direct3d_context_gg"></span><span id="DDK_DESTROYING_OBJECTS_ASSOCIATED_WITH_A_DIRECT3D_CONTEXT_GG"></span>


本主题适用于 DirectX 7.0 和更高版本。

若要防止内存泄漏、 显示驱动程序必须发布与 Direct3D 上下文关联的所有对象时，驱动程序的[ **D3dContextDestroy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)调用函数。 这些对象包括，例如，顶点和像素[着色器](direct3d-shaders.md)，[声明和顶点着色器代码](separating-declarations-and-code-for-vertex-shaders.md)，为资源[异步查询](supporting-asynchronous-query-operations.md)，和纹理资源。

 

 





