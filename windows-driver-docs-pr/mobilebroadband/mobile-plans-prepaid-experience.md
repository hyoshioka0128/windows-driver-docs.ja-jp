---
title: 前払いエクスペリエンスを Mobile の計画
description: このトピックでは、Mobile プラン プログラムのオプションのプリペイド エクスペリエンスについて説明します。
ms.assetid: 908AB4DE-A4C8-4758-9632-F7F7381FF737
keywords:
- Windows Mobile のプランを一括払いエクスペリエンスで、モバイル オペレーターが発生する Mobile プランの前払い
ms.date: 09/17/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 6f2e01b588a14eac4d9d17a59eff8811a91261d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550191"
---
# <a name="mobile-plans-prepaid-experience"></a>前払いエクスペリエンスを Mobile の計画

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

モバイル オペレーター用オプションが強化された前払いエクスペリエンスのサポートを有効にするモバイルのプランを持つオンボードしました。 このトピックでは、その他のトピックでは、このセクションでは、プリペイドのシナリオを点灯するために必要な相違点に重点を置くことで説明されているプライマリ後払いエクスペリエンスに増分の変更について説明します。 

## <a name="overview"></a>概要

プリペイドのエクスペリエンスを実装すると、ユーザーにこれらのメリットを提供することができます。

- データの量は、使用可能なコンシューマーを表示し、ネットワーク ポップアップで、そのサブスクリプションの有効期限までの残りの期間。
- コンシューマーは、プリペイド残高外で実行される場合や、サブスクリプションの有効期限が切れた場合でも、モバイル接続は、上の前払いサブスクリプションを上位ことができます。
- コンシューマーのサブスクリプションの状態に基づくネットワーク フライアウト オファリングを管理することができます。

一括払いを実装する、これらの手順に従います。

1. Windows COSA データベースを更新します。
2. Get 残高 API を実装します。
3. 高い庭を実装します。
4. Get 残高 API と高い庭を検証します。
5. API の負荷要件に準拠します。

## <a name="update-windows-cosa-database"></a>Windows COSA データベースの更新

Windows 接続マネージャーで、ネットワーク ポップアップとも呼ばれる、エクスペリエンスが示すように正しく Mobile プランを確実には、まず Windows COSA データベースを更新する必要があります。

> [!TIP]
> Windows デバイスで COSA を更新して、かなりの時間のかかる、ため、この要求をできるだけ早く送信する必要がありますが、プロジェクト制約になる可能性があります。

<img src="images/dynamo_prepaid_network_flyout_1_general.png" alt="Windows Connection Manager general example" title="Windows 接続マネージャーの一般的な例" width="250" />

COSA を更新した後の順にタップまたはクリックすると、ネットワーク ポップアップで、接続を使用すると (次の図では、「Contoso 携帯」と表示) オプションを含む展開されます。 ユーザーが携帯ネットワーク接続を展開ときに [データ プランでの接続] オプションが表示されます。 タップまたはクリックすると、このオプションでは、プランのモバイル アプリが起動します。

<img src="images/dynamo_prepaid_network_flyout_2_connect.png" alt="Windows Connection Manager showing Connect with Data Plan option" title="Windows 接続マネージャーがデータ プランのオプションを使用して接続を表示しています。" width="250" />

次の図は、ユーザーがデータと時刻の残りの前払いサブスクリプションでの量を表示する方法の例を示します。

<img src="images/dynamo_prepaid_network_flyout_3_balance.png" alt="Windows Connection Manager showing remaining time and data" title="Windows 接続マネージャーの残りの時間とデータの表示" width="250" />

### <a name="how-to-request-a-cosa-database-update"></a>COSA データベースの更新を要求する方法

COSA データベースの送信プロセスについては、次を参照してください。[計画デスクトップ COSA/APN データベース提出](planning-your-desktop-cosa-apn-database-submission.md)します。 

### <a name="cosa-database-settings-details"></a>COSA データベース設定の詳細

