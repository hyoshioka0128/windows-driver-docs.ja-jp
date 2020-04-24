---
title: 配送先住所ラベルの更新
description: このメソッドは、ハードウェア ダッシュ ボード API の配送先住所ラベルを更新します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 65cd448a3ed862f61cbe7fb894c19b3e87d40b96
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072155"
---
# <a name="update-a-shipping-label"></a>配送先住所ラベルの更新

*Microsoft ハードウェア API* の以下のメソッドを使用して、配送先住所ラベル情報を更新します。 このメソッドを使用する前に、配送先住所ラベルが既に作成されていることを確認してください。 配送先住所ラベルの作成について詳しくは、「[新しい配送先住所ラベルを作成する](create-a-new-shipping-label.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、このトピックの他のセクションをご覧ください。

| 認証方法 | 要求 URI |
|:--|:--|
| PATCH | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels/{shippingLabelId}` |

メソッド内の *ProductID*、 *submissionID*、*shippingLabelId* は、更新される製品、申請および配送先住所ラベルを表します。

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| 同意する | String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。 

### <a name="request-body"></a>[要求本文]

次の例は、配送先住所ラベルの JSON 要求本文を示しています。 配送先住所ラベルでは、次の種類の変更のみ加えることができます。

* ハードウェア ID の追加
* ハードウェア ID の削除/失効
* CHID の追加
* CHID の削除
* 対象ユーザーの追加
* 対象ユーザーの更新/削除
* 変更についてビジネス上の妥当性を示す

```json
{
  "targetingInfo": {
    "chids": [
      {
        "chid": "812fac65-9c26-473c-b3a9-1eb3803ac22c",
        "action": "add"
      },
      {
        "chid": "aed6336d-0958-444c-89b6-bf471191d6f0",
        "action": "remove"
      }
    ],
    "hardwareIds": [
      {
        "action": "remove",
        "bundleId": "a2dfbcd8-1d4a-4885-90a3-2ac8360542da",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_X64_RS3_FULL",
        "pnpString": "pci\\ven_8086&dev_5a85"
      },
      {
        "action": "add",
        "bundleId": "48140805-45a3-4a76-8818-e75c117adba9",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_X64_RS3_FULL",
        "pnpString": "pci\\ven_8086&dev_5a85"
      }
    ],
    "restrictedToAudiences": [
      "00000000-0000-0000-0000-000000000000",
      "00000000-0000-0000-0000-000000000001"
      ],
    "inServicePublishInfo": {
      "flooring": "RS1",
      "ceiling": "RS3"
    },
    "businessJustification": "Business justification for updating shipping label"
  }
}
```

要求内のフィールドについて詳しくは、「[ShippingLabel リソース](get-shipping-labels.md#shippinglabel-resource)」をご覧ください。

注意点:

* CHID や HardwareIDs を更新する場合は、*action* の値を指定する必要があります。

* *対象ユーザー*は更新専用のフィールドです。 このフィールドに値を指定すると、以前の値が上書きされます。 値を空白のままにすると、以前の値が削除されます。

* 組織の対象ユーザーの一覧を取得する方法については、「[対象ユーザー データの取得](get-audience-data.md)」をご覧ください。

* 新しい配送先住所ラベルを作成するとき、ハードウェア ID オブジェクトには、バンドル ID、PNP ID、OS コード、INF 名の有効な組み合わせが含まれる必要があります。 申請 (パッケージ) に対するこれらの属性の有効な/許可された組み合わせを取得するには、申請の詳細を取得するときに (リンクとして提供される) ドライバーのメタデータ ファイルをダウンロードします。 詳しくは、[ドライバー パッケージのメタデータ](driver-package-metadata.md)に関する記事をご覧ください。

### <a name="request-examples"></a>要求の例

次の例は、製品を更新する方法を示しています。

```json
PATCH https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964156/submissions/1152921504621467600/shippingLabels/1152921504606980300 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

応答は HTTP ステータスの 204 で空になります。

この手順の後、「[配送先住所ラベルの取得](get-a-shipping-label.md)」のメソッドを使用して、配送先住所ラベルの更新に関する詳細を取得してください。

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
