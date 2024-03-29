---
title: 处理设备管理的图面
description: 处理设备管理的图面
ms.assetid: 4403165f-c528-450e-9c96-77a9ce0778aa
keywords:
- Unidrv，设备管理的图面
- 设备管理面 WDK Unidrv
- surface 设备管理 WDK Unidrv
- 挂接图形 DDI 函数 WDK Unidrv
- DrvTextOut
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e468a5c320960b7d9f5d19ef2694499514f30f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378607"
---
# <a name="handling-device-managed-surfaces"></a>处理设备管理的图面





当 Unidrv 呈现打印的页面图像时，它使用 GDI 托管绘图图面。 所有图像都呈现为位图。 不能通过此方案中，例如能够绘制矢量，攻击者利用的功能的设备可以为设备管理的绘图图面提供自定义驱动程序支持。 若要支持设备管理面，必须提供插件，它实现以下呈现：

-   一组的挂钩所有 Unidrv 支持图形 DDI 绘图函数的函数。 以下函数必须挂接：[**DrvAlphaBlend**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvalphablend)
    [**DrvBitBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvbitblt)
    [**DrvCopyBits** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvcopybits)
     [ **DrvDitherColor**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvdithercolor)
    [**DrvFillPath** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvfillpath) 
     [ **DrvGradientFill**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvgradientfill)
    [**DrvLineTo** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvlineto) 
     [ **DrvPlgBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvplgblt)
    [**DrvRealizeBrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvrealizebrush)
    [**DrvStretchBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchblt) 
     [ **DrvStretchBltROP**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstretchbltrop)
    [**DrvStrokeAndFillPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokeandfillpath) 
     [ **DrvStrokePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvstrokepath)
    [**DrvTextOut**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout) 
     [ **DrvTransparentBlt**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtransparentblt)
-   [ **IPrintOemUni::EnableDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-enabledriver)方法，用于 Unidrv 提供图形 DDI 挂钩函数的指针。

-   [ **IPrintOemUni::DriverDMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-driverdms)方法，它告知设备管理的图面时要使用的 Unidrv，并指定在图面将使用该定义的挂钩函数。

挂钩函数无法回调到 GDI 的 Eng 前缀支持服务时在设备管理的表面上绘制。 但是，它们可以创建一个临时位图表面上，然后将该表面的句柄传递给 Eng 前缀绘图函数 (请参阅[呈现打印作业](rendering-a-print-job.md))。

[ **IPrintOemUni::DriverDMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-driverdms)每次打印作业时将要呈现，因此插件呈现可为每个指定的呈现图面 （GDI 管理或由设备管理） 的类型调用方法作业。 基于用户界面中的可选选项的图面上选择要求还提供[插件的用户界面](user-interface-plug-ins.md)。

### <a name="drawing-text-on-a-device-managed-surface"></a>设备管理的图面上绘制文本

插件呈现出 Unidrv 的必须挂接[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout) （以及所有其他图形 DDI 绘图函数） 的函数。 创建设备管理面文本过程包括以下四个函数之间的交互：

-   Unidrv 的[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)函数

-   插件的呈现[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)挂钩函数

-   Unidrv 的[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)方法

-   插件的呈现[ **IPrintOemUni::TextOutAsBitmap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)方法

在设备管理的图面上显示文本中所涉及的步骤如下所示：

1.  GDI 调用 Unidrv 的[ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)函数。

2.  呈现即插即用的项的调用 Unidrv [ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)挂钩函数。

3.  挂钩函数将命令发送到设备以指定文本的画笔、 旋转和剪辑区域。

4.  挂钩函数调用的 Unidrv [ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)方法，使用下载字体可将文本输出。 此方法还可以处理基于标志符号的剪辑。

5.  如果[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout) （因为字体不可用或旋转） 不能使用可下载的字体，它呈现即插即用的项的调用[ **IPrintOemUni::TextOutAsBitmap** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemuni-textoutasbitmap)方法，绘制为位图的文本。

6.  之后[ **IPrintOemDriverUni::DrvUniTextOut** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintoemdriveruni-drvunitextout)返回时， [ **DrvTextOut** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-drvtextout)挂钩函数必须绘制下划线和删除线取基于指定的矩形**DrvTextOut**函数的*prclExtra*参数，使用矢量命令 （如果支持）。

 

 




