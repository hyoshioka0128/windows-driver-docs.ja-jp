---
title: デバイスとサービスの検査のシナリオ
description: デバイスとサービスの検査のシナリオ
ms.assetid: 25e6ed92-e01c-4349-a614-b71bb08d71cd
keywords:
- WSDBIT ツール WDK、テストシナリオ
- WSDAPI 基本的な相互運用性ツール WDK、テストシナリオ
- WDK WSDBIT のシナリオ
- テストシナリオの WDK WSDBIT
- デバイスとサービスの検査のシナリオ WDK WSDBIT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03e99fa225a7d6784529272b413b81f406c5558c
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769628"
---
# <a name="device-and-service-inspection-scenarios"></a>デバイスとサービスの検査のシナリオ


デバイスとサービスの検査シナリオでは、デバイス検出とそれ以降のデバイスとサービス検査をテストします。

デバイスとホステッドサービスの基本的な検出は、残りのシナリオのインフラストラクチャを提供します。

デバイスは、検出のために、wsd: **anyURI testdevice**を**wsd: スコープ**要素として使用する必要があります。

次の表で、このシナリオについて説明します。

ステップクライアントアクションサーバーアクション成功-失敗条件**1.1**

**TestDevice ブートの \\ シャットダウン**

1.1.1

Nothing

TestDevice が起動し、Hello が送信されます。

クライアントで Hello が正しく受信されました。

1.1.2

Nothing

TestDevice がシャットダウンし、Bye を送信します。

Bye がクライアントで正しく受信されました。 **Wsa: EndpointReference/wsa: アドレス**は、手順1.1.1 で使用したものと同じである必要があります。

1.1.3

Nothing

TestDevice が再び開始され、Hello が送信されます。

Hello は、1.1.1 で同じメタデータバージョンを使用して正常に受信されました。 **Wsa: EndpointReference/wsa: アドレス**は、手順1.1.1 で使用したものと同じである必要があります。

**1.2**

**TestDevice の解決**

1.2.1

解決策を送信します。

ResolveMatches を使用して応答します。

手順1.2.2 に進みます。

1.2.2

GetMetadaRequest を TestDevice に送信します。

GetMetadatResponse で応答します。

手順1.2.3 に進みます。

1.2.3

このデバイスのメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.2.4

このモデルメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.2.5

Host、HostedService、EndpointReference を表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.2.6

Urn: uuid: 00000000-0000-0000-0000-000000000000 の解決策を送信します (これは、デバイスの**wsa: EndpointReference/wsa: アドレス**です)。

Nothing。 デバイスがこの**wsa: EndpointReference/wsa: アドレス**と一致しないため、応答しません。

サーバーは、どの ResolveMatches メッセージでも応答しません。

**1.3**

**TestDevice のプローブ**

1.3.1

ワイルドカードプローブを送信します。

-   既定の照合ルールを使用します。

-   **Wsd: Types**要素がありません。

-   **Wsd: スコープ**要素がありません。

ProbeMatches を使用して応答します。

手順 1.3.2 (または 1.3.3) にアクセスします。

1.3.2 (省略可能)。 この手順が必要なのは、1.3.1 の ProbeMatches に**wsd: XAddrs**が指定されていない場合のみです)。

1.2.1 から ProbeMatches に指定されている**wsa: EndpointReference/wsa: Addres**s に解決策を送信します。

ResolveMatches を使用して応答します。

手順1.3.3 に進みます。

1.3.3

GetMetadataRequest を TestDevice に送信します。

GetMetadataResponse で応答します。

手順1.3.4 に進みます。

1.3.4

このデバイスのメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.3.5

このモデルメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.3.6

Host、HostedService、EndpointReference を表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.3.7

次のものを指定するプローブを送信します。

-   既定の照合ルールを使用します。

-   照合する型: **wsdp: Device**。 (.上記の名前空間の表と、Web サービスのデバイスプロファイルの R1020 を参照してください。)

-   Wsd: スコープ要素がありません。

ProbeMatches を使用して応答します。

**Wsa: EndpointReference/wsa: アドレス**の値は、手順1.2.1 と同じです。

1.3.8

次のものを指定するプローブを送信します。

-   [Web サービスの動的検出 (ws-atomictransaction)](http://schemas.xmlsoap.org/ws/2005/04/discovery/)仕様で定義されている照合ルールを使用します。

-   Wsd: Types 要素がありません。

-   スコープの*testdevice*として次を使用します。

ProbeMatches を使用して応答します。

**Wsa: EndpointReference/wsa: アドレス**の値は、手順1.2.1 と同じです。

1.3.9

次のものを指定するプローブを送信します。

-   [Web サービス照合ルールのデバイスプロファイル](http://schemas.xmlsoap.org/ws/2006/02/devprof/)を使用します。

-   **Wsd: Types**要素がありません。

-   スコープの*Testdevice*として次を使用します。

Nothing。 このテストは、ProbeMatches では応答しません。

メッセージは受信されません。10秒間待機します。

1.3.10

次のものを指定するプローブを送信します。

-   既定の照合ルールを使用します。

-   次のように、架空の型を使用して照合します (例:) http://example.org/this/wont/work:Device) 。

-   **Wsd: スコープ**要素がありません。

Nothing。 このテストは、ProbeMatches では応答しません。

メッセージは受信されません。10秒間待機します。

**1.4**

**指示されたプローブ**

1.4.1

ワイルドカードプローブを HTTP 要求として送信します。

-   既定の照合ルールを使用します。

-   **Wsd: Types**要素がありません。

-   **Wsd: スコープ**要素がありません。

-   HTTP アドレスが指定されています。

HTTP 応答を使用する ProbeMatches で応答します。

TestDevice の**wsa: EndpointReference/wsa: アドレス**が正しいことを確認します。

**1.5**

**検出せずにメタデータを取得する**

1.5.1

GetMetadataRequest を TestDevice に送信します。

GetMetadataResponse で応答します。

手順1.5.2 に進みます。

1.5.2

このデバイスのメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.5.3

このモデルメタデータを表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

1.5.4

Host、HostedService、EndpointReference を表示します。

Nothing

送信された内容に対応します。 クライアント出力の例については、「[サンプルメタデータ応答の出力](sample-metadata-response-output.md)」を参照してください。

 

 

 





