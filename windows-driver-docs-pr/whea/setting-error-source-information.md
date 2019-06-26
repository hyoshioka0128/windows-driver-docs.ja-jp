---
title: エラー ソース情報の設定
description: エラー ソース情報の設定
ms.assetid: 87c61c3e-768a-4784-b9ec-1ec85d65ea81
keywords:
- エラー ソース WDK WHEA、情報を設定します。
- WDK WHEA、エラーのソースのエラー
- WHEA WDK、エラーのソース情報を設定します。
- エラー ソースの情報を設定する、Windows ハードウェア エラー アーキテクチャ WDK
- ハードウェア エラー ソース WDK WHEA、情報を設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d8415bb2d2e67b3c46230cb1721b5495227ba9d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387151"
---
# <a name="setting-error-source-information"></a>エラー ソース情報の設定


ユーザー モード アプリケーションが特定の情報を設定できます[エラー ソース](hardware-errors-and-error-sources.md)ハードウェア プラットフォームによって呼び出すことによってサポートされている、 [ **WHEAErrorSourceMethods::SetErrorSourceInfoRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)メソッド。 このような状況では、アプリケーションを提供する[ **WHEA\_エラー\_ソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/ns-ntddk-_whea_error_source_descriptor)用に設定する情報を記述する構造体、指定したエラーのソース。

次のコード例では、特定のエラーのソースのエラーのソース情報を設定する方法を示します。

```cpp
IWbemServices *pIWbemServices;
WHEA_ERROR_SOURCE_DESCRIPTOR ErrorSourceInfo;
BSTR ClassName;
BSTR MethodName;
HRESULT Result;
IWbemClassObject *pClass;
IWbemClassObject *pInParametersClass;
IWbemClassObject *pInParameters;
IWbemClassObject *pOutParameters;
VARIANT Parameter;
SAFEARRAY *Array;
PVOID ArrayData;
ULONG Status;

// The following example assumes that the application
// has previously connected to WMI on the local machine
// and that the pIWbemServices variable contains the
// pointer that was returned from the call to the
// IWbemLocator::ConnectServer method.

// The following also assumes that the ErrorSourceInfo
// contains the error source information to be set.

// Note that the SetErrorSourceInfoRtn method determines
// the identifier of the error source for which the
// information is being set from the ErrorSourceId
// member of the WHEA_ERROR_SOURCE_DESCRIPTOR structure.

// Specify the class and method to execute
ClassName = SysAllocString(L"WHEAErrorSourceMethods");
MethodName = SysAllocString(L"SetErrorSourceInfoRtn");

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

// Create a safe array for the error source information
Array =
  SafeArrayCreateVector(
    VT_UI1,
    0,
    sizeof(WHEA_ERROR_SOURCE_DESCRIPTOR)
    );

// Get access to the data buffer
Result =
  SafeArrayAccessData(
    Array,
    &ArrayData
    );

// Copy the error source information
*(PWHEA_ERROR_SOURCE_DESCRIPTOR)ArrayData =
  ErrorSourceInfo;

// Release access to the data buffer
SafeArrayUnaccessData(Array);

// Set the ErrorSourceInfo parameter
Parameter.vt = VT_ARRAY | VT_UI1;
Parameter.parray = Array;
Result =
  pInParameters->Put(
    L"ErrorSourceInfo",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Set the Length parameter
Parameter.vt = VT_UI4;
Parameter.ulVal = sizeof(WHEA_ERROR_SOURCE_DESCRIPTOR);
Result =
  pInParameters->Put(
    L"Length",
    0,
    &Parameter,
    0
    );
VariantClear(&Parameter);

// Call the SetErrorSourceInfoRtn method indirectly
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

// Free up resources
SysFreeString(ClassName);
SysFreeString(MethodName);
pInParameters->Release();
pInParametersClass->Release();
pClass->Release();
pOutParameters->Release();
```

エラー ソースの構成を変更すると、アプリケーションは通常、エラーの発生元の情報を設定します。 アプリケーションでは、次の手順を実行することによって、エラーの発生元の構成を変更できます。

1.  取得、WHEA\_エラー\_ソース\_特定のエラーのソースを記述する記述子構造体。

    すべてに関する情報の取得の詳細については、[エラー ソース](hardware-errors-and-error-sources.md)システムでは、次を参照してください。[エラー ソースのすべてのエラー ソース情報を取得する](getting-error-source-information-for-all-error-sources.md)します。

    システムで特定のエラーのソースに関する情報の取得の詳細については、次を参照してください。[特定のエラーの発生元のエラー ソース情報を取得する](getting-error-source-information-for-a-specific-error-source.md)します。

2.  WHEA の内容を変更\_エラー\_ソース\_エラー ソースの構成を変更する記述子構造体。

3.  呼び出すことによって、エラーの発生元のエラーのソース情報を設定、 [ **WHEAErrorSourceMethods::SetErrorSourceInfoRtn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_whea/)メソッド

エラー ソースの構成に加えた変更は反映されませんまで、システムの再起動後です。

 

 




