---
title: 製品データの更新
description: Microsoft ハードウェア API の以下のメソッドは、製品の詳細情報を更新します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9d2a835b10dec14903b21cb291faee22b643b95
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072185"
---
# <a name="update-product-data"></a>製品データの更新  
Microsoft ハードウェア API の以下のメソッドを使用して、製品の詳細情報を更新します。 このメソッドを使用する前に、製品を作成済みであることを確認します。 詳細については、「[新しい製品の作成](create-a-new-product.md)」を参照してください。 

## <a name="prerequisites"></a>前提条件 
Microsoft ハードウェア API に関するすべての前提条件がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。 
 
## <a name="request"></a>要求 
このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。 


| 認証方法 | 要求 URI |
|:--|:--|
| PATCH | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}` |

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String    | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| accept |  String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

次の例は、製品を更新するための JSON 応答本文を示しています。 製品に対して、announcementDate、marketingNames、productName の 3 種類の変更のみを行うことができます。

```json 
{
  "announcementDate": "2018-04-05T08:59:03.414Z",
  "marketingNames": ["name1"],
  "productName": "updatedProductName"
}
```

要求のフィールドの詳細については、「[製品リソース](get-product-data.md#product-resource)」を参照してください。

### <a name="request-examples"></a>要求の例
次の例は、製品を更新する方法を示しています。

```json 
PATCH https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

応答は HTTP ステータスの 204 で空になります。

このステップの後、メソッド [製品の詳細を取得する](get-a-product.md)を使用して製品の更新された詳細情報を取得します。

## <a name="error-codes"></a>エラー コード
詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
