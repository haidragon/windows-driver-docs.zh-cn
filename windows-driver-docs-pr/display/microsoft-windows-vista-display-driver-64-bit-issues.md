---
title: Windows 显示驱动程序模型 (WDDM) 64 位问题
description: Windows 显示驱动程序模型 (WDDM) 64 位问题
ms.assetid: ab391fca-bc98-4e98-9531-7a1d24ee173d
keywords:
- 64 位 WDK 显示
- 显示器驱动程序模型 WDK Windows Vista 中，64 位
- Windows Vista 显示器驱动程序模型 WDK，64 位
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84d7b39693502caf703b0991ad69bf777b5788f1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385604"
---
# <a name="windows-display-driver-model-wddm-64-bit-issues"></a>Windows 显示驱动程序模型 (WDDM) 64 位问题


若要允许 32 位应用程序在 64 位操作系统上运行，必须除了 64 位应用程序需要 64 位用户模式显示驱动程序提供 32 位用户模式显示驱动程序。 但是，仅显示微型端口驱动程序的 64 位版本需要 64 位操作系统上。 Windows (WOW64) 上的 Windows 允许 32 位应用程序在 64 位操作系统上运行。 有关详细信息，请参阅[在 64 位驱动程序中支持 32 位 I/O](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-32-bit-i-o-in-your-64-bit-driver)。

若要在 64 位操作系统上安装 32 位用户模式显示驱动程序，必须添加注册表部分中的图形设备显示微型端口驱动程序的 INF 文件中设置以下条目。 这必须发生，以便在安装驱动程序 32 位用户模式显示驱动程序的 DLL 名称添加到注册表：

```inf
 [Xxx_SoftwareDeviceSettings]
...
 HKR,, UserModeDriverNameWow, %REG_MULTI_SZ%, Xxx.dll
...
```

INF 文件必须包含信息以指示操作系统将 32 位用户模式显示驱动程序复制到系统的 %systemroot%\\SysWOW64 目录。 有关详细信息，请参阅[ **INF CopyFiles 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-copyfiles-directive)并[ **INF DestinationDirs 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-destinationdirs-section)。

因为 WOW64 中不能处理不透明或非类型化数据结构如[ **D3DDDICB\_分配**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_allocate)结构传递通过[ **pfnAllocateCb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_allocatecb)函数，它不能执行从 32 位到 64 位的自动转换。 因此，对于 WOW64 才能正常工作，必须考虑以下各项写入 32 位用户模式时显示在 64 位操作系统上运行的驱动程序：

-   避免指针或数据类型对敏感的多个操作系统，例如，大小\_T 或句柄。 使整个结构变量的大小，以及这些宽度可变的数据类型进行的对齐方式和各个成员的位置不同。 如果可变宽度成员都是不可避免的则可以添加另一个成员，以指示数据结构源自于 32 位用户模式显示驱动程序。 64 位显示微型端口驱动程序可以正确执行转换。

-   即使可变宽度成员不存在，可能需要考虑特定于体系结构的对齐需求。 例如，在 x64 上，UINT64 （或 QWORD） 应为 8 字节对齐。 标准的 32 位编译器编译的 32 位用户模式显示驱动程序可能无法正确对齐这些本机 64 位类型，因为 64 位显示微型端口驱动程序可能无法准确地从 32 位用户模式显示驱动程序访问数据。 但是，可以使用合适的强制对齐**杂注**编译器指令。 尽管使用**杂注**编译器指令可能会稍有浪费了空间导致 32 位操作系统上，这样便可以在 32 位和 64 位操作系统上使用相同的 32 位用户模式显示驱动程序。 如果你不能使用合适的强制对齐**杂注**编译器指令将在运行 64 位操作系统上使用 WOW64 32 位用户模式显示驱动程序必须不同于 32 位用户模式显示驱动程序在 32 位操作系统上运行。

 

 





