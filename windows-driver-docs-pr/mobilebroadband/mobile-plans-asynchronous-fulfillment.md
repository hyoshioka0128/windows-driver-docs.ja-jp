---
title: 非同期の調達を Mobile の計画
description: 非同期の調達を Mobile の計画
ms.assetid: 56AB67D6-59A9-4483-B455-2FCC309C8903
keywords:
- 非同期の調達携帯電話会社の Windows Mobile の計画
ms.date: 11/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7eda3efa87bb0811e2f465fe61d5bb3562b3b6e3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572119"
---
# <a name="mobile-plans-asynchronous-fulfillment"></a>非同期の調達を Mobile の計画

[!include[Mobile Plans Beta Prerelease](../mobile-plans-beta-prerelease.md)]

## <a name="overview"></a>概要

このトピックでは、次のシナリオのいずれかの非同期処理を必要があるモバイル オペレーター用 API の詳細を示します。

- 非同期接続: と携帯電話会社できませんすぐに接続ユーザーに付与、ユーザーは、購入後にプロファイルをダウンロードするときにします。
- 非同期のプロファイルの配信: プロファイルが利用できない場合の購入時にダウンロードします。

## <a name="asynchronous-connectivity"></a>非同期接続

次の図は、高レベルのフロー方法について*Mobile プラン*プログラムは、遅延の接続をサポートしています。

![遅延の接続シーケンス図のモバイルの計画](images/dynamo_async_connectivity_flow.png)

ユーザーには、通信事業者の MO 直接ポータルからプロファイルのダウンロードを必要とする購入が完了したら、後に、ポータル アプリケーションに通知 Mobile プラン、遅延の接続を使用してフローがトリガーすること、 `MobilePlans.notifyPurchaseWithProfileDownload` API。 

### <a name="mobileplansnotifypurchasewithprofiledownload"></a>MobilePlans.notifyPurchaseWithProfileDownload

| パラメーター名 | 型 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| activationCode | String | Esim 状のプロファイルをダウンロードするためのアクティブ化コード。 プロファイルの ICCID は、プロファイルのメタデータから推論されます。 |
| networkRegistrationInterval | 符号なし整数 | 携帯電話会社、ユーザーへの接続をプロビジョニングするのに必要な時間。 プランのモバイル アプリは、分単位で指定した期間内にネットワークに登録しようとします。 **注**この時間が最も近い 15 分間に丸められます。 たとえば、5 分として設定すると場合、アプリケーションは、ネットワークに約 15 分後に再登録しようとしています (ただし長い時間がかかる場合があります)。 |

次の Javascript 関数は、ユーザーの購入は、接続の遅延のプロビジョニングを必要とするアプリケーションを通知するために、API の例を示します。

 ```Javascript
function finishPurchaseWithDownload() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyPurchaseWithProfileDownload(metadata, "1$smdp.address$", 15);
}
```

| プロパティ名 | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| userAccount | String | 設定可能な値: <ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "userAccount":"New" |
| purchaseInstrument | String | 設定可能な値: <ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "purchaseInstrument":"New" |
| 行 | String | 設定可能な値: <ul><li>新規:ユーザー アカウントは、SIM カードが追加されたことを示します。</li><li>既存の。ユーザーがデバイスに既存の行を転送することを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "line":New" |
| moDirectStatus | String | 設定可能な値: <ul><li>完了します。ユーザーが購入を正常に完了したことを示します。</li><li>サービス エラー:ユーザーが月のサービス エラーのための購入を完了できなかったことを示します。</li><li>InvalidSIM:ポータルに渡される ICCID が正しいことを示します。</li><li>LogOnFailed: は、ユーザーが、MO ポータルへのログインに失敗したことを示します。</li><li>PurchaseFailed:課金エラーのために、購入が失敗したことを示します。</li><li>ClientError。引数が無効ですが、ポータルに渡されたことを示します。</li>BillingError:ユーザーの課金でエラーがあったことを示します。</li></ul> | "moDirectStatus":"Complete" |
| プラン名 | String | 成功したトランザクションでは、このフィールドは空にする必要がありますは、プランのわかりやすい名前を指定する必要があります。 失敗したトランザクションでは、このフィールドは空の文字列を指定する必要があります。 | 「プラン名」:"2 GB 毎月"|


## <a name="asynchronous-profile-delivery"></a>非同期のプロファイルの配信

次の図は、高レベルのフロー方法について*Mobile プラン*プログラムは、遅延のプロファイルのダウンロードをサポートしています。

![プロファイルのダウンロード シーケンス図を遅延 Mobile の計画](images/dynamo_async_profile_flow.png)

ユーザーには、通信事業者の MO 直接ポータルからプロファイルのダウンロードを必要とする購入が完了したら、後に、ポータル アプリケーションに通知 Mobile プラン、遅延のプロファイルのダウンロードを使用してフローがトリガーすること、 `MobilePlans.notifyPurchaseDelayedProfile` API。 

