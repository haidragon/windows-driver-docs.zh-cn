---
title: ndiskd.ndisslot
description: '**！ Ndiskd.ndisslot**扩展显示 NDIS 处理器每个变量的内容。'
ms.assetid: 0EF37FE7-31A1-4A71-9CAC-E2A43F0EEBCF
keywords:
- ndiskd.ndisslot Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisslot
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0b9ff3e98b774209d12f03da700967ce23dc6c6f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363134"
---
# <a name="ndiskdndisslot"></a>!ndiskd.ndisslot


**请注意**  第三方网络驱动程序开发人员不应手动使用此扩展命令。 你可以运行它以查看其显示的信息，但不能重复使用它提供了您的驱动程序的详细信息。

 

**！ Ndiskd.ndisslot**扩展显示 NDIS 处理器每个变量的内容。 如果不带任何参数运行此扩展 ！ ndiskd 将显示在系统上的 NDIS 每个处理器的所有变量的列表。

```console
!ndiskd.ndisslot [-handle <x>] [-itemtype <str>] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>参数


<span id="_______-handle______"></span><span id="_______-HANDLE______"></span> *-handle*   
槽的句柄。

<span id="_______-itemtype______"></span><span id="_______-ITEMTYPE______"></span> *-itemtype*   
在槽中存储的值的类型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Ndiskd.dll

<a name="examples"></a>示例
--------

运行 **！ ndiskd.ndisslot**扩展不带任何参数，以查看每个处理器插槽的所有变量的列表。 以下示例输出已 excised 为简洁起见列表的中间部分。

```console
1: kd> !ndiskd.ndisslot
    Per-processor slot                     Summary of contents                  
    ffffc804ae060000 - NDrw                All values are zero
    ffffc804ae060008 - NDrw                All values are zero
    ffffc804ae060010 - NDrw                All values are zero
    ffffc804ae060018 - NDrw                All values are zero
    ffffc804ae060020 - NDrw                All values are zero
    ffffc804ae060028 - NDrw                All values are zero
    ffffc804ae060030 - NDrw                All values are zero
    ffffc804ae060038 - NDrw                All values are zero
    ffffc804ae060040 - NDrw                All values are zero
    ffffc804ae060048 - NDrw                All values are zero

...

    ffffc804ae060910 - NDtk                All values are zero
    ffffc804ae060918 - NDtk                All values are zero
    ffffc804ae060920 - tsR                 All values are non-zero
    ffffc804ae060928 - NDrw                All values are zero
    ffffc804ae060930 - NDtk                All values are zero
    ffffc804ae060938 - NDtk                All values are zero
    ffffc804ae060940 - NDtk                All values are zero
    ffffc804ae060948 - NDtk                All values are zero
    ffffc804ae060950 - NDrw                All values are zero
    ffffc804ae060958 - NDrw                All values are zero

    Statistics
    Descriptors        1
    Total slots        512
    Slots available    275
    Slots used         237
    Efficiency         46%
```

单击每个处理器插槽变量的句柄之一上会显示该变量的详细信息。 下面的示例使用句柄 ffffc804ae060920 tsR 变量，从前面的示例。

```console
1: kd> !ndiskd.ndisslot ffffc804ae060920
    Processor          Slot value                                               
    00                 00000006
    01                 00000006
    02                 00000006
    03                 00000006
```

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[调试网络堆栈](https://go.microsoft.com/fwlink/p/?linkid=845311)

[**NDIS 扩展 (Ndiskd.dll)** ](ndis-extensions--ndiskd-dll-.md)

[ **!ndiskd.help**](-ndiskd-help.md)

 

 






