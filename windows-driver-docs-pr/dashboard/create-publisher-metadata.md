---
title: 発行元ドライバー メタデータの作成
description: パートナー センター申請のための発行元ドライバー パッケージ メタデータを作成するための API 呼び出しについて説明します。
author: VanathiGanesh
ms.author: vaganesh
ms.topic: article
ms.date: 11/06/2019
ms.openlocfilehash: 8c87896d245c2eb4ba3502f438d1448e696d464e
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072221"
---
# <a name="create-publisher-driver-metadata"></a>発行元ドライバー メタデータの作成

Microsoft ハードウェア API でこのメソッドを使用して、自分と共有された申請の発行元ドライバー メタデータを作成します。 発行元ドライバーのメタデータは、受信トレイまたはシステムの申請用に作成することはできません。 ドライバー メタデータ パッケージの詳細については、「[ドライバー パッケージ メタデータ](driver-package-metadata.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。


| 認証方法 | 要求 URI                                                                                                    |
|:-------|:---------------------------------------------------------------------------------------------------------------|
| POST   | https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionID}/createpublishermetadata |

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| accept | String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、申請用に発行元ドライバー メタデータを作成する方法を示しています。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14631253285588838/submissions/1152921504621465124/createpublishermetadata HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

### <a name="response-body"></a>応答本文

応答は HTTP の状態が 202 で空になります。

この手順の後、発行元ドライバー メタデータの作成が完了するまで数時間を見込んでください。 次に、[申請の取得](get-a-submission.md)メソッドを使用して、発行元ドライバーのメタデータ ファイルのリンクを取得します。

## <a name="error-codes"></a>エラー コード

詳細については、「[エラー コード](get-product-data.md#error-codes)」を参照してください。

## <a name="see-also"></a>関連項目

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
