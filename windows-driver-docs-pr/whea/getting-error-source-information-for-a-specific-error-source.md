---
title: 特定のエラー ソースのエラー ソース情報の取得
description: 特定のエラー ソースのエラー ソース情報の取得
ms.assetid: 9979d654-8214-4e2d-9c6e-fc29a7f4ab40
keywords:
- エラー ソース WDK WHEA、情報の取得
- WDK WHEA、エラーのソースのエラー
- WHEA WDK、エラーのソース情報を取得します。
- エラー ソースの情報を取得する、Windows ハードウェア エラー アーキテクチャ WDK
- ハードウェア エラー ソース WDK WHEA、情報の取得
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba1322c3e352a31377af83d55635d1698ec7cf1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63377396"
---
# <a name="getting-error-source-information-for-a-specific-error-source"></a>特定のエラー ソースのエラー ソース情報の取得


ユーザー モード アプリケーションが特定の情報を取得できます[エラー ソース](hardware-errors-and-error-sources.md)ハードウェア プラットフォームによって呼び出すことによってサポートされている、 [ **WHEAErrorSourceMethods::GetErrorSourceInfoRtn**](https://msdn.microsoft.com/library/windows/hardware/ff559530)メソッド。 このメソッドが戻る、 [ **WHEA\_エラー\_ソース\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff560505)指定したエラーのソースを記述する構造体。

次のコード例では、特定のエラーのソースのエラーのソース情報を取得する方法を示します。

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
ULONG Length;
SAFEARRAY *Array;
PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSourceInfo;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that the ErrorSourceID
// variable has previously been initialized with the
// identifier of the error source to be queried.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"GetErrorSourceInfoRtn");

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

// Call the GetErrorSourceInfoRtn method indirectly
// by calling the IWbemServices::ExecMethod method.
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

// Get the length from the output parameters object
Result =
  pOutParameters->Get(
    L"Length",
    0,
    &Parameter,
    NULL,
    NULL
    );
Length = Parameter.ulval;
VariantClear(&Parameter);

// Get the data buffer from the output parameters object
Result =
  pOutParameters->Get(
    L"ErrorSourceInfo",
    0,
    &Parameter,
    NULL,
    NULL
    );
Array = Parameter.parray;

// Get access to the data buffer
Result =
  SafeArrayAccessData(
    Array,
    &ErrorSourceInfo
    );

// Process the error source information.
...

// If the error source information is to be saved
// for later use, the data in the ErrorSourceInfo
// structure must be copied to an application-allocated
// WHEA_ERROR_SOURCE_DESCRIPTOR structure before
// freeing up the resources.
...

// Free the array containing the error source information
SafeArrayUnaccessData(Array);
VariantClear(&Parameter);

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

 

 




