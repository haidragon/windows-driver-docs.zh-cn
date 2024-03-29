---
title: 将上下文与数据流相关联
description: 将上下文与数据流相关联
ms.assetid: 75f5838e-626d-4a59-810e-fec9a40640ed
keywords:
- 分类标注 WDK Windows 筛选平台，与数据流关联上下文
- 上下文 WDK Windows 筛选平台
- flowContext 参数 WDK Windows 筛选平台
- 将上下文与数据流 WDK Windows 筛选平台相关联
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 24ce4858b40210b124a53cff2f0529cb106859bb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384420"
---
# <a name="associating-context-with-a-data-flow"></a>将上下文与数据流相关联


对于在支持数据流的筛选层处理数据的标注，标注驱动程序可以使用每个数据流关联上下文。 此类上下文是不透明的筛选器引擎。 标注[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数可以使用此上下文来调用由该数据流的筛选器引擎下一次将特定的状态信息保存到流的数据。 筛选器引擎传递给此上下文中的标注 classifyFn 标注函数通过*flowContext*参数。 如果没有上下文与数据流相关联*flowContext*参数为零。

若要将一个上下文与数据流，标注的相关联[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数调用[ **FwpsFlowAssociateContext0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowassociatecontext0)函数。 例如：

```cpp
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  .
  .  // Driver-specific content
  .
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
  if (FWPS_IS_METADATA_FIELD_PRESENT(
      inMetaValues,
      FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
    flowHandle = inMetaValues->flowHandle;

    // Allocate the flow context structure
    context =
      (PFLOW_CONTEXT)ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(FLOW_CONTEXT),
        FLOW_CONTEXT_POOL_TAG
      );

    // Check the result of the memory allocation
    if (context == NULL) 
    {
 
      // Handle memory allocation error
      ...
    }
    else
    {

      // Initialize the flow context structure
      ...

      // Associate the flow context structure with the data flow
      status = FwpsFlowAssociateContext0(
                flowHandle,
                FWPS_LAYER_STREAM_V4,
                calloutId,
                (UINT64)context
              );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }
    }
  }

  ...

}
```

如果上下文已与数据流相关联，它必须先删除之后，新的上下文可能会与数据流相关联。 若要删除从数据流，标注的上下文[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)标注函数调用[ **FwpsFlowRemoveContext0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowremovecontext0)函数。 例如：

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
 if (FWPS_IS_METADATA_FIELD_PRESENT(
    inMetaValues,
    FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
     flowHandle = inMetaValues->flowHandle;

    // Check whether there is a context associated with the data flow
     if (flowContext != 0) 
     {
        // Get a pointer to the flow context structure
        context = (PFLOW_CONTEXT)flowContext;

        // Remove the flow context structure from the data flow
        status = FwpsFlowRemoveContext0(
                  flowHandle,
                  FWPS_LAYER_STREAM_V4,
                  calloutId
                );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }

      // Cleanup the flow context structure
      ...

      // Free the memory for the flow context structure
      ExFreePoolWithTag(
        context,
        FLOW_CONTEXT_POOL_TAG
        );
    }
  }

  ...

}
```

在上一示例中， *calloutId*变量包含标注的运行时标识符。 运行时标识符是相同的标识符时标注驱动程序筛选器引擎注册标注返回到标注驱动程序。