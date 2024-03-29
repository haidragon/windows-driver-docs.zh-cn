---
title: 属性上下文
description: 属性上下文
ms.assetid: da33848c-a9bc-40c7-ab1b-0ca056f3e06d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fab194f3357ec9d722aba61bd1f337ff66c423e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374316"
---
# <a name="property-contexts"></a>属性上下文





属性上下文提供微型驱动程序可以标识多个属性在这些属性的验证过程中关注的简便方法。 使用属性上下文，微型驱动程序可以快速确定是否正在更改的任何标识属性。 微型驱动程序然后将属性上下文传递给 WIA 服务库函数之一 (例如， [ **wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat))，其中使用的上下文以确定是否为应用程序更改属性的值。

验证的 WIA 方法是，当应用程序更改属性时，任何依赖项属性还应更新。 如果，但是，应用程序也会更改依赖属性，只需选中顶级属性，以确定其新值是否有效。 与属性验证的 WIA 服务库功能使用这一原则以决定它们应该在何时更新依赖项属性，以及当它们应只需检查其有效性。

在中维护一组属性的上下文[ **WIA\_属性\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/ns-wiamindr_lh-_wia_property_context)结构，其中包含三个成员： 属性上下文中的属性的数目指向数组的属性标识符 (Propid) 和一个 BOOL 值数组的指针。 同时维护数组 (即，其属性标识符位于索引的属性*N*在属性标识符数组就是与布尔值数组中的相同索引处的 BOOL 值相关联)。

微型驱动程序调用 WIA 服务库函数时， [ **wiasCreatePropContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiascreatepropcontext)以分配内存并填写属性上下文的值。 其他 WIA 服务库函数，如[ **wiasGetChangedValueFloat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetchangedvaluefloat)，使用属性上下文来确定应更新属性的值。

 

 




