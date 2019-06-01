---
title: 従来のコールバック通知をモバイル プラン
description: このトピックでは、プランのモバイル アプリで通知をサポートするコールバックをについて説明します
ms.assetid: 5077A3EA 379C 4EB5 A05B BA1585E9594D
keywords:
- Windows Mobile プラン レガシ コールバック通知、モバイル プラン レガシ実装モバイル演算子
ms.date: 05/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6559d5e8437163f25bfc7cd5ca10fcc70d8d4209
ms.sourcegitcommit: 335096107bfc92718d9ba809527214113c993da7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2019
ms.locfileid: "66455867"
---
# <a name="mobile-plans-legacy-callback-notifications"></a>従来のコールバック通知をモバイル プラン

> [!NOTE]
> このページは、従来のコールバック通知を Mobile 計画を説明します。 この参照のみを使用してくださいと今後このコードを実装していません。

## <a name="inline-profile-delivery"></a>インラインのプロファイルの配信

次の図は、コントロール、MODirect ポータルを離れることがなく、プロファイルをダウンロード、Mobile プラン プログラムをサポートする方法の大まかな流れを示します。

![インラインのプロファイルのダウンロード シーケンス図を Mobile の計画](images/dynamo_inline_profile_flow.PNG)

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

参照してください[メタデータ プロパティを購入](mobile-plans-callback-notifications.md#purchase-metadata-properties-details)詳細については、`puchaseMetadata`オブジェクト。

## <a name="adding-balance-legacy"></a>追加の残高 (レガシ)

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

参照してください[メタデータ プロパティを購入](mobile-plans-callback-notifications.md#purchase-metadata-properties-details)詳細については、`puchaseMetadata`オブジェクト。

## <a name="other-legacy-callback-notifications"></a>その他のレガシ コールバック通知

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
