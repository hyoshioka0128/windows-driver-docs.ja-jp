---
title: イベント処理のシナリオ
description: イベント処理のシナリオ
ms.assetid: 6f7832ed-2b0b-4857-b47e-7db492a53855
keywords:
- WSDBIT ツール WDK、テストシナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テストシナリオ
- WDK WSDBIT のシナリオ
- テストシナリオの WDK WSDBIT
- イベントのシナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25edfccde1af22ac3d58f705f715f3fcac91430d
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769560"
---
# <a name="eventing-scenarios"></a>イベント処理のシナリオ


イベントのシナリオでは、 [Web サービス (DPWS) のデバイスプロファイル](http://schemas.xmlsoap.org/ws/2005/05/devprof/)で制限されているように、イベントをテストします。

このシナリオの目的は、ホステッドサービスのエンドポイントを検出することではありません。 このシナリオでは、このシナリオを開始する前に、これらのエンドポイントが検出または提供されているものとします。

これらのシナリオでは、NotifyTo と EndTo のアドレス形式は、 **uuid: f014e8aa-fc6a-49f5-b862-1e53663a85ff**型の仮想アドレスではなく、物理アドレスである必要があります。

詳細については、「 [WSDBIT テスト環境](wsdbit-testing-environment.md)での初期テストデバイスのセットアップ図」を参照してください。

ケース: クライアントアクションサーバーアクション成功-失敗基準**4.1**

**イベントのサブスクリプションと更新。**

4.1.1

SimpleEvent をサブスクライブする:

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse: Filter = =http://schemas.example.org/EventingService/SimpleEvent**

クライアントには、 **xs: duration**型の有効期限を含めることができます。

手順4.1.2 を完了するのに十分な有効期限の SubscribeResponse を送信します。 有効期限は**xs: duration**型にする必要があります。

このテストでは、クライアントから要求されたのと同じ**xs: duration**をサーバーで使用する必要はありません。

クライアントは応答を受信し、手順4.1.2 に進みます。

4.1.2

Nothing

SimpleEvent を発生させます。

イベントはクライアント側で受信されます。

4.1.3

更新を SimpleEvent に送信します。

クライアントがイベントの更新を送信する場合、元の SubscribeResponse メッセージに指定されている更新期間の半分が経過すると、更新を手動で開始するか、自動的に更新を送信するかを選択できます。

手順4.1.4 を完了するのに十分な有効期限がある RenewResponse を送信します。 有効期限は**xs: duration**型にする必要があります。

応答はクライアント側で受信され、手順4.1.4 に進むことができます。

4.1.4

Nothing

SimpleEvent を発生させます。

イベントはクライアント側で受信されます。

4.1.5

SimpleEvent の TestDevice にサブスクライブ解除を送信します。

UnsubscribeResponse を送信します。

クライアントは応答を受信し、手順4.1.6 に進むことができます。

4.1.6

Nothing

SimpleEvent を発生させます。

クライアントでイベントが受信されません。

**4.2**

**Expiries を使用したサブスクリプション**

4.2.1

の有効期限がある SimpleEvent をサブスクライブします。

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse: Filter = =http://schemas.example.org/EventingService/SimpleEvent**

- 有効期限は、手順4.2.2 を完了するのに十分な長さである必要があります。 有効期限は、 **xs: duration**にする必要があります。

wsdbit \_ client は、期間として60分を使用します。

次のように SubscribeResponse を送信します。

-   サブスクリプション要求で送信された有効期限は、SubscribeResponse に返されます。

クライアントは、正しい有効期限を持つ応答を受信し、手順4.2.2 に進むことができます。

4.2.2

Nothing

SimpleEvent を発生させます。

イベントはクライアントで受信されます。

4.2.3

SimpleEvent サブスクリプションの TestDevice に期限切れの更新を送信します。 有効期限は、手順4.2.4 を完了するのに十分な長さである必要があります。 有効期限は、 **xs: duration**にする必要があります。

クライアントがイベントの更新を送信する場合、元の SubscribeResponse メッセージに指定されている更新期間の半分が経過すると、更新を手動で開始するか、自動的に更新を送信するかを選択できます。

次のものと共に RenewResponse を送信します。

-   更新要求で送信された有効期限は、RenewResponse で返されます。

クライアントは正しい有効期限で応答を受信するため、手順4.2.4 に進むことができます。

4.2.4

Nothing

SimpleEvent を発生させます。

イベントはクライアントで受信されます。

**4.3**

**複数のイベントソースのサブスクリプション、更新、expiries**

4.3.1

で SimpleEvent をサブスクライブします

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse: Filter = =http://schemas.example.org/EventingService/SimpleEvent**

クライアントは、 **xs: duration**型の有効期限を含めることを選択できます。

手順4.3.3 を完了するのに十分な有効期限の SubscribeResponse を送信します。 有効期限は xs: duration 型にする必要があります。

このテストでは、クライアントから要求されたのと同じ**xs: duration**をサーバーで使用する必要はありません。

クライアントは応答を受信し、手順4.3.3 に進むことができます。

4.3.2

SimpleEvent をサブスクライブする:

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse: Filter = =http://schemas.example.org/EventingService/IntegerEvent**

クライアントは、 **xs: duration**型の有効期限を含めることを選択できます。

手順4.3.4 を完了するのに十分な有効期限の SubscribeResponse を送信します。 有効期限は**xs: duration**型にする必要があります。

このテストでは、クライアントから要求されたのと同じ**xs: duration**をサーバーで使用する必要はありません。

クライアントは応答を受信し、手順4.3.4 に進むことができます。

4.3.3

Nothing

SimpleEvent を発生させます。

イベントはクライアントで受信されます。

4.3.4

Nothing

整数のイベントを発生させます。

クライアントでイベントを受信し、正しい整数が表示されます。

4.3.5

更新を整数のイベントに送信します。

クライアントがイベントの更新を送信する場合、元の SubscribeResponse メッセージに指定されている更新期間の半分が経過すると、更新を手動で開始するか、自動的に更新を送信するかを選択できます。

手順4.3.8 を完了するのに十分な有効期限がある RenewResponse を送信します。 有効期限は**xs: duration**型にする必要があります。

応答はクライアント側で受信されます。

4.3.6

SimpleEvent の TestDevice にサブスクライブ解除を送信します。

UnsubscribeResponse を送信します。

クライアントは応答を受信し、手順4.3.7 に進むことができます。

4.3.7

Nothing

SimpleEvent を発生させます。

クライアントでイベントが受信されません。

4.3.8

Nothing

整数のイベントを発生させます。

クライアントでイベントを受信し、正しい整数が表示されます。

4.3.9

整数のイベントの TestDevice にサブスクライブ解除を送信します。

UnsubscribeResponse を送信します。

クライアントは応答を受信し、手順4.3.10 に進むことができます。

4.3.10

Nothing

整数のイベントを発生させます。

クライアントでイベントが受信されません。

**4.4**

**サブスクリプションの失敗とエラー**

4.4.1

次のものを使用して FaultingEvent をサブスクライブします。

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse: Filter = =http://schemas.example.org/EventingService/FaultingEvent**

このイベントはサポートされていないため、 **wsdp: FilterActionNotSupported** SOAP エラーを送信する必要があります。

サブスクライブに失敗した場合は、クライアントで確認されます。

 

 

 





