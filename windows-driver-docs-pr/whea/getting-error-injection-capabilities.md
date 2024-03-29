---
title: 获取错误注入功能
description: 获取错误注入功能
ms.assetid: d4ff0d9c-bb17-4dff-8008-bf8d59e44621
keywords:
- 错误注入功能 WDK WHEA
- 检索错误注入功能 WDK WHEA
- 错误 WDK WHEA，错误注入
- WHEA WDK，错误注入
- Windows 硬件错误体系结构 WDK，错误注入
- 注入硬件错误 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e02fb314100b8404ee8f6bf66807cd4228ba54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367993"
---
# <a name="getting-error-injection-capabilities"></a>获取错误注入功能


在用户模式应用程序可以获取有关错误的信息的硬件平台的注入功能通过调用[ **WHEAErrorInjectionMethods::GetErrorInjectionCapabilitiesRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)方法。 此方法返回[ **WHEA\_错误\_注入\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_injection_capabilities)结构，它介绍了支持的错误注入功能硬件平台。

下面的代码示例演示如何检索错误注入功能信息。

```cpp
IWbemServices *pIWbemServices;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;
WHEA_ERROR_INJECTION_CAPABILITIES ErrorInjectionCapabilities;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorInjectionMethods");
MethodName = SysAllocString(L"GetErrorInjectionCapabilitiesRtn");

// Call the GetErrorInjectionCapabilitiesRtn method indirectly
// by calling the IWbemServices::ExecMethod method.
Result =
  pIWbemServices->ExecMethod(
    ClassName,
    MethodName,
    0,
    NULL,
    NULL,
    &pOutParameters,
    NULL
    );

// Get the status from the output parameters object
Result =
  pOutParameters->Get(
    L"Status",
    0,
    &Parameter,
    NULL,
    NULL
    );
Status = Parameter.ulval;
VariantClear(Parameter);

// Get the capabilities from the output parameters object
Result =
  pOutParameters->Get(
    L"Capabilities",
    0,
    &Parameter,
    NULL,
    NULL
    );
ErrorInjectionCapabilities.AsULONG = Parameter.ulval;
VariantClear(Parameter);

// Process the error injection capabilities data
...

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pOutParameters->Release();
```

 

 




