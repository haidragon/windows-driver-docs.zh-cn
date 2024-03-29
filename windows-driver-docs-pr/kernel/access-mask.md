---
title: 指定访问权限
description: 指定访问权限
ms.assetid: 8ef4b4bb-5f4e-4095-b4ab-1182c0f75619
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e77526cb40bb9d43d099040fc06cbff517701437
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363471"
---
# <a name="specifying-access-rights"></a>指定访问权限


访问\_掩码类型是指定一组中的访问权限的一个位掩码[访问掩码](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-mask)的[访问控制项](https://docs.microsoft.com/windows-hardware/drivers/ifs/access-control-entry)。

``` syntax
typedef ULONG  ACCESS_MASK;
```

下面的标准的特定访问权限适用于所有类型的执行对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DELETE</p></td>
<td><p>调用方可以删除该对象。</p></td>
</tr>
<tr class="even">
<td><p>READ_CONTROL</p></td>
<td><p>调用方可以读取的访问控制列表 (ACL) 和文件的所有权信息。</p></td>
</tr>
<tr class="odd">
<td><p>同步</p></td>
<td><p>调用方可以执行对象的等待操作。 (例如，该对象可以传递给<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects" data-raw-source="[&lt;strong&gt;KeWaitForMultipleObjects&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)"> <strong>KeWaitForMultipleObjects</strong></a>。)</p></td>
</tr>
<tr class="even">
<td><p>WRITE_DAC</p></td>
<td><p>调用方可以更改对象的自由访问控制列表 (DACL) 信息。</p></td>
</tr>
<tr class="odd">
<td><p>WRITE_OWNER</p></td>
<td><p>调用方可以更改文件的所有权信息。</p></td>
</tr>
</tbody>
</table>

 

请注意，通常仅删除和同步的驱动程序编写人员感兴趣。

此外可以指定以下通用访问权限。 这些控件还适用于所有类型的执行对象。 每种通用权限的含义是对象的访问的特定于该类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Flag</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>GENERIC_READ</p></td>
<td><p>调用方可以执行在对象上的常规读取的操作。</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_WRITE</p></td>
<td><p>调用方可以执行常规写入操作的对象上。</p></td>
</tr>
<tr class="odd">
<td><p>GENERIC_EXECUTE</p></td>
<td><p>调用方可以执行对象。 （请注意这通常只是有意义的某些类型的对象，如文件对象和部分对象。）</p></td>
</tr>
<tr class="even">
<td><p>GENERIC_ALL</p></td>
<td><p>调用方可以执行所有对象上的正常操作。</p></td>
</tr>
</tbody>
</table>

 

此外定义了以下标准的特定访问权限的组合。 这些不通常情况下直接使用，但作为模板用于定义其他的位屏蔽。 (例如，当指定泛型\_读取的文件对象，系统映射这到的文件\_泛型\_读取的特定访问权限的位掩码。 文件\_泛型\_根据标准定义读取\_RIGHTS\_读取。)

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>位掩码</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STANDARD_RIGHTS_READ</p></td>
<td><p>标准的特定权限对应于 GENERIC_READ</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_WRITE</p></td>
<td><p>标准的特定权限对应于 GENERIC_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_EXECUTE</p></td>
<td><p>标准的特定权限对应于 GENERIC_EXECUTE</p></td>
</tr>
<tr class="even">
<td><p>STANDARD_RIGHTS_REQUIRED</p></td>
<td><p>标准对应于 generic_all 权限的特定权限。 这包括删除操作，但不是同步。</p></td>
</tr>
<tr class="odd">
<td><p>STANDARD_RIGHTS_ALL</p></td>
<td><p>标准访问权限的所有权限。</p></td>
</tr>
</tbody>
</table>

 

每种类型的对象可以具有其自己的其他访问权限。 适用于文件、 目录或设备的访问权限的说明，请参阅[ **ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)。 适用于对象管理器目录的访问权限的说明，请参阅[ **ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)。 适用于注册表项的访问权限的说明，请参阅[ **ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)。 适用于部分对象的访问权限的说明，请参阅[ **ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)。 适用于 WMI 数据块的访问权限的说明，请参阅[ **IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)。

有关访问权限的详细信息，请参阅 Microsoft Windows SDK 文档中的以下主题：

-   [访问权限和访问掩码](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-rights-and-access-masks)
-   [ACCESS\_MASK](https://docs.microsoft.com/windows/desktop/SecAuthZ/access-mask)

Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）

## <a name="related-topics"></a>相关主题
[**IoWMIOpenBlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiopenblock)  
[**ZwCreateDirectoryObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatedirectoryobject)  
[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)  
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)  
[**ZwOpenSection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopensection)  



