---
title: キャプチャの停止の分析
description: キャプチャの停止の分析
ms.assetid: 9a88deba-374c-4ccc-8bb8-18e3b4124158
keywords:
- カーネル デバッグは、例を示しますのストリーミング
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdeeacbaeba1a30770c714d9df0bef41f445ad58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578005"
---
# <a name="analyzing-a-capture-stall"></a>キャプチャの停止の分析


キャプチャの停止をシミュレートする人工的な作成のシナリオを次に示します。 これは、ストレス テストで似たような状況が頻繁に発生するために特に役に立つシナリオです。 シナリオは次のとおりです。

Sndrec32 の録音をプライマリ キャプチャ デバイスから、Windows の記録コンポーネントでは、クリエイティブな SBLive ここでデバイスを wave します。 一定期間が記録されます。ただし、このテストのための完全なキャプチャ Irp が portcls が明示的に発生するため、グラフは 8.50 秒に失速します。

を実行しているアプリケーションの表示が、ストリームの位置が進んでいません。 位置は 8.50 秒停止します。

このコンピューターでプライマリ キャプチャ デバイスは、PCI サウンド カードであるために、まず使用して、 [ **! ks.pciaudio** ](-ks-pciaudio.md)コマンドを開始点を把握してください。 実行中のすべてのストリームの表示を要求するのにには、フラグの値は 1 を使用します。

```dbgcmd
kd> !pciaudio 1

1 Audio FDOs found:
 Functional Device 8121c030 [\Driver\emu10k]
        Wave Cyclic Streams:
            Pin 812567c0 RUN [emu10k1m!CMiniportWaveCyclicStreamSBLive ff9ec7f8] 
```

ここでは、1 つだけの PCI オーディオ デバイスがあるし、Intel emu10k ドライバーがサービスを提供 (\\ドライバー\\emu10k)。 このドライバーは、現在実行中の単一ストリーム (0x812567C0) を持ちます。 使用して[ **! ks.graph** ](-ks-graph.md)カーネル グラフを表示します。 設定*レベル*と*フラグ*両方 7 失速で最大の詳細を取得します。

```dbgcmd
kd> !graph 812567c0 7 7
Attempting a graph build on 812567c0...  Please be patient...
Graph With Starting Point 812567c0:
"emu10k" Filter ff9ebb98, Child Factories 5
    Output Factory 0:
        Pin 812567c0 (File 811c6630, -> "splitter" 811df960) Irps(q/p) = 8, 0
 Queued: 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98 
```

上記は、0 を工場出荷時の詳細を表示します。 Emu10k 出力ピン 0x812567C0 は 0x811DF960 スプリッター入力ピンに接続されます。 ある emu10k の出力ピンに 8 つの Irp がキューに配置します。 出力[ **! ks.graph** ](-ks-graph.md)ように継続されます。

```dbgcmd
"splitter" Filter ffb18890, Child Factories 2
    Output Factory 0:
        Pin 811df430 (File ffa55f90) Irps(q/p) = 10, 0
 Queued: ffadd008 ffa73b00 ffa1e998 811de310 ffa54370 ffaaf008 811dee70 81250e70 811de580 811de8c0 
```

10 個の Irp が分割の出力ピンにキューに配置します。

```dbgcmd
    Input Factory 1:
        Pin 811df960 (File 81187820, <- "emu10k" 812567c0) Irps(q/p) = 0, 8
            Pending: 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98 
```

スプリッターの入力ピンには、キューに置かれた Irp; がありません。ただし、キューを入力する emu10k から 8 を待機しています。

```dbgcmd
Analyzing a Hung Graph From 812567c0:

Suspect Filters (For a Hung Graph):
 "emu10k" Filter ff9ebb98 or class "PortCls Wave Cyclic" is suspect.
        Reasons For This Analysis:
            - No critical pin has less than 8 queued Irps
            - Downstream "splitter" pin 811df960 is starved
        Irps to check:
 81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98
```

この情報から、アナライザーは emu10k または WaveCyclic のいずれかを障害にすることがありますを提案します。 問題のある Irp; の一覧も用意されています。これらは、emu10k の入力ピンにキューに置かれた Irp です。 完了するこれらの Irp のいずれかの場合は、スプリッターはデータをコピーし、IRP を完了し、グラフ、進行状況します。 何らかの理由で emu10k にこれらのキャプチャ Irp が完了しません。

 

 





