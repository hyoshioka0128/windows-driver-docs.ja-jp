---
title: 申請データの更新
description: Microsoft ハードウェア API の以下のメソッドは、申請の詳細情報を更新します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9303d6b4df89a80259b447e68eb7247c91ba1b90
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072151"
---
# <a name="update-submission-data"></a>申請データの更新 

Microsoft ハードウェア API の以下のメソッドを使用して、申請の詳細情報を更新します。 このメソッドを使用する前に、申請を作成済みであることを確認します。 詳細については、「[新しい申請の作成](create-a-new-hardware-submission.md)」を参照してください。


## <a name="prerequisites"></a>前提条件
Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求
このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| 認証方法 | 要求 URI |
|:--|:--|
| PATCH | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}`

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
|Authorization | String | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| accept | String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

次の例は、製品を更新するための JSON 応答本文を示しています。 申請には名前の変更のみが可能です。

```json
{
  "name": "updatedSubmissionName"
}
```

要求のフィールドの詳細については、「[申請のリソース](get-product-data.md#submission-resource)」を参照してください。

### <a name="request-examples"></a>要求の例
次の例は、製品を更新する方法を示しています。

```json 
PATCH https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504627422408 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

応答は HTTP ステータスの 204 で空になります。

このステップの後、メソッド [申請の詳細を取得する](get-a-submission.md)を使用して製品の更新された詳細を取得します。

## <a name="error-codes"></a>エラー コード
詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
