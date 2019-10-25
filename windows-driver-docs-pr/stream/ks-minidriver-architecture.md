---
title: KS ミニドライバーのアーキテクチャ
description: KS ミニドライバーのアーキテクチャ
ms.assetid: a9c17040-72a8-4290-831b-7fb46b00f532
keywords:
- カーネルストリーミング WDK, アーキテクチャ
- KS WDK、アーキテクチャ
- グラフのフィルター WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4c88a0d0f2ba81232e39944eb8bf30b753fe4f9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842510"
---
# <a name="ks-minidriver-architecture"></a>KS ミニドライバーのアーキテクチャ





カーネルストリーミングサービスは、ストリーミングされたデータのカーネルモード処理をサポートしています。 このモデルでは、ストリーミングデータは、フィルターと呼ばれるブロックにグループ化された一連のノードを介して流れます。 各フィルターは、データに対して実行される処理タスクをカプセル化します。 [KS フィルター](ks-filters.md)は、カーネルモード[**ドライバー\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)として実装されます。

KS フィルターは、プロキシを使用して、ユーザーモードで DirectShow フィルターとして表示されます。 そのため、グラフビルダーとユーザーモードアプリケーションは、KS フィルターと対話できます。 アクティブなグラフでは、カーネルモードのコンポーネントは直接通信し、ユーザーモードとカーネルモードの間でリソースを消費する遷移を排除します。

データは、[ピン](ks-pins.md)と呼ばれる接続ポイントでフィルターに出入りします。 Pin インスタンスは、デジタルオーディオなどのデータストリームをレンダリングまたはキャプチャします。

フィルターグラフは、接続されたフィルターのグループです。 フィルターグラフは、ストリームに対して実行される複数の処理タスクをリンクします。 Microsoft Windows Driver Kit (WDK) の GraphEdit ツールを使用して、さまざまな[フィルターグラフの構成](filter-graph-examples.md)をテストすることができます。 (GraphEdit の詳細については、[フィルターグラフエディターツール](https://go.microsoft.com/fwlink/p/?linkid=9230)の web サイトを参照してください)。

[オンボードクロック](ks-clocks.md)をサポートするドライバーは、ファイルオブジェクトとして時計を公開します。 ミニドライバーは、[クロック時間に対してクエリ](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-clock)を実行したり、クロックが特定の時刻に達したときに[**通知を受け取るように要求**](https://docs.microsoft.com/windows-hardware/drivers/stream/kseventsetid-clock)したりすることができます。

カスタムメモリ管理インターフェイスをサポートするミニドライバーは、[アロケーター](ks-allocators.md)と呼ばれるファイルオブジェクトとしてこのインターフェイスを公開します。 たとえば、オンボードメモリを処理するデバイスマネージャーは、このようなインターフェイスを公開する可能性があります。 ミニドライバーは、関連するファイルオブジェクトを使用して、メモリの割り当てと割り当て解除を行うことができます。

ここでは、次のトピックに関する追加情報について説明します。

[KS フィルター](ks-filters.md)

[KS の Pin](ks-pins.md)

[KS データ形式とデータ範囲](ks-data-formats-and-data-ranges.md)

[KS メディア](ks-mediums.md)

[KS インターフェイス](ks-interfaces.md)

[品質管理](quality-management.md)

 

 




