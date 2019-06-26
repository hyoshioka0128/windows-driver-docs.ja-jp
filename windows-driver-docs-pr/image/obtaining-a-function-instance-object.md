---
title: 関数のインスタンス オブジェクトの取得
description: 関数のインスタンス オブジェクトの取得
ms.assetid: 2c750281-031b-4b9f-9012-3b341ebe1cd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f6c879103e51038e9baf389d6ff1fa7e61598b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376590"
---
# <a name="obtaining-a-function-instance-object"></a>関数のインスタンス オブジェクトの取得


WIA ミニドライバーは、現在のハードウェア デバイスとで実行されているサービスを識別する必要があります。 これらの項目を識別するためには、ミニドライバーは、機能探索サービスから実行時に関数のインスタンスのオブジェクトを取得し、デバイスのプロパティを読み取ります。

関数の検出の COM インターフェイスを使用するミニドライバーのコードを含める必要があります、 *FunctionDiscovery.h*メイン ヘッダー ファイルは、次の例に示すように、Windows Vista SDK で使用できます。

```cpp
//
// Web Services Function Discovery main header:
//
#include <FunctionDiscovery.h>
```

初期化中とで行われる処理、 [ **IStiUSD::Initialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize)メソッド、ミニドライバーは適切な関数のインスタンスを表すオブジェクトを取得する機能の探索をクエリする必要があります、ハードウェア デバイスです。 このクエリを完了するには、次の手順 (および関連付けられているコード例は、) を使用します。

### <a name="step-1-create-the-function-discovery-object"></a>手順 1:機能探索オブジェクトを作成します。

```cpp
//
// Function Discovery object
//
IFunctionDiscovery *pFunctionDiscovery = NULL;
CoCreateInstance(__uuidof(FunctionDiscovery),
                 NULL,
                 CLSCTX_INPROC_SERVER,
                 __uuidof(IFunctionDiscovery),
  (void**)&pFunctionDiscovery);
```

### <a name="step-2-create-an-instance-collection-query-object"></a>手順 2:インスタンスのコレクションのクエリ オブジェクトを作成します。

```cpp
IFunctionInstanceCollectionQuery *pfiCollectionQuery = NULL;
pFunctionDiscovery->CreateInstanceCollectionQuery(FCTN_CATEGORY_PNP,
   NULL,
   FALSE,
   NULL,
   NULL,
   &pfiCollectionQuery);
```

### <a href="" id="step-3--add-a-constraint-to-the-instance-collection-query-object-to-sp"></a>手順 3:クエリの制約として (IStiDeviceControl::GetMyDevicePortName とその値を取得します) PNPX ID を指定するインスタンスのコレクションのクエリ オブジェクトに制約を追加します。

```cpp
PROPVARIANT PropVar = {0};
//
// Note that the wszDevicePath value is obtained by the WIA minidriver 
// calling IStiDeviceControl::GetMyDevicePortName during IStiUSD::Initialize
//
PropVariantInit(&PropVar);
PropVar.vt = VT_LPWSTR;
PropVar.pwszVal = (LPWSTR)wszDevicePath; 
pfiCollectionQuery->AddPropertyConstraint(PKEY_PNPX_ID, &PropVar, QC_EQUALS);
```

### <a name="step-4-execute-the-query"></a>手順 4:クエリを実行します

```cpp
IFunctionInstanceCollection *pfiCollection = NULL;
pfiCollectionQuery->Execute(&pfiCollection);
```

### <a name="step-5-retrieve-the-function-instance-object-that-is-returned"></a>手順 5:返される関数のインスタンス オブジェクトを取得します。

```cpp
//
// Function Instance object that represents our device instance
//
IFunctionInstance *pFunctionInstance;

pfiCollection->Item(0, &m_pFunctionInstance);
```

サンプル クラス (CWSDDevice) の宣言を含むコード例を参照してください。[関数インスタンスのオブジェクトを取得するためのコード サンプル](code-example-for-obtaining-a-function-instance-object.md)します。

 

 




