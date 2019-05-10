---
title: すべての製品の取得
description: Microsoft ハードウェア API の以下のメソッドは、Windows デベロッパー センター アカウントに登録されているすべての製品に関するデータを取得します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9b55e7b3cd77d39ec6d6ca39646b63068361a4af
ms.sourcegitcommit: 944535d8e00393531f6b265317a64da3567e4f2c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2019
ms.locfileid: "65106386"
---
# <a name="get-all-products"></a>すべての製品の取得

Microsoft ハードウェア API の以下のメソッドを使用して、Windows デベロッパー センター アカウントに登録されているすべての製品に関するデータを取得します。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

|メソッド|要求 URI|
|--|--|
|GET| `https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/` |

### <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|--|--|--|
|Authorization|string|必須。 **Bearer** \<トークン\> という形式の Azure AD アクセス トークン。|
|accept|string|(省略可能)。 コンテンツの種類を指定します。 許容値は “application/json” です|

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>要求本文

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、アカウントに登録するすべての製品に関する情報を取得する方法を示しています。

```cpp
GET https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/ HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、開発者アカウントに登録されているすべての製品に対する要求が成功した場合に返される JSON 応答本文を示しています。 簡潔にするために、この例では、要求によって返される最初の 2 つの製品のデータのみが示されています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "value": [
    {
            "id": 9007199267351834,
            "sharedProductId": 1152921504606971255,
            "links": [
                {
                    "href": "https://hardwareapi-int.microsoft.com/api/v1/hardware/products/9007199267351834",
                    "rel": "self",
                    "method": "GET"
                },
                {
                    "href": "https://hardwareapi-int.microsoft.com/api/v1/hardware/products/9007199267351834/submissions",
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
        },
        {
            "id": 9007199267351835,
            "sharedProductId": 1152921504606971256,
            "links": [
                {
                    "href": "https://hardwareapi-int.microsoft.com/api/v1/hardware/products/9007199267351835",
                    "rel": "self",
                    "method": "GET"
                },
                {
                    "href": "https://hardwareapi-int.microsoft.com/api/v1/hardware/products/9007199267351835/submissions",
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
            "announcementDate": "2016-10-22T00:00:00Z",
            "deviceMetadataCategory": "Input.Digitizer.Multitouch",
            "deviceMetadataIds": [],
            "deviceType": "internalExternal",
            "isTestSign": false,
            "isFlightSign": false,
            "marketingNames": [
                "MEU"
            ],
            "productName": "Mew2?",
            "selectedProductTypes": {
                "Windows_v100": "Touch",
                "Windows81": "Unclassified"
            },
            "requestedSignatures": [
                "WINDOWS_v100_X64_TH1_FULL",
                "WINDOWS_v63_X64"
            ],
            "additionalAttributes": {},
            "testHarness": "hlk"
        }
  ]
}
```

### <a name="response-body"></a>応答本文

| Value | 種類 | 説明 |
|:--|:--|:--|
| value | array | アカウントに登録されている各製品についての情報が含まれるオブジェクトの配列。 各オブジェクトのデータの詳細については、「[製品リソース](get-product-data.md#product-resource)」を参照してください。 |
| links | array | コンテナー エンティティに関する役立つリンクが含まれるオブジェクトの配列です。 詳細については、「[リンク オブジェクト](get-product-data.md#link-object)」を参照してください。  |


## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。 

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
