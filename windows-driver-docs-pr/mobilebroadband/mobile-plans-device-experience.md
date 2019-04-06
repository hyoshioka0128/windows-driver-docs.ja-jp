---
title: プランの Windows 10 のモバイル デバイス エクスペリエンス
description: このトピックではモバイルのプランをアクティブにした後、Windows デバイス エクスペリエンスについて説明します。
ms.assetid: E97AD441-86F7-439C-9800-7DD93AAC0545
keywords:
- デバイス エクスペリエンスの Windows Mobile の計画、携帯電話会社のモバイルの計画
ms.date: 03/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1f54fcbcdefaf32e22ed359c16acf1b74a571f81
ms.sourcegitcommit: 624427449978a8a82e77a3a31b9e22e3263793ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/05/2019
ms.locfileid: "59055723"
---
# <a name="mobile-plans-windows-10-device-experience"></a>プランの Windows 10 のモバイル デバイス エクスペリエンス

このトピックでは、その携帯電話会社にお客様のエクスペリエンスを確保する Mobile プラン プログラム提供は、通信事業者の内容と一致する機能について説明します。

## <a name="basic-device-experience"></a>基本的なデバイス エクスペリエンス

このセクションには、何を構成するオプションがについて説明します、*アカウントの表示*リンク Windows 接続マネージャーで、また既知と呼ばれることも、ネットワーク フライアウト表示します。

*アカウントの表示*リンクを設定します。

