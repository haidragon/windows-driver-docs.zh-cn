---
title: 宏块控制命令结构的第四部分
description: 宏块控制命令结构的第四部分
ms.assetid: 26540693-09a2-4664-b0ac-4cc69e909e99
keywords:
- 宏块 WDK DirectX VA，通用命令结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f587018c44ff39377b49b021bbb0b084dca44c0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372974"
---
# <a name="fourth-part-of-macroblock-control-command-structure"></a>宏块控制命令结构的第四部分


## <span id="ddk_fourth_part_of_macroblock_control_command_structure_gg"></span><span id="DDK_FOURTH_PART_OF_MACROBLOCK_CONTROL_COMMAND_STRUCTURE_GG"></span>


如果**bPicIntra**并**bMV\_RPS**成员[ **DXVA\_PictureParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_pictureparameters)均为零，宏块控制命令结构结尾的数据中所述[第三个部分组成的宏块控制命令的结构](third-part-of-macroblock-control-command-structure.md)。 宏块控制命令结构结尾填充零值的数据，如有必要下, 一步的宏块控制命令为 16 字节边界对齐结构的第三个部分。

如果**bPicIntra** DXVA 成员\_PictureParameters 为零并且**bMV\_RPS** DXVA 成员\_PictureParameters 为 1，第四部分宏块控制命令结构是一个名为字节数组*bRefPicSelect*。 该数组中的元素数是中的元素数相同**MVector**数组上表中所示。 数组的每个元素指定的索引中找到相应的动作矢量与关联的未压缩的图面**MVector**数组。 然后，宏块控制命令结构结束，则用零值数据填充，如有必要下, 一步宏块控制命令结构为 16 字节边界对齐。

 

 





