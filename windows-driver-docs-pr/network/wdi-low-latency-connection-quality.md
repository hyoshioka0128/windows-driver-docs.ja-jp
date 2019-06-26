---
title: WDI 低待機時間接続品質
description: このセクションでは、WDI で低待機時間の接続の品質を維持する方法をについて説明します
ms.assetid: 194A26DA-A138-4967-9A09-5843A38007E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0777b6f1f8134ba08beb72ee2d7c3148650f8f37
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387207"
---
# <a name="wdi-low-latency-connection-quality"></a>WDI 低待機時間接続品質


低待機時間データのトラフィック (たとえば、VoIP アプリケーション) が必要なシステムで実行されているアプリケーションがある場合、低待機時間モード操作用のポートを構成できます。 この操作モードの場合、ドライバーは低待機時間モード用に構成されているポートのチャネルから移動することを (ローミング AP 以上のスキャン) などの任意の動作を変更する必要があります。 指定したガイダンスに従う必要がありますも、 [NDIS\_状態\_WDI\_INDICATION\_リンク\_状態\_変更](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-link-state-change)を示す値。 ホスト提供[ **WDI\_TLV\_低\_待機時間\_接続\_品質\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-low-latency-connection-quality-parameters)するポートこのモードである場合に使用する必要があります。 ポートがチャネルとの接続が低待機時間のローミングを開始する前に下に分類する必要があります最小リンクの品質評価の値をオフにする必要がある最大時間を指定します (送信を含む[NDIS\_状態\_WDI\_INDICATION\_ローミング\_必要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed))。

スキャン、ホストは、チャネルの最大時間 (アクティブおよびパッシブ チャネルに別の値がある) と最大時間上、アダプターにならない必要があります。 ホストでは、不要なスキャンも調整します。 ただし、アダプターがさらに場合は、スキャンを調整できる、 [ **WDI\_スキャン\_トリガー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_scan_trigger)は**WDI\_スキャン\_トリガー\_バック グラウンド**または**WDI\_スキャン\_トリガー\_ローミング**します。 アダプターは、このモードでは、独自のスキャンを実行する場合を探しています (スリープから復帰した後である) 場合を除き、チャネルで時間を削減する SSID が含まれることをお勧めします。 さらに、全体的なチャネルをオフの時間制限できるように、1 つのチャネルからスキャンで複数のチャネルをスキャンを回避する必要があります。

ホストと見なします[NDIS\_状態\_WDI\_を示す値\_ローミング\_必要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)ローミング、このモードの場合、アダプターがする必要がありますので、アダプターから強力な要求この通知を送信する頻度について注意します。 アダプターは、独自のローミング/AP 選択決定を実行する場合、(近隣レポートや PMKIDs) などの適切なメカニズムを使用して検索と選択/順位の Ap をする必要があります。

関連付け処理を最適化するために、アダプターする必要がありますエントリを使用してキャッシュされた BSS 参加中に TSF タイマーの同期可能な場合。 キャッシュされたエントリは、TSF タイマー同期新鮮なほとんどの場合は、最近のプローブ要求から取得されているため、これで十分です。 TSF の同期は、ドライバー、最新の状態のキャッシュされたプローブ応答がないアプリを選択することを決定する場合でも、後で実行できます。 ドライバーは、通常は 100 ミリ秒内に発生します。 [次へ] 内ビーコンを受信するまで、省電力、Wi-fi を無効にできます。

マルチ チャネルの同時実行モードで使用する場合、あるアダプター採用 ECSA またはシームレス/いいえを有効にするためには、その他のメカニズム ジッター エクスペリエンス チャネルを多重化を実行するときにお勧めします。

 

 