### <a name="mobileplansnotifypurchasedelayedprofile"></a>MobilePlans.notifyPurchaseDelayedProfile

| パラメーター名 | 型 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| profileDownloadDelayInterval | 符号なし整数 | ユーザー プロファイルのプロファイルを作成し、それを携帯電話会社 SM DS からのダウンロードの準備完了に必要な時間。 プランのモバイル アプリがプロファイルをダウンロード SM DS からこの間隔の後の分。 **注**この時間が最も近い 15 分間に丸められます。 たとえば、5 分として設定すると場合、アプリケーションにダウンロードされようネットワーク (長くかかる場合があります) が約 15 分|

次の Javascript 関数は、ユーザーの購入が SM DS を使用して遅延のプロファイルのダウンロードが必要である、アプリケーションに通知するために、API の例を示します。

 ```Javascript
function finishPurchaseWithSMDS() {
        var metadata = MobilePlans.createPurchaseMetaData();
        metadata.userAccount = MobilePlansUserAccount.new;
        metadata.purchaseInstrument = MobilePlansPurchaseInstrument.new;
        metadata.moDirectStatus = MobilePlansMoDirectStatus.complete;
        metadata.line = MobilePlansLineType.new;
        metadata.planName = "2GB Monthly";
        MobilePlans.notifyPurchaseDelayedProfile(metadata, 15);
}
```

## <a name="inline-profile-delivery"></a>インラインのプロファイルの配信

次の図は、高レベルのフロー方法について*Mobile プラン*プログラムは、コントロール、MODirect ポータルを離れることがなく、プロファイルのダウンロードをサポートしています。

![インラインのプロファイルのダウンロード シーケンス図を Mobile の計画](images/dynamo_inline_profile_flow.png)

月の直接のポータルのプロファイルのダウンロード、インストール、およびアクティブ化する準備ができたら、ポータルで呼び出す必要があります`MobilePlansInlineProfile.notifyInlineProfileDownload`します。

### <a name="mobileplansinlineprofilenotifyinlineprofiledownload"></a>MobilePlansInlineProfile.notifyInlineProfileDownload

| パラメーター名 | 型 | 説明 |
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
    MobilePlansInlineProfileDownload.notifyInlineProfileDownload(purchaseMetaData , "1$smdp.address$"); 
}
```

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

プロファイルのアクティブ化イベントをリッスンするように、`MobilePlansInlineProfileDownload.profileActivationCompleteScript`の文字列を受け取る Javascript 関数の名前を指定する文字列に設定する必要があります、 `activationArgs`

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
| invalidCallback | String | MO ポータルが、無効なコールバックを指定されたことを示します。 |
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

## <a name="adding-balance"></a>残高を追加します。

ユーザーには、自分のアカウント (ユーザー、esim 状で、現在のプロファイルを使用するために必要なプロファイル ダウンロード) により多くのデータを追加することで、MO 直接ポータルでの購入が完了すると、MO ポータルを呼び出す必要がある、 `MobilePlans.notifyBalanceAddition` API は、モバイルのプランにコントロールを返すアプリ。

### <a name="mobileplansnotifybalanceaddition"></a>MobilePlans.notifyBalanceAddition

| パラメーター名 | 型 | 説明 |
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

## <a name="canceling-purchase-flow"></a>フローの購入をキャンセル

かどうか、ユーザーが、MO ポータルでの購入のフローをキャンセルし、ポータルを起動する必要があります、 `MobilePlans.notifyCancelledPurchase` API にコントロールを計画してモバイル アプリに戻ります。

### <a name="mobileplansnotifycancelledpurchase"></a>MobilePlans.notifyCancelledPurchase

| パラメーター名 | 型 | 説明 |
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

> [!NOTE]
> キャンセルと残高加算フローを使用して、 `DataMart.notifyPurchaseResult` API は引き続きサポートされます。 

## <a name="frequently-asked-questions"></a>よく寄せられる質問

1. *トランザクション ID*も必要ですか?  

    モバイルの演算子を返す必要はありません、*トランザクション ID*ポータルに渡されますが、トラブルシューティングの目的でこの値を格納する必要があります。  

2. API は、制御を転送するために使用する必要がありますに*Mobile プラン*と接続はすぐにで使用できますか?  

    `MobilePlans.notifyPurchaseDelayedProfile` API は今後このシナリオをサポートします。 この特定のケースで、 *networkRegistrationInterval*にパラメーターを設定する必要があります**0**します。  

    実装している場合、`MobilePlans.notifyPurchaseResult`として API が、統合ガイドで指定されたがまだサポートされています。  

3. ICCID 情報の eSIM のアクティブ化のコールバックを引き続き必要ですか。  

    ICCID 情報は追加の分散のシナリオでのみ必要時に、 `MobilePlans.notifyBalanceAddition` API のコールバックを使用します。  

    実装している場合、`MobilePlans.notifyPurchaseResult`として API が、統合ガイドで指定されたがまだサポートされています。  

4. What-if まだヘルプが必要ですか。  

    Microsoft の担当者にお問い合わせください。
