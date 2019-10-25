---
title: エラー挿入機能の取得
description: エラー挿入機能の取得
ms.assetid: d4ff0d9c-bb17-4dff-8008-bf8d59e44621
keywords:
- エラー挿入機能 WDK WHEA
- エラー挿入機能の取得 (WDK WHEA)
- エラー WDK WHEA、エラー挿入
- WHEA WDK、エラー挿入
- Windows ハードウェアエラーアーキテクチャ WDK、エラー挿入
- ハードウェアエラーの挿入 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fc751bcadc1090cc81d4980a9d43f62319d8948
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844406"
---
# <a name="getting-error-injection-capabilities"></a>エラー挿入機能の取得


ユーザーモードアプリケーションでは、 [**WHEAErrorInjectionMethods:: GetErrorInjectionCapabilitiesRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)メソッドを呼び出すことによって、ハードウェアプラットフォームのエラー挿入機能に関する情報を取得できます。 このメソッドは、ハードウェアプラットフォームでサポートされているエラー挿入機能を記述する、 [**WHEA\_エラー\_挿入\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_injection_capabilities)の構造体を返します。

次のコード例は、エラー挿入機能の情報を取得する方法を示しています。

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

 

 




