---
title: 使用具有 DXVA 2.0 加密会话解码器
description: 将加密会话与 DirectX 视频加速器 2.0 解码器配合使用
ms.assetid: 2a3577f5-bc44-4e0d-a5fa-217dc6c6f5f3
keywords:
- DXVA 2.0 解码器 WDK Windows 7 显示
- DXVA 2.0 解码器 WDK Windows Server 2008 R2 显示
- DXVA 2.0 解码器 WDK Windows 7 显示将与加密会话相关联
- DXVA 2.0 解码器 WDK Windows Server 2008 R2 显示将与加密会话相关联
- DirectX 视频 Accelerator 2.0 解码器 WDK Windows 7 显示
- DirectX 视频 Accelerator 2.0 解码器 WDK Windows Server 2008 R2 显示
- DirectX 视频 Accelerator 2.0 解码器 WDK Windows 7 显示将与加密会话相关联
- DirectX 视频 Accelerator 2.0 解码器 WDK Windows Server 2008 R2 显示将与加密会话相关联
- 加密会话 WDK Windows 7 显示
- 加密会话 WDK Windows Server 2008 R2 显示
- 加密会话 WDK Windows 7 显示，将与 DXVA 2.0 解码器相关联
- 加密会话 WDK Windows Server 2008 R2 显示，将与 DXVA 2.0 解码器相关联
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: a4793db5d8d594764be2fb5e5362bb8e340bc11a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370644"
---
# <a name="using-crypto-session-with-directx-video-accelerator-20-decoder"></a>将加密会话与 DirectX 视频加速器 2.0 解码器配合使用


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

用户模式显示驱动程序可以将相关联的加密会话与 DirectX 视频 Accelerator (VA) 2.0 解码设备以便使 DirectX VA 2.0 解码设备，请使用加密会话的会话密钥。 如果 Direct3D 运行时指定一个有效的解码中的 GUID **DecodeProfile**的成员[ **D3DDDIARG\_CREATECRYPTOSESSION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)结构时运行时调用的驱动程序[ **CreateCryptoSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数以创建加密的会话中，运行时可以随后调用的驱动程序[ **ConfigureAuthenticatedChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)函数与 D3DAUTHETICATEDCONFIGURE\_CRYPTOSESSION 设置为使用 DirectX VA 2.0 配置加密会话对设备进行解码。 在使用 DirectX VA 2.0 配置加密会话之前解码设备，在运行时必须调用的驱动程序[ **DecodeExtensionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)函数以检索有关 DirectX VA 2.0 的驱动程序句柄对设备进行解码。 在运行时设置的成员[ **D3DDDIARG\_DECODEEXTENSIONEXECUTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute)为以下值，以检索有关 DirectX VA 2.0 的驱动程序句柄的结构对设备进行解码：

```cpp
#define DXVA2_DECODE_GET_DRIVER_HANDLE    0x725
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_GET_DRIVER_HANDLE;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = 0;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = HANDLE*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = sizeof(HANDLE);
```

当运行时调用的驱动程序[ **CreateDecodeDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)函数来创建 DirectX VA 2.0 解码设备中，运行时指定的解码加密 Guid 内的零[**DXVADDI\_CONFIGPICTUREDECODE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_configpicturedecode)结构。

运行时调用的驱动程序后[ **CreateCryptoSession** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数与**CryptoType**隶属[ **D3DDDIARG\_CREATECRYPTOSESSION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)结构设置为 D3DCRYPTOTYPE\_AES128\_CTR 创建加密的会话中，设置**pPVPSetKey** 的成员[**D3DDDIARG\_DECODEBEGINFRAME** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)驱动程序的调用中的结构[ **DecodeBeginFrame** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)函数进行解码框架表示以下含义：

-   如果**pPVPSetKey**设置为**NULL**、 none 帧缓冲区包含加密的数据，因此不需要解密。

-   如果**pPVPSetKey**指向 NULL\_GUID （全部为零），帧缓冲区使用会话密钥进行加密。

-   如果**pPVPSetKey**指向内容密钥，它指示应用程序使用会话密钥加密内容密钥。 驱动程序应使用此内容密钥来解密此帧与相关联的所有加密的缓冲区。

显示在每个加密缓冲区的初始化向量**pCipherCounter**的成员[ **DXVADDI\_DECODEBUFFERDESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)的调用中的结构驱动程序的[ **DecodeExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)函数。 该驱动程序应失败的调用其*DecodeExecute*函数如果确定的初始化向量以前使用同一内容密钥 （或如果未使用的内容密钥的会话密钥）。 应用程序应递增**IV**的成员[ **DXVADDI\_PVP\_HW\_IV** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvaddi_pvp_hw_iv)为每个缓冲区应用程序进行加密。 因此，驱动程序*DecodeExecute*函数可能会失败，如果**IV**成员是小于或等于上一个**IV**传递到值*DecodeExecute*。

如果在运行时部分必须对缓冲区进行加密，则会调用驱动程序的[ **DecodeExtensionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)函数，并设置的成员[ **D3DDDIARG\_DECODEEXTENSIONEXECUTE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute)为下列值以指定可阻止将驱动程序的结构应该对进行加密：

```cpp
#define DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS    0x724
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = D3DENCRYPTED_BLOCK_INFO*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = sizeof(D3DENCRYPTED_BLOCK_INFO);
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = 0;
```

 

 





