---
title: セキュリティで保護された通信のシナリオ
description: セキュリティで保護された通信のシナリオ
ms.assetid: 0273f4e7-0b93-4ab1-8564-e51c14e91243
keywords:
- WSDBIT ツール WDK、テスト シナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テスト シナリオ
- WDK WSDBIT のシナリオ
- WDK WSDBIT のシナリオをテストします。
- セキュリティで保護された通信のシナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c40b21e295c17d62e4f2894e4fe3b65dfb27fa47
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340116"
---
# <a name="secure-communication-scenarios"></a>セキュリティで保護された通信のシナリオ


セキュリティで保護された通信のシナリオは、セキュリティで保護されたチャネルを使用して、検出、メタデータ交換、およびイベント処理をテストします。

これらのシナリオを試行する前にする必要がありますが正常に完了して、[デバイスとサービスの検査](device-and-service-inspection-scenarios.md)と[Eventing](eventing-scenarios.md)シナリオ。

これらの相互運用性のテスト_ケースを試行する前に、次を参照してください。[をセキュリティで保護されたチャネルを使用して WSDAPI](https://go.microsoft.com/fwlink/p/?linkid=81271)と[WSDAPI アプリケーションをセキュリティで保護されたチャネルを使用する構成](https://go.microsoft.com/fwlink/p/?linkid=81272)セキュリティで保護されたチャネルの詳細についてはします。

クライアント アクション サーバー アクションの不合格条件の場合**5.1**

**セキュリティで保護されたデバイスのプローブを呼び出す**

5.1.1

ワイルドカードのプローブを送信

-   既定の照合ルールを使用します。

-   いいえ**wsd:Types**要素。

-   いいえ**wsd:Scopes**要素。

ProbeMatches で応答します。

**注**  場合、 **wsd:XAddrs**は省略すると、このアドレスは https URI を指定する必要があります、 **wsa:EndpointReference/wsa: アドレス**と同じである必要があります、 **wsd:XAddrs**します。

 

5.1.2 (または 5.1.3) の手順に進みます。

5.1.2\[オプション

この手順は 5.1.1 で ProbeMatches で wsd:XAddrs が指定されていない場合にのみ\]

すると解決の送信、 **wsa:EndpointReference/wsa: アドレス**1.2.1 から ProbeMatches が指定されています。

ResolveMatches で応答します。

**注**   、 **wsd:XAddrs** https URI にする必要があります、 **wsa:EndpointReference/wsa: アドレス**と同じである必要があります、 **wsd:XAddrs**します。

 

5.1.3 の手順に進みます。

5.1.3

TestDevice、GetMetadataRequest を送信します。

GetMetadataResponse で応答します。

5.1.4 の手順に進みます。

5.1.4

ThisDevice メタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、次を参照してください。[メタデータ応答のサンプル出力](sample-metadata-response-output.md)します。

5.1.5

ようなモデルのメタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、次を参照してください。[メタデータ応答のサンプル出力](sample-metadata-response-output.md)します。

5.1.6

ホスト、HostedService、EndpointReference を表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、次を参照してください。[メタデータ応答のサンプル出力](sample-metadata-response-output.md)します。

**5.2**

**セキュリティで保護されたデバイスに有向プローブ**

5.2.1

ワイルドカードとして HTTPS プローブ要求を送信します。

-   既定の照合ルールを使用します。

-   wsd:Types 要素がないです。

-   wsd:Scopes 要素がないです。

-   HTTP アドレスを指定します。

HTTPS 応答を使用する ProbeMatches で応答します。

**注**  場合、 **wsd:XAddrs**は省略すると、このアドレスは https URI を指定する必要があります、 **wsa:EndpointReference/wsa: アドレス**と同じである必要があります、 **wsd:XAddrs**します。

 

いることを確認、 **wsa:EndpointReference/wsa: アドレス**TestDevice が正しい。

**5.3**

**サブスクリプションとイベントをセキュリティで保護されたデバイスの更新**

セキュリティで保護されたデバイスの検出は、5.1、5.2 にテストするメソッドを使用して決定されます。

5.3.1

SimpleEvent をサブスクライブします。

- **wse:Filter/@Dialect == "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse:Filter == http://schemas.example.org/EventingService/SimpleEvent**

クライアントは、型の有効期限を含めるように選択できる**xs:duration**します。

5.3.2 の手順を完了するのに十分な時間、有効期限を持つ SubscribeResponse を送信します。 型の有効期限がある必要があります**xs:duration**します。

このテストで、サーバーは同じを使用する必要ありませんが**xs:duration**クライアントからの要求に応じて。

クライアントは、応答を受け取り、5.3.2 の手順に進むことができます。

5.3.2

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

5.3.3

送信は、SimpleEvent を更新します。

イベントの更新をクライアントに送信、更新を手動で開始または元の SubscribeResponse メッセージで指定された更新期間の半分が経過すると、更新を自動的に送信するよう選択できます。

5.3.4 の手順を完了するのに十分な時間、有効期限を持つ RenewResponse を送信します。 型の有効期限がある必要があります**xs:duration**します。

応答は、クライアント側で受信され、5.3.4 の手順に進むことができます。

5.3.4

なし

SimpleEvent に発生します。

クライアント側でイベントを受信します。

5.3.5

送信する、TestDevice、SimpleEvent の購読を解除します。

UnsubscribeResponse、送信します。

クライアントは、応答を受け取り、5.3.6 の手順に進むことができます。

5.3.6

なし

SimpleEvent に発生します。

クライアントでは、イベントは受信されません。

 

 

 





