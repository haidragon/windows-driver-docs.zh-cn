---
title: WdfObjectAddCustomTypeWithData macro
description: WdfObjectAddCustomTypeWithData 宏 framework 对象相关联的自定义的类型，并根据需要将此对数据缓冲区和事件回调函数与相关联。
ms.assetid: 237F9BAA-A2E2-4F20-B52E-8F093B326E45
keywords:
- WdfObjectAddCustomTypeWithData macro
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 020c428597de68918546834a1ae104cae97246cd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372102"
---
# <a name="wdfobjectaddcustomtypewithdata-macro"></a>WdfObjectAddCustomTypeWithData macro


\[适用于 KMDF 和 UMDF\]

**WdfObjectAddCustomTypeWithData**宏 framework 对象相关联的自定义的类型，并根据需要将此对数据缓冲区和事件回调函数与相关联。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
NTSTATUS WdfObjectAddCustomTypeWithData(
    _handle,
    _type,
    _data,
    _cleanup,
    _destroy
);
```

<a name="parameters"></a>Parameters
----------

*_handle*   
Framework 对象的句柄。

*_type*   
自定义类型的驱动程序定义名称。

*_data*   
一个指向驱动程序提供的数据缓冲区，则为 NULL。 该参数为可选参数。

*_cleanup*   
驱动程序的一个指向[ *EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)回调函数，则为 NULL。 该参数为可选参数。

*_destroy*   
驱动程序的一个指向[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)回调函数，则为 NULL。 该参数为可选参数。

<a name="return-value"></a>返回值
------------

**WdfObjectAddCustomTypeWithData**返回 STATUS_SUCCESS，如果操作成功。 否则，此方法可能返回以下值之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>返回代码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>STATUS_OBJECT_PATH_INVALID</strong></td>
<td><p>指定句柄不能具有自定义类型添加到它。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td><p>未能分配自定义的类型。</p></td>
</tr>
<tr class="odd">
<td><strong>STATUS_OBJECT_NAME_EXISTS</strong></td>
<td><p>该驱动程序已添加指定的自定义类型。</p></td>
</tr>
<tr class="even">
<td><strong>STATUS_DELETE_PENDING</strong></td>
<td><p>正在删除句柄参数指定的对象。 在此情况下，该框架不会添加自定义的类型。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果您的驱动程序调用**WdfObjectAddCustomTypeWithData**与指向数据缓冲区的指针，该驱动程序可以提供[ *EvtCleanupCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)或[ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)解除分配的内存缓冲区时删除该对象的回调函数。

有关对象的自定义类型的详细信息，请参阅[Framework 对象的自定义类型](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-custom-types)。

有关代码示例，请参阅[ **WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">世界</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.11</p></td>
</tr>
<tr class="odd">
<td><p>最低 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wdfobject.h （包括 Wdf.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CUSTOM_TYPE**](wdf-declare-custom-type.md)

[**WdfObjectAddCustomType**](wdfobjectaddcustomtype.md)

[**WdfObjectGetCustomTypeData**](wdfobjectgetcustomtypedata.md)

[**WdfObjectIsCustomType**](wdfobjectiscustomtype.md)

 

 






