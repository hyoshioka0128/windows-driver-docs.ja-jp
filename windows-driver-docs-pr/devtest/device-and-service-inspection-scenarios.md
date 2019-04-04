---
title: デバイスとサービスの検査のシナリオ
description: デバイスとサービスの検査のシナリオ
ms.assetid: 25e6ed92-e01c-4349-a614-b71bb08d71cd
keywords:
- WSDBIT ツール WDK、テスト シナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テスト シナリオ
- WDK WSDBIT のシナリオ
- WDK WSDBIT のシナリオをテストします。
- デバイスとサービスの検査シナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee6870686ffc84ece4e16b5dc6b522defddff198
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580975"
---
# <a name="device-and-service-inspection-scenarios"></a>デバイスとサービスの検査のシナリオ


デバイスとサービスの検査のシナリオでは、デバイスの検出とそれ以降のデバイスとサービスの検査をテストします。

デバイスとホスト型サービスの探索の基本的なシナリオの残りの部分のインフラストラクチャを提供します。

デバイスを使用する必要があります**xs:anyURI testdevice**として、 **wsd:Scopes**検出用の要素。

次の表では、このシナリオについて説明します。

クライアント アクション サーバー アクションの不合格条件ステップ**1.1**

**TestDevice ブート\\シャット ダウン**

1.1.1

なし

TestDevice は起動し、こんにちはを送信します。

こんにちはクライアントで正常に受信します。

1.1.2

なし

TestDevice はシャット ダウンされ、Bye を送信します。

クライアントで正常に受信 bye します。 **Wsa:EndpointReference/wsa: アドレス**1.1.1 の手順で使用されるものと同じである必要があります。

1.1.3

なし

TestDevice では、もう一度起動し、こんにちはを送信します。

こんにちは 1.1.1 で同じメタデータのバージョンで正常に受信します。 **Wsa:EndpointReference/wsa: アドレス**1.1.1 の手順で使用されるものと同じである必要があります。

**1.2**

**解決するには、TestDevice の**

1.2.1

解決を送信します。

ResolveMatches で応答します。

1.2.2 の手順に進みます。

1.2.2

TestDevice、GetMetadaRequest を送信します。

GetMetadatResponse で応答します。

1.2.3 の手順に進みます。

1.2.3

ThisDevice メタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.2.4

ようなモデルのメタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.2.5

ホスト、HostedService、EndpointReference を表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.2.6

Urn: uuid:00000000 の解決の送信-0000-0000-0000-000000000000 (これは、i、 **wsa:EndpointReference/wsa: アドレス**デバイスの)。

なし。 このデバイスに一致しないため**wsa:EndpointReference/wsa: アドレス**も応答する必要があります

サーバーは、任意の ResolveMatches メッセージで応答しません。

**1.3**

**TestDevice のプローブ**

1.3.1

ワイルドカードのプローブを送信するには。

-   既定の照合ルールを使用します。

-   いいえ**wsd:Types**要素。

-   いいえ**wsd:Scopes**要素。

ProbeMatches で応答します。

1.3.2 (または 1.3.3) の手順に進みます。

1.3.2 (省略可能です。 この手順は場合にのみ必要ない**wsd:XAddrs** 1.3.1 の ProbeMatches が指定されました)。

すると解決の送信、 **wsa:EndpointReference/wsa:Addres**1.2.1 から ProbeMatches で指定されています。

ResolveMatches で応答します。

1.3.3 の手順に進みます。

1.3.3

TestDevice、GetMetadataRequest を送信します。

GetMetadataResponse で応答します。

1.3.4 の手順に進みます。

1.3.4

ThisDevice メタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.3.5

ようなモデルのメタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.3.6

ホスト、HostedService、EndpointReference を表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.3.7

次を指定するプローブを送信するには。

-   既定の照合ルールを使用します。

-   一致する型: **wsdp:Device**します。 (.参照名前空間、上の表と、デバイス プロファイルで R1020 Web サービス用)。

-   Wsd:Scopes 要素がありません。

ProbeMatches で応答します。

値、 **wsa:EndpointReference/wsa: アドレス**1.2.1 手順と同様です。

1.3.8

次を指定するプローブを送信するには。

-   使用されている、対応するルールが定義されている、 [Web Services Dynamic Discovery (Ws-discovery)](https://go.microsoft.com/fwlink/p/?linkid=81240)仕様。

-   Wsd:Types 要素がありません。

-   次を使用して、スコープとして*testdevice*します。

ProbeMatches で応答します。

値、 **wsa:EndpointReference/wsa: アドレス**1.2.1 手順と同様です。

1.3.9

次を指定するプローブを送信するには。

-   使用して、 [Web サービスのデバイス プロファイル](https://go.microsoft.com/fwlink/p/?linkid=163864)照合ルール。

-   いいえ**wsd:Types**要素。

-   次を使用して、スコープとして*testDEVICE*します。

なし。 このテストは、ProbeMatches に応答しません。

メッセージは受信されませんでした。10 秒間待ちます。

1.3.10

次を指定するプローブを送信するには。

-   既定の照合ルールを使用します。

-   照合する架空の型を使用して、: (たとえば、 http://example.org/this/wont/work:Device)します。

-   いいえ**wsd:Scopes**要素。

なし。 このテストは、ProbeMatches に応答しません。

メッセージは受信されませんでした。10 秒間待ちます。

**1.4**

**有向プローブ**

1.4.1

HTTP 要求としてワイルドカード プローブを送信します。

-   既定の照合ルールを使用します。

-   いいえ**wsd:Types**要素。

-   いいえ**wsd:Scopes**要素。

-   HTTP アドレスを指定します。

HTTP 応答を使用する ProbeMatches で応答します。

いることを確認、 **wsa:EndpointReference/wsa: アドレス**TestDevice が正しい。

**1.5**

**検出なしのメタデータの取得**

1.5.1

TestDevice、GetMetadataRequest を送信します。

GetMetadataResponse で応答します。

1.5.2 の手順に進みます。

1.5.2

ThisDevice メタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.5.3

ようなモデルのメタデータを表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

1.5.4

ホスト、HostedService、EndpointReference を表示します。

なし

送信された内容に対応します。 クライアントからの出力の例は、[メタデータ応答のサンプル出力](sample-metadata-response-output.md)を参照してください。

 

 

 





