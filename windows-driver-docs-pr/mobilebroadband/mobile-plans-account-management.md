---
title: モバイルプランアカウントの管理
description: このトピックでは、モバイルプランでの Windows アカウント管理エクスペリエンスについて説明します。
ms.assetid: E97AD441-86F7-439C-9800-7DD93AAC0545
keywords:
- Windows Mobile プランのアカウント管理、モバイルプランのモバイルオペレーター
ms.date: 03/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2682d58e6b246ad9ff142094c8e078e123a5a733
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242741"
---
# <a name="mobile-operator-account-management-in-windows-10"></a>Windows 10 での携帯電話会社アカウント管理

このトピックでは、Windows によって提供される携帯電話会社アカウント管理エクスペリエンスについて説明します。これは、モバイルプランで拡張できます。

## <a name="basic-account-management-experience"></a>基本的なアカウント管理エクスペリエンス

このセクションでは、 *[アカウントの表示*] リンクが Windows 接続マネージャーに表示する内容を構成するオプションについて説明します。これは、ネットワークフライアウトとも呼ばれます。

*[アカウントの表示*] リンクは次のように構成できます。

- Web ブラウザーを起動して、定義された web ページを開きます。
- モバイルプランアプリを起動し、携帯電話会社の web ポータルを開きます。

 これらのオプションのいずれかを決定したら、適切な動作を実装するために、COSA データベースの更新を依頼してください。 詳細については、「[デスクトップ COSA/APN データベースの送信を計画する](planning-your-desktop-cosa-apn-database-submission.md)」を参照してください。

上記のオプションには、次の設定が適用されます。

- *AccountExperienceURL*。 このパラメーターは、web ページを定義します。
- *AppID*。 このパラメーターは、どのアプリを起動するかを定義します。 モバイルプランアプリを使用するには、 _Microsoft OneConnect_8wekyb3d8bbwe を構成します。アプリ_。

次の図は、ネットワークのフライアウトの例を示しています。

<img src="images/mobile_plans_network_flyout_basic.png" alt="Windows Connection Manager showing basic MO" title="基本的な MO を示す Windows 接続マネージャー" width="250" />

## <a name="enhanced-account-management-experience"></a>強化されたアカウント管理エクスペリエンス

強化されたアカウント管理エクスペリエンスを実装することで、これらの特典を顧客に提供できます。

- ネットワークのフライアウトで、利用可能なデータの量とサブスクリプションの有効期限が切れるまでの残り時間を確認できます。
- 前払いの残高が不足している場合や、サブスクリプションの有効期限が切れている場合でも、お客様は、モバイル接続経由で前払いサブスクリプションを最上位に設定できます。
- お客様のサブスクリプションの状態に基づいて、ネットワークのフライアウトサービスを管理できます。

