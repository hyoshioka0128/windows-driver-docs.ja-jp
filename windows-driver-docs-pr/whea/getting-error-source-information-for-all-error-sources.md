---
title: すべてのエラー ソースのエラー ソース情報の取得
description: すべてのエラー ソースのエラー ソース情報の取得
ms.assetid: 78e3a015-128d-44d1-b0ec-4da43c359090
keywords:
- エラー ソース WDK WHEA、情報の取得
- WDK WHEA、エラーのソースのエラー
- WHEA WDK、エラーのソース情報を取得します。
- エラー ソースの情報を取得する、Windows ハードウェア エラー アーキテクチャ WDK
- ハードウェア エラー ソース WDK WHEA、informati を取得します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a2b12bc7b4758dd35502187089eab0537444fc9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386477"
---
# <a name="getting-error-source-information-for-all-error-sources"></a>すべてのエラー ソースのエラー ソース情報の取得


ユーザー モード アプリケーションは、すべての情報を取得できます、[エラー ソース](hardware-errors-and-error-sources.md)で呼び出すことによって、システム、 [ **WHEAErrorSourceMethods::GetAllErrorSourcesRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)メソッド。 このメソッドの配列を返します[ **WHEA\_エラー\_ソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_source_descriptor)でサポートされているエラーのソースのすべてを記述する構造体、ハードウェア プラットフォームです。

次のコード例では、すべてのエラーのソース システムでエラーのソース情報を取得する方法を示します。

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

 

 