- Web ブラウザーを起動し、定義されている web ページを開きます。
- プランのモバイル アプリを起動し、モバイルのプランの Web ポータルを開きます。

 これらのオプションのいずれかを決めたら、適切な動作を実装する COSA データベースの更新を要求してください。 詳細については、「[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。

上記のオプションについては、次の設定が適用されます。

- *AccountExperienceURL*します。 このパラメーターは、web ページを定義します。
- *AppID*します。 このパラメーターは、どのアプリが起動されるを定義します。 プランのモバイル アプリを使用する構成_Microsoft.OneConnect_8wekyb3d8bbwe!アプリ_します。

次の図は、ネットワーク ポップアップの例を示します。

<img src="images/mobile_plans_network_flyout_basic.png" alt="Windows Connection Manager showing basic MO" title="基本の月を示す Windows 接続マネージャー" width="250" />

## <a name="enhanced-device-experience"></a>強化されたデバイス エクスペリエンス

強化されたデバイス エクスペリエンスを実装すると、これらのメリットを顧客に提供できます。

- データの量がある顧客を表示し、ネットワーク ポップアップで、そのサブスクリプションの有効期限までの残りの期間。
- お客様は、プリペイド残高外で実行される場合や、サブスクリプションの有効期限が切れた場合でも、モバイル接続は、上の前払いサブスクリプションを上位ことができます。
- お客様のサブスクリプションの状態に基づくネットワーク フライアウト オファリングを管理できます。

上にこれらのエクスペリエンスを構築、[基本的なデバイス エクスペリエンス](#basic-device-experience)デバイスのネットワークのフライアウトで既定のエクスペリエンスであります。

### <a name="network-flyout-user-experience"></a>ネットワーク ポップアップのユーザー エクスペリエンス

受信する情報に応じて`GetBalance`API 呼び出しでは、ネットワーク ポップアップとは異なる動作、ユーザー エクスペリエンスが向上します。

ネットワーク ポップアップには、次の要素があります。

1. データ プランで接続します。 これは、プランのモバイル アプリを起動します。
2. 自分のアカウントを表示します。 動作に基づいて、[基本的なデバイス エクスペリエンス](#basic-device-experience)します。
3. 情報のバランスを取ります。 分散の使用可能なで提供されるを示しています、`GetBalance`応答します。

次の図は、これらのネットワーク フライアウト要素を示します。 データ接続 A で対応するプラン、B と自分のアカウントをビューの対応、および残高の情報が C. に対応

<img src="images/dynamo_prepaid_network_flyout_5_getbalance.png" alt="Windows Connection Manager showing behavior depending on GetBalance API calls" title="GetBalance API 呼び出しによって動作を示す Windows 接続マネージャー" width="600" />

MOs を提供するネットワーク ポップアップで、適切な情報を提供する*型*と*残高*(dataRemainingMB および timeRemaining) 情報で定義されている、 [GetBalance API](#getbalance-api)セクション。

次の表に、間の参照を`GetBalance`応答の種類と、ネットワーク ポップアップに表示される内容です。

| GetBalance 応答の種類 | ネットワーク ポップアップを表示しています. |
| --- | --- |
| MODIRECT | 残高情報なしでのみ「アカウントの表示」 |
| MODIRECTPAYG | 「自分のアカウントの表示」し、情報のバランスを取る |
| なし | 「データ プランで接続」 |
| NOTSUPPORTED | 「自分のアカウントの表示」のみ |

## <a name="getbalance-api"></a>GetBalance API

> [!IMPORTANT]
> 要求してください、[残高の取得を有効にする更新プログラムを Windows COSA](#how-to-enable-get-balance-in-windows-cosa) Windows でします。

`GetBalance` API は、現在のサブスクリプションの状態、Mobile のプランが発生するかどうかは、デバイスで、使用可能なコントロールのクエリを実行し、前払いサブスクリプションのネットワークのフライアウトで残りのデータと時刻を示します。 次の図は、高度なフローを`GetBalance`API。

<img src="images/mobile_plans_get_balance_api_flow.png" alt="GetBalance API flow" title="GetBalance API フロー" width="600" />

### <a name="resource-model"></a>リソース モデル

プランのモバイル サービスと月のサービス間の通信では、次の図内のリソースを操作する必要があります。 次の図は、テーブルは各リソースの説明です。

<img src="images/mobile_plans_get_balance_resource.png" alt="GetBalance API resource model diagram" title="GetBalance API リソース モデルのダイアグラム" width="600" />

#### <a name="sim-resource"></a>SIM のリソース

> [!NOTE]
> SIM リソースは現在サポートされていません「作成」、「読み取り」、"update"または「削除」操作。

| JSON のプロパティ | 種類 | 説明 |
| --- | --- | --- |
| Iccid | String | 作成されたプロファイルの ICCID します。 |

#### <a name="balance-resource"></a>分散リソース

| JSON のプロパティ | 種類 | 説明 |
| --- | --- | --- |
|id |String| トランザクションを追跡するために、携帯電話会社の内部 id |
種類 | 列挙型 | 設定可能な値: <ul><li>MODIRECT:ユーザーの残高が直接 MO かどうかを示します。</li><li>MODIRECTPAYG:ユーザーの残高が直接 PAYG の月を示します。</li><li>NONE:ユーザーには、残高がないことを示します。 残高が 0、プランの有効期限が切れていない場合は、ユーザーがデータ プランを購入できるように、"NONE"を受信する予定です。</li><li>NOTSUPPORTED:SIM は、モバイルのプランでサポートされていないことを示しますが発生します。 SIM にされない場合、"NOTSUPPORTED"が使用される、* Mobile プラン、サポートされている範囲です。 ネットワーク ポップアップでプランのモバイル エクスペリエンスをオフにされ、この型を受信すると、プランのモバイル アプリで一般的なエラー メッセージを返すことが。</li></ul> |
| dataRemainingInMB | Double | MB で、現在のユーザー プランでは残りのデータ。 |
| TimeRemaining | String | 指定した期間[ISO 8601](https://go.microsoft.com/fwlink/p/?linkid=866182)します。 |

### <a name="headers"></a>ヘッダー

モバイル プロバイダのエンドポイントに対するプランのモバイル サービスからのすべての要求では、次のヘッダーを含めることができます。

| ヘッダー名 | Value | 説明 |
| --- | --- | --- |
| X-MS-DM-TransactionId | String | プランのモバイル サービスと月のサービスの間には、この要求/応答操作を一意に識別する TransactionId します。 |
| (省略可能) の承認 | String | 必要に応じて、売り上げによって提供される基本認証文字列 |

### <a name="error-codes"></a>エラー コード

次の表は、HTTP 応答で使用する必要があるエラー コードを定義します。

| エラー コード | 説明 |
| --- | --- |
| HTTP 200 (OK) | 操作が完了しました。 このコードを行う必要がある、指定した場所にユーザーの 0 の残高を示すためにも使用する必要があります dataRemainingInMB を使用して = 0 および timeRemaining HTTP 200 では"PT0S"を = です。 |
  HTTP 201 (Created) | 正常に完了した操作とリソースが正常に作成されたことを示します。 |
| HTTP 400 (Bad Request) | 使用すると、無効なクエリ パラメーター、無効なヘッダーまたはペイロードが無効です。 応答本文でが正しくないパラメーターを指定する必要があります。 たとえば、無効な fieldsTemplate が指定されている場合、このエラー コードを応答本文で詳細を返す必要があります。 |
| HTTP 401 (未承認) | 認証の資格情報は、正しくないか、無効でした。 これは、渡される基本認証資格情報が正しくない場合に発生します。 |
| HTTP 403 (禁止) | クライアント証明書は、信頼されていないか、無効です。 MTLS の一部として含まれているクライアント証明書が有効でない場合は HTTP 403 が返されます。 |
| HTTP 404 (Not Found) | 月のサービスは、リソースが存在しない場合、このエラーを返す必要があります。 これは、正しくない ICCID が送信されるときに発生します。 これは、ユーザーが示されている HTTP 200 (OK) で指定された場所にバランスを持っていないことを示すために使用されませんする必要があります。 |
| HTTP 409 (Conflict) | TransactionId が繰り返し発生する場合に使用されます。 |
| HTTP 429 (Too 多数の要求) | プランのモバイル サービスが、一定の時間内で要求が多すぎるを送信しているかを示す、MO サービスで使用します。 応答には、月のサービスは、リソースの後、プランのモバイル サービスを再試行する時間を示す Retry-after 後ヘッダーを使用する必要があります。 応答本文では、省略可能な詳細を提供することができます。 |
| HTTP 500 (内部エラー) | 月のサービスで予期しない問題が発生しました。 月のサービスは、必要に応じてさらにデバッグのために使用できるように、可能であればエラーの原因を含める必要があります。 |

### <a name="getbalance-api-specification"></a>GetBalance API 仕様

`GetBalance` Windows デバイスでネットワークのフライアウトが表示されたら、API が呼び出されます。 プランのモバイル サービスは、この通信にプロキシです。

この呼び出しは、HTTP 要求で行われます、 *moBaseUrl* MO でホストされるサービスのエンドポイントと*sim id* ICCID は。

```HTTP
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US HTTP/1.1
```

クエリ パラメーター:

| クエリ パラメーター名 | Value | 説明 |
| --- | --- | --- |
| location | String | (省略可能)。 ユーザーの残高が照会されている場所です。 指定しない場合、すべてのアクティブな残高が必要です。 **注**location パラメーターは大文字小文字を区別します。 |
| limit | 整数型 |(省略可能)。 返される残高の最大数。 指定しない場合、すべての残高が返されます。 |
| fieldsTemplate | 列挙型 |リソースで返す必要があるフィールドの一覧を指定します。 <p>設定可能な値:</p><ul><li>Basic:*型*、 *dataRemainingInMB*、および*timeRemaining*残高にリソースを返す必要があります。</li><li>完全な。分散リソースのすべてのプロパティは返される必要があります。</li></ul> |

次の一連の例の通話フローを表示する、 `GetBalance` API。

#### <a name="example-1-returning-the-first-balance-that-is-available-for-the-user-in-us"></a>例 1:米国内のユーザーに使用される最初のバランスを返す

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

成功した場合、このメソッドは、ユーザーの分散を返します。

JSON の応答:

| データ | 種類 | 説明 |
| --- | --- | --- |
| 残高 | コレクション | 残高のコレクション。 |

#### <a name="example-2-the-expected-response-for-a-sim-that-is-in-the-cosa-iccid-range-but-should-not-be-supported-by-mobile-plans"></a>例 2:COSA ICCID 範囲でもモバイル プランではサポートされていない必要があります SIM の想定される応答

HTTP 要求:

```html
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US
HTTP/1.1
```

JSON の応答:

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

プランのモバイル サービスと通信事業者サービス間の通信は、相互トランスポート層セキュリティ (MTLS) を使用して認証する必要があります。 Microsoft を使用して、要求元をその id を検証するための証明書を提供します。 **moBaseUrl**します。

Microsoft では、オンボード プロセス中に、証明書を提供します。

### <a name="how-to-enable-get-balance-in-windows-cosa"></a>Windows COSA での分散の取得を有効にする方法

Windows デバイスでバランスの取得のサポートを有効にする Windows COSA database で、次の設定を構成することが必要です。

次の COSA 設定が必要です。

- SupportDataMarketplace ("Yes"に設定する必要があります)
- DataMarketplaceRoamingUIEnabled
- SIM ICCID 範囲 (開始と ICCID 範囲 – ICCID 範囲の終了)

サポートされているすべてのフィールドの詳細については、デスクトップ COSA 専用の設定を参照してください。[デスクトップ COSA/APN データベースの設定](desktop-cosa-apn-database-settings.md)します。

COSA/APN の更新プログラムのスプレッドシートをダウンロードするには、次のようにクリックします。[ここ](https://go.microsoft.com/fwlink/p/?linkid=851213)します。

## <a name="walled-garden"></a>高いガーデン

*ウォール ガーデン*データ外で実行されるときに、お客様をサポートするキーです。 Wi-fi などの別のインターネット接続がない場合でも、MO 直接ポータルに到達することができます。 これは、コンシューマーは追加のデータ プランを購入し、サブスクリプションの管理を有効になります。

> [!NOTE]
> Mobile のプランのアーキテクチャは、Walled Garden エンドポイントの IP 範囲をサポートしていません。 ホスト名は、ホワイト リスト登録のために使用する必要があります。

月の直接の web ポータルと`GetBalance`API エンドポイントはこの Walled Garden の一部にもあります。

### <a name="walled-garden-endpoints"></a>高いガーデン エンドポイント

エンドユーザーがアクセス可能な常に必要なエンドポイントの数が少ないがあります。 次の表では、Walled Garden の必要なエンドポイントを定義します。

| URL | HTTP/HTTPS |
| --- | --- |
| service.datamart.windows<span></span>.com | https |
| dogfood.datamart.windows<span></span>.com | https |
| windows.policies.live<span></span>.net | https |
| ctldl.windowsupdate<span></span>.com | http |
| cdp1.public 信頼<span></span>.com | http |
| ocsp.omniroot<span></span>.com | http |
| vassg142.ocsp.omniroot<span></span>.com | http |
| vassg142.crl.omniroot<span></span>.com | http |
| mscrl.microsoft<span></span>.com | http |
| crl.microsoft<span></span>.com | http |
| www.msftconnecttest<span></span>.com | http |
| crl3.digicert<span></span>.com | http |
| Ocsp.digicert<span></span>.com | http |
| login.live<span></span>.com | http と https |
| storagetos.datamart.windows<span></span>.com | http と https |
| mps.datamart.windows<span></span>.com | http と https |
| mps-service.datamart.windows<span></span>.com | http と https |
| staging.datamart.windows<span></span>.com | http と https |
| mps-staging.datamart.windows<span></span>.com | http と https |