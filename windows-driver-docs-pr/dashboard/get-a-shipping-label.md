---
title: 配送先住所ラベルの取得
description: Microsoft ハードウェア API の以下のメソッドは、ハードウェア デベロッパー センター アカウントに登録されているハードウェア製品のデータを取得します。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: d14bc2ed0b3a291062c1af4e83ca0d409a595d4c
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "77072213"
---
# <a name="get-a-shipping-label"></a>配送先住所ラベルの取得

このメソッドを使用すると、製品の特定の申請の特定の配送先住所ラベルに関するデータを取得できます。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。 これらのメソッドを使用するには、自分のデベロッパー センター アカウントに、製品および申請が既に存在している必要があります。 製品の申請を作成または管理する方法については、「[製品申請の管理](manage-product-submissions.md)」のメソッドを参照してください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

|認証方法|要求 URI|
|--|--|
|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/{shippingLabelId}`|

### <a name="request-header"></a>要求ヘッダー

| Header | 種類 | 説明 |
|:--|:--|:--|
| 承認 | string | 必須。 **Bearer** \*<トークン\>* という形式の Azure AD アクセス トークン。 |
| accept | string | 任意。 コンテンツの種類を指定します。 許容値は “application/json” です |

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは、要求パラメーターはオプションです。

|名前|種類|説明|
|:--|:--|:--|
| includeTargetingInfo | boolean | 任意。 このパラメーターが true に設定されている場合は、配送先住所ラベルで、配送先住所ラベルのターゲットの詳細が返されます (ハードウェア ID や CHID など)。 詳しくは、「[ターゲット オブジェクト](get-shipping-labels.md#targeting-object)」をご覧ください。|

### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、アカウントに登録する特定の製品に関する情報を取得する方法を示しています。

```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964156/submissions/1152921504621467600/shippingLabels/1152921504606980300 HTTP/1.1
Authorization: Bearer <your access token>
```

## <a name="response"></a>[応答]

次の例は、特定の配送先住所ラベルに対する要求が成功した場合に返される JSON 応答本文を示しています。 応答本文の値について詳しくは、次の表をご覧ください。

```json
{
  "id": 1152921504606978300,
  "productId": 14461751976964156,
  "submissionId": 1152921504621467600,
  "publishingSpecifications": {
    "goLiveDate": "2018-04-12T05:28:32.721Z",
    "visibleToAccounts": [
      27691110,
      27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": true,
    "isDisclosureRestricted": false,
    "publishToWindows10s": false,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@mcirosoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1",
        "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": true,
      "isForUnreleasedHardware": true,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "targeting": {
    "hardwareIds": [
      {
        "bundleId": "amd64",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
        "distributionState": "pendingAdd"
      },
      {
        "bundleId": "amd64",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_RS2_FULL",
        "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
        "distributionState": "pendingAdd"
      }
    ],
    "chids": [
      {
        "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
        "distributionState": "pendingAdd"
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
    "coEngDriverPublishInfo": {
      "flooringBuildNumber": 17135,
      "ceilingBuildNumber": 17139
    }
  },
  "workflowStatus": {
    "currentStep": "microsoftApproval",
    "state": "started",
    "messages": []
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978459",
      "rel": "self",
      "method": "GET"
    },
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978459",
      "rel": "update_shippinglabel",
      "method": "PATCH"
    }
  ],
  "name": "VR_RS4Build_DualPublishCheck",
  "destination": "windowsUpdate"
}
```
### <a name="response-body"></a>応答本文

応答本文について詳しくは、「[ShippingLabel リソース](get-shipping-labels.md#shippinglabel-resource)」をご覧ください。

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
