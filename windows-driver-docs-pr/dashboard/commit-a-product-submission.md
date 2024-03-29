---
title: 确认产品提交
description: 在 Microsoft 硬件 API 中使用此方法向合作伙伴中心确认新提交。
author: balapv
ms.author: balapv
ms.date: 04/05/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7683ab3a5f070fab756b98b040981d228eecdb85
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/13/2019
ms.locfileid: "63337276"
---
# <a name="commit-a-product-submission"></a>确认产品提交

在 Microsoft 硬件 API 中使用此方法向合作伙伴中心确认新提交。 这将通知合作伙伴中心你已完成产品提交并且将开始对提交进行验证。

## <a name="prerequisites"></a>必备条件

如果尚未开始操作，请先完成 Microsoft 硬件 API 的所有[先决条件](dashboard-api.md)，然后再尝试使用其中任何方法。

确认提交的另一个先决条件是完成将驱动程序包上传到[创建新提交](create-a-new-submission-for-a-product.md)时提供的 SAS URI。 有关确认操作如何适用通过使用 Microsoft 硬件 API 提交产品应用过程的详细信息，请参阅[管理产品提交](manage-product-submissions.md)。

## <a name="request"></a>请求

此方法具有以下语法。 请参阅以下部分，获取标头和请求正文的使用示例和描述。


| 方法 | 请求 URI                                                                                                    |
|:-------|:---------------------------------------------------------------------------------------------------------------|
| POST   | https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionID}/commit |

此方法中的 productId 是提交所适用于的产品。 此方法中的 submssionID 是正在确认的提交。

### <a name="request-header"></a>请求头

| 标头 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| 授权 | 字符串 | 必需。 Azure AD 访问令牌的格式为 **Bearer** \<token\>。 |
| accept | 字符串 | 可选。 指定内容的类型。 允许的值是“application/json” |

### <a name="request-parameters"></a>请求参数

请勿为此方法提供请求参数。

### <a name="request-body"></a>请求正文

请勿为此方法提供请求正文。

### <a name="request-examples"></a>请求示例

以下示例演示了如何确认提交。

```cpp
POST https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14631253285588838/submissions/1152921504621465124/commit HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>响应

以下示例演示了为产品创建新提交的成功请求所返回的 JSON 响应正文。 有关响应正文中这些值的详细信息，请参阅以下部分。

```json
{
  "commitStatus": "commitStarted",
}
```

### <a name="response-body"></a>响应正文

| 值 | 在任务栏的搜索框中键入 | 描述 |
|:--|:--|:--|
| commitStatus | 字符串 | 提交的状态。 返回的值将是 CommitStarted |

完成此步骤后，请使用[获取提交详细信息](get-a-submission.md)方法来获取提交的状态。

## <a name="error-codes"></a>错误代码

有关详细信息，请参阅[错误代码](get-product-data.md#error-codes)。

# <a name="see-also"></a>另请参阅

[硬件仪表板 API 示例 (GitHub)](https://aka.ms/hpc_async_api_samples)
