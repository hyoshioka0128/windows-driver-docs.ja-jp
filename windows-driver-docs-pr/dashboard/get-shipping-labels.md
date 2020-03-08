---
title: 配送先住所ラベルのデータを取得する
description: Microsoft Hardware API のこれらのメソッドでは、デベロッパー センター アカウントに登録されているハードウェア製品の配送先住所ラベルに関するデータが取得されます。
ms.topic: article
ms.date: 10/03/2019
ms.openlocfilehash: f4795fa7a29071c1eb2c83051cf68a2052caa447
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402375"
---
# <a name="get-shipping-label-data"></a>配送先住所ラベルのデータを取得する

API を使用するための前提条件など、Microsoft ハードウェア API の概要については、「[API を使用したハードウェア提出の管理](dashboard-api.md)」を参照してください。

ハードウェア デベロッパー センター アカウントに登録されているハードウェア製品の配送先住所ラベルに関するデータを取得するには、*Microsoft Hardware API* の以下のメソッドを使用します。

```html
https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/
```

これらのメソッドを使用するには、製品および申請をお客様自身のデベロッパー センター アカウントに用意しておく必要があります。 製品の申請を作成または管理する方法については、「[製品申請の管理](manage-product-submissions.md)」のメソッドを参照してください。

|説明|認証方法|URI|
|-|-|-|
|[申請のすべての配送先住所ラベルに関するデータを取得する](get-all-shipping-labels.md)|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/`|
|[申請の特定の配送先住所ラベルに関するデータを取得する](get-a-shipping-label.md)|GET|`https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/{productId}/submissions/{submissionId}/shippingLabels/{shippingLabelId}`|

## <a name="prerequisites"></a>前提条件

Microsoft Hardware API に関するすべての[前提条件](https://docs.microsoft.com/windows-hardware/drivers/dashboard/dashboard-api#complete-prerequisites-for-using-the-microsoft-hardware-api)がまだ満たされていない場合は、ここに記載されているメソッドを使用する前に前提条件を整えてください。

## <a name="data-resources"></a>データ リソース

配送先住所ラベル データを取得するための Microsoft Hardware Dashboard API のメソッドでは、次の JSON データ リソースが使用されます。

### <a name="shippinglabel-resource"></a>ShippingLabel リソース

このリソースは、お客様のアカウントに登録されている製品の申請用に作成された配送先住所ラベルを表します。

```json
{
  "id": 1152921504606978422,
  "productId": 14461751976964157,
  "submissionId": 1152921504621467613,
  "publishingSpecifications": {
    "goLiveDate": "2018-04-12T05:28:32.721Z",
    "visibleToAccounts": [
      27691110, 27691111
    ],
    "isAutoInstallDuringOSUpgrade": true,
    "isAutoInstallOnApplicableSystems": true,
    "isDisclosureRestricted": false,
    "publishToWindows10s": false,
    "additionalInfoForMsApproval": {
      "microsoftContact": "abc@microsoft.com",
      "validationsPerformed": "Validation 1",
      "affectedOems": [
        "OEM1", "OEM2"
      ],
      "isRebootRequired": false,
      "isCoEngineered": true,
      "isForUnreleasedHardware": true,
      "hasUiSoftware": false,
      "businessJustification": "This is a business justification"
    }
  },
  "recipientSpecifications": {
    "receiverPublisherId": "27691110",
    "enforceChidTargeting": true
  },
  "targeting": {
    "hardwareIds": [
      {
        "bundleId": "amd64",
        "infId": "foo.inf",
        "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
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
    "currentStep": "finalizePublishing",
    "state": "completed",
    "messages": [],
    "errorReport": ""
  },
  "links": [
    {
      "href": "https://manage.devcenter.microsoft.com/v2.0/my/hardware/products/14461751976964157/submissions/1152921504621467613/shippingLabels/1152921504606978422",
      "rel": "self",
      "method": "GET"
    }
  ],
  "name": "Shipping Label Name",
  "destination": "windowsUpdate"
}
```

このリソースには、次の値があります。

| 値 | 種類 | 説明 |
|:--|:--|:--|
|id|long|配送先住所ラベルの ID|
|productId|long|この配送先住所ラベルが関連付けられているプライベート製品 ID|
|submissionId|long|この配送先住所ラベルが関連付けられている申請 ID|
|publishingSpecifications|オブジェクト|詳しくは、「[公開仕様オブジェクト](#publishing-specifications-object)」をご覧ください|
|recipientSpecifications|オブジェクトの配列|詳しくは、「[受信者仕様オブジェクト](#recipient-specifications-object)」をご覧ください|
|ターゲット設定|オブジェクト|詳しくは、「[ターゲット オブジェクト](#targeting-object)」をご覧ください|
|workflowStatus|オブジェクト|このオブジェクトでは、この配送先住所ラベルに対するワークフローの状態が示されています。 詳しくは、「[配送先住所ラベル ワークフロー状態オブジェクト](#shipping-label-workflow-status-object)」をご覧ください|
|links|オブジェクトの配列|詳しくは、「[リンク オブジェクト](get-product-data.md#link-object)」をご覧ください。|
|name|string|配送先住所ラベルの名前|
|destination|string|配送先住所ラベルの送付先を示します。 使用できる値は次のとおりです (かっこ内に説明があります)。 <ul><li>anotherPartner ("*この配送先住所ラベルは、別のパートナーと申請を共有するためのものです*")</li><li>windowsUpdate ("*この配送先住所ラベルは、Windows Update に公開するためのものです*")</li><li>notSet</li></ul>|

### <a name="publishing-specifications-object"></a>公開仕様オブジェクト

このオブジェクトは、Windows Update にオブジェクトを公開する方法の仕様を表します。 このオブジェクトは、配送先住所ラベルの *destination* が *windowsUpdate* の場合にのみ使用可能/必要です

```json
{
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
    "microsoftContact": "abc@microsoft.com",
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
}
```

このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|goLiveDate|datetime|Windows Update でドライバーがダウンロードできるようになる日時。 日時を指定しないと、ドライバーは認定後すぐに公開されます。|
|visibleToAccounts|long の配列|ドライバーと配送先住所ラベルに対して読み取り専用アクセス許可を持っている SellerID のリスト。 この情報は、パートナーの代わりにドライバーを公開する場合など、配送先住所ラベルの要求をパートナーに通知する必要がある場合に役に立ちます。|
|isAutoInstallDuringOSUpgrade|boolean|オペレーティング システムのアップグレードの間にドライバーを該当するコンピューターに配信するかどうか。|
|isAutoInstallOnApplicableSystems|boolean|ドライバーを該当するコンピューターに自動的に配信するかどうか。|
|isDisclosureRestricted|boolean|ドライバーを WSUS および Windows Update カタログで非表示にする/する必要があるかどうか。|
|publishToWindows10s|boolean|ドライバーを Windows 10 S に公開するかどうか|
|additionalInfoForMsApproval|オブジェクト|詳しくは、「[Microsoft オブジェクトに関する追加情報](#additional-information-for-the-microsoft-object)」をご覧ください。|

### <a name="additional-information-for-the-microsoft-object"></a>Microsoft オブジェクトに関する追加情報

このオブジェクトは、Microsoft が配送先住所ラベルを確認するために必要な追加情報を表します。 このオブジェクトは、配送先住所ラベルの *destination* が *windowsUpdate* であり、配送先住所ラベルが *isAutoInstallDuringOSUpgrade* または *isAutoInstallOnApplicableSystems* とマークされている場合にのみ、使用可能/必要です。

```json
{
    "microsoftContact": "abc@microsoft.com",
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
```
このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|microsoftContact|string|この要求においてお客様と協力する Microsoft スポンサーのメール アドレス|
|validationsPerformed|string|ドライバーの検証方法についての説明。 この情報は、レビュー中に Microsoft によって使用されます。|
|affectedOems|string|この公開によって影響を受ける OEM の名前のリスト。 Microsoft は、レビューの間にこの情報を使います。|
|isRebootRequired|boolean|ドライバーのインストールの後で再起動が必要かどうか。 この情報は、レビュー中に Microsoft によって使用されます。|
|isCoEngineered|boolean|ドライバーが Windows のアクティブな (リリースされていない) ビルドで共同エンジニアリングされているドライバーかどうか。 Microsoft は、レビューの間にこの情報を使います。|
|isForUnreleasedHardware|boolean|ドライバーで新規デバイスまたは未リリース デバイスがサポートされているかどうか。 この情報は、レビュー中に Microsoft によって使用されます。|
|hasUiSoftware|boolean|ドライバーで UI かソフトウェアまたはその両方が展開されるかどうか。 この情報は、レビュー中に Microsoft によって使用されます。|
|businessJustification|string|この公開要求をプロモーションするビジネス上の正当性。 この情報は、レビュー中に Microsoft によって使用されます。|

### <a name="recipient-specifications-object"></a>受信者仕様オブジェクト

このオブジェクトは、別のパートナーとの申請の共有に関する詳細と条件を表します。 このオブジェクトは、配送先住所ラベルの *destination* が *anotherPartner* の場合にのみ使用可能/必要です。

```json
{
    "receiverPublisherId": "27691110",
    "enforceChidTargeting": false
}
```
このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|receiverPublisherId|string|ドライバーを共有する相手の販売者 ID。 受信者は、ドライバーをダウンロードし、Windows Update に公開して、DUA パッケージを作成することができます。 受信者は、他のパートナーとさらに共有することはできません。|
|enforceChidTargeting|boolean|パートナーがこのドライバー申請に対して作成するすべての配送先住所ラベルに CHID を適用する必要があるかどうかを示します。 これにより、多くのパートナー企業とハードウェア ID を共有する場合に、ユーザーを保護することができます。|

### <a name="targeting-object"></a>ターゲット オブジェクト

このオブジェクトは、Windows Update に公開するときに必要な配送先住所ラベルのターゲットの詳細を表します。

```json
{
  "hardwareIds": [
    {
      "bundleId": "amd64",
      "infId": "foo.inf",
      "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
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
}
```
このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|hardwareIds|オブジェクトの配列|詳しくは、「[ハードウェア ID オブジェクト](#hardware-id-object)」をご覧ください|
|chids|オブジェクトの配列|詳しくは、「[CHID オブジェクト](#chids-object)」をご覧ください。|
|restrictedToAudiences|String の配列|対象ユーザーを表す文字列の配列。 対象ユーザーを使用すると、この公開を特定の構成のコンピューターに限定できます。 たとえば、テスト対象ユーザーは、特定のレジストリ キーがインストールされているクライアントのみに配信されます。 組織に適用可能な対象ユーザーの識別と管理については、「[Get audience data (対象ユーザーのデータを取得する)](get-audience-data.md)」をご覧ください。|
|inServicePublishInfo|オブジェクト|詳しくは、「[サービス内公開情報オブジェクト](#in-service-publish-information-object)」をご覧ください。 ターゲット オブジェクトは、inServicePublishInfo "*または*" coEngDriverPublishInfo のどちらか一方のみを含むことができ、両方を含むことはできません。|
|coEngDriverPublishInfo|オブジェクト|詳しくは、「[共同エンジニアリング ドライバー公開情報オブジェクト](#co-engineering-driver-publish-information-object)」をご覧ください。 ターゲット オブジェクトは、inServicePublishInfo "*または*" coEngDriverPublishInfo のどちらか一方のみを含むことができ、両方を含むことはできません。|

### <a name="hardware-id-object"></a>ハードウェア ID オブジェクト

このオブジェクトは、配送先住所ラベルの対象とする必要があるハードウェア ID の詳細を表します。 詳しくは、「[Hardware ID (ハードウェア ID)](https://docs.microsoft.com/windows-hardware/drivers/install/hardware-ids)」をご覧ください。

```json
{
    "bundleId": "amd64",
    "infId": "foo.inf",
    "operatingSystemCode": "WINDOWS_v100_SERVER_X64_RS5_FULL",
    "pnpString": "hid\\vid_dummy256f&pid_dummyc62f",
    "distributionState": "pendingAdd"
}
```
このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|bundleId|string|ハードウェア ID が存在するバンドルを表す ID。|
|infId|string|このハードウェア ID が含まれる inf ファイルの名前|
|operatingSystemCode|string|この特定のハードウェア ID とアーキテクチャの組み合わせに対して適用されるオペレーティング システム コード。 使用可能な値については、「[list of OS codes (OS コードの一覧)](get-product-data.md#list-of-operating-system-codes)」をご覧ください。|
|pnpString|string|ターゲットにする PNP ID またはハードウェア ID。|
|distributionState|string|このハードウェア ID の現在のターゲットの状態を表します。 使用できる値は次のとおりです (かっこ内に説明があります)。<ul><li>pendingAdd ("*このハードウェア ID に対して追加が要求され、処理が進行中です*")</li><li>pendingRemove ("*このハードウェア ID に対して削除 (期限切れ) が要求され、処理が進行中です*")</li><li>added ("*このハードウェア ID は、この配送先住所ラベルのターゲットとして正常に追加されました*")</li><li>notSet ("*このハードウェア ID では、操作が行われていないか、または状態が設定されていません*")</li></ul>|
|action|string|これは、配送先住所ラベルの更新/パッチの間にのみ適用されます。 設定できる値は次のとおりです。 <ul><li>追加</li><li>削除</li></ul> |

新しい配送先住所ラベルを作成するとき、ハードウェア ID オブジェクトには、バンドル ID、PNP ID、OS コード、INF 名の有効な組み合わせが含まれる必要があります。 申請 (パッケージ) に対するこれらの属性の許可された/有効な組み合わせは、申請の詳細を取得するときにリンクとして提供されるドライバーのメタデータ ファイルをダウンロードすることで取得できます。 詳しくは、「[ドライバー パッケージ メタデータ](driver-package-metadata.md)」をご覧ください。

### <a name="chids-object"></a>CHID オブジェクト

このオブジェクトは、配送先住所ラベルの対象とする必要がある CHID (コンピューター ハードウェア ID) を表します。 詳しくは、[using CHIDs (CHID の使用)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/using-chids) に関する記事をご覧ください。

```json
{
    "chid": "346511cf-ccee-5c6d-8ee9-3c70fc7aae83",
    "distributionState": "pendingAdd"
}
```

このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|chid|GUID|ターゲットにする必要がある CHID|
|distributionState|string|この CHID の現在のターゲットの状態を表します。 使用できる値は次のとおりです (かっこ内に説明があります)。<ul><li>pendingAdd ("*このハードウェア ID に対して追加が要求され、処理が進行中です*")</li><li>pendingRemove ("*このハードウェア ID に対して削除 (期限切れ) が要求され、処理が進行中です*")</li><li>added ("*このハードウェア ID は、この配送先住所ラベルのターゲットとして正常に追加されました*")</li><li>notSet ("*このハードウェア ID では、操作が行われていないか、または状態が設定されていません*")</li></ul>|
|action|string|これは、配送先住所ラベルの更新/パッチの間にのみ適用されます。 設定できる値は次のとおりです。 <ul><li>追加</li><li>削除</li></ul> |

### <a name="in-service-publish-information-object"></a>サービス内公開情報オブジェクト

このオブジェクトは、下限と上限によって定義される配布の範囲を表します。 下限はドライバーが配布される最も古い Windows バージョンを示し、上限は最新バージョンを示します。 下限と上限を追加することによって、ドライバーの配布を制限できます。
```json
{
  "flooring": "RS1",
  "ceiling": "RS3",

}
```
このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|下限|string|このオプションは、示されているもの以降の Windows 10 オペレーティング システムに対してのみ、ドライバーを提供する場合に使用します。 たとえば、RS4 を下限として選択すると、Windows 10 1803 (RS4) 以降を実行しているシステムに対してのみ、このドライバーが提供されることを意味します。 設定可能な値は、次のとおりです。 <ul><li>TH</li><li>RS1</li><li>RS2</li><li>RS3</li><li>RS4</li><li>RS5</li><li>19H1</li></ul> 設定可能な値は、OS の最新バージョンを含むように拡張されることにご注意ください。 |
|ceiling|string|"*この機能へのアクセスは制限されています*"。 このオプションは、示されているもの以前のオペレーティング システムに対してのみドライバーを提供する場合に使用します。 たとえば、Windows 10 1607 RS1 認定ドライバーについて、RS3 を上限として選択すると、Windows 10 1803 (RS4) 以降を実行しているシステムにドライバーは提供されません。設定可能な値は、次のとおりです。 <ul><li>TH</li><li>RS1</li><li>RS2</li><li>RS3</li><li>RS4</li><li>RS5</li><li>19H1</li></ul> 設定可能な値は、OS の最新バージョンを含むように拡張されることにご注意ください。 |

これらの値について詳しくは、「[Limiting driver distribution by Windows versions (Windows のバージョンによるドライバーの配布の制限)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/limit-driver-distribution)」をご覧ください。

### <a name="co-engineering-driver-publish-information-object"></a>共同エンジニアリング ドライバー公開情報オブジェクト

このオブジェクトは、新しい未リリースのバージョンの Windows 用ドライバーを開発するときに、下限と上限によって定義された配布範囲を表します。 "*このオブジェクトは、Microsoft の共同エンジニアリング パートナーに対してのみ使用できます*"。 下限はドライバーが配布される最も古い Windows バージョンを示し、上限は最新バージョンを示します。 下限と上限を追加することによって、ドライバーの配布を制限できます。 
```json
{
  "flooringBuildNumber": 17135,
  "ceilingBuildNumber": 17139
}
```
このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
|flooringBuildNumber|number|ドライバーを提供する下限のリリースのビルド番号。 たとえば、下限を 10.1.17135 にする必要がある場合は、「17135」と入力する必要があります。 メジャー バージョン (10.1) は、常に既定で適切なバージョンに自動的に設定されます。|
|ceiling|number|ドライバーを提供する上限のリリースのビルド番号。 たとえば、上限を 10.1.17139 にする必要がある場合は、「17139」と入力する必要があります。 メジャー バージョン (10.1) は、常に既定で適切なバージョンに自動的に設定されます。|

詳しくは、「[Limiting driver distribution by Windows versions (Windows のバージョンによるドライバーの配布の制限)](https://docs.microsoft.com/windows-hardware/drivers/dashboard/limit-driver-distribution)」をご覧ください。

### <a name="shipping-label-workflow-status-object"></a>配送先住所ラベル ワークフロー状態オブジェクト

このオブジェクトは、特定のエンティティのワークフローの状態を表します。

```json
{
      "currentStep": "Created",
      "state": "completed",
      "messages": []
    }
```

このオブジェクトには、次の値があります

| 値 | 種類 | 説明 |
|:--|:--|:--|
| currentStep | string | このエンティティの全体的なワークフローにおける現在のステップの名前。 <br>Windows Update に対して公開される配送先住所ラベルの場合、使用可能な値は次のとおりです (かっこ内に説明があります)。<ul><li>Created ("*配送先住所ラベルを作成しています*")</li><li>PreProcessShippingLabel ("*ターゲット情報を検証しています*")</li><li>FinalizePreProcessing ("*前処理の後で適切な次のステップを呼び出しています*")</li><li>PublishJobValidation ("*パッケージの取り込み/申請が完了したかどうかを確認しています*")</li><li>UpdateGeneration ("*WU の公開の詳細を生成しています*")</li><li>MicrosoftApproval ("*プロモーション中/フライト中です*")</li><li>Publishing ("*WU に公開の詳細をプッシュしています*")</li><li>FinalizePublishing ("*公開プロセスを完了しています*")</li></ul> 他のパートナーと共有される配送先住所ラベルの場合、使用可能な値は次のとおりです (かっこ内に説明があります)。 <ul><li>Created ("*配送先住所ラベルを作成しています*")</li><li>PreProcessShippingLabel ("*ターゲット情報を検証しています*")</li><li>FinalizePreProcessing ("*前処理の後で適切な次のステップを呼び出しています*")</li><li>PublishJobValidation ("*パッケージの取り込み/申請が完了したかどうかを確認しています*")</li><li>ProcessSharing ("*受信者に対する共有の詳細を生成しています*")</li><li>FinalizeSharing ("*共有プロセスを完了しています*")</li></ul>|
| State | string | 現在のステップの状態。 設定可能な値は、次のとおりです。<ul><li>notStarted</li><li>started</li><li>失敗</li><li>完了</li></ul> |
| Messages | array | (特に障害発生時に) 現在のステップに関するメッセージを提供する文字列の配列 |

## <a name="error-codes"></a>エラー コード

エラー コードについて詳しくは、「[Error codes (エラー コード)](get-product-data.md#error-codes)」をご覧ください。

## <a name="see-also"></a>関連項目

- [ハードウェア ダッシュボード API のサンプル (GitHub)](https://aka.ms/hpc_async_api_samples)
