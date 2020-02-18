---
title: 新しい配送先住所ラベルを作成する
description: このメソッドでは、Microsoft Hardware API で新しい配送先住所ラベルを作成する方法を示します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 6febf7bad14ccb343c45c81ed23abc09ddbb57f1
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072219"
---
# <a name="create-a-new-shipping-label"></a>新しい配送先住所ラベルを作成する

新しい配送先住所ラベルを作成するには、*Microsoft Hardware API* のこのメソッドを使用します。 これを使用する前に、製品を作成し、その製品の申請を作成してください。 詳しくは、[製品の作成](create-a-new-product.md)および[申請の作成](create-a-new-submission-for-a-product.md)に関する記事をご覧ください。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

| 認証方法 | 要求 URI |
|:--|:--|
| POST | `https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels` | 

メソッドの productID と submissionID では、配送先住所ラベルを作成する対象の申請を表します。

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| Authorization | String | 必須。 **Bearer** \<トークン\>という形式の Azure AD アクセス トークン。 |
| 同意する | String | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |


### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。 

### <a name="request-body"></a>[要求本文]

次の例では、新しい配送先住所ラベルを作成するための JSON 要求本文の例を示します。

```json
{
  "publishingSpecifications": {
    "goLiveDate": "2018-02-22T06:50:54.793Z",
    "visibleToAccounts": [
      27691110,
      27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": false,
    "manualAcquisition": false,
    "isDisclosureRestricted": false,
    "publishToWindows10s": true,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@microsoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1",
        "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": false,
      "isForUnreleasedHardware": false,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "targeting": {
    "hardwareIds": [
      {
        "bundleId": "3aba7558-10ca-42db-b1d1-57af5718aea3",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_RS3_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f"
      }
    ],
    "chids": [
      {
        "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
        "distributionState": "pendingAdd"
      }
    ],
    "restrictedToAudiences": [
      "00000000-0000-0000-0000-000000000001",
      "00000000-0000-0000-0000-000000000002"
      ],
    "inServicePublishInfo": {
      "flooring": "RS1",
      "ceiling": "RS3"
    }
  },
  "name": "Shipping Label Name",
  "destination": "windowsUpdate"
}
```

要求内のフィールドについて詳しくは、「[ShippingLabel resource (ShippingLabel リソース)](get-shipping-labels.md#shippinglabel-resource)」をご覧ください。

#### <a name="points-to-remember-when-creating-shipping-labels"></a>配送先住所ラベルを作成するときの注意点

- Windows Update に公開するときは (*destination* が **windowsUpdate**)、[publishingSpecifications](get-shipping-labels.md#publishing-specifications-object) オブジェクトを含める必要があります。 自動インストールの場合は (*isAutoInstallDuringOSUpgrade* または *isAutoInstallOnApplicableSystems* が true)、*additionalInfoForMsApproval* を設定する必要があります。
- 配送先住所ラベルで *isAutoInstallDuringOSUpgrade* または *isAutoInstallOnApplicableSystems* が true の場合、*manualAcquisition* は false である必要があり、ドライバーは [May request user input]\(ユーザーの入力が必要\) が false に設定されて公開されます。
- 配送先住所ラベルで *isAutoInstallDuringOSUpgrade* と *isAutoInstallOnApplicableSystems* が false の場合、*manualAcquisition* は true である必要があり、ドライバーは [May request user input]\(ユーザーの入力が必要\) が true に設定されて公開されます。
- 他のパートナーと共有する場合は (*destination* は **anotherPartner**)、[recipientSpecifications](get-shipping-labels.md#recipient-specifications-object) オブジェクトを含める必要があります。

#### <a name="populating-targeting-information"></a>ターゲットの情報の設定

**targeting** オブジェクトには、Windows Update に対して次のことを指示するデータが含まれます。

- ハードウェア ID に関してドライバーのターゲットを設定する方法。

- CHID または制限を適用する必要があるかどうか。

新しい配送先住所ラベルを作成するとき、ハードウェア ID オブジェクトには、バンドル ID、PNP ID、OS コード、INF 名の有効な組み合わせが含まれる必要があります。 申請に対するこれらの属性の許可された有効な組み合わせを取得するには、(申請の詳細を取得するときにリンクとして提供される) ドライバーのメタデータ ファイルをダウンロードします。 詳しくは、「[ドライバー パッケージ メタデータ](driver-package-metadata.md)」をご覧ください。

### <a name="request-examples"></a>要求の例

次の例は、新しい製品を作成する方法を示しています。

```cpp
POST https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productID}/submissions/{submissionId}/shippingLabels HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

次の例では、配送先住所ラベルを作成する要求が成功した場合に返される JSON 応答本文を示します。 応答本文の値について詳しくは、次の表をご覧ください。

```json
{
  "id": 1152921504606997500,
  "productId": 14461751976964156,
  "submissionId": 1152921504621467600,
  "publishingSpecifications": {
    "goLiveDate": "2018-02-22T06:50:54.793+00:00",
    "visibleToAccounts": [
      27691110,
      27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": false,
    "isDisclosureRestricted": false,
    "publishToWindows10s": true,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@microsoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1",
        "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": false,
      "isForUnreleasedHardware": false,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    },
    "manualAcquisition": false
  },
  "workflowStatus": {
    "currentStep": "preProcessShippingLabel",
    "state": "notStarted",
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606997603",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606997603",
      "rel": "update_shippinglabel",
      "method": "PATCH"
    }
  ],
  "name": "Shipping Label Name",
  "destination": "windowsUpdate"
}
```

### <a name="response-body"></a>応答本文

応答本文について詳しくは、「[ShippingLabel resource (ShippingLabel リソース)](get-shipping-labels.md#shippinglabel-resource)」をご覧ください。

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

[ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
