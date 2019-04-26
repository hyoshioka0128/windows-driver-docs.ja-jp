---
title: WSDBIT の概要
description: WSDBIT の概要
ms.assetid: 8a8ee9de-95b2-43df-ba96-3b09fcd5751c
keywords:
- WSDBIT について、WDK をツールします。
- WSDAPI の基本的な相互運用性について、WDK のツール
- デバイス API の WDK のサービスを web について
- WSDAPI WDK, 概要
- WDK WSDBIT のテストの相互運用性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad97975e0ead86529c1b5891ea8ad691f3d9b63d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356552"
---
# <a name="introduction-to-wsdbit"></a>WSDBIT の概要


Web Services for Devices (WSD) API (WSDAPI) は、次の種類のメッセージ交換を有効にします。

-   DPWS デバイスを検出します。

-   DPWS デバイスを記述します。 呼ばれる、*メタデータ交換*します。

-   DPWS サービスとの間は、バイナリの添付ファイルと共に、サービス固有のメッセージを送信します。

-   サブスクライブし、DPWS サービスからイベントを受信します。

次の図に示すように WSDAPI の基本的な相互運用性ツール (WSDBIT) は、DPWS メッセージを送受信する WSDAPI を使用します。 WSDBIT を使用して、クライアントとデバイスで実行されている DPWS スタックで実行されている WSDAPI 間の相互運用性をテストできます。

![wsdapi 基本的な相互運用性ツール (wsdbit) と関連コンポーネントを示す図](images/wsdbit2.png)

[相互運用性シナリオ](client-scenarios-for-wsdbit.md)前のメッセージ交換で使用されるプロトコルとメッセージ形式を確認する対象としています。 シナリオでは、クライアントの観点から定義され、次のカテゴリに分類されます。

-   *デバイスとサービスの検査*をテストし、DPWS デバイスの検出とメタデータの交換のことを確認します。

-   *単純なと高度な制御*をテストし、サービス固有のメッセージを確認します。

-   *添付ファイル*をテストして、メッセージの添付ファイルで定義されている、 [SOAP Message Transmission Optimization Mechanism (MTOM)](https://go.microsoft.com/fwlink/p/?linkid=81254)仕様。

-   *イベント*をテストして[Web サービスのイベント処理](https://go.microsoft.com/fwlink/p/?linkid=81245)します。

-   *セキュリティ保護された通信*前に示したすべてのシナリオの要素が含まれます。

相互運用性のテストの特定のニーズに応じて、デバイス、クライアント、またはその両方を実装できます。

セクションでは、テスト_ケースの選択的に実装できます。 のみを実装できますなど、[デバイスとサービスの検査](device-and-service-inspection-scenarios.md)と[シンプルで高度なコントロール](device-control-scenarios.md)テスト_ケースの相互運用性。

**注**  には、少なくとも他のテスト_ケースで必要なために、デバイスとサービスの検査の相互運用性のテスト ケースを実装する必要があります。

 

 

 





