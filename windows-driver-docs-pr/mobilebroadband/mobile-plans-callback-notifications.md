---
title: モバイルプランのコールバック通知
description: このトピックでは、モバイルプランアプリによるコールバック通知のサポートについて説明します。
ms.assetid: A3CE0B7D-80C5-4A98-8615-250A3C760B85
keywords:
- Windows Mobile プランのコールバック通知、モバイルプランの実装のモバイルオペレーター
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: f778f8bcdc7ae093d846af6196d9d90969e3c773
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402293"
---
# <a name="mobile-plans-callback-notifications"></a>モバイルプランのコールバック通知

## <a name="overview"></a>概要

ユーザーがモバイルオペレーター web ポータルでアクティブ化フローを完了すると、ポータルは、フローが完了したことをモバイルプランアプリに知らせるシグナルを提供する必要があります。 これを行うには、web ポータルとのユーザー操作の結果を含む通知をアプリに発行します。

Web ポータルでサポートされるトランザクションには、次のものが含まれますが、これらに限定されません。

- (ライセンス認証コードを使用して) 新しい eSIM プロファイルを発行しています。
- 新規または既存のサブスクリプションにデバイスを関連付ける。
- 新しいデータプラン (前払い支払いまたは前払い) を購入する。
- の追加データを前払いプランに購入します。
- サブスクリプションをキャンセルしています。

> [!NOTE]
> コールバック通知は、モバイルオペレーターの[サービス構成](mobile-plans-service-configuration.md)で定義されているホストから返される必要があります。

## <a name="inline-profile-download-and-connectivity"></a>インラインプロファイルのダウンロードと接続

コールバックメソッドは、ユーザーを携帯電話会社の web ポータルで保持しながら、eSIM プロファイルをバックグラウンドでダウンロードするときに使用する必要があります。 これにより、プロファイルのダウンロードが完了した後に、ポータルでアカウント管理ページなどの追加のコンテンツを表示できるようになります。 また、プロファイルによって、アクティブ化の直後に携帯ネットワークにデバイスが登録されるようにすることが求められます。時間の遅延は必要ありません。


次の図は、インラインプロファイルダウンロードコールバックの呼び出しフローを示しています。

![モバイルプランインラインプロファイルのダウンロードシーケンス図](images/mobile_plans_inline_profile_flow.png)

