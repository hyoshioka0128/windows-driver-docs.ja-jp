---
title: 製品申請のコミット
description: Microsoft Hardware API の以下のメソッドを使用して、パートナー センターに新しい申請をコミットします。
author: balapv
ms.author: balapv
ms.date: 04/05/2018
ms.topic: article
ms.localizationpriority: medium
ms.openlocfilehash: 7683ab3a5f070fab756b98b040981d228eecdb85
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518757"
---
# <a name="commit-a-product-submission"></a>製品申請のコミット

Microsoft Hardware API の以下のメソッドを使用して、パートナー センターに新しい申請をコミットします。 これで、製品の申請を完了したことがパートナー センターに通知され、申請の検証が開始されます。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

申請をコミットするための別の前提条件は、[新しい申請の作成](create-a-new-submission-for-a-product.md)中に提供された SAS URI へのドライバー パッケージのアップロードを完了することです。 コミット操作が Microsoft ハードウェア API を使った製品アプリ申請プロセスにどのように適合するかについては、「[製品申請の管理](manage-product-submissions.md)」を参照してください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。


| メソッド | 要求 URI                                                                                                    |
|:-------|:---------------------------------------------------------------------------------------------------------------|
| POST   | https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/{productID}/submissions/{submissionID}/commit |

メソッド内の productId は、申請の対象となる製品です。 メソッド内の submssionID は、コミット中の申請です。

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String | 必須。 **Bearer** \<トークン\> という形式の Azure AD アクセス トークン。 |
| accept | String | (省略可能)。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>要求本文

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、申請をコミットする方法を示しています。

```cpp
POST https://manage.devcenter.microsoft.com/v1.0/my/hardware/products/14631253285588838/submissions/1152921504621465124/commit HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>応答

次の例は、製品の新しい申請を作成する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次のセクションをご覧ください。

```json
{
  "commitStatus": "commitStarted",
}
```

### <a name="response-body"></a>応答本文

| Value | 種類 | 説明 |
|:--|:--|:--|
| commitStatus | string | 申請の状態。 返される値は CommitStarted です |

この手順の後、メソッド [get submission details](get-a-submission.md) を使用して申請の状態を取得します。

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

# <a name="see-also"></a>関連項目

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
