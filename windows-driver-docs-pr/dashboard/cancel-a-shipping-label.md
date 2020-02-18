---
title: 配送先住所ラベルの取り消し
description: Microsoft による承認または段階的なロールアウトで配送先住所ラベルの取り消しを要求するには、Microsoft ハードウェア API のこのメソッドを使用します。
ms.topic: article
ms.date: 11/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7532f0275676300aa320449823c62dd70db21333
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072169"
---
# <a name="cancel-a-shipping-label"></a>配送先住所ラベルの取り消し

Microsoft による承認または段階的なロールアウトで配送先住所ラベルの取り消しを要求するには、"*Microsoft ハードウェア API*" のこのメソッドを使用します。 このメソッドを使用する前に、配送先住所ラベルが Microsoft による承認または段階的なロールアウトにあることを確認してください。 配送先住所ラベルの取得について詳しくは、[新しい配送先住所ラベルの取得](get-a-shipping-label.md)に関する記事をご覧ください。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)をまだ満たしていない場合は、このメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、このトピックの他のセクションをご覧ください。

| 認証方法 | 要求 URI |
|:--|:--|
| PUT | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels/{shippingLabelId}/cancel` |

メソッド内の *ProductID*、*submissionID*、*shippingLabelId* は、取り消される製品、申請および配送先住所ラベルを表します。

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| 同意する | String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。 

### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。 

### <a name="request-examples"></a>要求の例

次の例は、配送先住所ラベルの取り消しを要求する方法を示しています。

```json
PUT https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964156/submissions/1152921504621467600/shippingLabels/1152921504606980300/cancel HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

応答は HTTP ステータスの 204 で空になります。

この手順の後、「[配送先住所ラベルの取得](get-a-shipping-label.md)」のメソッドを使用して、配送先住所ラベルの更新に関する詳細を取得してください。 ドライバーのフライティング システムでのドライバーの実際の取り消しは、完了するまでに 1 日以上かかる場合があることに注意してください。

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
