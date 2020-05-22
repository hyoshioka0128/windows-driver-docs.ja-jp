---
title: WSDBIT の概要
description: WSDBIT の概要
ms.assetid: 8a8ee9de-95b2-43df-ba96-3b09fcd5751c
keywords:
- WSDBIT ツール WDK、概要
- WSDAPI 基本相互運用性ツール WDK, 概要
- デバイス用 Web サービス API WDK、概要
- WSDAPI WDK、概要
- WDK WSDBIT の相互運用性テスト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e5a04f18df6fad3b0376bb02f583d9858f74989
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769654"
---
# <a name="introduction-to-wsdbit"></a>WSDBIT の概要


Web Services for Devices (WSD) API (WSDAPI) では、次の種類のメッセージ交換を行うことができます。

-   DPWS デバイスを検出しています。

-   DPWS デバイスについて説明します。 これは、*メタデータ交換*と呼ばれます。

-   バイナリ添付ファイルと共に、サービス固有のメッセージを DPWS サービスとの間で送信します。

-   DPWS サービスからのイベントのサブスクライブと受信。

次の図に示すように、WSDAPI の基本的な相互運用性ツール (WSDBIT) では、WSDAPI を使用して DPWS メッセージを送受信します。 WSDBIT を使用すると、クライアントで実行されている WSDAPI と、デバイスで実行されている DPWS スタック間の相互運用性をテストできます。

![wsdapi 基本相互運用性ツール (wsdbit) と関連コンポーネントを示す図](images/wsdbit2.png)

[相互運用性のシナリオ](client-scenarios-for-wsdbit.md)は、前のメッセージ交換で使用されているプロトコルと共にメッセージ形式を確認することを目的としています。 これらのシナリオは、クライアントの観点から定義され、次のカテゴリに分類されます。

-   *デバイスとサービスの検査*では、dpws デバイスの検出とメタデータの交換をテストおよび検証します。

-   *単純なコントロールと高度なコントロール*は、サービス固有のメッセージをテストして検証します。

-   *添付ファイル*は、 [SOAP メッセージ伝送最適化メカニズム (MTOM)](https://www.w3.org/TR/2005/REC-soap12-mtom-20050125/)の仕様で定義されているように、メッセージの添付ファイルをテストおよび検証します。

-   *イベント*をテストし、 [Web サービスのイベント](https://docs.microsoft.com/previous-versions/ms951233(v=msdn.10))を確認します。

-   *セキュリティで保護された通信*には、上記のすべてのシナリオの要素が含まれます。

相互運用性テストの特定のニーズに応じて、デバイス、クライアント、またはその両方を実装できます。

テストケースのセクションを選択して実装することもできます。 たとえば、[デバイスとサービスの検査](device-and-service-inspection-scenarios.md)と、[単純および高度なコントロール](device-control-scenarios.md)の相互運用性テストケースのみを実装できます。

**メモ**   少なくとも、デバイスとサービス検査の相互運用性テストケースを実装する必要があります。これは、他のテストケースで必要になるためです。

 

 

 





