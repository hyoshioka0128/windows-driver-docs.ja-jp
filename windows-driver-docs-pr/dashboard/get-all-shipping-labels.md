---
title: 申請のすべての配送先住所ラベルを取得する
description: Microsoft Hardware API のこれらのメソッドでは、ハードウェア ダッシュボード アカウントに登録されているハードウェア製品の配送先住所ラベルに関するデータが取得されます。
author: balapv
ms.author: balapv
ms.topic: article
ms.date: 08/21/2018
ms.openlocfilehash: 4f5f1626ee3cb79eec1e8ee76e7cdaa752b13668
ms.sourcegitcommit: f64e64c9b2f15df154a5702e15e6a65243fc7f64
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77072203"
---
# <a name="get-all-shipping-labels"></a>すべての配送先住所ラベルを取得する

*Microsoft ハードウェア API* の以下のメソッドを使用して、製品の特定の申請の、すべての配送先住所ラベルに関するデータを取得します。

## <a name="prerequisites"></a>前提条件

Microsoft ハードウェア API に関するすべての[前提条件](dashboard-api.md)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。 これらのメソッドを使用するには、自分のデベロッパー センター アカウントに、製品および申請が既に存在している必要があります。 製品の申請を作成または管理する方法については、「[製品申請の管理](manage-product-submissions.md)」のメソッドを参照してください。

## <a name="request"></a>要求

このメソッドの構文は次のとおりです。 ヘッダーと要求本文の使用例と説明については、次のセクションをご覧ください。

|認証方法|要求 URI|
|--|--|
|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/`|

### <a name="request-header"></a>要求ヘッダー

|Header|種類|説明|
|--|--|--|
|Authorization|string|必須。 **Bearer** \*<トークン\>* という形式の Azure AD アクセス トークン。|
|accept|string|任意。 コンテンツの種類を指定します。 許容値は “application/json” です|

### <a name="request-parameters"></a>要求パラメーター

このメソッドでは要求パラメーターを指定しないでください。

### <a name="request-body"></a>[要求本文]

このメソッドでは要求本文を指定しないでください。

### <a name="request-examples"></a>要求の例

次の例は、アカウントに登録するすべての製品に関する情報を取得する方法を示しています。

```cpp
GET https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/ HTTP/1.1
Authorization: Bearer <your access token>
```
## <a name="response"></a>[応答]

次の例は、開発者アカウントに登録されている特定の製品申請の、すべての配送先住所ラベルの要求が成功した場合に返される、JSON 応答本文を示しています。 簡潔にするために、この例では、要求によって返される最初の 3 つの配送先住所ラベルのデータのみが示されています。 応答本文の値について詳しくは、次の表をご覧ください。

```json
{
  "value": [
    {
      "id": 1152921504606980300,
      "productId": 14461751976964156,
      "submissionId": 1152921504621467600,
      "publishingSpecifications": {
        "goLiveDate": "2018-04-04T16:11:27.2965057+00:00",
        "visibleToAccounts": [],
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
      "workflowStatus": {
        "currentStep": "microsoftApproval",
        "state": "started",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606980231",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606980231",
          "rel": "update_shippinglabel",
          "method": "PATCH"
        }
      ],
      "name": "Publish to Windows Update with promotions",
      "destination": "windowsUpdate"
    },
    {
      "id": 1152921504606978500,
      "productId": 14461751976964156,
      "submissionId": 1152921504621467600,
      "recipientSpecifications": {
        "receiverPublisherId": "27691110",
        "enforceChidTargeting": false
      },
      "workflowStatus": {
        "currentStep": "finalizeSharing",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978460",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978460",
          "rel": "update_shippinglabel",
          "method": "PATCH"
        }
      ],
      "name": "Share submission with another Partner",
      "destination": "anotherPartner"
    },
    {
      "id": 1152921504606978500,
      "productId": 14461751976964156,
      "submissionId": 1152921504621467600,
      "publishingSpecifications": {
        "goLiveDate": "2018-04-03T04:50:52.2293001+00:00",
        "visibleToAccounts": [],
        "isAutoInstallDuringOSUpgrade": false,
        "isAutoInstallOnApplicableSystems": false,
        "isDisclosureRestricted": false,
        "publishToWindows10s": false
      },
      "workflowStatus": {
        "currentStep": "finalizePublishing",
        "state": "completed",
        "messages": []
      },
      "links": [
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978538",
          "rel": "self",
          "method": "GET"
        },
        {
          "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978538",
          "rel": "update_shippinglabel",
          "method": "PATCH"
        }
      ],
      "name": "Publish to Windows Update without promotions",
      "destination": "windowsUpdate"
    }
  ],
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products?pageSize=50",
      "rel": "self",
      "method": "GET"
    }
  ]
}
```
このリソースには、次の値があります。

| 値 | 種類 | 説明 |
|:--|:--|:--|
| value | array | 各配送先住所ラベルに関する情報を含むオブジェクトの配列です。 各オブジェクトのデータについて詳しくは、「[配送先住所ラベルのリソース](get-shipping-labels.md#shippinglabel-resource)」をご覧ください。 |
| links | array | コンテナー エンティティに関する役立つリンクが含まれるオブジェクトの配列です。 詳しくは、「[リンク オブジェクト](get-product-data.md#link-object)」をご覧ください。|

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
