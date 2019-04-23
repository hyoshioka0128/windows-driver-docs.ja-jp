---
title: コールバック通知をモバイル プラン
description: このトピックでは、プランのモバイル アプリで通知をサポートするコールバックをについて説明します
ms.assetid: A3CE0B7D-80C5-4A98-8615-250A3C760B85
keywords:
- Windows Mobile プラン コールバック通知、モバイルのプランの実装モバイル演算子
ms.date: 03/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: e59e43bb970484ef4d1a344ec941847e052346b6
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903466"
---
# <a name="mobile-plans-callback-notifications"></a>コールバック通知をモバイル プラン

## <a name="overview"></a>概要

ユーザーには、MO ポータル フローが完了すると、MO ポータルは、プランのモバイル アプリにコントロールを返す必要があります。 これは、MO ポータルを使用したユーザーの操作の結果と、アプリに通知を発行することによって行います。

MO ポータルをサポートするトランザクションでは、含めるには、これを次に限定されません。

- (アクティブ化コードを発行する) 新しい eSIM プロファイルを販売します。
- サブスクリプションをアクティブにします。
- 新しいデータを購入 (後払いまたは一括払い) を計画します。
- サブスクリプションをキャンセルしています。

> [!NOTE]
> このコールバックで定義されているホストから返される[サービス構成](mobile-plans-service-configuration.md)します。

## <a name="inline-profile-delivery"></a>インラインのプロファイルの配信

次の図は、コントロール、MODirect ポータルを離れることがなく、プロファイルをダウンロード、Mobile プラン プログラムをサポートする方法の大まかな流れを示します。

![インラインのプロファイルのダウンロード シーケンス図を Mobile の計画](images/dynamo_inline_profile_flow.png)

月の直接のポータルのプロファイルのダウンロード、インストール、およびアクティブ化する準備ができたら、ポータルで呼び出す必要があります`MobilePlansInlineProfile.notifyInlineProfileDownload`します。

### <a name="mobileplansinlineprofilenotifyinlineprofiledownload"></a>MobilePlansInlineProfile.notifyInlineProfileDownload

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| activationCode | String | Esim 状のプロファイルをダウンロードするためのアクティブ化コード。 プロファイルの ICCID は、プロファイルのメタデータから推論されます。 |

インラインのプロファイルをダウンロードするアプリケーションを通知するために、API の例は、まず次の Javascript 関数を示しています。

```Javascript
function NotifyMobilePlans() { 
    var purchaseMetaData = MobilePlans.createPurchaseMetaData(); 
    purchaseMetaData.userAccount = MobilePlansUserAccount.new; 
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new; 
    purchaseMetaData.lineType = MobilePlansLineType.new; 
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete; 
    purchaseMetaData.planName = "My Plan"; 
    MobilePlansInlineProfileDownload.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineProfileDownload.profileActivationCompleteScript = "onActivationComplete";
    MobilePlansInlineProfileDownload.notifyInlineProfileDownload(purchaseMetaData , "1$smdp.address$matchingID"); 
}
```

