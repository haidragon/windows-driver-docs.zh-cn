---
title: KSPROPSETID\_Pin
description: KSPROPSETID\_Pin
ms.assetid: a74a9cb2-2809-4e03-95da-71eeb5f079e9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd70aee31074338f1bccb30cc316d39a89175b67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384649"
---
# <a name="kspropsetidpin"></a>KSPROPSETID\_Pin


## <span id="ddk_kspropsetid_pin_ks"></span><span id="DDK_KSPROPSETID_PIN_KS"></span>


客户端使用属性中 KSPROPSETID\_Pin 属性设置为查询有关它所支持的每个 pin 工厂信息 KS 筛选器。

[ **KSPROPERTY\_PIN\_CTYPES** ](ksproperty-pin-ctypes.md)属性指定多少 pin 工厂 KS 筛选支持。 设置此属性中的所有其他属性指定有关单个 pin 工厂的信息。 KS 筛选器标识由一个 ID，范围为 0 的数减一的 pin 工厂到每个 pin 工厂。 客户端包括中的 pin 工厂 T [ **KSP\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)它时它会发出属性请求使用的结构。

KSPROPSETID\_Pin 属性集包括：

[**KSPROPERTY\_PIN\_CATEGORY**](ksproperty-pin-category.md)

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

[**KSPROPERTY\_PIN\_通信**](ksproperty-pin-communication.md)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

[**KSPROPERTY\_PIN\_CTYPES**](ksproperty-pin-ctypes.md)

[**KSPROPERTY\_PIN\_DATAFLOW**](ksproperty-pin-dataflow.md)

[**KSPROPERTY\_PIN\_DATAINTERSECTION**](ksproperty-pin-dataintersection.md)

[**KSPROPERTY\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

[**KSPROPERTY\_PIN\_GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)

[**KSPROPERTY\_PIN\_INTERFACES**](ksproperty-pin-interfaces.md)

[**KSPROPERTY\_PIN\_媒体**](ksproperty-pin-mediums.md)

[**KSPROPERTY\_PIN\_NAME**](ksproperty-pin-name.md)

[**KSPROPERTY\_PIN\_NECESSARYINSTANCES**](ksproperty-pin-necessaryinstances.md)

[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](ksproperty-pin-physicalconnection.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](ksproperty-pin-proposedataformat2.md)

 

 





