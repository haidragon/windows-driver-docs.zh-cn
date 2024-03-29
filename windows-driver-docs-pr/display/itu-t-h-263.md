---
title: ITU-T H.263
description: ITU-T H.263
ms.assetid: 08926037-da17-4ab0-81c5-9fd78cb1133c
keywords:
- ITU-T H.263 WDK DirectX VA
- H.263 WDK DirectX VA
- OBMC WDK DirectX VA
- INTER4V WDK DirectX VA
- 双向预测 WDK DirectX VA
- 动作矢量 WDK DirectX VA
- 舍入控制 WDK DirectX VA
- 图片边界 WDK DirectX VA
- macroblocks WDK DirectX VA , ITU-T H.263
- PB 帧 WDK DirectX VA
- 消除筛选器 WDK DirectX VA 马赛克功能
- 多个参考帧 WDK DirectX VA
- 逆变离散余弦 WDK DirectX VA
- IDCT WDK DirectX VA
- 独立段解码 WDK DirectX VA
- 减少解析更新 WDK DirectX VA
- 引用图片来重新采样 WDK DirectX VA
- 可伸缩性 WDK DirectX VA
- 引用照片选择 WDK DirectX VA
- 预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aca82a82b423dfedcc8cc55565a1d50b4e8b901d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372917"
---
# <a name="itu-t-h263"></a>ITU-T H.263


## <span id="ddk_itu_t_h_263_gg"></span><span id="DDK_ITU_T_H_263_GG"></span>


ITU-T 建议 H.263 的标题为视频编码为低位速率通信。 此建议提供相对于 H.261、 MPEG-1 和 mpeg-2 改进的压缩性能。 标准 H.263 包含支持仅 H.263 的最基本功能的操作的基线模式。 它还包含大量的可选的增强型可用于各种目的的操作模式。 基线 H.263 预测操作在此界面使用 mpeg-1 功能的子集。 基线模式包含没有双向预测 âˆ 只转发预测。

**舍入控制：** 多个 H.263 可选模式需要舍入控制。 此功能受**bRcontrol**的成员[ **DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)。

**通过图片边界的动作矢量：** 几个 H.263 可选模式允许动作矢量边界之外的图片，该地址位置 H.263 附录 D.中定义**BPicExtrapolation**的成员[ **DXVA\_PictureParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)，指示快捷键是否需要支持此类运动。 有两种方法加速器可以支持通过图片边界的动作矢量。 在任一情况下，结果是相同的：

-   每个示例提取时，确保其始终图片边界内剪辑地址的值。

-   通过使用图片填充复制示例以扩大一个宏块宽度和高度由在每个图片的边框之间的实际内存区域。

**双向运动预测：** 双向运动预测时使用一些可选 H.263 预测操作中使用不同舍入运算符比 MPEG-1。 （它使用向下四舍五入的一半的整数值，而不是向上舍入。）**BBidirectionalAveragingMode**的成员[ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)指示用于组合中的预测飞机的舍入方法双向运动补偿。

**四个 MV 运动补偿 (INTER4V)** :尽管 H.263 中的每个宏块是 16 x 16 的大小，但某些可选模式 （例如，附录 F 和附录 J 的 H.263） 允许四个动作矢量为单个宏块中，对一个动作矢量发送为每个宏块中的四个 8 x 8 亮度块发送。 相应的 8 x 8 色度区域使用单个、 派生动作矢量。

**重叠的块运动补偿 (OBMC)** :H.263 附录 F 亮度采样，除了 INTER4V 支持包含重叠的块运动补偿 (OBMC)。 12 动作矢量要发送的宏块的正向预测，从而支持 OBMC 预测。

为组合的预测划分为三个平面，可以在硬件加速器中实现 OBMC 预测块：

-   当前平面 （与零的平面索引）

-   大/小写平面 （与平面索引为 1 时）

-   左/右平面 （与平面索引为 2 时）

三个平面可用作临时存储的基块*q(x,y)* ， *r(x,y)* ，并*s(x,y)* H.263 部分 F.3 中定义。 三个平面的每个都已填写所有四个块后，可以根据 H.263 部分 F.3 中的公式合并并按其各自加权*H* H.263 附录 F.在给定的矩阵

例如，OBMC 亮度宏块预测可能包含 8 x 4 形状，4 x 8 形状的八个左/右块和 8 x 8 形状的四个当前块的八个顶部/底部预测块。 如果所有四个索引为 0 的平面的运动向量具有相同动作矢量 （即，在非 INTER4V 宏块中），可以使用单一的 16x16 宏块预测以填充整个 16 x 16 平面。

