---
title: 稼働状態への遷移
description: 稼働状態への遷移
ms.assetid: ad8eb6d7-b542-4208-85f7-fba42c27a9f3
keywords:
- 作業の電源状態の WDK ネットワーク
- ネットワーク インターフェイス カード WDK ネットワーク、電源の状態遷移
- Nic の WDK ネットワーク、電源の状態遷移
- 電源管理 WDK NDIS ミニポート、電源の状態遷移
- デバイスの電源状態が WDK ネットワーク
- WDK ネットワークの状態を電源します。
- WDK のネットワークの状態遷移の電源
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9bda3e5b96d9e79259d2ab0289fb479d2312c1c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379738"
---
# <a name="transitioning-to-the-working-state"></a>稼働状態への遷移





NDIS ミニポート ドライバーを送信することによって作業電源の状態 (D0) への移行を開始する、 [OID\_PNP\_設定\_POWER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power) D0 の状態を指定する要求。 ミニポート ドライバーでは、ネットワーク アダプターを動作状態に復元するために必要なすべてのデバイスに依存する操作を実行する必要があります。 ミニポート ドライバーでは、任意のハードウェア コンテキスト--パケット フィルター、マルチキャスト アドレス、現在のメディア アクセス制御 (MAC) アドレスまたはネットワーク アダプターが失われている可能性があります--ウェイク アップ パターンも復元する必要があります。

**注**  NDIS 6.30、以降、ミニポート ドライバーをサポートする[NDIS パケット結合](ndis-packet-coalescing.md)にまとめられたパケット カウンターをオフにする必要があります。 ドライバーには、低電力の遷移の前に 1 つにまとめ、すべてのパケットをフラッシュするネットワーク アダプター構成もする必要があります。 詳細については、次を参照してください。[処理パケット結合受信フィルター](handling-packet-coalescing-receive-filters.md)します。

 

返します NDIS ミニポート ドライバー\_状態\_OID への応答の成功\_PNP\_設定\_POWER 要求、ミニポート ドライバーおよびネットワーク アダプターは、通常の操作に対応する必要があります。

 

 





