---
title: 完整内存转储
description: 完整内存转储
ms.assetid: ccc4d22a-89af-4c7d-a982-f77c682cd001
keywords:
- 转储文件中，完全内存转储
- 完整内存转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e75ed9601f91934f1e2654fd02f54bb2745cfd37
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367011"
---
# <a name="complete-memory-dump"></a>完整内存转储


## <span id="ddk_complete_memory_dump_dbg"></span><span id="DDK_COMPLETE_MEMORY_DUMP_DBG"></span>


一个*完全内存转储*是最大的内核模式转储文件。 此文件包含所有 Windows 使用的物理内存。 完全内存转储不，默认情况下，包括平台固件使用的物理内存。

从 Windows 8 开始，你可以注册[ *BugCheckAddPagesCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kbugcheck_reason_callback_routine)过程完全内存转储中调用的例程。 你*BugCheckAddPagesCallback*例程可以指定要添加到转储文件的特定于驱动程序的数据。 例如，这些额外的数据可以包括物理页的未映射到虚拟内存中的系统地址范围，但已包含可帮助你调试您的驱动程序的信息。 *BugCheckAddPagesCallback*例程可能会添加到转储文件 （任何驱动程序拥有物理页未映射或并将其映射到用户模式虚拟内存中的地址。

此转储文件需要至少与主系统内存; 一样大的启动驱动器上的页面文件它应能够容纳的大小等于整个 RAM 再加上一个兆字节的文件。

完全内存转储文件写入到 %systemroot%\\Memory.dmp 默认情况下。

如果第二个 bug 检查发生，并且创建另一个完全内存转储 （以后或内核内存转储） 时，将覆盖以前的文件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[类型的内核模式转储文件](varieties-of-kernel-mode-dump-files.md)

 

 






