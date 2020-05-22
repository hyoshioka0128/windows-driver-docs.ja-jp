---
title: セキュリティで保護された通信のシナリオ
description: セキュリティで保護された通信のシナリオ
ms.assetid: 0273f4e7-0b93-4ab1-8564-e51c14e91243
keywords:
- WSDBIT ツール WDK、テストシナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テストシナリオ
- WDK WSDBIT のシナリオ
- テストシナリオの WDK WSDBIT
- セキュリティで保護された通信のシナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee9220c9d8634fa4f4209afe473d5d1fc01aa18e
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769676"
---
# <a name="secure-communication-scenarios"></a>セキュリティで保護された通信のシナリオ


セキュリティで保護された通信シナリオでは、セキュリティで保護されたチャネルを使用して、検出、メタデータ交換、およびイベントをテストします。

これらのシナリオを試行する前に、[デバイスとサービスの検査](device-and-service-inspection-scenarios.md)と[イベント](eventing-scenarios.md)のシナリオを正常に完了している必要があります。

一般的な WSDAPI 仕様準拠の詳細については、「 [Wsdapi 仕様準拠](https://docs.microsoft.com/windows/win32/wsdapi/wsdapi-specification-compliance)」を参照してください。

ケース: クライアントアクションサーバーアクション成功-失敗基準**5.1**

**セキュリティで保護されたデバイスのプローブを呼び出す**

5.1.1

ワイルドカードプローブを送信する

-   既定の照合ルールを使用します。

-   **Wsd: Types**要素がありません。

-   **Wsd: スコープ**要素がありません。

ProbeMatches を使用して応答します。

**メモ**   **Wsd: XAddrs**が指定されている場合、このアドレスは https URI で、 **wsa: EndpointReference/wsa: アドレス**は**wsd: XAddrs**と同じである必要があります。

 

手順 5.1.2 (または 5.1.3) にアクセスします。

5.1.2 \[ (オプション)

この手順は、5.1.1: XAddrs が5.1.1 の ProbeMatches に提供されていない場合にのみ必要です。\]

ProbeMatches で指定されている**wsa: EndpointReference/wsa: アドレス**に解決策を送信します。

ResolveMatches を使用して応答します。

**メモ**   **Wsd: XAddrs**は https URI で、 **wsa: EndpointReference/wsa: アドレス**は**wsd: XAddrs**と同じである必要があります。

 

手順5.1.3 に進みます。

5.1.3

GetMetadataRequest を TestDevice に送信します。

GetMetadataResponse で応答します。

手順5.1.4 に進みます。

5.1.4

このデバイスのメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

5.1.5

このモデルメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

5.1.6

Host、HostedService、EndpointReference を表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

**5.2**

**セキュリティで保護されたデバイスへのダイレクトプローブ**

5.2.1

次のものを使用して、ワイルドカードプローブを HTTPS 要求として送信します。

-   既定の照合ルールを使用します。

-   wsd: Types 要素がありません

-   wsd: スコープ要素がありません

-   HTTP アドレスが指定されています。

HTTPS 応答を使用する ProbeMatches で応答します。

**メモ**   **Wsd: XAddrs**が指定されている場合、このアドレスは https URI で、 **wsa: EndpointReference/wsa: アドレス**は**wsd: XAddrs**と同じである必要があります。

 

TestDevice の**wsa: EndpointReference/wsa: アドレス**が正しいことを確認します。

**5.3**

**セキュリティで保護されたデバイスに対するイベントのサブスクリプションと更新**

セキュリティで保護されたデバイスの検出は、5.1 または5.2 でテストされたメソッドを使用して決定されます。

5.3.1

SimpleEvent をサブスクライブする:

- **wse:Filter/@Dialect== "<http://schemas.xmlsoap.org/ws/2006/02/devprof/Action>"**

- **wse: Filter = =http://schemas.example.org/EventingService/SimpleEvent**

クライアントは、 **xs: duration**型の有効期限を含めることを選択できます。

手順5.3.2 を完了するのに十分な有効期限の SubscribeResponse を送信します。 有効期限は**xs: duration**型にする必要があります。

このテストでは、クライアントから要求されたのと同じ**xs: duration**をサーバーで使用する必要はありません。

クライアントは応答を受信し、手順5.3.2 に進むことができます。

5.3.2

Nothing

SimpleEvent を発生させます。

イベントはクライアント側で受信されます。

5.3.3

更新を SimpleEvent に送信します。

クライアントがイベントの更新を送信する場合、元の SubscribeResponse メッセージに指定されている更新期間の半分が経過すると、更新を手動で開始するか、自動的に更新を送信するかを選択できます。

手順5.3.4 を完了するのに十分な有効期限がある RenewResponse を送信します。 有効期限は**xs: duration**型にする必要があります。

応答はクライアント側で受信され、手順5.3.4 に進むことができます。

5.3.4

Nothing

SimpleEvent を発生させます。

イベントはクライアント側で受信されます。

5.3.5

SimpleEvent の TestDevice にサブスクライブ解除を送信します。

UnsubscribeResponse を送信します。

クライアントは応答を受信し、手順5.3.6 に進むことができます。

5.3.6

Nothing

SimpleEvent を発生させます。

クライアントでイベントが受信されません。

 

 

 





