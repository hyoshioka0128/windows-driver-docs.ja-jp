---
title: すべての申請の取得
description: Microsoft ハードウェア API の以下のメソッドは、製品のすべての申請に関するデータを取得します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: aad98eb7801aec7062ea2cc670fa779298e04617
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072201"
---
# <a name="get-all-submissions"></a>すべての申請の取得

Microsoft ハードウェア API の以下のメソッドを使用して、製品のすべての申請に関するデータを取得します。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

|認証方法|要求 URI|
|:--|:--|
|GET| `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions` |

### <a name="request-header"></a>要求ヘッダー

|Header|種類|説明
|:--|:--|:--|
|Authorization|string|必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。|
|accept|string|任意。 コンテンツの種類を指定します。 許容値は “application/json” です|

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、製品のすべての申請に関する情報を取得する方法を示しています。


```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

次の例は、製品のすべての申請に対する要求が成功した場合に返される JSON 応答本文を示しています。 簡潔にするために、この例では、要求によって返される最初の 2 つの申請のデータのみが示されています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "value": [
    {
      "id": 1152921504621442000,
      "productId": 13635057453741328,
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441944",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441944",
          "rel": "update_submission",
          "method": "PATCH"
        }
      ],
      "isExtensionInf": true,
      "isUniversal": true,
      "isDeclarativeInf": true,
      "name": "HARRY-Duatest2",
      "type": "derived"
    },
    {
      "id": 1152921504621442000,
      "productId": 13635057453741328,
      "workflowStatus": {
        "currentStep": "finalizeIngestion",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441946",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441946",
          "rel": "update_submission",
          "method": "PATCH"
        }
      ],
      "isExtensionInf": true,
      "isUniversal": true,
      "isDeclarativeInf": true,
      "name": "updated-1",
      "type": "derived"
    },
    {
      "id": 1152921504621442000,
      "productId": 13635057453741328,
      "workflowStatus": {
        "currentStep": "finalizeIngestion",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions/1152921504621441930",
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
  ],
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/13635057453741329/submissions",
      "rel": "self",
      "method": "GET"
    }
  ]
}
```

### <a name="response-body"></a>応答本文

|値|種類|説明|
|:--|:--|:--|
|value|array|製品の各申請に関する情報を含むオブジェクトの配列です。 各オブジェクトのデータの詳細については、「[申請のリソース](get-product-data.md#submission-resource)」を参照してください。|
|links|array|コンテナー エンティティに関する役立つリンクが含まれるオブジェクトの配列です。 詳細については、「[リンク オブジェクト](get-product-data.md#link-object)」を参照してください。|

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
