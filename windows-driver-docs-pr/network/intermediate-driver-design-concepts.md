---
title: 中間ドライバー設計の概念
description: 中間ドライバー設計の概念
ms.assetid: cee13268-5df0-4d71-a115-3168c56be06c
keywords:
- 中間ドライバー WDK ネットワーク、書き込み
- NDIS 中間ドライバー WDK、書き込み
- NDIS 中間ドライバー WDK ネットワークの作成
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fae498f7fd0b4ac3c6e025b32f95e1df192ec3ed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527652"
---
# <a name="intermediate-driver-design-concepts"></a>中間ドライバー設計の概念





このセクションでは、NDIS intermediate ドライバーの記述を開始するための基本的な情報を提供します。 NDIS 中間ドライバを作成するには、NDIS ミニポート ドライバーとドライバーのプロトコル操作および関数を理解する必要があります。

MUX 中間ドライバー サンプル Microsoft Windows Driver Kit (WDK) での基本的な例を提供する、 *n*-に-特定のニーズに適応できる 1 つのマルチプレクサー中間ドライバー。

NDIS 中間ドライバーの仮想ミニポートを逆シリアル化する必要があります。 *ドライバーを逆シリアル化*独自の操作をシリアル化*MiniportXxx*関数とキューのすべての着信を内部的には、これらの操作を実行する NDIS ではなくネットワーク データを送信します。 この操作の結果、ドライバーの重要なセクション (一度に 1 つのスレッドで実行できるコード) の小さなが保持される場合、全二重のパフォーマンスが大幅に向上します。 逆シリアル化されたドライバーの詳細については、次を参照してください。 [NDIS ミニポート ドライバーの逆シリアル化](deserialized-ndis-miniport-drivers.md)します。

NDIS 中間ドライバーでは、仮想ミニポートのコネクションレス通信のみをサポートできます。 そのプロトコル インターフェイスでただし、NDIS 中間ドライバーをサポートできますコネクションレスの通信と通信の接続指向のいずれか。 接続指向の通信の詳細については、次を参照してください。 [Connection-Oriented NDIS](connection-oriented-ndis.md)します。

通常、中間のドライバーは、1 つまたは複数の NDIS ミニポート ドライバー上と下トランスポート ドライバーに位置します。 中間ドライバーは、他の中間ドライバーも階層化できます。

次のトピックでは、NDIS 中間ドライバの書き込みに関する追加情報を提供します。

[中間ドライバー DriverEntry 関数](intermediate-driver-driverentry-function.md)

[中間のドライバーでの動的バインド](dynamic-binding-in-an-intermediate-driver.md)

[クエリの中間ドライバーおよびセット操作](intermediate-driver-query-and-set-operations.md)

[中間ドライバー ネットワーク データの管理](intermediate-driver-network-data-management.md)

[中間のドライバーのデータの受信](receiving-data-in-an-intermediate-driver.md)

[中間ドライバーを通じてネットワーク データの送信](transmitting-network-data-through-an-intermediate-driver.md)

[PnP イベントおよび中間のドライバーで電源管理イベントの処理](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)

[中間ドライバーのリセット操作](intermediate-driver-reset-operations.md)

[中間のドライバーで状態インジケーター](status-indications-in-an-intermediate-driver.md)

 

 