このセクションでは、COSA のどの設定はモバイルのプランをオンボーディングするために必要なおよび推奨されるについて説明します。

サポートされているすべてのフィールドの詳細については、デスクトップ COSA 専用の設定を参照してください。[デスクトップ COSA/APN データベースの設定](desktop-cosa-apn-database-settings.md)します。

COSA/APN の更新プログラムのスプレッドシートをダウンロードするには、次のようにクリックします。[ここ](https://go.microsoft.com/fwlink/p/?linkid=851213)します。

次の COSA 設定が必要です。

- SupportDataMarketplace ("Yes"に設定する必要があります)
- DataMarketplaceRoamingUIEnabled
- SIM ICCID 範囲 (開始と ICCID 範囲 – ICCID 範囲の終了)

特定のビジネス ニーズの適用によって、次の設定があります。

- AccountExperienceURL
- BrandingName
- BrandingIcon (スプレッドシートのアイコンを指定する必要があります)
- UseBrandingNameOnRoaming

次の図は、ネットワーク ポップアップでブランド MO 例を示します。

<img src="images/dynamo_prepaid_network_flyout_4_branding.png" alt="Windows Connection Manager showing MO branding" title="月のブランド化を示す Windows 接続マネージャー" width="250" />

## <a name="get-balance-api"></a>API の残高を取得します。

バランスの取得 API クエリ現在サブスクリプションの状態をコントロール Mobile プランが発生するかどうか、デバイスを使用できると、前払いサブスクリプションのネットワークのフライアウトで残りのデータと時刻を示します。 次の図は、バランスの取得 API のおおまかなフローを示します。 

<img src="images/dynamo_prepaid_get_balance_api_flow.png" alt="Get Balance API flow" title="分散 API フローを取得します。" width="600" />

### <a name="resource-model"></a>リソース モデル

プランのモバイル サービスと月のサービス間の通信では、次の図内のリソースを操作する必要があります。 次の図は、テーブルは各リソースの説明です。

<img src="images/dynamo_prepaid_get_balance_api_resource_model.png" alt="Get Balance API resource model diagram" title="分散 API リソース モデル図を取得します。" width="600" />

#### <a name="sim-resource"></a>SIM のリソース

> [!NOTE]
> SIM リソースは現在サポートされていません「作成」、「読み取り」、"update"または「削除」操作。

| JSON のプロパティ | 種類 | 説明 |
| --- | --- | --- |
| activationCode | String | アクティブ化コードを以下に、クライアントは、ダウンロードして、プロファイルをアクティブ化を使用できます。 |
| Iccid | String | 作成されたプロファイルの ICCID します。 |
| eId | String | Esim 状の eId します。 |

#### <a name="balance-resource"></a>分散リソース

| JSON のプロパティ | 種類 | 説明 |
| --- | --- | --- |
| 種類 | 列挙型 | 設定可能な値: <ul><li>MODIRECT:ユーザーの残高が直接 MO かどうかを示します。</li><li>MODIRECTPAYG:ユーザーの残高が直接 PAYG の月を示します。</li><li>NONE:ユーザーには、残高がないことを示します。 残高が 0、プランの有効期限が切れていない場合は、ユーザーがデータ プランを購入できるように、"NONE"を受信する予定です。</li><li>NOTSUPPORTED:SIM は、モバイルのプランでサポートされていないことを示しますが発生します。 "NOTSUPPORTED"は、SIM が Mobile プラン、サポートされている範囲にされないときに使用されます。 ネットワーク ポップアップでプランのモバイル エクスペリエンスをオフにされ、この型を受信すると、プランのモバイル アプリで一般的なエラー メッセージを返すことが。</li></ul> |
| dataRemainingInMB | Double | MB で、現在のユーザー プランでは残りのデータ。 |
| TimeRemaining | String | 指定した期間[ISO 8601](https://go.microsoft.com/fwlink/p/?linkid=866182)します。 |
| 場所 | 文字列のコレクション | 2 つの文字の ISO コード内の場所の配列。 これは、移動体通信ネットワーク接続がない場合に MCC または IP の逆引き参照から。 |

### <a name="headers"></a>ヘッダー

Mobile プロバイダーのエンドポイントに対するプランのモバイル サービスのすべての要求では、次のヘッダーを含めることができます。

| ヘッダー名 | Value | 説明 |
| --- | --- | --- |
| X-MS-DM-TransactionId | String | プランのモバイル サービスと月のサービスの間には、この要求/応答操作を一意に識別する TransactionId します。 |
| (省略可能) の承認 | String | 必要に応じて、売り上げによって提供される基本認証文字列 |

### <a name="error-codes"></a>エラー コード

| エラー コード | 説明 |
| --- | --- |
| HTTP 200 (OK) | 操作が完了しました。 このコードを行う必要がある、指定した場所にユーザーの 0 の残高を示すためにも使用する必要があります dataRemainingInMB を使用して = 0 および timeRemaining HTTP 200 では"PT0S"を = です。 |
  HTTP 201 (Created) | 正常に完了した操作とリソースが正常に作成されたことを示します。 |
| HTTP 400 (Bad Request) | 無効なため、無効なクエリ パラメーター、無効なヘッダーまたはペイロードが無効です。 応答本文でが正しくないパラメーターを指定する必要があります。 たとえば、無効な fieldsTemplate が指定されている場合、このエラー コードを応答本文で詳細を返す必要があります。 |
| HTTP 401 (未承認) | 認証の資格情報は、正しくないか、無効でした。 これは、渡される基本認証資格情報が正しくない場合に発生します。 |
| HTTP 403 (禁止) | クライアント証明書は、信頼されていないか、無効です。 MTLS の一部として含まれているクライアント証明書が有効でない場合は HTTP 403 が返されます。 |
| HTTP 404 (Not Found) | 月のサービスは、リソースが存在しない場合、このエラーを返す必要があります。 これは、正しくない ICCID が送信されるときに発生します。 これは、ユーザーが示されている HTTP 200 (OK) で指定された場所にバランスを持っていないことを示すために使用されませんする必要があります。 |
| HTTP 409 (Conflict) | TransactionId が繰り返し発生する場合に使用されます。 |
| HTTP 429 (Too 多数の要求) | プランのモバイル サービスが、一定の時間内で要求が多すぎるを送信しているかを示す、MO サービスで使用します。 応答には、月のサービスは、リソースの後、プランのモバイル サービスを再試行する時間を示す Retry-after 後ヘッダーを使用する必要があります。 応答本文では、省略可能な詳細を提供することができます。 |
| HTTP 500 (内部エラー) | 月のサービスで予期しない問題が発生しました。 月のサービスは、必要に応じてさらにデバッグのために使用できるように、可能であればエラーの原因を含める必要があります。 |

### <a name="get-balance-api-specification"></a>分散 API 仕様を取得します。

Mobile のプランのうち最も重要なこと、現在の残高に基づく新しいプランを購入するユーザーを許可する必要がありますを決定 Mobile プランは、いくつかの理由から、サブスクリプションの状態を理解する必要があります。 ユーザーは、エクスペリエンス内でいつでも現在残高をチェックすることもあります。

バランスの取得 API は、ネットワーク ポップアップが表示される場合、またはプランのモバイル アプリを起動すると呼び出されます。

次の一連の例では、バランスの取得 API の呼び出しフローを示します。

#### <a name="example-1-checking-balance-any-time-within-the-experience"></a>例 1:エクスペリエンス内でいつでも残高をチェック

HTTP 要求を*moBaseUrl* MO でホストされるサービスのエンドポイントと*sim id* ICCID は。

```html
GET https://{moBaseUrl}/sims/{sim id}/balances?fieldsTemplate=basic&limit=1&location=US HTTP/1.1
```

クエリ パラメーター:

| クエリ パラメーター名 | Value | 説明 |
| --- | --- | --- |
| location | String | (省略可能)。 ユーザーの残高が照会されている場所です。 指定しない場合、すべてのアクティブな残高が必要です。 |
| 制限 | 整数型 |(省略可能)。 返される残高の最大数。 指定しない場合、すべての残高が返されます。 |
| fieldsTemplate | 列挙型 |リソースで返す必要があるフィールドの一覧を指定します。 <p>設定可能な値:</p><ul><li>Basic:*型*、 *dataRemainingInMB*、および*timeRemaining*残高にリソースを返す必要があります。</li><li>完全な。分散リソースのすべてのプロパティは返される必要があります。</li></ul> |

#### <a name="example-2-returning-the-first-balance-that-is-available-for-the-user-in-us"></a>例 2:米国内のユーザーに使用される最初のバランスを返す

```html
GET https://moendpoint.com/v1/sims/iccid: 8988247000100003319/balances?fieldsTemplate=basic&limit=1&location=us HTTP/1.1
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”
```

HTTP 応答:

```html
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

#### <a name="example-3-the-expected-response-when-fieldstemplate-is-set-as-full"></a>例 3: FieldsTemplate が完全に設定されている場合は、想定される応答

```html
GET https://moendpoint.com/v1/sims/iccid: 8988247000100003319/balances?fieldsTemplate=full HTTP/1.1
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”

HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: “MSFT-12345678-1234-1234-1234-123456789abc”

{
“balances”: [
    {
         “id”: “23445”,
         “type”: “MODIRECTPAYG”,
         “dataRemaininginMB”: 123.0,
         “timeRemaining”: “P23DT23H”,
         “locations”: [“US”, “CA”],
         “ms-provisioningDataSet”: [“xxxxx”, “yyyyy”]
    },
    {
         “id”: “12345”,
         “type”: “MODIRECTPAYG”,
         “dataRemaininginMB”: 1367.0,
         “timeRemaining”: “P23DT23H”,
         “locations”: [“UK”, “FR”],
         “ms-provisioningDataSet”: [“xxxxx”, “yyyyy”]
    }
  ]
}
```

#### <a name="example-4-the-expected-response-for-a-sim-that-is-in-the-cosa-iccid-range-but-should-not-be-supported-by-mobile-plans"></a>例 4:COSA ICCID 範囲でもモバイル プランではサポートされていない必要があります SIM の想定される応答

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

Microsoft サービスと、サービス間の通信は、相互トランスポート層セキュリティ (MTLS) を使用して認証する必要があります。 Microsoft が提供する証明書を要求元の id の検証に使用する**moBaseUrl**します。

## <a name="walled-garden"></a>高いガーデン

高いガーデンは、データを使い果たしたときに、前払い顧客をサポートするキーです。 Wi-fi などの別のインターネット接続がない場合でも、MO 直接ポータルに到達することができます。 これは、コンシューマーは追加のデータ プランを購入し、サブスクリプションの管理を有効になります。

MO 直接 web ポータルとのバランスの取得 API エンドポイントもこの Walled Garden の一部である必要があります。

エンドユーザーがアクセス可能な常に必要なエンドポイントの数が少ないがあります。 次の表では、Walled Garden の必要なエンドポイントを定義します。 

| URL | HTTP/HTTPS |
| --- | --- |
| service.datamart.windows<span></span>.com | https |
| dogfood.datamart.windows<span></span>.com | https |
| windows.policies.live<span></span>.net | https |
| ctldl.windowsupdate<span></span>.com | http |
| msftncsi<span></span>.com | http |
| login.live<span></span>.com | http と https |
| storagetos.datamart.windows<span></span>.com | http と https |
| cdp1.public 信頼<span></span>.com | http |
| ocsp.omniroot<span></span>.com | http |
| vassg142.ocsp.omniroot<span></span>.com | http |
| vassg142.crl.omniroot<span></span>.com | http |
| mscrl.microsoft<span></span>.com | http |
| crl.microsoft<span></span>.com | http |
| msftconnecttest<span></span>.com | http |
| crl3.digicert<span></span>.com | http |
| Ocsp.digicert<span></span>.com | http |

## <a name="prepaid-implementation-validation"></a>前払い実装の検証

このセクションには、テストと検証の統合のフェーズに移動する準備ができていることを確認する必要がありますがについて説明します。

### <a name="prerequisites"></a>前提条件

1. Windows 10 のテストに使用する PC のバージョン 1607 をインストールします。
2. 一般公開の前に、結合することにより、最新の Windows バージョンを取得、 [Windows Insider Program](https://go.microsoft.com/fwlink/p/?linkid=866189)します。

### <a name="test-cases-to-be-executed"></a>テスト_ケースを実行するには

#### <a name="walled-garden"></a>高いガーデン

1. ユーザーには、残高がない、Walled Garden のサイトで定義されているをユーザーがアクセスできることを確認します[Walled Garden](#walled-garden)します。

#### <a name="getting-balance"></a>残高を取得します。

1. ユーザーは、Walled Garden 状態が、返される残高はゼロでなければなりません。
2. ユーザーに Microbalance が割り当てられているときに返される残高はゼロでなければなりません。
3. ユーザーは、データを消費するよう、残高が返されますが残りのデータを反映するようにデクリメントする必要があります。
4. ように、割り当てられた時間順序 API の作成後に経過が呼び出されたは、残りの期間、残りの期間を反映するようにデクリメントする必要があります。

#### <a name="test-with-expired-mtls-certificate"></a>MTLS の有効期限が切れた証明書を使用してテストします。

1. MTLS 証明書がない、MO Api を検証します。
予期される状態:401 許可されていません。
2. 有効期限が切れた MTLS 証明書を検証します。
予期される状態:401 許可されていません。

#### <a name="get-balance-negative-tests"></a>残高を取得するには、負の値のテスト

1. 無効な SIM で検証します。
予期される状態:404 not Found です。
2. 不明な場所または不適切な場所の文字列/数値を検証します。
予期される状態:400 (bad Request)。
3. 負の数値としてフィルターの制限を使用して検証し、INT の制限を超える
予期される状態:400-正しくない要求。
フィルターの制限 (整数) ステータス 200 OK が必要です。
4. 検証なしの残高を取得する*場所*(または空の場所)、 *fieldTemplate*、*制限*、およびパラメーターの詳細について多くの組み合わせ。
予期される状態:不適切なパラメーターの値の 400 (bad Request) をします。
OK ステータス 200 – が必要です。

## <a name="get-balance-api-load-test"></a>API の分散ロード テストを取得します。

バランスの取得 API は、実稼働環境で有効になっている、前に、予想される負荷を処理できるかどうかに表示する Microsoft サービスと通信事業者のサービスの両方をテストしてください。 携帯電話会社は、ロード テストの実行が必要です。  経過するとモバイルのプランと、次のセクションで構成されているには 6 時間のロード テストが実行されます。 

このテスト構成は、10,000 Sim の予想されるトラフィックから生成されます。 ピーク RPS は 3 回このトラフィック投影に基づいて計算されます。

- ロード テストは、25 のテスト エージェントから実行されます。
- ロード テストが実行されます。
    - 1 RPS でさまざまなユーザー (#ICCIDs) 100 で 1 時間です。
    - 1 RPS でさまざまなユーザー (#ICCIDs) 500 で 4 時間です。
    - 3 RPS (ピーク時) にさまざまなユーザー (#ICCIDs) 1000 と 1 時間です。
- 負荷分散は、クロス Api は次のようになります。

| API | 負荷分散 | 予想される RPS | ピーク時の RPS |
| --- | --- | --- | --- |
| GetBalance | 96% | 1 | 3 |

テストの実行中に予期される成功率は次のとおりです。99.9%. この成功率を実現するのには、運用環境のプランのモバイル サービスで、MO API を有効になります。