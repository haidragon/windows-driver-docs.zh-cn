---
title: 容器对非 DX Api 的支持
description: 非 DX Api 必须更直接与驱动程序和内核交互, 因此它们的复杂性更高
ms.assetid: 6c4a6974-c67b-4710-80c6-48a5b378e088
ms.date: 05/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8b5f2a7be3b55ed9d51e6eca4ada8a261a857c97
ms.sourcegitcommit: 44f09d983954f27fd90b737a2dd142aad7dffd9d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2019
ms.locfileid: "70059171"
---
# <a name="container-support-for-non-dx-apis"></a>容器对非 DX Api 的支持

Windows 10 添加了多个功能, 这些功能明显影响非 DX Api, 还增加了它们依赖的更低级别的 WDDM 体系结构详细信息。
1. 半虚拟化 WDDM 适配器 
2. 用户现在可以控制不区分自身的应用程序所使用的适配器
3. [通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)引入了一组新的设计原则

若要保持与最新的 Windows 10 功能的兼容性, 需要进行以下修改:

## <a name="driver-inf-modifications"></a>驱动程序 INF 修改
驱动程序必须将非 DX 运行时注册到相应的注册表位置, 以将其二进制文件安装到 Windows 安装的 system32 和 syswow64 子目录中。
在安装 INF 中, 驱动程序可以在图形适配器注册表项的下列子项中定义多个值:
- CopyToVmOverwrite
- CopyToVmWhenNewer
- CopyToVmOverwriteWow64
- CopyToVmWhenNewerWow64

以前的子键会修改 system32 目录, 而后一子项会修改 syswow64 目录。
__更新__的是通过比较文件的[ChangeTime](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_file_basic_information)来定义的。
子项下的每个值类型必须为 REG_MULTI_SZ 或 REG_SZ。 如果值类型为 REG_MULTI_SZ, 则值中必须包含最多2个字符串。 这意味着每个值都定义了一对 stings, 其中的第二个字符串可能为空。
对中的第一个名称是指向驱动程序存储区中的文件的路径。 路径相对于驱动程序存储区的根路径, 可以包含子目录。
对中的第二个名称是文件的名称, 该名称将显示在 system32 或 syswow64 目录中。
第二个名称必须只是文件名, 不能包含路径。 如果第二个名称为空, 则文件名与驱动程序存储区中的名称相同 (子目录除外)。
这使得驱动程序可以在主机驱动程序存储和来宾中具有不同的名称。 

### <a name="example-1"></a>示例 1：
INF [DDInstall] 部分  
HKR、"softgpukmd\CopyToVmOverwrite"、SoftGpuFiles、% REG_MULTI_SZ%、"CopyToVm\softgpu1.dll"、"softgpu2"  

指令将在软件 (适配器) 密钥中创建注册表项:"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<number > \CopyToVmOverwrite", SoftGpuFiles = REG_MULTI_SZ, "CopyToVm\softgpu1.dll", "softgpu2"

OS 会将 DriverStorePath \<> \CopyToVm\softgpu1.dll 复制到%windir%\system32\softgpu2.dll

### <a name="example-2"></a>示例 2：
INF [DDInstall] 部分:  
HKR、"CopyToVmOverwrite"、SoftGpuFiles1、% REG_MULTI_SZ%、"softgpu1"、"softgpu"  
HKR, "CopyToVmOverwrite", SoftGpuFiles2,% REG_SZ%, "softgpu2"  

指令将在软件 (适配器) 密钥中创建注册表项:  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<number > \CopyToVmOverwrite", SoftGpuFiles1 = REG_MULTI_SZ, "softgpu1", "softgpu"  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<number > \CopyToVmOverwrite", SoftGpuFiles = REG_SZ, "softgpu2 .dll"  

OS 会将 DriverStorePath \<> \softgpu1.dll 复制到%windir%\system32\softgpu.dll, \<DriverStorePath > \softgpu2.dll 复制到%windir%\system32\softgpu2.dll

### <a name="example-3"></a>示例 3：
INF [DDInstall] 部分:  
HKR、"CopyToVmOverwriteWow64"、SoftGpuFiles、% REG_MULTI_SZ%、"Subdir1\Subdir2\softgpu2wow64.dll"、"softgpu"  

指令将在软件 (适配器) 密钥中创建注册表项:  
"HKLM\SYSTEM\CurrentControlSet\Control\Class\\{4d36e968-e325-11ce-bfc1-08002be10318}\\\<number > \CopyToVmOverwriteWow64", SoftGpuFiles = REG_MULTI_SZ, "Subdir1\Subdir2\softgpu2wow64.dll", "softgpu "  

OS 会将 DriverStorePath \<> \Subdir1\Subdir2\softgpu2wow64.dll 复制到%windir%\syswow64\softgpu.dll

## <a name="driver-modifications-to-registry-and-file-paths"></a>注册表和文件路径的驱动程序修改
在容器中, 驱动程序存储区并不一致地位于与通常相同的规范路径中。
若要一致地使用正确调整的路径, 必须通过[KMTQAITYPE_QUERYREGISTRY](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/ne-d3dkmthk-_kmtqueryadapterinfotype)和[D3DDDI_QUERYREGISTRY_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_queryregistry_info)的[D3DKMTQueryAdapterInfo](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtqueryadapterinfo)间接访问注册表和驱动程序存储区。

## <a name="honor-os-default-adapter-setting"></a>遵循 OS 默认适配器设置
默认适配器必须遵循操作系统中存储的用户选择, 这需要:
1. 通过 DXGI 的[IDXGIFactory:: EnumAdapters](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgifactory-enumadapters)枚举适配器, 因为 dxgi 是用户的选择。 适配器0根据[用户的设置](https://blogs.windows.com/windowsexperience/2018/02/07/announcing-windows-10-insider-preview-build-17093-pc/)进行了更改。
2. 使适配器从[D3DKMTEnumAdapters2](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmthk/nf-d3dkmthk-d3dkmtenumadapters2)到 DXGI 的顺序匹配。
可以通过关联两个枚举技术之间的 LUID 来匹配适配器标识。
DXGI 通过[IDXGIAdapter:: GetDesc](https://docs.microsoft.com/windows/desktop/api/dxgi/nf-dxgi-idxgiadapter-getdesc)返回其 LUID。

## <a name="dchu-design-modifications"></a>DCHU 设计修改
请考虑尽可能多的[通用驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/getting-started-with-universal-drivers)设计主体, 这可能会根据所支持的确切设备而有所不同。

## <a name="wdk-dependency"></a>WDK 依赖项

前面提到的许多方法和类型仅在 WDK 中可用。
尽管 WDK 主要用于构建驱动程序, 但它还为与驱动程序捆绑的组件提供更低级别的接口。
如果非 dx Api 包含 WDK, 或将 WDK 依赖项本地化为非 DX 运行时或驱动程序加载器, 则 Microsoft 会提供非 DX API 项目的权限, 以便有效地应对 WDK 依赖关系。
可以通过使用 Microsoft 的公共文档, 并在项目中创建与二进制兼容的类型和函数声明, 来切断 WDK 依赖关系。
这些 typenames 不能与 Microsoft 使用的相同, 因此, 如果其他人有意利用 WDK 处理非 DX API 项目, 则可避免名称冲突。

