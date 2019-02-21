---
title: エラーのソースを無効にします。
description: エラーのソースを無効にします。
ms.assetid: a481ac98-0ff1-4583-a81a-1d2e4f968111
keywords:
- エラー ソース WDK WHEA、無効にします。
- エラーのソースを無効にすると、Windows ハードウェア エラー アーキテクチャ WDK
- WHEA WDK、エラーのソースを無効にします。
- エラーのソースを無効にすると、WDK WHEA エラー
- ハードウェア エラー ソース WDK WHEA、無効にします。
- エラーのソースを無効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d01e04118828f3822bee50df7c620e7d8769198e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535329"
---
# <a name="disabling-an-error-source"></a>エラーのソースを無効にします。


ユーザー モード アプリケーションを無効にすることができます、[エラー ソース](hardware-errors-and-error-sources.md)呼び出すことによって、 [ **WHEAErrorSourceMethods::DisableErrorSourceRtn** ](https://msdn.microsoft.com/library/windows/hardware/ff559523)メソッド。

次のコード例では、エラーのソースを無効にする方法を示します。

```cpp
IWbemServices *pIWbemServices;
ULONG ErrorSourceID;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pClass;
IWbemClassObject *pInParametersClass;
IWbemClassObject *pInParameters;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that the ErrorSourceID
// variable has previously been initialized with the
// identifier of the error source to be disabled.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"DisableErrorSourceRtn");

// Get the class object for the method definition
Result =
  pIWbemServices->GetObject(
    ClassName,
    0,
    NULL,
    &pClass,
    NULL
    );

// Get the input parameter class object for the method
Result =
  pClass->GetMethod(
    MethodName,
    0,
    &pInParametersClass,
    NULL
    );

// Create an instance of the input parameter class
Result =
  pInParametersClass->SpawnInstance(
    0,
    &pInParameters
    );

// Set the ErrorSourceId parameter
Parameter.vt = VT_UI4;
Parameter.ulVal = ErrorSourceId;
Result =
  pInParameters->Put(
    L"ErrorSourceId",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Call the DisableErrorSourceRtn method indirectly by
// calling the IWbemServices::ExecMethod method.
Result =
  pIWbemServices->ExecMethod(
    ClassName,
    MethodName,
    0,
    NULL,
    &pInParameters,
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
VariantClear(&Parameter);

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

ユーザー モード アプリケーションを再度有効にする[エラー ソース](hardware-errors-and-error-sources.md)呼び出すことによって、 [ **WHEAErrorSourceMethods::EnableErrorSourceRtn** ](https://msdn.microsoft.com/library/windows/hardware/ff559525)メソッド。 エラーのソースを有効にする方法の詳細については、次を参照してください。 [、エラーの発生元を有効にする](enabling-an-error-source.md)します。

 

 




