---
title: 创建和销毁上下文
description: 创建和销毁上下文
ms.assetid: 31462b0a-ed06-4138-ab91-7ec98bc5ff14
keywords:
- 上下文 WDK Direct3D，创建
- 上下文 WDK Direct3D 销毁
- D3dContextCreate
- D3dContextDestroy
- 销毁上下文 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c054cfb77603e54fd25747a864b075afe8fd91da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370219"
---
# <a name="creating-and-destroying-a-context"></a>创建和销毁上下文


## <span id="ddk_creating_and_destroying_a_context_gg"></span><span id="DDK_CREATING_AND_DESTROYING_A_CONTEXT_GG"></span>


驱动程序必须创建并初始化，它需要用于执行呈现的状态信息进行封装的特定于设备的上下文。 上下文; 之间不共享状态因此，驱动程序必须维护它会创建每个上下文的完整状态信息。

若要创建一个上下文，该驱动程序应执行以下步骤：

-   分配的设备特定的上下文和零初始化。

-   请参阅[ **D3dContextCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)需要在该回调完成的额外步骤。 **D3dContextCreate**应用程序创建 Direct3D HAL 设备时调用回调。 该驱动程序必须实现此回调。

该驱动程序必须能够引用由创建的所有纹理句柄[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)创建上下文中。 这使驱动程序以进行相关的纹理时调用此上下文中创建的所有特定于驱动程序的数据清除[ **D3dContextDestroy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)进行函数。

Direct3D 调用[ **D3dContextDestroy** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)应用程序请求 Direct3D HAL 设备被销毁。 该驱动程序应释放它分配到指定的上下文的所有资源。 这些资源包括，例如，纹理资源、 顶点和像素[着色器](direct3d-shaders.md)，[声明和顶点着色器代码](separating-declarations-and-code-for-vertex-shaders.md)，并为资源[异步查询](supporting-asynchronous-query-operations.md).

 

 





