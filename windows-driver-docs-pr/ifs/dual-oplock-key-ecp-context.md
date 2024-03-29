---
title: 双\_OPLOCK\_密钥\_ECP\_上下文结构
description: 双\_OPLOCK\_密钥\_ECP\_上下文结构包含额外创建双 oplock 密钥的参数上下文。 可以在此结构中设置 Oplock 键的目标和父文件对象。
ms.assetid: 7E337D2F-7292-4D18-B750-8361A83C8B1F
keywords:
- DUAL_OPLOCK_KEY_ECP_CONTEXT 结构可安装文件系统驱动程序
- PDUAL_OPLOCK_KEY_ECP_CONTEXT 结构指针可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- DUAL_OPLOCK_KEY_ECP_CONTEXT
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad5182048de61499d8e8bb36fe41a87af6761fb1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386094"
---
# <a name="dualoplockkeyecpcontext-structure"></a>双\_OPLOCK\_密钥\_ECP\_上下文结构


**双\_OPLOCK\_密钥\_ECP\_上下文**结构包含额外创建双 oplock 密钥的参数上下文。 可以在此结构中设置 Oplock 键的目标和父文件对象。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _DUAL_OPLOCK_KEY_ECP_CONTEXT {
  GUID    ParentOplockKey;
  GUID    TargetOplockKey;
  BOOLEAN ParentOplockKeySet;
  BOOLEAN TargetOplockKeySet;
} DUAL_OPLOCK_KEY_ECP_CONTEXT, *PDUAL_OPLOCK_KEY_ECP_CONTEXT;
```

<a name="members"></a>成员
-------

**ParentOplockKey**  
一个**GUID**表示父 oplock 密钥值。

**TargetOplockKey**  
一个**GUID**表示目标 oplock 密钥值。

**ParentOplockKeySet**  
设置为 TRUE **ParentOplockKey**包含父级的 oplock 密钥是有效的 GUID。

**TargetOplockKeySet**  
设置为 TRUE **TargetOplockKey**包含目标的 oplock 密钥的有效 GUID。

<a name="remarks"></a>备注
-------

**双\_OPLOCK\_密钥\_ECP\_上下文**结构提供了双 oplock 密钥以允许将文件和目录的机会锁请求。 像[ **OPLOCK\_密钥\_ECP\_上下文**](oplock-key-ecp-context.md)结构**双\_OPLOCK\_密钥\_ECP\_上下文**在额外设置创建参数列表 ([**ECP\_列表**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))) 和更高版本的文件对象与关联处理的过程[**IRP\_MJ\_创建**](irp-mj-create.md)通过文件系统或文件系统筛选器驱动程序。

该值**GUID\_ECP\_双\_OPLOCK\_密钥**调用如支持例程时使用[ **FsRtlAllocateExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff545609)， [ **FsRtlInitializeExtraCreateParameter**](https://msdn.microsoft.com/library/windows/hardware/ff546113)，或[ **FltRemoveExtraCreateParameter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltremoveextracreateparameter)。

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
<td align="left"><p>此结构是从 Windows 8 开始提供。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h （包括 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ECP\_LIST**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540148(v=vs.85))

[**IO\_DRIVER\_CREATE\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_io_driver_create_context)

[**IoCreateFileEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefileex)

[**IRP\_MJ\_CREATE**](irp-mj-create.md)

[**OPLOCK\_KEY\_ECP\_CONTEXT**](oplock-key-ecp-context.md)

[Oplock 语义](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-semantics)

 

 






