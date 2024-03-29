---
title: 使用 TmXxx 例程
description: 使用 TmXxx 例程
ms.assetid: 8bc763e9-e67c-4810-9901-e5dc1a1cfd0c
keywords:
- 内核事务管理器 WDK，TmXxx 例程
- KTM WDK，TmXxx 例程
- TmXxx 例程 WDK KTM
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 081b22b2d05539b084c6bdce69632947c7e0645d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358170"
---
# <a name="using-tmxxx-routines"></a>使用 TmXxx 例程


大多数[KTM 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)使用的命名格式为 **Zw*Xxx * * *。 这些例程都基于句柄。 即，至少一个其输入或输出参数是 KTM 对象的句柄。

KTM 还提供了较小数目的例程使用的命名格式为 **Tm*Xxx * * *。 这些例程都是基于指针的。 至少一个其输入或输出参数是指向 KTM 对象的指针。

某些**Tm * Xxx*** 例程重复**Zw * Xxx*** 例程。 其他**Tm * Xxx*** 例程没有**Zw * Xxx*** 等效项。

在大多数情况下，应使用**Zw * Xxx*** 例程。 但是，应使用**Tm * Xxx*** 在以下情况下的例程：

- 资源管理器使用[ **ResourceManagerNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ptm_rm_notification)提供一个指针指向登记对象而不是一个句柄的回调例程。

  可以将登记对象指针传递给登记对象**Tm * Xxx*** 例程。

- 在事务处理系统 (TPS) 组件执行许多快速调用 KTM，这可能会导致系统性能，以速度很慢。

  在这种情况下，可以调用你的组件[ **ObReferenceObjectByHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obreferenceobjectbyhandle)若要将每个 KTM 对象句柄转换为一个指针，保存指针，，然后将传递指向**Tm * Xxx*** 例程。 此转换不需要 KTM 将每个句柄的指针的指针在内部每个时间转换的**Zw * Xxx*** 调用例程。

  每次调用**ObReferenceObectByHandle**应包括访问掩码，其中包含相应 KTM 定义标志。 对于 KTM 的创建和打开例程上参考页介绍了这些标志。

  完成后使用 KTM 对象的组件，它必须取消该对象引用通过调用[ **ObDereferenceObjectDeferDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobjectdeferdelete)或[ **ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject).

  -   必须使用**ObDereferenceObjectDeferDelete**如果组件中或任何其他组件在您的驱动程序堆栈，持有任何系统提供的锁，例如自旋锁、 mutex 对象或快速互斥体。

  -   可以使用**ObDereferenceObject**是否确保该驱动程序堆栈上的组件不包含系统提供的锁。

  如果您的组件调用，则会发生死锁**ObDereferenceObject**时持有锁，因为 KTM 可能也持有的锁的对象命名空间。 此外，可以调用你的组件[ **TmGetTransactionId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmgettransactionid)快速相对于调用更高效地获取事务的标识符[ **ZwQueryInformationTransaction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ntqueryinformationtransaction).

- 必须具有一项功能， **Zw * Xxx*** 例程不提供。

  具体而言，资源管理器可以调用以下例程：

  -   [**TmEnableCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmenablecallbacks)启用异步传送的通知的回调例程。
  -   [**TmReferenceEnlistmentKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmreferenceenlistmentkey)并[ **TmDereferenceEnlistmentKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmdereferenceenlistmentkey)要递增或递减登记对象的键引用计数。
  -   [**TmRequestOutcomeEnlistment** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmrequestoutcomeenlistment)以请求用于登记的立即提交或回滚通知。
  -   [**TmIsTransactionActive** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-tmistransactionactive)以确定事务是否处于活动状态。

 

 




