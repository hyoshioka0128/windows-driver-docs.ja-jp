---
title: NDISWAN の概要
description: NDISWAN の概要
ms.assetid: bc092222-5418-4a57-9811-5d97c1c10a73
keywords:
- ネットワーク NDISWAN WDK
- NDIS 中間ドライバー WDK、NDISWAN ドライバー
- 中間ドライバー WDK ネットワー キング、NDISWAN ドライバー
- アーキテクチャの WDK WAN NDISWAN
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6a9982052d9d98523bff1a205612b96eac0a632
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392403"
---
# <a name="ndiswan-overview"></a>NDISWAN の概要





NDISWAN は、システム提供 NDIS 中間ドライバーなど、データ圧縮、暗号化、ループバック、および WAN ミニポート ドライバーで使用される PPP フレームを単純な機能を提供します。 WAN ミニポート ドライバーがメディアに固有の機能のみを実装するために必要なため (たとえば、Q931 シグナル通知は必要 ISDN)。

次の図は、RAS アーキテクチャでは、他のコンポーネントと NDISWAN のインターフェイスを示します。

![ndiswan が ras アーキテクチャの他のコンポーネントとやり取りする方法を示す図](images/ndiswan-1.png)

プロトコル ドライバーを関連する NDISWAN は両方の NDIS およびいる CoNDIS ミニポートをドライバー インターフェイスに表示されます。 基になる WAN ミニポート ドライバーには、NDISWAN は、WAN に固有のいくつかの要素を含む NDIS およびいる CoNDIS の両方のプロトコル インターフェイスを表示します。

いる CoNDIS 環境では、WAN ミニポート ドライバーは接続指向のミニポート ドライバーまたは統合ミニポート コール マネージャー (MCM) を指定できます。

NDISWAN は、次の機能を提供します。

-   **パケット変換**

    NDISWAN に変換は、渡されるプロトコル ドライバーによって LAN から PPP 形式にパケットを送信します。 NDISWAN 実行逆の変換では、WAN ミニポート ドライバーによって渡されたパケットを受信します。 NDISWAN では、単純な HDLC フレームを使用します。 ミニポート ドライバーでは、メディア固有のフレームの大部分を実行する必要があります。 WAN のパケットのフレーミングの詳細については、次を参照してください。 [WAN パケットのフレーミング](wan-packet-framing.md)します。

-   **パケットの処理**

    パケット ヘッダーの圧縮、データの圧縮および暗号化の構成オプションは、送信します。 NDISWAN では、送信パケットの順序でこれらの操作が適用されます。 逆の順序でこれらのオプションを適用する NDISWAN でパケットを受信します。 NDISWAN 圧縮や暗号化などの構成オプションが有効であると判断した場合、NDISWAN は基になる WAN ミニポート ドライバーに通知する OID を送信します。

-   **ドライバーの簡略化されたバインド**

    NDISWAN は、プロトコルおよび WAN ミニポート ドライバー間のバインドを簡略化します。 WAN のドライバーのバインディングの詳細については、次を参照してください。 [WAN のドライバーのバインドと接続](wan-driver-bindings-and-connections.md)します。

-   **データの転送**

    NDIS WAN 環境では、NDISWAN は、送信パケットの記述子のヘッダーを検査し、リンク、パケットを送信を決定します。 NDISWAN では、連続したバッファーにパケットをコピーし、基になるミニポート ドライバーに転送します。 いる CoNDIS WAN 環境では、NDISWAN は、パケットの関連付けられている仮想接続 (VC) に基づいてパケットを転送します。 ドライバーの WAN リンクと接続の詳細については、次を参照してください。 [WAN のドライバーのバインドと接続](wan-driver-bindings-and-connections.md)します。

 

 





