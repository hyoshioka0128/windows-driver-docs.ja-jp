---
title: エラー ソースを有効にする
description: エラー ソースを有効にする
ms.assetid: a65357fa-e600-47fe-8719-b67c36542711
keywords:
- エラー ソース WDK WHEA、有効にします。
- エラーのソースを有効にすると、Windows ハードウェア エラー アーキテクチャ WDK
- WHEA WDK、エラーのソースを有効にします。
- エラーのソースを有効にすると、WDK WHEA エラー
- ハードウェア エラーのソースを有効にする、WDK WHEA
- エラー ソース WDK を有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c791344a61b3854be1a31937249ef8d65db6ae9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362593"
---
# <a name="enabling-an-error-source"></a>エラー ソースを有効にする


ユーザー モード アプリケーションを有効にすることができます、[エラー ソース](hardware-errors-and-error-sources.md)呼び出すことによって、 [ **WHEAErrorSourceMethods::EnableErrorSourceRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)メソッド。

次のコード例では、エラーのソースを有効にする方法を示します。

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
// identifier of the error source to be enabled.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"EnableErrorSourceRtn");

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

// Call the EnableErrorSourceRtn method indirectly by
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

ユーザー モード アプリケーションを無効にすることができます、[エラー ソース](hardware-errors-and-error-sources.md)呼び出すことによって、 [ **WHEAErrorSourceMethods::DisableErrorSourceRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)メソッド。 エラーのソースを無効にする方法の詳細については、次を参照してください。 [、エラーのソースを無効にする](disabling-an-error-source.md)します。

 

 




