---
title: WSDAPI Basic Interoperability Tool
description: WSDAPI Basic Interoperability Tool
ms.assetid: c4a610d4-3adf-406d-88d6-0879eb98b54f
keywords:
- WDK、ドライバーのテスト ツール
- WDK の WSDBIT ツール
- WSDAPI 基本的な相互運用性ツール WDK
- DWPS WDK
- WDK の Web サービス用のデバイス プロファイル
- デバイス API WDK 用の web サービス
- WSDAPI WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db83d5879d5cc8b4c1d66ea078c67e3dcd5d8c35
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358050"
---
# <a name="wsdapi-basic-interoperability-tool"></a>WSDAPI Basic Interoperability Tool


[デバイス プロファイルの Web サービス (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)は参照の仕様をアセンブルし、さまざまな Web サービス (WS) 仕様を制限します。 [Devices (WSD) での Web サービス](https://go.microsoft.com/fwlink/p/?linkid=163865)API (WSDAPI) は Windows に含まれている DPWS の実装です。 Windows では、WSDAPI を使用して、任意の型の DPWS デバイスを検出して、プリンター、スキャナー、およびネットワーク プロジェクターなどのいくつかのデバイス クラスをコントロール メッセージを発行する WSDAPI を使用しています。

Windows は WSDAPI 以外の DPWS スタックと相互運用することを確認するのには、WSDAPI の基本的な相互運用性ツール (WSDBIT) を使用できます。 このツールは、主にデバイス開発者 DPWS を実装して、Windows と相互運用性をテストしたいです。 いくつか WSDBIT テストでは、デバイスがなど、高度な DPWS 機能を実行するために使用する特別なテスト インターフェイスを実装する必要があります[SOAP Message Transmission Optimization Mechanism (MTOM)](https://go.microsoft.com/fwlink/p/?linkid=81254) (に使用されるメッセージ添付ファイル) と[Web サービスのイベント処理](https://go.microsoft.com/fwlink/p/?linkid=81245)します。 これらのインターフェイスが必須ではありません。 ただしは WSDBIT でこの機能をカバーする唯一の方法です。

WSDAPI は、仕様のセクションでは、クライアントとデバイスの両方を実装し、WSDBIT がクライアントまたはデバイスとして、WSDAPI を練習することできます。 WSDBIT は、テストし、非 WSDAPI デバイスまたは非 WSDAPI クライアントの検証に使用できます。

WSD 相互運用性ツールの詳細を読む前に知っておくべき DPWS 仕様とその[仕様を参照](referenced-namespaces.md)します。

**注**  WSDBIT は、デバイス、DPWS の実装を支援するために使用することが一般的なデバッグ ツールを使用するものではありません。 その他の[WSDAPI 開発ツール](https://go.microsoft.com/fwlink/p/?linkid=163866)(など、[デバッグ ツール WSDAPI](https://go.microsoft.com/fwlink/p/?linkid=163867)) トラフィックを観察し、障害の診断に適しています。 これらのツールはデスクトップ アプリ用 Windows SDK で利用できるを参照してください[デスクトップ アプリ開発者向けダウンロード]( https://go.microsoft.com/fwlink/p/?linkid=309790)します。

 

ここでは、次のトピックについて説明します。

[WSDBIT の概要](introduction-to-wsdbit.md)

[参照先の名前空間](referenced-namespaces.md)

[WSDBIT テスト環境](wsdbit-testing-environment.md)

[WSDBIT のクライアントのシナリオ](client-scenarios-for-wsdbit.md)

[WSDBIT 参照](wsdbit-reference.md)

WSD と WSDAPI する方法の詳細については、Windows ソフトウェア開発キット (SDK) で次のトピックを参照してください。

-   [WSD デバイス開発](https://go.microsoft.com/fwlink/p/?linkid=163868)

-   [Windows 上の WSD アプリケーションの開発](https://go.microsoft.com/fwlink/p/?linkid=163869)

-   [WSDAPI トラブルシューティング ガイド](https://go.microsoft.com/fwlink/p/?linkid=163870)

 

 