参照してください[メタデータ プロパティを購入](#Purchase-Metadata-Properties-details)puchaseMetadata オブジェクトに関する詳細。

### <a name="listening-for-network-registration-changes"></a>ネットワーク登録の変更のリッスン

ネットワーク登録の変更をリッスンするように、`MobilePlansInlineProfileDownload.registrationChangedScript`の文字列を受け取る Javascript 関数の名前を指定する文字列に設定する必要があります、`registrationArgs`します。

登録の引数は、JSON オブジェクトを表す文字列です。

#### <a name="profileregistrationcompleteargs"></a>ProfileRegistrationCompleteArgs

| プロパティ名 | 型 | 説明 |
| --- | --- | -- |
| networkRegistrationState | String | 現在のネットワーク登録状態を表す文字列。 このプロパティの値で確認できます`MobilePlansNetworkRegistrationState`します。 |
| Iccid | String | 対象のネットワーク登録状態が変更された ICCID します。 |

#### <a name="mobileplansnetworkregistrationstate"></a>MobilePlansNetworkRegistrationState

| プロパティ名 | 型 | 説明 |
| --- | --- | -- |
| なし | String | 接続がないです。 |
| 登録解除されました | String | デバイスが登録されていませんし、ネットワーク プロバイダーが検索されません。 |
| 検索 | String | デバイスが登録されていませんし、ネットワーク プロバイダーが検索します。 |
| ホーム | String | デバイスは、ホーム ネットワーク プロバイダーには。 |
| ローミング | String | デバイスがローミング ネットワーク プロバイダーです。 |
| パートナー (partner) | String | デバイスは、ローミングのパートナー ネットワーク プロバイダーには。 |
| 拒否されました | String | デバイスの登録が拒否されました。 |

次の Javascript の例では、ネットワークの登録の変更イベントのリスナーを実装する方法を示します。

```Javascript
function onRegistrationChanged(registrationArgs) {
    var registrationObj = JSON.parse(registrationArgs);
    if(registrationObj.networkRegistrationState == MobilePlansNetworkRegistrationState.home ||
       registrationObj.networkRegistrationState == MobilePlansNetworkRegistrationState.roaming ||
       registrationObj.networkRegistrationState == MobilePlansNetworkRegistrationState.partner)
    {
        Log('Registration Successful!');
    }
}
```

### <a name="listening-for-profile-activation"></a>プロファイルのアクティブ化の待機

プロファイルのアクティブ化イベントをリッスンするように、`MobilePlansInlineProfileDownload.profileActivationCompleteScript`の文字列を受け取る Javascript 関数の名前を指定する文字列に設定する必要があります、`activationArgs`します。

`activationArgs`は JSON オブジェクトを表す文字列です。

#### <a name="profileactivationcompleteargs"></a>ProfileActivationCompleteArgs

| プロパティ名 | 型 | 説明 |
| --- | --- | -- |
| activationResult | String | アクティブ化の結果。 このプロパティの値で確認できます`MobilePlansActivationError`します。 |
| Iccid | String | アクティブになったプロファイルの ICCID します。 |

#### <a name="mobileplansactivationerror"></a>MobilePlansActivationError

| プロパティ名 | 型 | 説明 |
| --- | --- | -- |
| 成功 | String | 操作が成功したことを示します。 |
| notAuthorized | String | 操作が承認されていないことを示します。 |
| notFound | String | Esim 状の指定されたプロファイルが見つからなかったことを示します。 |
| PolicyViolation | String | 操作にポリシーに違反していることを示します。 |
| insufficientSpaceOnCard | String | ありません十分な記憶域スペースで操作を完了するカードを示します。 |
| serverFailure | String | 操作中にサーバーに障害が発生したことを示します。 |
| serverNotReachable | String | 操作中に、サーバーができなかったことを示します。 |
| timeoutWaitingForUserConsent | String | 操作のタイムアウト期間内のユーザーの同意が許可されていなかったことを示します。 |
| incorrectConfirmationCode | String | 間違った確認コードが操作中に指定されたことを示します。 |
| confirmationCodeMaxRetriesExceeded | String | 間違った確認コードが、操作中に指定されたことと以上再試行が許可されていることを示します。 |
| cardRemoved | String | SIM カードが削除されたことを示します。 |
| cardBusy | String | SIM カードがビジー状態であることを示します。 |
| その他 | String | 詳細な状態によっては考慮されない状態を示します。 |
| cardGeneralFailure | String | カード エラーが発生した、ダウンロード、インストール、または他の操作を正常に完了しなかったことを示します。 |
| confirmationCodeMissing | String | Esim 状のプロファイルをダウンロードする確認コードが必要であることを示します。 |
| invalidMatchingId | String | アクティブ化コードまたは検出されたイベントから一致する ID が拒否されたことを示します。 |
| noEligibleProfileForThisDevice | String | このデバイスと互換性の eSIM プロファイルが検出できなかったことを示します。 たとえば、プロファイルが見つかった LTE のサポートが必要ですが、デバイスでは、3 G のみがサポートされます。 |
| operationAborted | String | 操作が中止されたことを示します。 |
| eidMismatch | String | デバイスが 1 よりも異なる eSIM EID の携帯電話会社サーバー上の eSIM プロファイルが既に割り当てられていることを示します。 |
| profileNotAvailableForNewBinding | String | ユーザーが既に要求またはダウンロード eSIM プロファイルをダウンロードしようとしていることを示します。 |
| profileNotReleasedByOperator | String | ESIM プロファイルでは、まだとしてマークされていない通信事業者によってダウンロード リリースされたことを示します。 MO がリリースされると、プロファイルをマークする必要があるため、リリースされたプロファイルのみをダウンロードできます。 |
| operationProhibitedByProfileClass | String | Esim 状の profile クラスの操作が許可されないことを示します。 |
| profileNotPresent | String | Esim 状プロファイルが検出できなかったことを示します。 |
| noCorrespondingRequest | String | 対応する要求を検出しない可能性がありますを示します。 |
| された | String | 以下に、不明なエラーが返されることを示します。 |
| lpaInitializationError | String | 以下を初期化しようとするときにエラーが発生したことを示します。 |
| modemNotFound | String | デバイスに携帯電話のモデムが見つかりませんだったことを示します。 |
| localSettingsAccessFailed | String | 失敗したアプリのローカル設定にアクセスすることを示します。 |
| invalidJson | String | プランのモバイル アプリの呼び出し時に、MO ポータルが無効な JSON を指定することを示します。 |
| invalidActivationCode | String | MO ポータルが無効なアクティブ化コードを指定されたことを示します。 |
| invalidIccid | String | MO ポータルが、無効な ICCID を指定されたことを示します。 |

次の Javascript の例では、プロファイルのアクティブ化イベントのリスナーを実装する方法を示します。

```Javascript
function onActivationComplete(activationArgs) {
    var activationObj = JSON.parse(activationArgs);
    if(activationObj.activationResult == MobilePlansActivationError.success)
        Log('Activation Success');
}
```

## <a name="asynchronous-connectivity"></a>非同期接続

次の図は、Mobile プラン プログラムで遅延の接続をサポートする方法の大まかな流れを示します。

![遅延の接続シーケンス図のモバイルの計画](images/dynamo_async_connectivity_flow.png)

ユーザーには、通信事業者の MO 直接ポータルからプロファイルのダウンロードを必要とする購入が完了したら、後に、ポータル アプリケーションに通知 Mobile プラン、遅延の接続を使用してフローがトリガーすること、 `MobilePlans.notifyPurchaseWithProfileDownload` API。 

### <a name="mobileplansnotifypurchasewithprofiledownload"></a>MobilePlans.notifyPurchaseWithProfileDownload

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| activationCode | String | Esim 状のプロファイルをダウンロードするためのアクティブ化コード。 プロファイルの ICCID は、プロファイルのメタデータから推論されます。 |
| networkRegistrationInterval | 符号なし整数 | 携帯電話会社、ユーザーへの接続をプロビジョニングするのに必要な時間。 プランのモバイル アプリは、分単位で指定した期間内にネットワークに登録しようとします。 **注**この時間が最も近い 15 分間に丸められます。 たとえば、5 分として設定すると場合、アプリケーションは、ネットワークに約 15 分後に再登録しようとしています (ただし長い時間がかかる場合があります)。 場合にすぐに登録すると、デバイスは「0」に設定します。 |

次の Javascript 関数は、ユーザーの購入は、接続の遅延のプロビジョニングを必要とするアプリケーションを通知するために、API の例を示します。

 ```Javascript
function finishPurchaseWithDownload() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyPurchaseWithProfileDownload(metadata, "1$smdp.address$matchingID", 15);
}
```

参照してください[メタデータ プロパティを購入](#Purchase-Metadata-Properties-details)puchaseMetadata オブジェクトに関する詳細。

## <a name="adding-balance"></a>残高を追加します。

ユーザーには、自分のアカウント (ユーザー、esim 状で、現在のプロファイルを使用するために必要なプロファイル ダウンロード) により多くのデータを追加することで、MO 直接ポータルでの購入が完了すると、MO ポータルを呼び出す必要がある、 `MobilePlans.notifyBalanceAddition` API は、モバイルのプランにコントロールを返すアプリ。

### <a name="mobileplansnotifybalanceaddition"></a>MobilePlans.notifyBalanceAddition

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| Iccid | String | データが割り当てられている ICCID します。 この ICCID がアクティブでない場合、プランのモバイル アプリには、対応するプロファイルがアクティブにします。|

次の Javascript 関数例を示しています、ユーザーのプロファイルを使用して購入が完了したことをアプリケーションに通知するために API を既に使用できますが、必ずしも非アクティブ、eSIM。

 ```Javascript
function finishPurchaseWithBalanceAddition() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.none;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyBalanceAddition(metadata, "89000000000000000000");
    }
```

参照してください[メタデータ プロパティを購入](#Purchase-Metadata-Properties-details)詳細については、`puchaseMetadata`オブジェクト。

## <a name="canceling-purchase-flow"></a>フローの購入をキャンセル

かどうか、ユーザーが、MO ポータルでの購入のフローをキャンセルし、ポータルを起動する必要があります、 `MobilePlans.notifyCancelledPurchase` API にコントロールを計画してモバイル アプリに戻ります。

### <a name="mobileplansnotifycancelledpurchase"></a>MobilePlans.notifyCancelledPurchase

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |

次の Javascript 関数は、ユーザーが購入を取り消されたことをアプリケーションに通知するために、API の例を示します。

 ```Javascript
function finishPurchaseWithCancellation() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.cancelled;
        metadata.line = MobilePlansLineType.bailed;
        metadata.planName = "";
        MobilePlans.notifyCancelledPurchase(metadata);
    }
```

参照してください[メタデータ プロパティを購入](#Purchase-Metadata-Properties-details)詳細については、`puchaseMetadata`オブジェクト。

## <a name="purchase-metadata-properties-details"></a>購入のメタデータ プロパティの詳細

次の表では、購入のメタデータで使用される詳細情報について説明します。

| プロパティ名 | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| userAccount | String | 設定可能な値: <ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "userAccount":"New" |
| purchaseInstrument | String | 設定可能な値: <ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "purchaseInstrument":"New" |
| 行 | String | 設定可能な値: <ul><li>新規:ユーザー アカウントは、SIM カードが追加されたことを示します。</li><li>既存の。ユーザーがデバイスに既存の行を転送することを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "line":New" |
| moDirectStatus | String | 設定可能な値: <ul><li>完了します。ユーザーが購入を正常に完了したことを示します。</li><li>サービス エラー:ユーザーが月のサービス エラーのための購入を完了できなかったことを示します。</li><li>InvalidSIM:ポータルに渡される ICCID が正しいことを示します。</li><li>LogOnFailed: は、ユーザーが、MO ポータルへのログインに失敗したことを示します。</li><li>PurchaseFailed:課金エラーのために、購入が失敗したことを示します。</li><li>ClientError。引数が無効ですが、ポータルに渡されたことを示します。</li>BillingError:ユーザーの課金でエラーがあったことを示します。</li></ul> | "moDirectStatus":"Complete" |
| プラン名 | String | 成功したトランザクションでは、このフィールドは空にする必要がありますは、プランのわかりやすい名前を指定する必要があります。 失敗したトランザクションでは、このフィールドは空の文字列を指定する必要があります。 | 「プラン名」:"2 GB 毎月"|

## <a name="legacy-callback-notifications"></a>従来のコールバック通知

> [!NOTE]
> このセクションでは、参照専用として機能します。 この通知はプランのモバイル アプリでサポートされていますが、新しい Mobile 計画の実装に実装がお勧めします。

次の構文で JavaScript を使用して、プランのモバイル アプリに通知を送信します。

```javascript
DataMart.notifyPurchaseResult(notificationPayload);
```

Esim 状の通知ペイロードの例は次のとおりです。

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"New\",\"purchaseInstrument\":\"New\",\"line\":\"New\",\"moDirectStatus\":\"Complete\",\"planName\":\"MyPlan\"}";
notificationPayload.success = true;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.activationCode = '1$trl.prod.ondemandconnectivity.com$JO46UQDI07IKQDGG';
notificationPayload.iccid = '8988247000101997790';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

物理 SIM の通知ペイロードの例は次のとおりです。

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"New\",\"purchaseInstrument\":\"New\",\"line\":\"New\",\"moDirectStatus\":\"Complete\",\"planName\":\"MyPlan\"}";
notificationPayload.success = true;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.iccid = '8988247000101997790';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

ユーザーが成功したトランザクションなし、MO ポータルを破棄する eSIM の通知ペイロードの例は次のとおりです。 特定の実装に適用されるすべてのケースを実装するには、例では、次の表を参照してください。

```javascript
let notificationPayload = new Object();
notificationPayload.ver = '1';
notificationPayload.purchaseResult = "{\"userAccount\":\"Bailed\",\"purchaseInstrument\":\"None\",\"line\":\"None\",\"moDirectStatus\":\"None\",\"planName\":\"\"}";
notificationPayload.success = false;
notificationPayload.transactionId = 'MSFT_ecf5a4d6-024c-46c3-8fcd-2c1f0deed572';
notificationPayload.activationCode = '';
notificationPayload.iccid = '';

DataMart.notifyPurchaseResult(JSON.stringify(notificationPayload));
```

通知の送信元となる MO ポータル URI は、セキュリティで保護されたでなければなりません*https*プロトコル。 ホストが、必ずしも、今後のいくつかの柔軟性のまま、完全なパスを指定できます。 

次の表では、通知の JSON ペイロード内の各フィールドについて説明します。

| JSON フィールド         | 種類    | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      | 例                                |
| ------------------ | ------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| 成功            | ブール値 | **True** MO ダイレクト プランを購入した場合。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `“success”:true`                     |
| Iccid              | String  | ESIM は、購入月ダイレクト プランを使用するために、クライアントが使用する必要があります ICCID を示します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       | `iccid:”8988247000100297655”`        |
| activationCode     | String  | アクティブ化コード esim 状のプロファイルを取得します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `“ActivationCode”`                   |
| transactionId      | String  | MO ポータルは、ポータルを起動したときにクエリ パラメーターとして受信したトランザクション ID。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | `transctionId= rRi8OzhI3EiR02nm.2.0.1` |
| purchaseResult     | String  | MO ポータルを使用したユーザーの操作の詳細が含まれています。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |                                        |
| userAccount        | 列挙型    | このフィールドは必須です。 <p>設定可能な値:</p><ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul>                                                                                                                                                                                                                                                                                                                 | `“userAccount”:”New”`              |
| purchaseInstrument | 列挙型    | このフィールドは必須です。 <p>設定可能な値:</p><ul><li>新規:ユーザーが新しい支払方法を使用することを示します。</li><li>既存の。ユーザーがファイル内にある既存の支払い方法を使用することを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul>                                                                                                                                                                                                                                                                                                             | `“purchaseInstrument”:”New”`       |
| 行               | 列挙型    | このフィールドは必須です。 <p>設定可能な値:</p><ul><li>新規:ユーザー アカウントは、SIM カードが追加されたことを示します。</li><li>既存の。示すこと、転送された既存の行をデバイスにします。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul>                                                                                                                                                                                                                                                                                                                     | `“line”:”New”`                     |
| moDirectStatus     | 列挙型    | このフィールドは必須です。 <p>設定可能な値:</p><ul><li>完了します。ユーザーが購入を正常に完了したことを示します。</li><li>サービス エラー:ユーザーが月のサービス エラーのための購入を完了できなかったことを示します。</li><li>InvalidSIM:ポータルに渡される ICCID が正しいことを示します。</li><li>LogOnFailed:ユーザーが、MO ポータルへのログインに失敗したことを示します。</li><li>PurchaseFailed:課金エラーのために、購入が失敗したことを示します。</li><li>ClientError。引数が無効ですが、ポータルに渡されたことを示します。</li><li>None:ユーザーが特定のエラーが発生せず、トランザクションを終了したことを示します。</li></ul> | `“moDirectStatus”:”Complete”`      |
| プラン名           | String  | 成功したトランザクションでは、このフィールドは空にする必要がありますは、プランのわかりやすい名前を指定する必要があります。 失敗したトランザクションでは、このフィールドは空の文字列を指定する必要があります。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | `“planName”:”prepaid_3GperMonth”`  |
