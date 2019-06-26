---
title: コールバック通知をモバイル プラン
description: このトピックでは、プランのモバイル アプリで通知をサポートするコールバックをについて説明します
ms.assetid: A3CE0B7D-80C5-4A98-8615-250A3C760B85
keywords:
- Windows Mobile プラン コールバック通知、モバイルのプランの実装モバイル演算子
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1aa695f92c24639a44557b4b0dbeee4afc5a7d01
ms.sourcegitcommit: 19575e9a2aed6bebe7c465e561c10c86baf8d24b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2019
ms.locfileid: "67395431"
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

## <a name="immediate-esim-profile-download-and-activation"></a>イミディ エイト eSIM プロファイルのダウンロードとアクティブ化

次の図は、コントロール、MODirect ポータルを離れることがなく、プロファイルをダウンロード、Mobile プラン プログラムをサポートする方法の大まかな流れを示します。

![インラインのプロファイルのダウンロード シーケンス図を Mobile の計画](images/mobile_plans_inline_profile_flow.png)

これは、進化[インライン プロファイル配信](mobile-plans-legacy-callback-notifications.md#inline-profile-delivery)、ようになりましたが、以前のドキュメント ページに記載されています。

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode"></a>MobilePlansInlineOperations.notifyProfileDownload (purchaseMetaData、activationCode)

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| activationCode | String | Esim 状、プロファイルのダウンロードに使用されるアクティブ化コード

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作にどの一致する識別子を持つオブジェクト。

Esim 状、プロファイルのダウンロードのプロセスを開始します。 コントロールは、呼び出しのすぐ後に、MO ポータルに返されます。 通知の形式で月のポータルの上部でプロファイルのダウンロードの進行状況を表示する UI が表示されます。 MO ポータルは、このプロセス中にナビゲートを継続できます。

次の Javascript 関数は、プロファイルのダウンロードを開始するアプリケーションを通知するために、API の例を示しています。

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

参照してください[メタデータ プロパティを購入](#purchase-metadata-properties-details)puchaseMetadata オブジェクトに関する詳細。

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

## <a name="deferred-esim-profile-download-and-activation"></a>遅延 eSIM プロファイルのダウンロードとアクティブ化

次の図は、Mobile プラン プログラムでコントロール、MODirect ポータルを離れることがなく esim 状のプロファイルの遅延ダウンロードをサポートする方法の大まかな流れを示します。

![遅延のプロファイルのダウンロード シーケンス図のモバイルの計画](images/mobile_plans_delay_profile_flow.png)

### <a name="mobileplansinlineoperationsnotifyprofiledownloadpurchasemetadata-activationcode-downloaddelay"></a>MobilePlansInlineOperations.notifyProfileDownload (purchaseMetaData、activationCode、downloadDelay)

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| activationCode | String | アクティブ化コードまたは SM-DP + アドレス、プロファイルがある場所
| downloadDelay | uint | Esim 状のプロファイルをダウンロードしようとする前に待機する分数

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作にどの一致する識別子を持つオブジェクト。

コントロールは、呼び出しのすぐ後に、MO ポータルに返されます。 プロファイルをインストールすることをユーザーに通知するために、UI が表示されます。 後に、`downloadDelay`分が発生しました、通知に表示される、ユーザーは、プロファイルのダウンロードのプロセスを開始するように招待します。

次の Javascript 関数は、遅延時間でプロファイルのダウンロードを開始するアプリケーションを通知するために、API の例を示しています。

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

参照してください[メタデータ プロパティを購入](#purchase-metadata-properties-details)puchaseMetadata オブジェクトに関する詳細。

参照してください[ネットワーク登録の変更のリッスン](#listening-for-network-registration-changes)前のセクション。

参照してください[プロファイルのアクティブ化のリッスン](#listening-for-profile-activation)前のセクション。

## <a name="cancel-esim-profile-download"></a>Esim 状のプロファイルのダウンロードをキャンセルします。

現時点では、これは、プロファイルのダウンロードのシナリオの遅延の esim 状に適用されますが、今後のユーザーの場合にされる可能性があります。

次の図は、Mobile プラン プログラムでコントロール、MODirect ポータルを離れることがなく eSIM プロファイルのダウンロードのキャンセルをサポートする方法の大まかな流れを示します。

![Esim 状プロファイルのダウンロード シーケンス図をキャンセルする Mobile の計画](images/mobile_plans_cancel_profile_download_flow.png)

### <a name="mobileplansinlineoperationsnotifyoperationcancelmobileplansoperationcontext"></a>MobilePlansInlineOperations.notifyOperationCancel(MobilePlansOperationContext)

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| operationContext | オブジェクト | このオブジェクトには、前の操作を一意に識別する情報が含まれています。 |

ユーザーが開始する準備がそれらをダウンロードすることを通知、トースト通知を表示する前に、この操作を取り消すことができます。

次の Javascript 関数は、非同期の操作をキャンセルする API の例を示します。

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

参照してください[メタデータ プロパティを購入](#purchase-metadata-properties-details)puchaseMetadata オブジェクトに関する詳細。

## <a name="adding-balance"></a>残高を追加します。

ユーザーより多くのデータを自分のアカウントに追加することで、MO 直接ポータルでの購入が完了すると、MO ポータルを呼び出す必要がある、 `MobilePlansInlineOperations.notifyBalanceAddition` API は、プランのモバイル アプリにコントロールを返します。 これを使用できます*物理 SIM*または*eSIM プロファイル*デバイスに既にインストールされています。

次の図は、Mobile プラン残高を追加するサポートをプログラミングする方法の大まかな流れを示します。

![Balancesequence ダイアグラムを追加する Mobile の計画](images/mobile_plans_add_balance_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata"></a>MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData)

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作にどの一致する識別子を持つオブジェクト。

MO は、指定したアカウントに残高を追加するには、MO で呼び出す必要があります、 `MobilePlansInlineOperations.notifyBalanceAddition` API。

次の Javascript 関数は、残高加算が行われたアプリケーションを通知するために、API の例を示します。

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

参照してください[メタデータ プロパティを購入](#purchase-metadata-properties-details)詳細については、`puchaseMetadata`オブジェクト。

## <a name="adding-balance-and-activate-esim-profile"></a>残高を追加して、esim 状のプロファイルをアクティブ化

ユーザーより多くのデータを自分のアカウントに追加することで、MO 直接ポータルでの購入が完了すると、MO ポータルを呼び出す必要がある、 `MobilePlansInlineOperations.notifyBalanceAddition` API は、プランのモバイル アプリにコントロールを返します。 これを使用できます*eSIM プロファイル*デバイスに既にインストールされています。 ICCID パラメーターは、eSIM プロファイルをアクティブ化することを示します。

次の図は、Mobile プラン iccid 情報とのバランスを追加するサポートをプログラミングする方法の大まかな流れを示します。

![Balancesequence ダイアグラムを追加する Mobile の計画](images/mobile_plans_add_balance_iccid_flow.png)

### <a name="mobileplansinlineoperationsnotifybalanceadditionpurchasemetadata-iccid"></a>MobilePlansInlineOperations.notifyBalanceAddition(purchaseMetaData, iccid)

| パラメーター名 | 種類 | 説明 |
| --- | --- | -- |
| purchaseMetadata | オブジェクト | このオブジェクトには、ユーザーの購入に関するメタデータが含まれています。 これが含まれています、ユーザー アカウント、purchase メソッドまたはインストルメント化に関する情報を詳細、新しい行で、ユーザーが購入したプランの名前、ユーザーを追加する場合。 これらすべては、レポートに使用されます。 |
| Iccid | String | 必要がある active 残高加算後 ICCID

| 戻り値の型 | 説明 |
| --- | --- |
| MobilePlansOperationContext | この一意のダウンロード操作にどの一致する識別子を持つオブジェクト。

プロファイルの ICCID がわかっている場合、残高加算記録はでも非アクティブなプロファイルを作成できます。 使用して、`MobilePlansInlineOperations.notifyBalanceAddition`と ICCID は Mobile は、残高加算のプランに通知するだけでなく Mobile プランが提供されている ICCID に対応するプロファイルにアクティブなプロファイルを切り替えます。

次の Javascript 関数は、残高加算が行われたアプリケーションを通知するために、API の例を示します。

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

参照してください[メタデータ プロパティを購入](#purchase-metadata-properties-details)詳細については、`puchaseMetadata`オブジェクト。

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

参照してください[メタデータ プロパティを購入](#purchase-metadata-properties-details)詳細については、`puchaseMetadata`オブジェクト。

## <a name="purchase-metadata-properties-details"></a>購入のメタデータ プロパティの詳細

次の表では、購入のメタデータで使用される詳細情報について説明します。

| プロパティ名 | 型 | 説明 | 例 |
| --- | --- | --- | --- |
| userAccount | String | 設定可能な値: <ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "userAccount":"New" |
| purchaseInstrument | String | 設定可能な値: <ul><li>新規:新しいユーザー アカウントがユーザーによって作成されたことを示します。</li><li>既存の。既存のユーザー アカウントでユーザーをログオンすることを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "purchaseInstrument":"New" |
| 行 | String | 設定可能な値: <ul><li>新規:ユーザー アカウントは、SIM カードが追加されたことを示します。</li><li>既存の。ユーザーがデバイスに既存の行を転送することを示します。</li><li>内緒。ユーザーがこの手順で購入のフローを終了したことを示します。</li><li>None:ユーザーがこのステップに到達していないことを示します。</li></ul> | "line":New" |
| moDirectStatus | String | 設定可能な値: <ul><li>完了します。ユーザーが購入を正常に完了したことを示します。</li><li>サービス エラー:ユーザーが月のサービス エラーのための購入を完了できなかったことを示します。</li><li>InvalidSIM:ポータルに渡される ICCID が正しいことを示します。</li><li>LogOnFailed: は、ユーザーが、MO ポータルへのログインに失敗したことを示します。</li><li>PurchaseFailed:課金エラーのために、購入が失敗したことを示します。</li><li>ClientError。引数が無効ですが、ポータルに渡されたことを示します。</li>BillingError:ユーザーの課金でエラーがあったことを示します。</li></ul> | "moDirectStatus":"Complete" |
| プラン名 | String | 成功したトランザクションでは、このフィールドは空にする必要がありますは、プランのわかりやすい名前を指定する必要があります。 失敗したトランザクションでは、このフィールドは空の文字列を指定する必要があります。 | 「プラン名」:"2 GB 毎月"|

## <a name="legacy-callback-notifications"></a>レガシ コールバック通知

従来のすべてのコールバックが記載されている特定のページを参照してください[ここ](mobile-plans-legacy-callback-notifications.md)