これは、以前の[インラインプロファイル配信](mobile-plans-legacy-callback-notifications.md#inline-profile-delivery)コールバックの改訂版です。ドキュメント用の付録で参照できます。 携帯電話では、前の手順で変更したコールバックメソッドを使用することをお勧めします。

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode"></a>MobilePlansInlineOperations のダウンロード (purchaseMetaData、activationCode)

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| purchaseMetadata | Object | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これには、ユーザーアカウント、購入方法またはインストルメント、ユーザーが新しい行を追加する場合の詳細、ユーザーが購入したプランの名前などの詳細が含まれます。 これらは、ビジネスレポートに使用されます。 |
| activationCode | String | ESIM プロファイルをダウンロードするために使用されるアクティベーションコード

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作と一致する識別子を持つオブジェクト。

このコールバック通知の受信時に、eSIM プロファイルのダウンロードが開始されます。 コントロールは、呼び出しの直後に web ポータルに返されます。 Web ポータルの上部に表示されるポップアップ要素として、プロファイルのダウンロードの進行状況を示す UI が表示されます。 このプロセスの間、web ポータルは引き続き移動できます。

次の Javascript 関数は、プロファイルのダウンロードを開始する必要があることをアプリケーションに通知する API の例を示しています。

```Javascript
var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineOperations.profileActivationCompleteScript = "onActivationComplete";
    MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData , "1$smdp.address$matchingID");
```

PuchaseMetadata オブジェクトの詳細については、「[購入メタデータのプロパティ](#purchase-metadata-properties-details)」を参照してください。

### <a name="listening-for-network-registration-changes"></a>ネットワーク登録の変更をリッスンしています

ネットワーク登録の変更をリッスンするには、をに `MobilePlansInlineProfileDownload.registrationChangedScript` 文字列を受け取る Javascript 関数の名前である文字列に設定する必要があり `registrationArgs` ます。

登録引数は、JSON オブジェクトを表す文字列です。

#### <a name="profileregistrationcompleteargs"></a>ProfileRegistrationCompleteArgs

| プロパティ名 | Type | 説明 |
| --- | --- | -- |
| networkRegistrationState | String | 現在のネットワーク登録状態を表す文字列。 このプロパティの値は、で確認でき `MobilePlansNetworkRegistrationState` ます。 |
| iccid | String | ネットワーク登録状態が変更された ICCID。 |

#### <a name="mobileplansnetworkregistrationstate"></a>MobilePlansNetworkRegistrationState

| プロパティ名 | Type | 説明 |
| --- | --- | -- |
| ありません | String | 接続なし。 |
| 解除 | String | デバイスが登録されていないため、ネットワークプロバイダーを検索していません。 |
| 検索 | String | デバイスは登録されていないため、ネットワークプロバイダーを検索しています。 |
| home | String | デバイスはホームネットワークプロバイダー上にあります。 |
| ローミング | String | デバイスはローミングネットワークプロバイダー上にあります。 |
| パートナー (partner) | String | デバイスは、ローミングパートナーネットワークプロバイダー上にあります。 |
| 拒否 | String | デバイスの登録が拒否されました。 |

次の Javascript の例は、ネットワーク登録変更イベントのリスナーを実装する方法を示しています。

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

### <a name="listening-for-profile-activation"></a>プロファイルのアクティブ化を待機しています

プロファイルのアクティブ化イベントをリッスンするには、をに `MobilePlansInlineProfileDownload.profileActivationCompleteScript` 文字列を受け取る Javascript 関数の名前である文字列に設定する必要があり `activationArgs` ます。

`activationArgs`は、JSON オブジェクトを表す文字列です。

#### <a name="profileactivationcompleteargs"></a>ProfileActivationCompleteArgs

| プロパティ名 | Type | 説明 |
| --- | --- | -- |
| activationResult | String | アクティブ化の結果。 このプロパティの値は、で確認でき `MobilePlansActivationError` ます。 |
| iccid | String | アクティブ化されたプロファイルの ICCID。 |

#### <a name="mobileplansactivationerror"></a>MobilePlansActivationError

| プロパティ名 | Type | 説明 |
| --- | --- | -- |
| success | String | 操作が成功したことを示します。 |
| notAuthorized | String | 操作が承認されていないことを示します。 |
| notFound | String | 指定された eSIM プロファイルが見つからなかったことを示します。 |
| policyViolation | String | 操作がポリシーに違反していることを示します。 |
| insufficientSpaceOnCard | String | 操作を完了するのに十分なストレージ領域がカードにないことを示します。 |
| serverFailure | String | 操作中にサーバーエラーが発生したことを示します。 |
| serverNotReachable 可能 | String | 操作中にサーバーに到達できなかったことを示します。 |
| timeoutWaitingForUserConsent | String | 操作のタイムアウト期間内にユーザーの同意が許可されなかったことを示します。 |
| incorrectConfirmationCode | String | 操作中に間違った確認コードが指定されたことを示します。 |
| confirmationCodeMaxRetriesExceeded | String | 操作中に間違った確認コードが指定されたこと、および再試行が許可されていないことを示します。 |
| カードが削除されました | String | SIM カードが削除されたことを示します。 |
| cardBusy | String | SIM カードがビジー状態であることを示します。 |
| その他 | String | より具体的なステータスによって考慮されていない状態を示します。 |
| Cardの一般エラー | String | ダウンロード、インストール、またはその他の操作が正常に完了できないようにするカードエラーが発生したことを示します。 |
| confirmationCodeMissing | String | ESIM プロファイルをダウンロードするために確認コードが必要であることを示します。 |
| invalidMatchingId | String | アクティベーションコードまたは検出されたイベントの一致する ID が拒否されたことを示します。 |
| noEligibleProfileForThisDevice | String | このデバイスと互換性のある eSIM プロファイルが見つからないことを示します。 たとえば、LTE サポートを必要とするプロファイルが見つかりましたが、デバイスは3G のみをサポートしています。 |
| operationAborted | String | 操作が中止されたことを示します。 |
| eidMismatch | String | モバイルオペレーターサーバーの eSIM プロファイルが、デバイスとは異なる eSIM EID に対して既に割り当てられていることを示します。 |
| Profilenotの Fornewbinding | String | ユーザーが既に要求またはダウンロードされている eSIM プロファイルをダウンロードしようとしていることを示します。 |
| profileNotReleasedByOperator | String | は、eSIM プロファイルが使用可能であることを示しますが、携帯電話事業者がダウンロード用にリリース済みとしてマークされていません。 リリース済みのプロファイルのみをダウンロードできます。そのため、MO はプロファイルをリリース済みとしてマークする必要があります。 |
| operationProhibitedByProfileClass | String | は、この操作が eSIM プロファイルクラスで許可されていないことを示します。 |
| profileNotPresent | String | ESIM プロファイルが見つからなかったことを示します。 |
| Norequest | String | 対応する要求が見つからなかったことを示します。 |
| unknownError | String | LPA が不明なエラーを返したことを示します。 |
| lpaInitializationError | String | LPA を初期化しようとしたときにエラーが発生したことを示します。 |
| modemNotFound | String | デバイスで携帯電話モデムが見つからなかったことを示します。 |
| localSettingsAccessFailed | String | アプリのローカル設定へのアクセスに失敗したことを示します。 |
| invalidJson | String | モバイルプランアプリを呼び出すときに、MO ポータルで無効な JSON が提供されたことを示します。 |
| invalidActivationCode | String | MO ポータルに無効なアクティベーションコードが指定されていることを示します。 |
| invalidIccid | String | MO ポータルに無効な ICCID が指定されていることを示します。 |

次の Javascript の例は、プロファイルアクティブ化イベントのリスナーを実装する方法を示しています。

```Javascript
function onActivationComplete(activationArgs) {
    var activationObj = JSON.parse(activationArgs);
    if(activationObj.activationResult == MobilePlansActivationError.success)
        Log('Activation Success');
}
```

## <a name="delayed-esim-profile-download-and-activation"></a>ダウンロードとアクティブ化の遅延された eSIM プロファイル

次の図は、モバイルプランアプリが eSIM プロファイルの遅延ダウンロードとアクティブ化をサポートする方法の呼び出しフローを示しています。 これは、eSIM プロファイルが SM DP + サーバーによってリリースされない場合に使用する必要があり、しばらくするとダウンロードできます。 プロファイルがダウンロードされてアクティブになると、デバイスは携帯ネットワークに登録できることが想定されます。

![モバイルプラン遅延プロファイルダウンロードシーケンス図](images/mobile_plans_delay_profile_flow.png)

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode-downloaddelay"></a>MobilePlansInlineOperations Download (purchaseMetaData、activationCode、downloadDelay)

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| purchaseMetadata | Object | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これには、ユーザーアカウント、購入方法またはインストルメント、ユーザーが新しい行を追加する場合の詳細、ユーザーが購入したプランの名前などの詳細が含まれます。 これらはすべてレポートに使用されます。 |
| activationCode | String | プロファイルが配置されているアクティブ化コードまたは SM DP + アドレス
| downloadDelay | uint | ESIM プロファイルのダウンロードを試行するまでの待機時間 (分)

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作と一致する識別子を持つオブジェクト。

制御は、呼び出しの直後にモバイルオペレーターポータルに返されます。 プロファイルが後でインストールされることをユーザーに通知するための UI が表示されます。 分が経過すると、 `downloadDelay` ユーザーに通知が表示され、プロファイルのダウンロードプロセスを開始するように招待されます。

次の Javascript 関数は、遅延のあるプロファイルのダウンロードを開始する必要があることをアプリケーションに通知する API の例を示しています。

```Javascript
var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineOperations.profileActivationCompleteScript = "onActivationComplete";
    MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData , "1$smdp.address$matchingID", 15);
```

PuchaseMetadata オブジェクトの詳細については、「[購入メタデータのプロパティ](#purchase-metadata-properties-details)」を参照してください。

上[の「ネットワーク登録の変更のリッスン](#listening-for-network-registration-changes)」セクションを参照してください。

前[の「プロファイルのアクティブ化のリッスン](#listening-for-profile-activation)」セクションを参照してください。

## <a name="cancel-esim-profile-download"></a>ESIM プロファイルのダウンロードの取り消し

これは、新しい eSIM プロファイルのダウンロードシナリオに適用されますが、将来のユースケースにも使用できます。

次の図は、モバイルプランプログラムが MODirect ポータルから制御せずに、eSIM プロファイルのダウンロードの取り消しをサポートする方法の大まかな流れを示しています。

![モバイルプランのキャンセル eSIM プロファイルのダウンロードシーケンス図](images/mobile_plans_cancel_profile_download_flow.png)

### <a name="mobileplansinlineoperationsnotifyoperationcancelmobileplansoperationcontext"></a>MobilePlansInlineOperations (MobilePlansOperationContext)

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| operationContext | Object | このオブジェクトには、前の操作を一意に識別する情報が含まれています。 |

この操作は、ダウンロードの準備ができていることを知らせるトースト通知がユーザーに表示される前にキャンセルできます。

次の Javascript 関数は、非同期アクションをキャンセルする API の例を示しています。

```Javascript
var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.registrationChangedScript = "onRegistrationChanged";
    MobilePlansInlineOperations.profileActivationCompleteScript = "onActivationComplete";
    var op = MobilePlansInlineOperations.notifyProfileDownload(purchaseMetaData , "1$smdp.address$matchingID", 15);
    MobilePlansInlineOperations.notifyOperationCancel(op);
```

## <a name="asynchronous-connectivity"></a>非同期接続

次の図は、モバイルプランアプリが遅延接続をサポートする方法の大まかな流れを示しています。 このコールバックメソッドは、eSIM プロファイルが既に SM DP + サーバーによってリリースされている場合に使用する必要がありますが、デバイスは、携帯ネットワークに登録する前にしばらく待つ必要があります。

![モバイルプランの遅延接続シーケンス図](images/dynamo_async_connectivity_flow.png)

ユーザーがアクティブ化フローを正常に完了すると、web ポータルは、API を使用して遅延接続フローをトリガーする必要があることをモバイルプランアプリに通知し `MobilePlans.notifyPurchaseWithProfileDownload` ます。

### <a name="mobileplansnotifypurchasewithprofiledownload"></a>MobilePlans.notifyPurchaseWithProfileDownload

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| purchaseMetadata | Object | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これには、ユーザーアカウント、購入方法またはインストルメント、ユーザーが新しい行を追加する場合の詳細、ユーザーが購入したプランの名前などの詳細が含まれます。 これらはすべてレポートに使用されます。 |
| activationCode | String | ESIM プロファイルをダウンロードするためのアクティベーションコード。 プロファイルの ICCID は、プロファイルメタデータから推論されます。 |
| networkRegistrationInterval | 符号なし整数 | 携帯電話会社がユーザーに接続を準備するために必要な時間。 モバイルプランアプリは、指定された時間間隔 (分) 内にネットワークへの登録を試みます。 **メモ**この時間は、15分間隔で丸められます。 たとえば、これが5分に設定されている場合、アプリケーションは約15分後にネットワークに再登録しようとします (ただし、時間がかかる場合があります)。 "0" に設定すると、デバイスはすぐに登録を試みます。 |

次の Javascript 関数は、ユーザーの購入によって接続の遅延プロビジョニングが必要であることをアプリケーションに通知する API の例を示しています。

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

PuchaseMetadata オブジェクトの詳細については、「[購入メタデータのプロパティ](#purchase-metadata-properties-details)」を参照してください。

## <a name="adding-balance"></a>残高の追加

ユーザーが既存のアカウントに残高を追加することによって web ポータルで購入を完了すると、web ポータルは `MobilePlansInlineOperations.notifyBalanceAddition` API 復帰制御を呼び出して、Mobile plan アプリに戻ります。 これは、デバイスに既にインストールされている*物理 SIM*または*eSIM プロファイル*に使用できます。

次の図は、モバイルプランアプリがバランスの追加をサポートする方法の大まかな流れを示しています。

![モバイルプランによる順序の追加シーケンス図](images/mobile_plans_add_balance_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata"></a>MobilePlansInlineOperations の追加 (purchaseMetaData)

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| purchaseMetadata | Object | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これには、ユーザーアカウント、購入方法またはインストルメント、ユーザーが新しい行を追加する場合の詳細、ユーザーが購入したプランの名前などの詳細が含まれます。 これらはすべてレポートに使用されます。 |

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作と一致する識別子を持つオブジェクト。

携帯電話会社が特定のアカウントに残高を追加する場合、web ポータルは API を呼び出す必要があり `MobilePlansInlineOperations.notifyBalanceAddition` ます。

次の Javascript 関数は、バランスの追加が行われたことをアプリケーションに通知する API の例を示しています。

```Javascript
function NotifyMobilePlans() {
    var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData);
}
```

オブジェクトの詳細については、「[購入メタデータのプロパティ](#purchase-metadata-properties-details)」を参照してください `puchaseMetadata` 。

## <a name="adding-balance-and-activate-esim-profile"></a>[残高の追加] と [eSIM プロファイルのアクティブ化]

ユーザーが既存のアカウントにデータを追加して web ポータルで再生を完了すると、web ポータルは `MobilePlansInlineOperations.notifyBalanceAddition` API のリターンコントロールを呼び出して、モバイルプランアプリに戻る必要があります。 これは、デバイスに既にインストールされている*eSIM プロファイル*に使用できます。 ICCID パラメーターは、どの eSIM プロファイルをアクティブ化する必要があるかを示します。

次の図は、Mobile plan アプリが iccid 情報による残高の追加をサポートする方法の呼び出しフローを示しています。

![モバイルプランによる順序の追加シーケンス図](images/mobile_plans_add_balance_iccid_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata-iccid"></a>MobilePlansInlineOperations の追加 (purchaseMetaData、iccid)

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| purchaseMetadata | Object | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これには、ユーザーアカウント、購入方法またはインストルメント、ユーザーが新しい行を追加する場合の詳細、ユーザーが購入したプランの名前などの詳細が含まれます。 これらはすべてレポートに使用されます。 |
| iccid | String | 残高の追加後にアクティブにする必要がある ICCID

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作と一致する識別子を持つオブジェクト。

また、プロファイルの ICCID がわかっている場合は、非アクティブなプロファイルに均衡を加えることもできます。 を `MobilePlansInlineOperations.notifyBalanceAddition` ICCID と共に使用すると、バランスの追加をアプリに通知するだけでなく、指定された ICCID に対応するプロファイルにアクティブなプロファイルを切り替えることができます。

次の Javascript 関数は、バランスの追加が行われたことをアプリケーションに通知する API の例を示しています。

```Javascript
function NotifyMobilePlans() {
    var purchaseMetaData = MobilePlans.createPurchaseMetaData();
    purchaseMetaData.userAccount = MobilePlansUserAccount.new;
    purchaseMetaData.purchaseInstrument = MobilePlansPurchaseInstrument.new;
    purchaseMetaData.lineType = MobilePlansLineType.new;
    purchaseMetaData.modirectStatus = MobilePlansMoDirectStatus.complete;
    purchaseMetaData.planName = "My Plan";
    MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData, "8900000000000000001");
}
```

オブジェクトの詳細については、「[購入メタデータのプロパティ](#purchase-metadata-properties-details)」を参照してください `puchaseMetadata` 。

## <a name="canceling-purchase-flow"></a>購入フローを取り消しています

ユーザーが web ポータルでアクティブ化フローをキャンセルした場合、ポータルは API を呼び出して、 `MobilePlans.notifyCancelledPurchase` モバイルプランアプリに制御を戻す必要があります。

### <a name="mobileplansnotifycancelledpurchase"></a>MobilePlans の購入

| パラメーター名 | Type | 説明 |
| --- | --- | -- |
| purchaseMetadata | Object | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これには、ユーザーアカウント、購入方法またはインストルメント、ユーザーが新しい行を追加する場合の詳細、ユーザーが購入したプランの名前などの詳細が含まれます。 これらはすべてレポートに使用されます。 |

次の Javascript 関数は、ユーザーが購入を取り消したことをアプリケーションに通知する API の例を示しています。

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

オブジェクトの詳細については、「[購入メタデータのプロパティ](#purchase-metadata-properties-details)」を参照してください `puchaseMetadata` 。

## <a name="purchase-metadata-properties-details"></a>購入メタデータプロパティの詳細

次の表では、購入メタデータで使用される詳細について説明します。

| プロパティ名 | Type | 説明 | 例 |
| --- | --- | --- | --- |
| userAccount | String | 指定できる値 <ul><li>新規: 新しいユーザーアカウントがユーザーによって作成されたことを示します。</li><li>Existing: ユーザーが既存のユーザーアカウントでログオンしたことを示します。</li><li>一言おじさん: ユーザーがこのステップで購入フローを終了したことを示します。</li><li>None: ユーザーがこのステップに届かなかったことを示します。</li></ul> | "userAccount": "New" |
| purchaseInstrument | String | 指定できる値 <ul><li>新規: 新しいユーザーアカウントがユーザーによって作成されたことを示します。</li><li>Existing: ユーザーが既存のユーザーアカウントでログオンしたことを示します。</li><li>一言おじさん: ユーザーがこのステップで購入フローを終了したことを示します。</li><li>None: ユーザーがこのステップに届かなかったことを示します。</li></ul> | "purchaseInstrument": "New" |
| line | String | 指定できる値 <ul><li>新規: SIM カードがユーザーアカウントによって追加されたことを示します。</li><li>Existing: ユーザーがデバイスに既存の行を転送したことを示します。</li><li>一言おじさん: ユーザーがこのステップで購入フローを終了したことを示します。</li><li>None: ユーザーがこのステップに届かなかったことを示します。</li></ul> | "line": New " |
| moDirectStatus | String | 指定できる値 <ul><li>Complete: ユーザーが購入を正常に完了したことを示します。</li><li>ServiceError: ユーザーが、MO サービスエラーのために購入を完了できなかったことを示します。</li><li>InvalidSIM: ポータルに渡された ICCID が正しくないことを示します。</li><li>LogOnFailed: ユーザーが MO ポータルにログインできなかったことを示します。</li><li>PurchaseFailed: 課金エラーが原因で購入が失敗したことを示します。</li><li>ClientError: 無効な引数がポータルに渡されたことを示します。</li>複数のエラー: ユーザーの請求にエラーがあったことを示します。</li></ul> | "moDirectStatus": "Complete" |
| planName | String | トランザクションが成功した場合、このフィールドを空にすることはできません。また、説明的なプラン名を指定する必要があります。 トランザクションが失敗した場合、このフィールドは空の文字列である必要があります。 | "プラン名": "2 GB の月"|

## <a name="legacy-callback-notifications"></a>レガシ コールバック通知

すべての[レガシコールバックが記載さ](mobile-plans-legacy-callback-notifications.md)れている特定のページを参照してください。
