---
title: 製品の新しい申請の作成
description: Microsoft ハードウェア API の以下のメソッドを使用して、製品の新しい申請を作成します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e153d22e6fcd54eb9706e150f8547eb89d74f1a2
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072159"
---
# <a name="create-a-new-submission-for-a-product"></a>製品の新しい申請の作成

Microsoft ハードウェア API の以下のメソッドを使用して、製品の新しい申請を作成します。 このメソッドを使用する前に、新しい製品を作成済みであることを確認します。 詳細については、「[新しい製品の作成](create-a-new-product.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| 認証方法 | 要求 URI |
|:--|:--|
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions` |


メソッド内の productId は、申請の対象となる製品です。

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| 同意する | String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |


### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

次の例は、新しい製品を作成するための JSON 要求本文の例を示しています。

```json
{
  "name": "VST_apdevtest1_init",
  "type": "initial"
}
```

要求のフィールドの詳細については、「[申請のリソース](get-product-data.md#submission-resource)」を参照してください。

### <a name="request-examples"></a>要求の例

次の例は、新しい申請を作成する方法を示しています。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

次の例は、製品の新しい申請を作成する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "id": 1152921504621465124,
  "productId": 14631253285588838,
  "downloads": {
    "items": [
      {
        "type": "initialPackage",
        "url": "https://ingestionpackages.blob.core.windows.net/ingestion/38c19eaf-7377-4834-893c-28d5791f7896?sv=2017-04-17&sr=b&sig=SlD5j5e067oA4Y3hdk1sPW3UycTSUVlIp80WbWvj4A8%3D&se=2018-03-20T05:00:14Z&sp=rwl"
      }
    ],
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504621465124",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504621465124",
      "rel": "update_submission",
      "method": "PATCH"
    }
  ],
  "commitStatus": "commitPending",
  "isExtensionInf": true,
  "isUniversal": true,
  "isDeclarativeInf": true,
  "name": "VST_apdevtest1_init",
  "type": "initial"
}
```

### <a name="response-body"></a>応答本文

詳細については、「[申請のリソース](get-product-data.md#submission-resource)」を参照してください。

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
