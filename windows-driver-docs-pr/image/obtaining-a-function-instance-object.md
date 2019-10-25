---
title: 関数のインスタンス オブジェクトの取得
description: 関数のインスタンス オブジェクトの取得
ms.assetid: 2c750281-031b-4b9f-9012-3b341ebe1cd9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81a2e7c6b14454f71366fd53bcbdd73b5247f18f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840780"
---
# <a name="obtaining-a-function-instance-object"></a>関数のインスタンス オブジェクトの取得


WIA ミニドライバーは、現在のハードウェアデバイスと、それが実行されているサービスを識別する必要があります。 これらの項目を識別するために、ミニドライバーは関数探索サービスから関数インスタンスオブジェクトを実行時に取得し、デバイスのプロパティを読み取ります。

関数探索 COM インターフェイスを使用するには、次の例に示すように、ミニドライバーコードに、Windows Vista SDK で使用できる*Functiondiscovery. h*メインヘッダーファイルを含める必要があります。

```cpp
//
// Web Services Function Discovery main header:
//
#include <FunctionDiscovery.h>
```

初期化中に、 [**iミニドライバー:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)メソッドで発生する場合がありますが、関数検出をクエリして、ハードウェアデバイスを表す適切な関数インスタンスオブジェクトを取得する必要があります。 このクエリを完了するには、次の手順 (および関連するコード例) を使用します。

### <a name="step-1-create-the-function-discovery-object"></a>手順 1: 関数検出オブジェクトを作成する

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

### <a name="step-2-create-an-instance-collection-query-object"></a>手順 2: インスタンスコレクションのクエリオブジェクトを作成する

```cpp
IFunctionInstanceCollectionQuery *pfiCollectionQuery = NULL;
pFunctionDiscovery->CreateInstanceCollectionQuery(FCTN_CATEGORY_PNP,
   NULL,
   FALSE,
   NULL,
   NULL,
   &pfiCollectionQuery);
```

### <a href="" id="step-3--add-a-constraint-to-the-instance-collection-query-object-to-sp"></a>手順 3: インスタンスコレクションのクエリオブジェクトに制約を追加して、PNPX ID を指定します (その値は IGetMyDevicePortName を使用して取得されます)。

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

### <a name="step-4-execute-the-query"></a>手順 4: クエリを実行する

```cpp
IFunctionInstanceCollection *pfiCollection = NULL;
pfiCollectionQuery->Execute(&pfiCollection);
```

### <a name="step-5-retrieve-the-function-instance-object-that-is-returned"></a>手順 5: 返された関数インスタンスオブジェクトを取得する

```cpp
//
// Function Instance object that represents our device instance
//
IFunctionInstance *pFunctionInstance;

pfiCollection->Item(0, &m_pFunctionInstance);
```

サンプルクラス (CWSDDevice) の宣言を含むコード例については、「[関数インスタンスオブジェクトを取得するためのコードサンプル](code-example-for-obtaining-a-function-instance-object.md)」を参照してください。

 

 




