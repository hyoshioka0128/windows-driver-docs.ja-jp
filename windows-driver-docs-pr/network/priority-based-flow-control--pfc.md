---
title: 優先順位ベースのフロー制御 (PFC)
description: 優先順位ベースのフロー制御 (PFC)
ms.assetid: 9DD8A66F-273F-4E5A-99EF-33C2EDF3240C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b01cb4a7c8193a56f83e2715a4454ecb68dc8f59
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843493"
---
# <a name="priority-based-flow-control-pfc"></a>優先順位ベースのフロー制御 (PFC)


優先順位ベースのフロー制御 (PFC) は、IEEE 802.1 Qbb ドラフト標準で指定されています。 この標準は、IEEE 802.1 データセンターブリッジング (DCB) インターフェイスのフレームワークの一部です。

PFC を使用すると、ローカルエリアネットワーク (LAN) および記憶域ネットワーク (SAN) テクノロジに対して、統合された802.3 イーサネットメディアインターフェイス (*ファブリック*) に対するフロー制御が可能になります。 PFC は、ネットワークリンクの輻輳に起因するパケット損失をなくすことを目的としています。 これにより、ファイバーチャネル over Ethernet (FCoE) などの損失の影響を受けやすいプロトコルを、同じ統合ファブリックを介して、従来の損失を区別しないプロトコルと共存させることができます。

PFC は、直接接続されているピア間のリンクレイヤーフロー制御メカニズムを指定します。 PFC は IEEE 802.3 の一時停止フレームに似ていますが、代わりに個別の 802.1 p 優先度レベルで動作します。 これにより、受信者は任意の 802.1 p 優先度レベルでトランスミッタを一時停止できます。

PFC は 802.3 PAUSE フレームを使用し、次の PFC フィールドで拡張します。

-   一時停止する 802.1 p 優先度レベルを指定する8ビットマスク。

-   優先度レベルのトラフィックを一時停止する時間を指定する各優先度のタイマー値。

受信者が PFC データを使用して802.3 の一時停止フレームを送信すると、スイッチによって、受信側が接続されているポートに対して、指定した優先度レベルのフレームの送信がブロックされます。 タイマーの値が期限切れになると、スイッチによって、ポートで一時停止しているフレームの送信が再開されます。

NDIS Quality of Service (QoS) パラメーターは、 [**ndis\_QoS\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)構造体によって指定されます。 **Pfcenable**メンバーにはビットマップが含まれており、各ビットは pfc を 802.1 p 優先度レベルに対して有効にするかどうかを指定します。

優先度レベルの詳細については、「 [IEEE 802.1 p Priority levels](ieee-802-1p-priority-levels.md)」を参照してください。

 

 





