---
title: イベント処理のシナリオ
description: イベント処理のシナリオ
ms.assetid: 6f7832ed-2b0b-4857-b47e-7db492a53855
keywords:
- WSDBIT ツール WDK、テスト シナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テスト シナリオ
- WDK WSDBIT のシナリオ
- WDK WSDBIT のシナリオをテストします。
- イベント処理シナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3eaf46b6a30cdc2684a373b2c746c7d655ec174
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549076"
---
# <a name="eventing-scenarios"></a>イベント処理のシナリオ


制約付きのイベント処理のシナリオ テスト イベントを[デバイス プロファイルの Web サービス (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)します。

このシナリオの目的は、ホストされるサービス エンドポイントの検出ではありません。 このシナリオは、これらのエンドポイントが検出されたか、このシナリオを開始する前に指定されたことを想定しています。

物理アドレスと仮想のアドレス型のこのようなシナリオのために、NotifyTo とツー アドレスの形式があります**uuid: f014e8aa-fc6a-49f5-b862-1e53663a85ff**します。

詳細についてでの初期テスト デバイス設定のダイアグラムを参照してください。[テスト環境の WSDBIT](wsdbit-testing-environment.md)します。

クライアント アクション サーバー アクションの不合格条件の場合**4.1**

**サブスクリプションとイベントの更新。**

4.1.1

SimpleEvent をサブスクライブします。

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

クライアントは、型の有効期限を含めることができます**xs:duration**します。

4.1.2 の手順を完了するのに十分な時間、有効期限を持つ SubscribeResponse を送信します。 型の有効期限がある必要があります**xs:duration**します。

このテストで、サーバーは同じを使用する必要ありませんが**xs:duration**クライアントからの要求に応じて。

クライアントは、応答を受け取り、4.1.2 の手順に進むことができます。

4.1.2

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

4.1.3

送信は、SimpleEvent を更新します。

イベントの更新をクライアントに送信、更新を手動で開始または元の SubscribeResponse メッセージで指定された更新期間の半分が経過すると、更新を自動的に送信するよう選択できます。

4.1.4 の手順を完了するのに十分な時間、有効期限を持つ RenewResponse を送信します。 型の有効期限がある必要があります**xs:duration**します。

応答は、クライアント側で受信され、4.1.4 の手順に進むことができます。

4.1.4

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

4.1.5

送信する、TestDevice、SimpleEvent の購読を解除します。

UnsubscribeResponse、送信します。

クライアントは、応答を受け取り、4.1.6 の手順に進むことができます。

4.1.6

なし

SimpleEvent に発生します。

クライアントでは、イベントは受信されません。

**4.2**

**切れのサブスクリプション**

4.2.1

有効期限が SimpleEvent をサブスクライブしています。

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

- 有効期間は、4.2.2 の手順を完了するのに十分な時間である必要があります。 有効期限があります。 **xs:duration**します。

wsdbit\_クライアントは、期間として 60 分を使用します。

SubscribeResponse に送信します。

-   サブスクリプションの要求で送信された有効期限、SubscribeResponse が返されます。

クライアントは、適切な有効期限が切れると、応答を受け取り、4.2.2 の手順に進むことができます。

4.2.2

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

4.2.3

TestDevice にその SimpleEvent サブスクリプションの有効期限の更新を送信します。 有効期間は 4.2.4 の手順を完了するのに十分な時間である必要があります。 有効期限があります。 **xs:duration**します。

イベントの更新をクライアントに送信、更新を手動で開始または元の SubscribeResponse メッセージで指定された更新期間の半分が経過すると、更新を自動的に送信するよう選択できます。

RenewResponse を送信します。

-   書き換え要求で送信された有効期限、RenewResponse が返されます。

クライアントは、適切な有効期限を含む応答を受け取り、4.2.4 の手順に進むことができます。

4.2.4

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

**4.3**

**サブスクリプション、更新、複数のイベント ソースの切れ**

4.3.1

SimpleEvent をサブスクライブしています。

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

クライアントは、型の有効期限を含めるように選択できる**xs:duration**します。

4.3.3 の手順を完了するのに十分な時間、有効期限を持つ SubscribeResponse を送信します。 Xs:duration 型の有効期限があります。

このテストで、サーバーは同じを使用する必要ありませんが**xs:duration**クライアントからの要求に応じて。

クライアントは、応答を受け取り、4.3.3 の手順に進むことができます。

4.3.2

SimpleEvent をサブスクライブします。

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/IntegerEvent**

クライアントは、型の有効期限を含めるように選択できる**xs:duration**します。

4.3.4 の手順を完了するのに十分な時間、有効期限を持つ SubscribeResponse を送信します。 型の有効期限がある必要があります**xs:duration**します。

このテストで、サーバーは同じを使用する必要ありませんが**xs:duration**クライアントからの要求に応じて。

クライアントは、応答を受け取り、4.3.4 の手順に進むことができます。

4.3.3

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

4.3.4

なし

IntegerEvent に発生します。

クライアント側でイベントを受信して、適切な整数が表示されます。

4.3.5

送信は、IntegerEvent を更新します。

イベントの更新をクライアントに送信、更新を手動で開始または元の SubscribeResponse メッセージで指定された更新期間の半分が経過すると、更新を自動的に送信するよう選択できます。

4.3.8 の手順を完了するのに十分な時間、有効期限を持つ RenewResponse を送信します。 型の有効期限がある必要があります**xs:duration**します。

クライアント側で応答を受信します。

4.3.6

送信する、TestDevice、SimpleEvent の購読を解除します。

UnsubscribeResponse、送信します。

クライアントは、応答を受け取り、4.3.7 の手順に進むことができます。

4.3.7

なし

SimpleEvent に発生します。

クライアントでは、イベントは受信されません。

4.3.8

なし

IntegerEvent に発生します。

クライアント側でイベントを受信して、適切な整数が表示されます。

4.3.9

送信する、TestDevice、IntegerEvent の購読を解除します。

UnsubscribeResponse、送信します。

クライアントは、応答を受け取り、4.3.10 の手順に進むことができます。

4.3.10

なし

IntegerEvent に発生します。

クライアントでは、イベントは受信されません。

**4.4**

**サブスクリプション エラーとエラー**

4.4.1

FaultingEvent をサブスクライブします。

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/FaultingEvent**

このイベントがサポートされていないため、 **wsdp:FilterActionNotSupported** SOAP エラーを送信する必要があります。

クライアントでサブスクライブする障害が発生します。

 

 

 





