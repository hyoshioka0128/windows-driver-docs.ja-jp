---
title: WSDAPI Basic Interoperability Tool
description: WSDAPI Basic Interoperability Tool
ms.assetid: c4a610d4-3adf-406d-88d6-0879eb98b54f
keywords:
- ツール WDK、テストドライバー
- WSDBIT ツール WDK
- WSDAPI 基本相互運用性ツール WDK
- DWPS WDK
- Web サービス WDK のデバイスプロファイル
- デバイス用 Web サービス API WDK
- WSDAPI WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe9df72d7ef2dbc2aa2241c5704eafec32c2371
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769508"
---
# <a name="wsdapi-basic-interoperability-tool"></a>WSDAPI Basic Interoperability Tool


[Web サービス (DPWS) のデバイスプロファイル](http://schemas.xmlsoap.org/ws/2005/05/devprof/)は、いくつかの web サービス (WS) 仕様をアセンブルして制約する参照仕様です。 [Web Services On Devices (WSD)](https://docs.microsoft.com/windows/win32/wsdapi/wsd-portal) API (WSDAPI) は、Windows に付属している dpws を実装したものです。 Windows では、すべての種類の DPWS デバイスを検出するために WSDAPI を使用します。また、複数のデバイスクラス (プリンター、スキャナー、ネットワークプロジェクターなど) に制御メッセージを発行するために、WSDAPI も使用します。

WSDAPI 基本相互運用性ツール (WSDBIT) を使用して、Windows が WSDAPI 以外の DPWS スタックと相互運用できることを確認できます。 このツールは、主に DPWS を実装し、Windows との相互運用性をテストするデバイス開発者を対象としています。 一部の WSDBIT テストでは、デバイスが高度な DPWS 機能を実行するために使用される特別なテストインターフェイスを実装する必要があります。これには、SOAP メッセージの添付ファイルに使用される[MTOM (SOAP Message 伝送最適化機構](https://www.w3.org/TR/2005/REC-soap12-mtom-20050125/)) や[Web サービスのイベント](https://docs.microsoft.com/previous-versions/ms951233(v=msdn.10))処理などがあります。 これらのインターフェイスは、厳密には必須ではありません。 ただし、WSDBIT でこの機能をカバーする唯一の方法です。

WSDAPI は、仕様のクライアントとデバイスの両方のセクションを実装し、WSDBIT を使用して、クライアントまたはデバイスとして WSDAPI を実行できます。 WSDBIT を使用して、非 WSDAPI デバイスまたは非 WSDAPI クライアントをテストおよび検証できます。

WSD 相互運用性ツールの概要を確認する前に、DPWS の仕様とその参照されている[仕様](referenced-namespaces.md)について理解しておく必要があります。

**メモ**   WSDBIT は、デバイスでの DPWS の実装を支援するために使用できますが、汎用的なデバッグツールとしては使用できません。 他の[wsdapi 開発ツール](https://docs.microsoft.com/windows/win32/wsdapi/wsdapi-development-tools)( [wsdapi デバッグツール](https://docs.microsoft.com/windows/win32/wsdapi/debugging-tools)など) は、トラフィックの監視と障害の診断に適しています。 これらのツールは、デスクトップアプリの Windows SDK で利用できます。「[デスクトップアプリを開発するためのダウンロード](https://developer.microsoft.com/windows/downloads/windows-10-sdk/)」を参照してください。

 

ここでは、次のトピックについて説明します。

[WSDBIT の概要](introduction-to-wsdbit.md)

[参照されている名前空間](referenced-namespaces.md)

[WSDBIT のテスト環境](wsdbit-testing-environment.md)

[WSDBIT のクライアント シナリオ](client-scenarios-for-wsdbit.md)

[WSDBIT リファレンス](wsdbit-reference.md)

WSD と WSDAPI の詳細については、Windows ソフトウェア開発キット (SDK) の次のトピックを参照してください。

-   [WSD デバイス開発](https://docs.microsoft.com/windows/win32/wsdapi/wsd-device-development)

-   [Windows での WSD アプリケーション開発](https://docs.microsoft.com/windows/win32/wsdapi/wsd-application-development-on-windows)

-   [WSDAPI トラブルシューティングガイド](https://docs.microsoft.com/windows/win32/wsdapi/wsdapi-troubleshooting-guide)

 

 





