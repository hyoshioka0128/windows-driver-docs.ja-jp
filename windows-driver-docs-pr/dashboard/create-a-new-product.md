---
title: 新しい製品の作成
description: Microsoft ハードウェア API の以下のメソッドを使用して、新しいハードウェア製品を作成します。
ms.date: 04/05/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 31e32fa44d981da56e848bf9fc3ba9e67780fc62
ms.sourcegitcommit: f68ab92a8f1c13502e070297cf5410f6bbe4a9dc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2020
ms.locfileid: "86213175"
---
# <a name="create-a-new-product"></a>新しい製品の作成

Microsoft ハードウェア API の以下のメソッドを使用して、新しいハードウェア製品を作成します。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| 認証方法 | 要求 URI |
|:--|:--|
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products` |


### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | string | 必須。 **Bearer** \<token\> という形式の Azure AD アクセス トークン。 |
| accept | string | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |


### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

次の例は、新しい製品を作成するための JSON 要求本文を示しています。 要求本文の値の詳細については、JSON の下の表を参照してください。

```json
{
  "productName": "Test_Network_Product2-R",
  "testHarness": "Attestation",
  "announcementDate": "2018-01-01T00:00:00",
  "deviceMetadataIds": [],
  "firmwareVersion": "980",
  "deviceType": "external",
  "isTestSign": false,
  "isFlightSign": false,  
  "marketingNames": [],
  "selectedProductTypes": {
    "windows_v100_RS3": "Unclassified"
  },
  "requestedSignatures": [
    "WINDOWS_v100_RS3_FULL",
    "WINDOWS_v100_X64_RS3_FULL",
    "WINDOWS_VISTA"
  ],
  "additionalAttributes": {},
  "packageType": "HLK"
}
```

要求のフィールドの詳細については、「[製品リソース](get-product-data.md#product-resource)」を参照してください。

### <a name="request-examples"></a>要求の例

次の例は、新しい製品を作成する方法を示しています。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

次の例は、製品を作成する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "id": 14631253285588838,
  "sharedProductId": 1152921504607010608,
  "links": [
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v1/hardware/products/14631253285588838",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https:// manage.devcenter.microsoft.com/api/v1/hardware/products/14631253285588838/submissions",
      "rel": "get_submissions",
      "method": "GET"
    }
  ],
  "isCommitted": false,
  "isExtensionInf": false,
  "announcementDate": "2018-01-01T00:00:00",
  "deviceMetadataIds": [],
  "firmwareVersion": "980",
  "deviceType": "external",
  "isTestSign": false,
  "isFlightSign": false,  
  "marketingNames": [],
  "productName": "VST_apdevtest1",
  "selectedProductTypes": {
    "windows_v100_RS3": "Unclassified"
  },
  "requestedSignatures": [
    "WINDOWS_v100_RS3_FULL",
    "WINDOWS_v100_X64_RS3_FULL",
    "WINDOWS_VISTA"
  ],
  "additionalAttributes": {},
  "testHarness": "attestation"
}
```

### <a name="response-body"></a>応答本文

詳細については、「[製品リソース](get-product-data.md#product-resource)」を参照してください

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
