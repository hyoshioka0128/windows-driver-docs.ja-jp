---
title: エラーの挿入機能を取得します。
description: エラーの挿入機能を取得します。
ms.assetid: d4ff0d9c-bb17-4dff-8008-bf8d59e44621
keywords:
- エラーの挿入機能 WDK WHEA
- エラーの挿入機能 WDK WHEA を取得します。
- エラー WDK WHEA、エラーの挿入
- WHEA WDK、エラーの挿入
- Windows ハードウェア アーキテクチャ WDK のエラー、エラーの挿入
- ハードウェア エラー WDK WHEA の挿入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a778288b41c07419acb4dea2ce44223130d943e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539529"
---
# <a name="getting-error-injection-capabilities"></a>エラーの挿入機能を取得します。


ユーザー モード アプリケーション機能を取得できます、エラーに関する情報の挿入、ハードウェア プラットフォームの呼び出すことによって、 [ **WHEAErrorInjectionMethods::GetErrorInjectionCapabilitiesRtn** ](https://msdn.microsoft.com/library/windows/hardware/ff559516)メソッド。 このメソッドが戻る、 [ **WHEA\_エラー\_インジェクション\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff560460)でサポートされているエラーの挿入機能を記述する構造体、ハードウェア プラットフォームです。

次のコード例では、エラーの挿入機能情報を取得する方法を示します。

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

 

 




