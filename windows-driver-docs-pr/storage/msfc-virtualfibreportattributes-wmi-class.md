---
title: MSFC\_VirtualFibrePortAttributes WMI 类
description: MSFC\_VirtualFibrePortAttributes WMI 类
ms.assetid: D605D63F-0EBF-44C0-8ADE-729F2DE48487
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fea9070d809025aa05047279a2f42e82253e820f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376704"
---
# <a name="msfcvirtualfibreportattributes-wmi-class"></a>MSFC\_VirtualFibrePortAttributes WMI 类


WMI 客户端使用 MSFC\_VirtualFibrePortAttributes 类来检索虚拟端口的属性。

MSFC\_VirtualFibrePortAttributes 类定义中，如下所示*Npivwmi.mof*:

```mof
class MSFC_VirtualFibrePortAttributes  
{  
    [WmiDataId(1), Description("Status of the virtual port"):Amended,  
    uint32 Status;  
  
    [WmiDataId(2), Description("FC Id"):Amended]  
    uint32 FCId;  
      
    [WmiDataId(3), Description("Port symbolic name"):Amended]  
    uint16 VirtualName[64];  
  
    [WmiDataId(4), Description("An opaque tag passed in by the app. 128 bit so that a guid can be stored in it."):Amended]  
    uint8 Tag[16];  
  
    [WmiDataId(5), Description("The world wide port name of the virtual port"):Amended]  
    uint8 WWPN[8];   
  
    [WmiDataId(6), Description("The world wide node name of the virtual port"):Amended]  
    uint8 WWNN[8];   
  
    [WmiDataId(7), Description("The world wide node name of fabric"):Amended]  
    uint8 FabricWWN[8];  
};  
```

编译时通过 WMI 工具套件，此类定义将生成以下数据结构：

[**MSFC\_VirtualFibrePortAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/npivwmi/ns-npivwmi-_msfc_virtualfibreportattributes)

没有与此 WMI 类相关联的方法。

 

 





