---
title: エラー ソース情報の設定
description: エラー ソース情報の設定
ms.assetid: 87c61c3e-768a-4784-b9ec-1ec85d65ea81
keywords:
- WDK WHEA のエラーソース、設定情報
- エラー WDK WHEA、エラーソース
- WHEA WDK、エラーソース情報の設定
- Windows ハードウェアエラーアーキテクチャ WDK、エラーソース情報の設定
- ハードウェアエラーソース WDK WHEA、設定情報
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 490cd16d833ae8520ca45abc7865f0461096ad61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843284"
---
# <a name="setting-error-source-information"></a>エラー ソース情報の設定


ユーザーモードアプリケーションでは、 [**WHEAErrorSourceMethods:: SetErrorSourceInfoRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)メソッドを呼び出すことによって、ハードウェアプラットフォームでサポートされている特定の[エラーソース](hardware-errors-and-error-sources.md)の情報を設定できます。 この場合、アプリケーションは、指定されたエラーソースに対して設定される情報を記述する[**WHEA\_エラー\_ソース\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_source_descriptor)の構造体を提供します。

次のコード例は、特定のエラーソースのエラーソース情報を設定する方法を示しています。

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

通常、アプリケーションは、エラーソースの構成を変更するときに、エラーソースの情報を設定します。 アプリケーションでは、次の手順を実行して、エラーソースの構成を変更できます。

1.  特定のエラーソースを記述する\_ソース\_記述子構造体の WHEA\_エラーを取得します。

    システム内のすべての[エラーソース](hardware-errors-and-error-sources.md)に関する情報を取得する方法の詳細については、「[すべてのエラーソースのエラーソース情報の取得](getting-error-source-information-for-all-error-sources.md)」を参照してください。

    システム内の特定のエラーソースに関する情報を取得する方法の詳細については、「[特定のエラーソースのエラーソース情報を取得する](getting-error-source-information-for-a-specific-error-source.md)」を参照してください。

2.  WHEA\_エラー\_ソース\_記述子構造体の内容を変更して、エラーソースの構成を変更します。

3.  [**WHEAErrorSourceMethods:: SetErrorSourceInfoRtn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/_whea/)メソッドを呼び出して、エラーソースのエラーソース情報を設定します。

エラーソースの構成に加えられた変更は、システムが再起動されるまで有効になりません。

 

 