これらのエクスペリエンスは、[基本的なアカウント管理エクスペリエンス](#basic-account-management-experience)の上に構築されます。これは、デバイスネットワークのフライアウトの既定のエクスペリエンスです。

### <a name="network-flyout-user-experience"></a>ネットワークフライアウトのユーザーエクスペリエンス

`GetBalance` API 呼び出しから受信した情報によっては、ネットワークのフライアウトの動作が異なり、ユーザーエクスペリエンスが向上します。

ネットワークフライアウトには、次の要素があります。

1. データプランを使用して接続します。 これにより、モバイルプランアプリが起動します。
2. 自分のアカウントを表示します。 [基本的なアカウント管理エクスペリエンス](#basic-account-management-experience)に基づいて動作します。
3. 残高情報。 `GetBalance` の応答で提供される使用可能な残高を示します。

次の図は、これらのネットワークフライアウト要素を示しています。 データプランを使用した接続は、に対応します。 [アカウントの表示] は B と対応し、残高情報は C と対応しています。

<img src="images/dynamo_prepaid_network_flyout_5_getbalance.png" alt="Windows Connection Manager showing behavior depending on GetBalance API calls" title="GetBalance API 呼び出しに応じて動作を示す Windows 接続マネージャー" width="600" />

ネットワークのフライアウトに適切な情報を提供するために、MOs は[Getbalance API](#getbalance-api)セクションで定義されているように、*型*と*バランス*(dataRemainingMB および timeRemaining) の情報を提供します。

次の表に、`GetBalance` 応答の種類と、ネットワークのフライアウトに表示される内容との間の参照を示します。

| GetBalance 応答の種類 | ネットワークフライアウトの表示... |
| --- | --- |
| MODIRECT | "自分のアカウントを表示する" は、残高情報がありません |
| MODIRECTPAYG | "アカウントの表示" と残高の情報 |
| なし | "データプランを使用して接続する" |
| NOTSUPPORTED | "自分のアカウントを表示する" のみ |

## <a name="getbalance-api"></a>GetBalance API

> [!IMPORTANT]
> Windows で[残高を取得できるようにするには、windows COSA の更新プログラム](#how-to-enable-get-balance-in-windows-cosa)を要求してください。

`GetBalance` API は、現在のサブスクリプションの状態を照会し、モバイルプランのエクスペリエンスがデバイスで利用可能かどうかを制御し、前払いサブスクリプションのネットワークのフライアウトで残りのデータと時間を表示します。 次の図は、`GetBalance` API の高レベルのフローを示しています。

<img src="images/mobile_plans_get_balance_api_flow.png" alt="GetBalance API flow" title="GetBalance API フロー" width="600" />

### <a name="resource-model"></a>リソースモデル

モバイルプランサービスとモバイルオペレーター API の間の通信には、次の図のリソースの操作が含まれます。 各リソースの説明は、図の後の表に記載されています。

<img src="images/mobile_plans_get_balance_resource.png" alt="GetBalance API resource model diagram" title="GetBalance API リソースモデルの図" width="600" />

#### <a name="sim-resource"></a>SIM リソース

> [!NOTE]
> SIM リソースでは、現在、"作成"、"読み取り"、"更新"、"削除" の各操作はサポートされていません。

| JSON プロパティ | 種類 | 説明 |
| --- | --- | --- |
| Iccid | String | 作成されたプロファイルの ICCID。 |

#### <a name="balance-resource"></a>リソースのバランスを取る

| JSON プロパティ | 種類 | 説明 |
| --- | --- | --- |
|id |String| トランザクションを追跡するための携帯電話会社の内部 id |
種類 | Enum | 次の値を使用できます。 <ul><li>MODIRECT: ユーザーのバランスが MO ダイレクトかどうかを示します。</li><li>MODIRECTPAYG: ユーザーのバランスが MO ダイレクト PAYG かどうかを示します。</li><li>NONE: ユーザーに残高がないことを示します。 残りの残高が0でも、プランの有効期限が切れていない場合は、ユーザーがデータプランを購入できるように "NONE" を受け取ることになります。</li><li>NOTSUPPORTED: SIM がモバイルプランのエクスペリエンスでサポートされていないことを示します。 "NOTSUPPORTED" は、SIM が * モバイルプランでサポートされている範囲内にない場合に使用されます。 ここでは、ネットワークフライアウトのモバイルプランのエクスペリエンスを無効にして、この種類の受信時にモバイルプランアプリで一般的なエラーメッセージを返します。</li></ul> |
| dataRemainingInMB | Double | 現在のユーザープランの残りのデータ (MB 単位)。 |
| timeRemaining | String | [ISO 8601](https://go.microsoft.com/fwlink/p/?linkid=866182)で指定された期間。 |

### <a name="headers"></a>ヘッダー

次のヘッダーは、モバイルプランサービスからモバイルプロバイダーのエンドポイントへのすべての要求に含まれる場合があります。

| ヘッダー名 | 値 | 説明 |
| --- | --- | --- |
| X-y-TransactionId | String | Mobile plan サービスと MO サービス間のこの要求/応答の相互作用を一意に識別する TransactionId。 |
| 承認 (省略可能) | String | オプションで、MO によって提供される基本認証文字列。 |

### <a name="error-codes"></a>エラー コード

次の表は、HTTP 応答で使用する必要があるエラーコードを定義しています。

| エラー コード | 説明 |
| --- | --- |
| HTTP 200 (OK) | 操作は正常に完了しました。 このコードは、ユーザーが指定した場所で残高が0であるかどうかを示すためにも使用します。これは、HTTP 200 で dataRemainingInMB = 0 と timeRemaining = "PT0S です" を使用して行う必要があります。 |
  HTTP 201 (作成済み) | 操作が正常に完了し、リソースが正常に作成されたことを示します。 |
| HTTP 400 (無効な要求) | 無効なクエリパラメーター、無効なヘッダー、または無効なペイロードに対して使用されています。 応答本文で、正しくないパラメーターを指定する必要があります。 たとえば、無効な fieldsTemplate が指定されている場合、このエラーコードは応答本文の詳細と共に返される必要があります。 |
| HTTP 401 (承認されていません) | 認証資格情報が正しくないか、無効でした。 これは、渡された基本認証資格情報が正しくない場合に発生する可能性があります。 |
| HTTP 403 (許可されていません) | クライアント証明書が信頼されていないか、無効です。 MTLS の一部として含まれているクライアント証明書が無効な場合は、HTTP 403 が返されます。 |
| HTTP 404 (見つかりません) | MO サービスは、リソースが存在しない場合にこのエラーを返します。 これは、正しくない ICCID が送信されたときに発生する可能性があります。 これは、指定された場所にユーザーが残高を持たないことを示すためには使用しないでください。これは、HTTP 200 (OK) で示されます。 |
| HTTP 409 (競合) | TransactionId が繰り返される場合に使用されます。 |
| HTTP 429 (要求が多すぎます) | Mobile plan サービスが、指定された時間内に過剰な要求を送信していることを示すために、MO サービスによって使用されます。 応答では、MO サービスは再試行後のヘッダーを使用して、モバイルプランサービスがリソースを再試行するまでの時間を示す必要があります。 応答本文では、オプションの詳細を指定できます。 |
| HTTP 500 (内部エラー) | MO サービスで予期しない問題が発生しました。 必要に応じてさらにデバッグするために使用できるように、MO サービスには、可能な限りエラーの原因が含まれている必要があります。 |

### <a name="getbalance-api-specification"></a>GetBalance API 仕様

`GetBalance` API は、Windows デバイスにネットワークフライアウトが表示されたときに呼び出されます。 Mobile plan サービスは、この通信のプロキシです。

この呼び出しは、HTTP 要求を使用して行われます。 *Mobaseurl*は、MO でホストされるサービスのエンドポイントであり、 *SIM id*は ICCID です。

```HTTP
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US HTTP/1.1
```

クエリパラメーター:

| クエリパラメーター名 | 値 | 説明 |
| --- | --- | --- |
| 位置 | String | 省略可。 ユーザーのバランスがクエリされる場所。 指定しない場合は、すべてのアクティブな残高が想定されます。 **メモ**Location パラメーターでは、大文字と小文字が区別されます。 |
| limit | 整数型 |省略可。 返される残高の最大数。 指定しない場合は、すべての残高が返されます。 |
| fieldsTemplate | Enum |リソースで返される必要があるフィールドのリストを指定します。 <p>次の値を使用できます。</p><ul><li>基本: Balance リソースの*type*、 *DataRemainingInMB*、および*timeRemaining*が返される必要があります。</li><li>Full: 残高リソースのすべてのプロパティを返す必要があります。</li></ul> |

次の一連の例は、`GetBalance` API の呼び出しフローを示しています。

#### <a name="example-1-returning-the-first-balance-that-is-available-for-the-user-in-us"></a>例 1: 米国でユーザーに対して使用可能な最初の残高を取得する

```HTTP
GET https://moendpoint.com/v1/sims/iccid: 8988247000100003319/balances?fieldsTemplate=basic&limit=1&location=us HTTP/1.1
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”
```

HTTP 応答:

```HTTP
HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: “12345”

{
“balances”: [
    {
         “id”: “23445”,
         “type”: “MODIRECTPAYG”,
         “dataRemaininginMB”: 123.0,
         “timeRemaining”: “P23DT23H”
    }
  ]
}
```

成功した場合、このメソッドはユーザーの残高を返します。

応答 JSON:

| Data | 種類 | 説明 |
| --- | --- | --- |
| 残高 | [コレクション] | 残高のコレクション。 |

#### <a name="example-2-the-expected-response-for-a-sim-that-is-in-the-cosa-iccid-range-but-should-not-be-supported-by-mobile-plans"></a>例 2: COSA ICCID 範囲に含まれているが、モバイルプランではサポートされていない SIM に対する予期される応答

HTTP 要求:

```html
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US
HTTP/1.1
```

応答 JSON:

```json
HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: “12345”

{
“balances”: [
    {
         “id”: “23445”,
         “type”: “NOTSUPPORTED”,
         “dataRemaininginMB”: 0.0,
         “timeRemaining”: “PT0S”
    }
  ]
}
```

### <a name="authentication"></a>認証

モバイルプランサービスとモバイルオペレーター API の間の通信は、相互トランスポート層セキュリティ (MTLS) を使用して認証される必要があります。 Microsoft は、要求元の id を**Mobaseurl**に検証するために使用する証明書を提供します。

Microsoft は、オンボードプロセス中に証明書を提供します。

### <a name="how-to-enable-get-balance-in-windows-cosa"></a>Windows COSA での残高の取得を有効にする方法

Windows デバイスでの [残高のサポート] を有効にするには、Windows COSA データベースで次の設定を構成する必要があります。

次の COSA 設定が必要です。

- SupportDataMarketplace ("Yes" に設定する必要があります)
- DataMarketplaceRoamingUIEnabled
- SIM ICCID range (ICCID Range – Start and ICCID Range – End)

サポートされているすべてのフィールドの詳細については、desktop cosa [/APN データベース設定](desktop-cosa-apn-database-settings.md)のデスクトップ cosa のみの設定に関する情報を参照してください。

COSA/APN 更新プログラムのスプレッドシートをダウンロードするには、[ここ](https://go.microsoft.com/fwlink/p/?linkid=851213)をクリックしてください。
