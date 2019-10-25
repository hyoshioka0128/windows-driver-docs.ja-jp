---
title: すべてのエラー ソースのエラー ソース情報の取得
description: すべてのエラー ソースのエラー ソース情報の取得
ms.assetid: 78e3a015-128d-44d1-b0ec-4da43c359090
keywords:
- WDK WHEA のエラーソース、情報の取得
- エラー WDK WHEA、エラーソース
- WHEA WDK、エラーソース情報の取得
- Windows ハードウェアエラーアーキテクチャ WDK、エラーソース情報の取得
- ハードウェアエラーソース WDK WHEA、情報を入手する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f291455824d38afb274051ce9268323d4510e6b4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844404"
---
# <a name="getting-error-source-information-for-all-error-sources"></a>すべてのエラー ソースのエラー ソース情報の取得


ユーザーモードアプリケーションでは、 [**WHEAErrorSourceMethods:: GetAllErrorSourcesRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)メソッドを呼び出すことによって、システム内のすべての[エラーソース](hardware-errors-and-error-sources.md)に関する情報を取得できます。 このメソッドは、ハードウェアプラットフォームでサポートされているすべてのエラーソースを記述する、 [**WHEA\_エラー\_ソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)構造体の配列を返します。

次のコード例は、システム内のすべてのエラーソースのエラーソース情報を取得する方法を示しています。

```cpp
IWbemServices *pIWbemServices;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
ULONG Status;
ULONG Count;
ULONG Length;
SAFEARRAY *Array;
PWHEA_ERROR_SOURCE_DESCRIPTOR ErrorSourceList;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"GetAllErrorSourcesRtn");

// Call the GetAllErrorSourcesRtn method indirectly
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
VariantClear(&Parameter);

// Get the count from the output parameters object
Result =
  pOutParameters->Get(
    L"Count",
    0,
    &Parameter,
    NULL,
    NULL
    );
Count = Parameter.ulval;
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
    L"ErrorSourceArray",
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
    &ErrorSourceList
    );

// Process the error source information.
...

// If the error source information is to be saved
// for later use, the data in the ErrorSourceList
// array must be copied to an application-allocated
// array of WHEA_ERROR_SOURCE_DESCRIPTOR structures
// before freeing up the resources.
...

// Free the array containing the error source information
SafeArrayUnaccessData(Array);
VariantClear(&Parameter);

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pOutParameters->Release();
```

 

 




