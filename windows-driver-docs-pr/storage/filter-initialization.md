---
title: 筛选器初始化
description: 筛选器初始化
ms.assetid: c39dc5a6-f529-40a2-87d4-bac325b4fa1a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76db8b4f15d2ade619f941a84c67b547c7130db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356009"
---
# <a name="filter-initialization"></a>筛选器初始化


崩溃转储驱动程序是在系统崩溃或休眠状态恢复进程的早期阶段中初始化的。 但是，一旦加载，将初始化筛选器驱动程序。 这使筛选器驱动程序有机会执行任何必要的初始化过程崩溃初始化时，如分配内存中不能完成。

在崩溃转储驱动程序堆栈，筛选器驱动程序在系统启动时初始化。 可以禁用并重新运行系统时，因此故障转储筛选器驱动程序不应进行任何假设驱动程序加载和卸载时间在任何时候启用故障转储。 为休眠状态，筛选器驱动程序加载和初始化启动休眠状态时。

筛选器驱动程序加载到内存后，故障转储驱动程序将调用筛选器驱动程序的驱动程序入口函数来初始化筛选器驱动程序。 标准 DriverEntry 函数采用两个参数 （DriverObject 和 RegistryPath）。 调用筛选器驱动程序时，到点 DriverObject [**筛选器\_扩展**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/ns-ntdddump-_filter_extension)结构和 RegistryPath 指向[**筛选器\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/ns-ntdddump-_filter_initialization_data)结构。

若要完成初始化过程，筛选器驱动程序应初始化[**筛选器\_初始化\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntdddump/ns-ntdddump-_filter_initialization_data)结构，并将其返回到崩溃转储驱动程序。

 

 




