---
title: 将 I/O 请求发送到较低的驱动程序
description: 将 I/O 请求发送到较低的驱动程序
ms.assetid: 89868b4d-e2c1-4f38-b81e-a96b8cff3e4f
keywords:
- I/O 请求 WDK UMDF，较低的驱动程序
- 请求处理 WDK UMDF，较低的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1d8471a29a645cd427643b603381f7aa1651482
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567367"
---
# <a name="sending-io-requests-to-lower-drivers"></a>将 I/O 请求发送到较低的驱动程序


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

当驱动程序收到不能完全处理的 I/O 请求时，该驱动程序通常将转发到堆栈中下一个较低的驱动程序收到的请求。 驱动程序调用[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)方法将请求转发。 若要以同步方式转发，驱动程序通过了 WDF\_请求\_发送\_选项\_同步标志中*标志*参数。 否则，该驱动程序将转发请求以异步方式。 该驱动程序将转发请求之前，它应注册完成例程。 有关详细信息，请参阅[完成 I/O 请求](completing-i-o-requests.md)。

 

 




