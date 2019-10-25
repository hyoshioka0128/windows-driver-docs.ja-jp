---
title: WDI 低待機時間接続品質
description: このセクションでは、WDI で低待機時間接続を使用して品質を維持する方法について説明します。
ms.assetid: 194A26DA-A138-4967-9A09-5843A38007E9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a9d01cbe64e6c0d16169c2cba2715d3e0cf1bef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842921"
---
# <a name="wdi-low-latency-connection-quality"></a>WDI 低待機時間接続品質


待機時間の短いデータトラフィック (たとえば、VoIP アプリケーション) を必要とするアプリケーションがシステム上で実行されている場合は、低待機時間モードの操作用にポートを構成できます。 この操作モードでは、ドライバーは、低待機時間モード用に構成されたポートのチャネルからの移動を引き起こす動作 (スキャンや、AP ローミングの向上など) を変更する必要があります。 また、NDIS\_STATUS\_WDI\_に指定されたガイダンスに従って[\_リンク\_状態\_変更](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-link-state-change)を示すことになります。 このホストは、ポートがこのモードのときに使用する必要がある[ **\_\_低の待機時間\_接続\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-low-latency-connection-quality-parameters)を提供します。 これにより、ポートがチャネルをオフにする最長時間と、低待機時間の\_\_\_ローミングを開始する前に接続を切断する必要がある最小リンク品質の値が指定され[\_ローミング\_必要](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed))。

スキャンの場合、ホストは最大チャネル熟考時間 (アクティブチャネルとパッシブチャネルに異なる値がある) を提供し、アダプターは最大時間を超えないようにする必要があります。 また、ホストは不要なスキャンを調整します。 ただし、アダプターでは、 [**WDI\_scan\_トリガー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_scan_trigger)が**WDI\_scan\_トリガー\_バックグラウンド**または**WDI\_スキャン**\_\_のローミングをトリガーする場合に、さらにスキャンを調整できます。 アダプターがこのモードで独自のスキャンを実行する場合は、そのアダプターが探している SSID (スリープからの再開後) を含めて、チャネルの熟考時間を短縮することをお勧めします。 また、1つのオフチャネルスキャンで複数のチャネルをスキャンして、全体のオフチャネルの時間制限を下回るようにする必要があります。

ホストは、 [NDIS\_状態\_WDI\_\_示す](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-roaming-needed)ことを考慮して、ローミング\_アダプターからの強い要求が必要であることを示します。このモードでは、アダプターは、この通知が送信される頻度に注意する必要があります。 アダプターが独自のローミング/AP 選択の決定を行う場合は、適切なメカニズム (近隣レポートや PMKIDs など) を使用して、Ap を検索および選択する必要があります。

アソシエーションプロセスを最適化するには、アダプターは、可能であれば、結合時に TSF タイマー同期にキャッシュされた BSS エントリを使用する必要があります。 キャッシュされたエントリは、最新のプローブ要求から取得されたものであるため、できるだけ多くの時間を必要とする TSF のタイマー同期に適しています。 TSF の同期は、ドライバーが最新のキャッシュされたプローブ応答を持たない AP を選択した場合でも、後で行うことができます。 ドライバーは、次のビーコンを受信するまで Wi-fi 電力の保存を無効にすることができます。これは通常、100ミリ秒内で発生します。

マルチチャネルの同時実行モードで動作している場合は、チャネルの多重化を実行するときに、アダプターが ECSA またはその他のメカニズムを使用して、シームレスな非ジッターエクスペリエンスを有効にすることをお勧めします。

 

 





