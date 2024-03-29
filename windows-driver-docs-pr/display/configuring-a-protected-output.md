---
title: 配置受保护输出
description: 配置受保护输出
ms.assetid: ff740b37-6e4a-4243-8e83-97dc2a46e3f1
keywords:
- OPM WDK 显示中，配置受保护的输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5256ac7da2398f628bbc63530114b1fb8793183d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375394"
---
# <a name="configuring-a-protected-output"></a>配置受保护输出


显示微型端口驱动程序可以接收请求，以配置受保护与图形适配器的物理输出连接器相关联的输出。 显示微型端口驱动程序[ **DxgkDdiOPMConfigureProtectedOutput** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_opm_configure_protected_output)函数传递一个指向[ **DXGKMDT\_OPM\_配置\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_dxgkmdt_opm_configure_parameters)结构，它指定如何配置受保护的输出。 **GuidSetting**并**abParameters** DXGKMDT 成员\_OPM\_配置\_参数指定配置请求。

**请注意**  之前**DxgkDdiOPMConfigureProtectedOutput**返回时，显示微型端口驱动程序必须验证一个密钥加密块链接 (CBC)-是的模式消息身份验证代码 (OMAC)中指定**omac** DXGKMDT 成员\_OPM\_配置\_参数是否正确。 有关验证 OMAC 的详细信息，请参阅[OMAC 1 算法](https://go.microsoft.com/fwlink/p/?linkid=70417)。 此外必须验证该驱动程序中的序列号，指定**ulSequenceNumber** DXGKMDT 成员\_OPM\_配置\_参数匹配序列号驱动程序当前已存储。 然后，该驱动程序必须递增存储的序列号。

 

显示微型端口驱动程序应支持以下配置请求：

-   [保护级别设置为受保护的输出](setting-the-protection-level-for-a-protected-output.md)

-   [配置保护的视频信号](configuring-protection-for-the-video-signal.md)

-   [设置 HDCP SRM 版本](setting-the-hdcp-srm-version.md)

 

 





