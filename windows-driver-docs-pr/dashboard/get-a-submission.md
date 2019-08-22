---
title: 申請の取得
description: Microsoft パートナー センターで、ハードウェア ダッシュボードへの製品の特定の申請に関するデータを取得します。
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 71e94fc186e6302964e147b8c3232457ce411702
ms.sourcegitcommit: 3de5c4aa7df9c21fc26dd063c8c4b65d67c83c58
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223982"
---
# <a name="get-a-submission"></a>申請の取得

Microsoft ハードウェア API の以下のメソッドを使用して、製品の特定の申請に関するデータを取得します。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

|メソッド|要求 URI|
|:--|:--|
|GET|`https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionID}` |

### <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|:--|:--|:--|
|Authorization|string|必須。 **Bearer** \<トークン\> という形式の Azure AD アクセス トークン。|
|accept|string|(省略可能)。 コンテンツの種類を指定します。 許容値は “application/json” です|

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>要求本文

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、製品のすべての申請に関する情報を取得する方法を示しています。


```cpp
GET https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/13635057453741329/submissions/1152921504621441930 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、製品の特定の申請に対する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "id": 1152921504621442000,
  "productId": 13635057453741328,
  "workflowStatus": {
    "currentStep": "finalizeIngestion",
    "state": "completed",
    "messages": []
  },
  "downloads": {
    "items": [
      {
        "type": "initialPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/dc55b8c6-a01c-40b6-b815-cac8bc08812a?sv=2016-05-31&sr=b&sig=ipjW3RsVC75lZrcEZRh9JmTX89L4gTIKkxwqv9F8Axs%3D&se=2018-03-12T15:32:10Z&sp=rl"
      },
      {
        "type": "derivedPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/6bd77dbf-a851-46d2-b703-29ea4efae006?sv=2016-05-31&sr=b&sig=O5XQf%2FzMbI2FFt5WwSUJWL1JbWY4JXXPRkCKAnX7IRs%3D&se=2018-03-12T15:32:10Z&sp=rl&rscd=attachment%3B filename%3DShell_1152921504621441930.hlkx"
      },
      {
        "type": "signedPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/0b83a294-c1d1-4136-82a1-dd52f51841e3?sv=2016-05-31&sr=b&sig=zTfxKJmaTwpbFol%2FpAKG0QuXJTTxm5aZ0F2wQQI8whc%3D&se=2018-03-12T15:32:10Z&sp=rl"
      },
      {
        "type": "certificationReport",
        "url": "https:// manage.devcenter.microsoft.com/dashboard/hardware/Driver/DownloadCertificationReport/29963920/13635057453741329/1152921504621441930"
      }
    ],
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
      "rel": "update_submission",
      "method": "PATCH"
    }
  ],
  "isExtensionInf": true,
  "isUniversal": true,
  "isDeclarativeInf": true,
  "name": "HARRY-Duatest2",
  "type": "initial"
}
```

### <a name="response-body"></a>応答本文

詳細については、「[申請のリソース](get-product-data.md#submission-resource)」を参照してください

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
