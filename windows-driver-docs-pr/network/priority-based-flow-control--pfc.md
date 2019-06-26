---
title: 優先順位ベースのフロー制御 (PFC)
description: 優先順位ベースのフロー制御 (PFC)
ms.assetid: 9DD8A66F-273F-4E5A-99EF-33C2EDF3240C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b319526c9c8c7fd1ca29d7169ad557c98330575a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385477"
---
# <a name="priority-based-flow-control-pfc"></a>優先順位ベースのフロー制御 (PFC)


IEEE 802.1 qbb で優先度に基づくフロー制御 (PFC) が指定されたドラフト標準。 この標準は、IEEE 802.1 データ センター ブリッジング (DCB) インターフェイスのフレームワークの一部です。

PFC により、フロー制御統一された 802.3 イーサネット メディア インターフェイス、または*fabric*、ローカル エリア ネットワーク (LAN) および記憶域エリア ネットワーク (SAN) のテクノロジ。 PFC はネットワーク リンクの混雑により、パケット損失を回避するためのものです。 これにより、同じ統合されたファブリック経由で損失を区別しない従来のプロトコルと共存させる Fibre Channel over Ethernet (FCoE) などの損失するプロトコルです。

PFC は、直接接続されているピア間のリンク層フロー制御メカニズムを指定します。 PFC は、IEEE 802.3 PAUSE フレームに似ていますが、代わりに個々 の 802.1p の優先度レベルで動作します。 これにより、受信側が、802.1 p の優先度レベルでの送信を一時停止できます。

PFC は、802.3 PAUSE フレームを使用して、以下の PFC フィールド拡張されています。

-   802.1p の優先度レベルを指定する 8 ビット マスクを一時停止する必要があります。

-   優先度レベルのトラフィックを停止する必要がどのくらいの期間を指定する各優先度のタイマー値。

受信側は、802.3 PAUSE フレーム PFC データを送信するとき、スイッチは、受信側が接続されているポートに指定された優先順位のフレームの送信をブロックします。 タイマー値が経過すると、スイッチには、ポート上の一時停止したフレームの送信が再開します。

NDIS のサービス品質 (QoS) パラメーターを使用して指定、 [ **NDIS\_QOS\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体。 **PfcEnable**メンバーには、各ビットが PFC 802.1p の優先度レベルが有効かどうかを指定し、ビットマップが含まれています。

優先度レベルの詳細については、次を参照してください。 [IEEE 802.1p の優先度レベル](ieee-802-1p-priority-levels.md)します。

 

 





