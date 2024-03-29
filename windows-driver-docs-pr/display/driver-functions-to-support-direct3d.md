---
title: 用于支持 Direct3D 的驱动程序函数
description: 用于支持 Direct3D 的驱动程序函数
ms.assetid: 949551c3-2172-454c-b398-eba468b90705
keywords:
- Direct3D WDK Windows 2000 显示中函数
- WDK Direct3D 函数
- 回调函数 WDK Direct3D
- LPD3DHAL_MYFUNCTIONDATA
- D3DHAL_MYFUNCTIONDATA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32d64ea7b6c1a20f51807a8afc56d6843c7d8d93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381091"
---
# <a name="driver-functions-to-support-direct3d"></a>用于支持 Direct3D 的驱动程序函数


## <span id="ddk_driver_functions_to_support_direct3d_gg"></span><span id="DDK_DRIVER_FUNCTIONS_TO_SUPPORT_DIRECT3D_GG"></span>


支持 Direct3D 的驱动程序提供 Direct3D 回调函数和 DirectDraw DDI 函数。 Direct3D DDI 回调原型如下所示：

```cpp
typedef DWORD (APIENTRY *LPD3DHAL_MYFUNCTIONCB) (LPD3DHAL_MYFUNCTIONDATA);
```

在前面的语法：

-   LPD3DHAL\_MYFUNCTIONCB 指向驱动程序实现可调用的回调*MyFunction*。 所有回调名称都是 pseudonames 确定显示驱动程序编写器。

-   LPD3DHAL\_MYFUNCTIONDATA 是指向 D3DHAL\_MYFUNCTIONDATA 结构传递给回调。 回调参数结构的特征，如下所示：
    -   每个结构的第一个成员**dwhContext**，是描述应在其中操作回调的 3D 上下文的上下文句柄。 此规则的唯一例外是 D3DHAL\_CONTEXTCREATEDATA 结构。
    -   每个结构的最后一个成员是**ddrval**。 此成员用于回调的返回值传递回 Direct3D，因此它可以返回到调用应用程序。

若要确定如何初始化 Direct3D 回调函数，请参阅[Direct3D 驱动程序初始化](direct3d-driver-initialization.md)。

下表列出了在 Direct3D 驱动程序中实现的 Direct3D 回调函数。 所有的回调函数所需的除[ **D3dValidateTextureStageState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)，它是可选的具体取决于硬件功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb" data-raw-source="[&lt;strong&gt;D3dContextCreate&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)"><strong>D3dContextCreate</strong></a></p></td>
<td align="left"><p>创建上下文。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb" data-raw-source="[&lt;strong&gt;D3dContextDestroy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb)"><strong>D3dContextDestroy</strong></a></p></td>
<td align="left"><p>销毁一个上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"><strong>D3dCreateSurfaceEx</strong></a></p></td>
<td align="left"><p>创建的纹理句柄和图面之间的关联。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal" data-raw-source="[&lt;strong&gt;D3dDestroyDDLocal&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_destroyddlocal)"><strong>D3dDestroyDDLocal</strong></a></p></td>
<td align="left"><p>销毁以前创建的所有 Direct3D 图面<a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex" data-raw-source="[&lt;strong&gt;D3dCreateSurfaceEx&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)"> <strong>D3dCreateSurfaceEx</strong> </a> ，属于同一个给定本地 DirectDraw 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb" data-raw-source="[&lt;strong&gt;D3dDrawPrimitives2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)"><strong>D3dDrawPrimitives2</strong></a></p></td>
<td align="left"><p>呈现基元，并返回到 Direct3D 的更新后的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate" data-raw-source="[&lt;strong&gt;D3dGetDriverState&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)"><strong>D3dGetDriverState</strong></a></p></td>
<td align="left"><p>返回状态为 DirectDraw 和 Direct3D 的运行时驱动程序有关的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb" data-raw-source="[&lt;strong&gt;D3dValidateTextureStageState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_validatetexturestagestatecb)"><strong>D3dValidateTextureStageState</strong></a></p></td>
<td align="left"><p>执行纹理阶段状态验证，所需的所有驱动程序的支持纹理。</p></td>
</tr>
</tbody>
</table>

 

为了支持 Direct3D，驱动程序必须至少支持 Microsoft DirectDraw，还必须实现某些 DirectDraw DDI 函数。 下表中列出与 Direct3D 支持有关的功能。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo" data-raw-source="[&lt;strong&gt;DrvGetDirectDrawInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgetdirectdrawinfo)"><strong>DrvGetDirectDrawInfo</strong></a></p></td>
<td align="left"><p>此函数可检索图形硬件的功能。 在此函数中初始化该驱动程序表明它支持 Direct3D。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo" data-raw-source="[&lt;strong&gt;DdGetDriverInfo&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverinfo)"><strong>DdGetDriverInfo</strong></a></p></td>
<td align="left"><p>运行时将查询此 Guid 与驱动程序有关的其他信息的回调函数。 多个 Guid 专属于 Direct3D 的驱动程序的支持。</p></td>
</tr>
</tbody>
</table>

 

DirectDraw 函数和回调实现详细信息的介绍[DirectDraw](directdraw.md)。

 

 





