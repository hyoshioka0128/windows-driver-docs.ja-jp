---
title: オーディオ フィルター、ピン、ノード
description: オーディオ フィルター、ピン、ノード
ms.assetid: 5f30703c-bf33-49bb-bce2-990ad5b54a9c
keywords:
- WDM オーディオ ドライバー WDK、フィルター
- オーディオ ドライバー WDK、フィルター
- WDM オーディオ ドライバー WDK、ピン
- オーディオ ドライバー WDK、ピン
- WDM オーディオ ドライバー WDK、ノード
- オーディオ ドライバー WDK、ノード
- WDK のオーディオをフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bcfe9e7f7e492e56c7cd9a15803ff86d8c712d1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331637"
---
# <a name="audio-filters-pins-and-nodes"></a>オーディオ フィルター、ピン、ノード


## <span id="audio_filters_pins_and_nodes"></span><span id="AUDIO_FILTERS_PINS_AND_NODES"></span>


Microsoft Windows Driver Model (WDM) ドライバーでは、それぞれの 1 つまたは複数のフィルター インスタンスを作成することができます、フィルター ファクトリのコレクションとして、オーディオ ハードウェアを公開します。 (KS) フィルター オブジェクトをストリームのカーネルは、何らかの種類のデジタル処理 wave オーディオ データのストリームをフィルターを実行するオーディオ ハードウェア関数をカプセル化できます。 たとえば、フィルターは、レンダリングや、ストリームの合成を行う可能性があります。 またはリバーブがストリームに追加します。

フィルターのインスタンスは、暗証番号 (pin) ファクトリ、それぞれが 1 つまたは複数の暗証番号 (pin) インスタンスを作成できますを公開します。 これらのピンは、フィルター グラフを生成するために他のフィルターのピンに接続することができます。 オーディオ フィルターのグラフの一部にするには、フィルターは、1 つ以上の暗証番号 (pin) のインスタンスが必要です。

Pin は、データ ストリームを開始または終了したフィルターを入力または出力の接続ポイントを表します。 各ピンには、データ形式をサポートできるし、互換性のある形式のストリームだけは、暗証番号 (pin) を経由できますの範囲を指定します。

WDM オーディオ デバイスのフィルターでは、その内部のトポロジ ノードと接続の形式で公開します。

トポロジのノードは、フィルターを通過するデータ パス上に存在します。 ノードは、フィルター内のコントロール ポイントを表します。 各ノードは論理的にフィルターの機能のモジュールのチャンクをカプセル化し、ノードを通過するデータ ストリームのデジタル信号処理を実行します。 ノードには、例では、ソフトウェアの管理下にある調整できるため、ボリューム コントロールを表すことができます。

フィルター オブジェクトには、そのさまざまな pin とノード間の接続も指定します。 これらの接続に暗黙の型では、フィルター内で各データ パスに沿ってノードの順序付けします。

このセクションでは、フィルター、pin、および WDM オーディオ ドライバーに固有であるノードの機能を表示します。 次のトピックについて説明します。

[オーディオ フィルター](audio-filters.md)

[フィルター ファクトリ](filter-factories.md)

[暗証番号 (pin) ファクトリ](pin-factories.md)

[ノードと接続](nodes-and-connections.md)

[オーディオ フィルター グラフ](audio-filter-graphs.md)

[Wave フィルター](wave-filters.md)

[MIDI と DirectMusic フィルター](midi-and-directmusic-filters.md)

[トポロジのフィルター](topology-filters.md)

カーネル ストリーミングのフィルター、pin、およびノードの参照の全般的な説明の[KS ミニドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff567656)します。

 

 




