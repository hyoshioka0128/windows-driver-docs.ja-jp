---
title: 製品の取得
description: Microsoft ハードウェア API の以下のメソッドは、Windows デベロッパー センター アカウントに登録されている特定の製品のデータを取得します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 349dcb2238ba7dedf71f28c8bf02cea57a770516
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072217"
---
# <a name="get-a-product"></a>製品の取得

Windows デベロッパー センター アカウントに登録されている特定の製品に関するデータを取得するには、Microsoft ハードウェア API の以下のメソッドを使います。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

|認証方法|要求 URI|
|:--|:--|
|GET|https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}|

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| 承認 | string | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| accept | string | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |


### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、アカウントに登録する特定の製品に関する情報を取得する方法を示しています。

```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14039471039847257 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

次の例は、開発者アカウントに登録されている特定の製品に対する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
    "id": 9007199267351834,
    "sharedProductId": 1152921504606971255,
    "links": [
        {
            "href": "https://hardwareapi.microsoft.com/api/v1/hardware/products/9007199267351834",
            "rel": "self",
            "method": "GET"
        },
        {
            "href": "https://hardwareapi.microsoft.com/api/v1/hardware/products/9007199267351834/submissions",
            "rel": "get_submissions",
            "method": "GET"
        }
    ],
    "isCommitted": true,
    "isExtensionInf": false,
    "originType": "author",
    "sourceProductId": 0,
    "sourcePublisherId": 0,
    "isRetpolineCompiled": false,
    "message": "",
    "deviceMetadataIds": [],
    "deviceType": "notSet",
    "isTestSign": false,
    "isFlightSign": false,
    "marketingNames": [],
    "productName": "NewDriverHacked",
    "selectedProductTypes": {},
    "requestedSignatures": [
        "WINDOWS_v100_X64_TH1_FULL",
        "WINDOWS_v63_X64"
    ],
    "additionalAttributes": {},
    "testHarness": "hlk"
}
```

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
