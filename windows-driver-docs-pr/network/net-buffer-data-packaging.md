---
title: NET_BUFFER データのパッケージ化
description: NET_BUFFER データのパッケージ化
ms.assetid: f0d539ab-c6ed-4cd9-9891-ef4235016d50
keywords:
- NDIS WDK、データを送受信します。
- データ パッケージの WDK ネットワーク
- WDK ネットワークのデータを送信します。
- 受信側のデータの WDK ネットワーク
- NDIS_PACKET
- NET_BUFFER データ パッケージの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db03f7007f271cc3fbfa19e4018669a3a8cd46ea
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353325"
---
# <a name="netbuffer-data-packaging"></a>NET\_バッファー データのパッケージ化





データのパッケージ化は、NDIS 6.0 で再設計されました。 送信および受信のアーキテクチャに基づいている、 [ **NDIS\_パケット**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff557086(v=vs.85))構造に基づいているアーキテクチャで置き換えられました[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)と[ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)構造体。 NET\_バッファーの構造は、NDIS と同等の機能\_パケットの構造体。 NET\_バッファーの構造体は、NDIS、プロトコルのドライバー、およびミニポート ドライバーの予約領域と同様に、ネットワーク データのバッファー (MDL チェーン) を指定します。 NET\_バッファーの構造体は、NET によって定義された一覧にまとめてリンクできます\_バッファー\_リスト構造体。 NET\_バッファー\_リスト構造は、すべてのネットワークに適用されるアウト オブ バンド (OOB) データにストレージを提供するも\_リスト内のバッファーの構造体。

Microsoft 次世代ネットワーク ドライバー スタック、Winsock、TCP/IP トランスポートをなどのすべてのコンポーネントを使用して、NET\_バッファー データのパッケージ化します。 ドライバー スタック全体で一貫したデータのパッケージ化は、データを再パッケージ化する必要はありません、データの処理を簡略化され、関数呼び出しの数を減らします。

NDIS を使用して古いドライバーに対応するために\_パケットの構造体、NDIS 6.0 変換 NDIS\_ネットへのパケット構造\_バッファーの構造体、またはその逆。 この変換は、NDIS ドライバーに対して透過的です。

NDIS より高度なドライバーをドライバーのデータのバックフィル要件を反映します。 NET を割り当てるときに\_バッファーと NET\_バッファー\_リストの構造体のデータを送信するより高度なドライバーは、スタック内のすべての下位のドライバーを対応するために十分なデータ領域を割り当てます。 その結果、下位レベルのドライバーは、レイヤーに固有のヘッダーに対応する追加のバッファー領域を割り当てることはありません。 代わりに、この目的のバックフィルを事前に割り当てられた領域を使用できます。

詳細については、NET\_アーキテクチャのバッファーを参照してください[NET\_バッファー アーキテクチャ](net-buffer-architecture.md)します。

 

 





