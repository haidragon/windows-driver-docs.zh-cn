---
title: OID_CO_ADD_PVC
description: 本主题介绍 OID_CO_ADD_PVC 对象标识符 (OID)。
ms.assetid: 182d5bdb-9cfe-4e9c-a2cf-4d5440bfdb76
keywords:
- OID_CO_ADD_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: aea642db33b32baed46a003986407657851713d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357690"
---
# <a name="oidcoaddpvc"></a>OID_CO_ADD_PVC

OID_CO_ADD_PVC OID 是客户端发送到呼叫管理器将永久性虚拟连接 (PVC) 添加到的已配置 Pvc 呼叫管理器的列表。 PVC 格式化为 CO_PVC 定义的结构，按如下所示：

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
```

此结构的成员包含下列信息：

**NdisAfHandle**  
指定返回的 NDIS 提供句柄[NdisClOpenAddressFamilyEx](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisclopenaddressfamilyex)。

**PvcParameters**  
一个格式化[CO_SPECIFIC_PARAMETERS](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545396(v=vs.85))结构。 此结构包含描述 PVC 的特定于协议的参数。

PVC 由管理员手动配置。 监视此类活动的客户端通知新配置 PVC 呼叫管理器通过将此 OID 发送到呼叫管理器。 其他客户端然后可以使用新配置 PVC。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

