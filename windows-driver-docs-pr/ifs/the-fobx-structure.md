---
title: FOBX 结构
description: FOBX 结构
ms.assetid: 95177b38-4ca5-49ed-9f9d-bafedd156044
keywords:
- 引用计数 WDK RDBSS
- FOBX 结构
- FILE_OBJECT 结构
- 计数引用 WDK RDBSS
- backpointers WDK RDBSS
- 数据结构 WDK 文件系统
- RDBSS WDK 的文件系统、 连接和文件结构
- 重定向驱动器缓冲子系统 WDK 的文件系统、 连接和文件结构
- 连接结构 WDK RDBSS
- 文件结构 WDK RDBSS
- 结构 WDK RDBSS
- WDK RDBSS 的连接信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bd23be595f067a95b7389e90d132ca9bc028bdf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371295"
---
# <a name="the-fobx-structure"></a>FOBX 结构


## <span id="ddk_the_fobx_structure_if"></span><span id="DDK_THE_FOBX_STRUCTURE_IF"></span>


文件对象扩展 (FOBX) 结构是对 RDBSS 扩展[**文件\_对象**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_object)结构。 指向 FOBX 结构**FileObjectExtension**字段中的文件对象。 FOBX 结构包含以下元素：

-   签名和引用计数

-   反向指针相关联的 FCB 结构

-   为关联 SRV 的反向指针\_打开结构

-   有关此打开结构的上下文信息

-   根据网络微型重定向或 FOBX 结构的创建者的请求的其他存储

FOBX 结构包含所有需要每个文件对象，通常不会存储 I/O 系统的信息。 固定大小的文件系统对象中的 I/O 系统存储文件对象的信息。 FOBX 结构处理网络微型-重定向程序文件对象上所需的其他信息。

引用的任何文件对象的 FOBX 结构**FsContext2**字段中的文件对象。 即使 FOBX 结构通常是终点 RDBSS 结构中的，FOBX 结构目前仍要计数的引用。

FOBX 标志要拆分成两个组：

-   对网络微型-重定向程序可见的标志

-   在内部使用，通过 RDBSS 和对网络微型-重定向程序不可见的标志

对网络微型-重定向程序可见的标志包含可能 FOBX 标志的低 16 位。 较高的 16 位被保留供内部 RDBSS。

 

 




