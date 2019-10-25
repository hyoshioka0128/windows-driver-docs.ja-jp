---
title: エラー ソースを無効にする
description: エラー ソースを無効にする
ms.assetid: a481ac98-0ff1-4583-a81a-1d2e4f968111
keywords:
- WDK WHEA、無効化、エラーソース
- Windows ハードウェアエラーアーキテクチャ WDK、エラーソースの無効化
- WHEA WDK、エラーソースの無効化
- エラー WDK WHEA、エラーソースの無効化
- ハードウェアエラーソース WDK WHEA、無効化
- エラー sourc を無効にする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06e1f1285809df70bc09191daa1606b8969ed26a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844382"
---
# <a name="disabling-an-error-source"></a>エラー ソースを無効にする


ユーザーモードアプリケーションでは、 [**WHEAErrorSourceMethods::D isableErrorSourceRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)メソッドを呼び出すことによって、[エラーソース](hardware-errors-and-error-sources.md)を無効にすることができます。

次のコード例は、エラーソースを無効にする方法を示しています。

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

ユーザーモードアプリケーションでは、 [**WHEAErrorSourceMethods:: EnableErrorSourceRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)メソッドを呼び出すことによって、[エラーソース](hardware-errors-and-error-sources.md)を再度有効にすることができます。 エラーソースを有効にする方法の詳細については、「[エラーソースの有効化](enabling-an-error-source.md)」を参照してください。

 

 




