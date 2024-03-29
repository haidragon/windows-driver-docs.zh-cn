---
title: FLT_PARAMETERS IRP_MJ_SET_INFORMATION 联合
description: 联合组件时使用 FLT MajorFunction 字段\_IO\_参数\_操作的块结构是 IRP\_MJ\_设置\_信息。
ms.assetid: 860973bf-a98d-4495-9d6c-093ee985f360
keywords:
- FLT_PARAMETERS IRP_MJ_SET_INFORMATION 联合可安装文件系统驱动程序
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97377e2f3af757c4aa9d6fea04515da780e5a761
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380497"
---
# <a name="fltparameters-for-irpmjsetinformation-union"></a>FLT\_IRP 的参数\_MJ\_设置\_信息并集


联合组件时使用**MajorFunction**字段[ **FLT\_IO\_参数\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构操作已[ **IRP\_MJ\_设置\_信息**](irp-mj-set-information.md)。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                                    Length;
    FILE_INFORMATION_CLASS POINTER_ALIGNMENT FileInformationClass;
    PFILE_OBJECT                             ParentOfTarget;
    union {
      struct {
        BOOLEAN ReplaceIfExists;
        BOOLEAN AdvanceOnly;
      };
      ULONG  ClusterCount;
      HANDLE DeleteHandle;
    };
    PVOID                                    InfoBuffer;
  } SetFileInformation;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

<a name="members"></a>成员
-------

**SetFileInformation**  
结构，它包含以下成员。

**长度**  
在缓冲区的长度，以字节为单位， **InfoBuffer**。

**FileInformationClass**  
要为文件设置的信息类型。 下列情况之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllocationInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_allocation_information" data-raw-source="[&lt;strong&gt;FILE_ALLOCATION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_allocation_information)"> <strong>FILE_ALLOCATION_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)"> <strong>FILE_BASIC_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileDispositionInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_disposition_information" data-raw-source="[&lt;strong&gt;FILE_DISPOSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_disposition_information)"> <strong>FILE_DISPOSITION_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileEndOfFileInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information" data-raw-source="[&lt;strong&gt;FILE_END_OF_FILE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information)"> <strong>FILE_END_OF_FILE_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileLinkInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_link_information" data-raw-source="[&lt;strong&gt;FILE_LINK_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_link_information)"> <strong>FILE_LINK_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)"> <strong>FILE_POSITION_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileRenameInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_rename_information" data-raw-source="[&lt;strong&gt;FILE_RENAME_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_rename_information)"> <strong>FILE_RENAME_INFORMATION</strong> </a>文件。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileValidDataLengthInformation</strong></p></td>
<td align="left"><p>设置<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_valid_data_length_information" data-raw-source="[&lt;strong&gt;FILE_VALID_DATA_LENGTH_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_valid_data_length_information)"> <strong>FILE_VALID_DATA_LENGTH_INFORMATION</strong> </a>文件。</p></td>
</tr>
</tbody>
</table>

 

**ParentOfTarget**  
重命名或链接的操作。 如果**InfoBuffer-&gt;文件名**包含一个完全限定的文件名，或者如果**InfoBuffer-&gt;RootDirectory**为非**NULL**，此成员是操作的目标的文件的父目录文件对象指针。 否则它是**NULL**。

(*未命名结构*)  
结构，它包含以下成员。

**ReplaceIfExists**  
重命名或链接的操作。 设置为 **，则返回 TRUE**来指定要替换与给定文件已存在具有相同名称的文件。 设置为**FALSE**如果已存在具有给定名称的文件重命名或链接的操作应失败。

**AdvanceOnly**  
文件尾操作的标志。 这将确定使用**EndOfFile**成员[**文件\_最终\_OF\_文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information)结构何时**FileInformationClass** == **FileEndOfFileInformation**。 如果 **，则返回 TRUE**，该文件的新有效的数据长度将设置从**EndOfFile**才会增加当前有效的数据长度。 如果**FALSE**，新的文件大小设置从**EndOfFile**。

**ClusterCount**  
保留供系统使用。 不使用。

**DeleteHandle**  
保留供系统使用。 不使用。

**InfoBuffer**  
指向包含要设置的文件信息的输入缓冲区的指针。

<a name="remarks"></a>备注
-------

[ **FLT\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)结构 IRP\_MJ\_设置\_操作包含的参数的设置信息的信息表示回调数据的操作 ([**FLT\_回调\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 包含在 FLT\_IO\_参数\_块结构。

IRP\_MJ\_设置\_信息是基于 IRP 的操作。

**AdvanceOnly**成员设置为**TRUE**缓存管理器以通知文件系统，从而提升在磁盘上的新有效的数据长度中的当前有效的数据长度**EndOfFile**. 如果**AdvanceOnly**是**FALSE**，新的文件大小**EndOfFile**正在设置成员，这可以是大于或小于当前文件大小。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Fltkernel.h （包括 Fltkernel.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**文件\_分配\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_allocation_information)

[**文件\_BASIC\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)

[**文件\_处置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_disposition_information)

[**文件\_最终\_OF\_文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_end_of_file_information)

[**文件\_链接\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_link_information)

[**文件\_位置\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_position_information)

[**文件\_重命名\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/ns-ntifs-_file_rename_information)

[**文件\_VALID\_数据\_长度\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_file_valid_data_length_information)

[**FLT\_CALLBACK\_DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT\_IO\_PARAMETER\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT\_IS\_FASTIO\_OPERATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[**FLT\_IS\_FS\_FILTER\_OPERATION**](https://docs.microsoft.com/previous-versions/ff544648(v=vs.85))

[**FLT\_IS\_IRP\_操作**](https://docs.microsoft.com/previous-versions/ff544654(v=vs.85))

[**FLT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/ns-fltkernel-_flt_parameters)

[**IRP\_MJ\_SET\_INFORMATION**](irp-mj-set-information.md)

 

 