若要在 DirectX VA 实现 OBMC 进程，10 个动作矢量会发送宏块，如下图中所示。 第四个动作矢量的为当前宏块中的 Y₀、 Y₁、 Y₂ 和 Y₃ 块。 随后会按以下顺序发送远程动作矢量：

1.  宏块的顶部左侧和右侧部分。

2.  顶部和底部的左侧和右侧的宏块的部分。

3.  顶部和底部的宏块右侧的部分。

下图显示了使用 OBMC 处理时发送的宏块的动作矢量。 （字母 C 表示当前宏块动作的矢量。 字母 R 表示为相对于当前宏块远程的动作矢量。）

![说明时使用重叠的块运动补偿 (obmc) 处理为宏块发送的十个动作矢量的关系图](images/10vectors.png)

请注意 H.263 为宏块的底部左侧和右侧部分不会使用不同的远程向量 — 它重用当前宏块的向量。

如下图所示方式一个 8 x 8 块被置于三种类型的预测平面由 OBMC H.263 中的处理。

![说明 h.263 注册一个 8 x 8 块重叠的块运动补偿 (obmc) 预测平面中的关系图](images/h263reg.png)

**PB 框架 （附录 G 和 M）** :在此模式下，P 帧和 pseudoâˆ 块效应 B 帧进行多路复用一起到编码类型的唯一 PB 帧图片。 每个宏块的 B 部分利用的编码宏块的 P 部分的信息： B 帧向前和向后移动矢量 P 帧向量中进行缩放，并重新构造的 P 帧宏块 b 作为后向引用部分。 PB 框架包括仅 pseudoâˆ'B 帧，因为每个宏块的向后预测只能引用同一 PB 宏块中包含重新构造 P 宏块。 但是，作为与传统的 B 帧语义，PB 框架内 B 宏块可以引用的任何位置前向引用范围内。 向后引用的限制创建较小的向后预测块形状 （如在 H.263 图 G.2 中所述）。 在 DirectX VA 支持 PB 帧通过表示为 P 帧 PB 框架的 P 部分，并作为单独 B-P 双向预测的图片包含具有两个动作矢量的宏块的唯一 B 中 PB 类型 PB 帧的 B 部分。

**消除马赛克功能筛选器 （附录 J）** :定义特殊的命令是为了加速消除马赛克功能筛选器，经过运动补偿预测中使用是否必须创建的观察的块 (GOB) 或切片段边界组，如有必要消除马赛克功能命令。

**引用照片选择 （附录 N 和 U）** :使用预测的每个块的图片索引选择字段的加速器支持多个参考帧。

**可伸缩性 （附录 O）** :临时表，在 SNR 和功能指定 H.263 Annex O.H.263 临时可伸缩性 B 帧中的空间可伸缩性是在 DirectX VA 非常类似于 mpeg-1 B 帧。 空间可伸缩性要求升频较低层引用图片，然后作为引用图片中编写代码的增强功能层图片的使用采样图片 （在所有其他方面，空间可伸缩性是实质上是干扰信号相同比率和临时的可伸缩性）。 相应的双向求平均值舍入控件应设置为向下偏差为 H.263 求平均值。 （mpeg-1 和 mpeg-2 使用向上偏差求平均值和 H.263 使用向下偏离平均值）。

**引用来重新采样 （附录 P） 的图片**:本附录简单窗体被受支持引用缓冲区来重新采样。 对于高级窗体的 Annex P 来重新采样，必须通过外部方式重新采样和存储为参考帧缓冲区进行寻址的快捷键重新构造的框架，以作为参考帧。

**减少解析更新 （附录 Q）** :不当前支持 H.263 减少解析更新模式，因为它的不寻常的残留升频要求、 消除马赛克功能筛选器的不同的窗体和不同的窗体的高级预测 OBMC。 但是，可以在使用基于主机的 IDCT 处理 deblocking 的筛选器模式和高级的预测模式处于非活动状态时此界面中支持减少解析更新模式操作。

**解码 （附录 R） 的独立段**:没有独立段边框 accelerator 知道。 某些形式的 Annex R 可以支持而无需任何特殊处理 （例如，基线加 Annex R）。 需要图片段外推的 Annex R 窗体可以受解码为图片的每个段，然后构造完整的输出图片从这些较小的图片。

**IDCT （附录 W）：** 此接口支持 W 附录的 H.263 中指定的离散的反余弦值转换 (IDCT)。

**其他 H.263 可选功能：** 可以不会影响对 DirectX VA 设计支持 H.263 其他可选功能。 例如，通过更改不会影响在加速器上的软件解码器是轻松地处理附录 I、 K、 S 和 T。

 

 





