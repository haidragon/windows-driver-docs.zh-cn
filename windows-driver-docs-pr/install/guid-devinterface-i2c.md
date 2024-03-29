---
title: GUID_DEVINTERFACE_I2C
description: GUID_DEVINTERFACE_I2C
ms.assetid: 765cecb7-b8ea-48ef-bdab-742da722e169
keywords:
- GUID_DEVINTERFACE_I2C 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_I2C
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 236d96ef0a56eec667bacf8ec7fbf5baf7f2c2a2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375284"
---
# <a name="guiddevinterfacei2c"></a>GUID_DEVINTERFACE_I2C


GUID_DEVINTERFACE_I2C[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)显示适配器驱动程序的上下文中运行，为定义[Windows Vista 显示器驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)和 I2C 使用执行事务监视子设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVINTERFACE_I2C</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2564AA4F-DDDB-4495-B497-6AD4A84163D7}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

驱动程序注册通知的操作系统和应用程序的与监视子设备执行事务的 I2C 接口存在此设备接口类的实例。

如果显示微型端口驱动程序支持直接调用 I2C 接口的这[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)，内核模式组件可以通过调用微型端口驱动程序检索直接调用接口[ **DxgkDdiQueryInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数并提供 GUID_DEVINTERFACE_I2C 指定接口类型。

I2C 总线有关的信息，请参阅[I2C 总线和子设备的显示适配器](https://docs.microsoft.com/windows-hardware/drivers/display/i2c-bus-and-child-devices-of-the-display-adapter)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h （包括 Dispmprt.h）</td>
</tr>
</tbody>
</table>

 

 





