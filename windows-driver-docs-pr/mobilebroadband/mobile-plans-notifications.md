---
title: モバイルプランの通知
description: このトピックでは、モバイルプランでトースト通知を構成する方法について説明します。
ms.assetid: 20A59FB6-9EEF-4B55-940C-79B6FB2C99CA
keywords:
- Windows Mobile プランのトースト通知
ms.date: 06/11/2019
ms.localizationpriority: medium
ms.openlocfilehash: 006b1ae5c513a35d3d10ebea26517a39558e7bfd
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948045"
---
# <a name="mobile-plans-notifications"></a>モバイルプランの通知

## <a name="overview"></a>概要

このトピックでは、携帯電話会社がエンドユーザーとの通信にテキストやイメージを使用してカスタマイズできる、モバイルプランでのトースト通知について説明します。 モバイルプランの通知は、 [Windows 10 のトースト通知フレームワーク](https://docs.microsoft.com/windows/uwp/design/shell/tiles-and-notifications/adaptive-interactive-toasts)に基づいています。

> [!Note]
> この機能の使用を計画する前に、Microsoft の担当者にお問い合わせください。

Mobile plan アプリでは、2種類のトースト通知の表示がサポートされています。SMS でトリガーされ、アプリケーションによってトリガーされます。

## <a name="sms-triggered-notifications"></a>SMS によってトリガーされる通知

携帯電話会社は、デバイスに SMS を送信することによって、ユーザーのデバイスに通知を表示するようにトリガーできます。 SMS の本文には、モバイルプランアプリにメッセージをルーティングする文字列識別子が含まれ、通知が表示されます。 この<accept>ボタンをクリックすると、モバイルプランアプリが起動し、携帯電話会社の[ゲートウェイページ](mobile-plans-gateway.md)が表示されます。

Mobile オペレーターは SMS を使用して通知をトリガーするため、デバイスにはアクティブなプロファイルがあり、SMS を受信できるように携帯ネットワークに登録されている必要があります。 デバイスは、通知コンテンツを要求するために、モバイルプランサービスへのデータアクセスを持っている必要もあります。

### <a name="sms-triggered-notification-content"></a>SMS によってトリガーされる通知コンテンツ

通知コンテンツは、事前に定義された要素を持つテンプレートを使用して、携帯電話会社がカスタマイズできます。 下の強調表示されている要素は、携帯電話会社が定義できます。

![SMS 通知テンプレート](images/mobile_plans_sms_notification_template.png)

[フィールド名] | 説明 | 例
---------- | ----------- | -------
通知の種類 | いくつかの事前定義済みの種類の SMS 通知がサポートされています。 各型は同じように動作します。 <accept> および<decline>ボタンに表示される文字列のみが、型に応じて変化します。 | 低残高、ゼロバランス、新しいプラン、試用プラン、試用期間終了、試用終了
[タイトル] | アクションに対する1行の呼び出し | "ほぼデータが不足しています"
本文 | エンドユーザーにオファリングの値を強調表示する短いメッセージ | "現在のデータプランでは、5 MB 未満です。 今すぐアクションを実行して、接続が維持されるようにしてください。 "
イメージ | 中心的な場所として PC を使用する、ライフスタイル指向の写真。 画像サイズは 100% のスケーリングで 364x180 ピクセルです。 | https://picsum.photos/id/1/364/180
ロゴ | これは、オンボード中に提供される資産の一部です。 | 

### <a name="sample-sms-triggered-notification"></a>SMS によってトリガーされる通知の例

![SMS 通知のサンプル](images/mobile_plans_sms_notification_sample.png)

### <a name="using-multiple-notification-templates"></a>複数の通知テンプレートの使用

モバイルオペレーターには、複数の SMS 通知テンプレートを定義するオプションがあります。 この処理が完了すると、Mobile plan サービスは実行時に Mobile Operator API を呼び出して、通知に使用するテンプレートの ID を要求します。

要求にはデバイス上のアクティブなプロファイルの識別子が含まれるため、携帯電話事業者は、ユーザーセグメントごとに、または A/B テスト用に複数のテンプレートを定義できます。 SMS-通知は、モバイルプランアプリに表示されている[拡張ゲートウェイページ](mobile-plans-gateway.md#enhanced-gateway-page)と組み合わせて、高度な対象 campaings を作成することもできます。

通知の取得要求では、ユーザーに表示される通知に使用されるテンプレート ID が返されます。

![モバイルプランの通知の呼び出しフロー](images/mobile_plans_get_notifications_callflow.png)


### <a name="getnotifications-api-specification"></a>GetNotifications API の仕様
`GetOffers` API は、モバイルプランアプリケーションによって SMS メッセージの受信時に呼び出されます。 Mobile plan サービスは、この要求のプロキシです。

```HTTP
GET https://{notificationUri}sims/{simmri}/notifications
```

- *{notificationuri}* は、携帯電話会社のサービス構成の一部としてオンボード notificationuri 値です。

エンドポイントには、次の3つのクエリパラメーターがあります。
- [*制限*]。この値は必須で、返される通知の数を指定します。
- *imei*。クライアントの imei を指定します (省略可能)。
- *notificationType*。これは必須で、返される通知の種類を指定します。 *NotificationType*パラメーターは、常に、モバイルプランの [通知の取得] 要求で受け入れられる列挙された文字列の1つです。

応答は、通知のリストを含む notification という名前の1つのプロパティを持つ JSON オブジェクトです。 この一覧に表示される通知の数は、要求の*上限に達し*ています。 この一覧の各通知は、 *Notificationid*という単一のプロパティを持つオブジェクトです。このオブジェクトは、モバイルオペレーターのサービス構成で既存の通知を識別する必要があります。

このエンドポイントを使用した相互作用の例を次に示します。

```HTTP
GET https://moendpoint.com/v1/sims/iccid:8988247000100003319/notifications?notificationType=lowBalance&limit=1&imei=1234
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"

HTTP/1.1 200 OK
Content-type: application/json
X-MS-DM-TransactionId: "MSFT-12345678-1234-1234-1234-123456789abc"
{
  "notifications": [
    {
      "notificationId": 1,
      "notificationType": "lowBalance"
    }
  ]
}
```

## <a name="app-triggered-notifications"></a>アプリによってトリガーされる通知

また、一部の市場の携帯電話では、esim が有効になっている Windows 10 Pc で、eSIM プロファイルがインストールされていないプロモーション通知を表示することもできます。 プロモーション通知は、ユーザーがすぐに利用可能なエクスペリエンスでデバイスのセットアップを完了した直後に、アプリによってトリガーされます。 この<accept>ボタンをクリックすると、モバイルプランアプリが起動し、携帯電話会社の[ゲートウェイページ](mobile-plans-gateway.md)が表示されます。

### <a name="app-triggered-notification-content"></a>アプリによってトリガーされる通知コンテンツ

キャンペーンの通知コンテンツは、事前に定義された要素を持つテンプレートを使用して、携帯電話会社がカスタマイズできます。 下の強調表示されている要素は、携帯電話会社が定義できます。

![プロモーション通知テンプレート](images/mobile_plans_promo_notification_template.png)

[フィールド名] | 説明 | 例
---------- | ----------- | -------
[タイトル] | アクションに対する1行の呼び出し | "無料試用版をアクティブ化する"
本文 | エンドユーザーにオファリングの値を強調表示する短いメッセージ | "30 GB のフリーデータを入手して、どこからでも接続しておくことができます。"
イメージ | 中心的な場所として PC を使用する、ライフスタイル指向の写真。 画像の大きさは、100% のスケーリングで360x243 ピクセルです。 | https://picsum.photos/id/1/360/234
ロゴ | これは、オンボード中に提供される資産の一部です。 | 

通知[ビジュアライザーアプリ](https://www.microsoft.com/store/productId/9NBLGGH5XSL1)を使用して、通知コンテンツのモックアップとテストを行うことができます。

### <a name="sample-app-triggered-notification"></a>アプリによってトリガーされる通知のサンプル

![モバイルプランの通知例](images/mobile_plans_notifications.png)
