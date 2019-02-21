---
title: Ks.graph を使用します。
description: Ks.graph を使用します。
ms.assetid: 05dcd5d3-fac6-4af5-8149-955435fb016f
keywords:
- カーネル デバッグは、グラフを表示するストリーム
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea6be6966026bc039c0ffbf3706da9c247b305f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535422"
---
# <a name="using-ksgraph"></a>使用してください ks.graph。


[ **! Ks.graph** ](-ks-graph.md)コマンドは、カーネル モジュールの拡張機能をストリーミングでの最も強力な拡張機能コマンドのいずれか。 このコマンドから、開始点を特定のカーネル モードでグラフ全体の画像を表示します。

実行する前に[ **! ks.graph**](-ks-graph.md)、アクティブにされていることができるすべてのライブラリの拡張機能を有効にすることがあります。 これを行うには、発行、 [ **! ks.libexts enableall** ](-ks-libexts.md)コマンド。 出力 **! ks.graph**位相的に並べ替えられた順序で、カーネル モードのグラフの説明テキストになります。 以下に例を示します。

```dbgcmd
kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
```

この例では、テレックス USB マイクから 2 つの Sndrec32.exe をキャプチャするキャプチャ グラフが表示されます。 個々 のレコードが名前 (前のセクションでは usbaudio) で始まり、フィルターにフィルターのアドレス (0xFFAAA768) と子 pin ファクトリ (2) の数量を示します。

以下の各エントリは、各ファクトリが列挙され、各ピンのインスタンス (0xFFB1CAF0)、各インスタンスに対応するファイル オブジェクト (0x811DEEB8)、接続の方向、その接続のコピー先のアドレスとアドレスの一覧を示します、変換先の pin (0xFFA8B008)。 各ピンのキューに置かれた (7) および Irp (1) 保留中の数も表示されます。

順方向のシンボルの接続 (-&gt;)、暗証番号 (pin) が出力ピンがあり、入力ピンに接続されていることを示します。 シンボルの逆方向の接続 (&lt;-)、その一方で、入力ピンには、接続の発信元を表示します。 出力は次のように続行されます。

```dbgcmd
"splitter" Filter ffa0c660, Child Factories 2
    Output Factory 0:
        Pin 81250008 (File ffb10028, -> "kmixer" 8123c000) Irps(q/p) = 3, 0
        Pin 811df9c0 (File ffaaf2f0, -> "kmixer" 81236000) Irps(q/p) = 3, 0
    Input Factory 1:
        Pin ffa8b008 (File ffb26d68, <- "usbaudio" ffb1caf0) Irps(q/p) = 1, 7
"kmixer" Filter ffa65b70, Child Factories 4
    Input Factory 2:
        Pin 81236000 (File ffaaf7d0, <- "splitter" 811df9c0) Irps(q/p) = 0, 0
    Output Factory 3:
        Pin 81252d00 (File 811df1d8) Irps(q/p) = 10, 0
"kmixer" Filter ffb03808, Child Factories 4
    Input Factory 2:
        Pin 8123c000 (File ffb10130, <- "splitter" 81250008) Irps(q/p) = 0, 0
    Output Factory 3:
        Pin ffa1e9c0 (File 81253468) Irps(q/p) = 10, 0
```

グラフには、するには、次の手順を使用します。

**このグラフに従います。**

1.  目的の pin を確認します。 0xFFB1CAF0 を検討してください。 usbaudio の pin (factory 0) を出力します。

2.  接続の pin を確認します。 この例では、スプリッター pin 0xFFA8B008 です。

3.  接続の方向を確認し、フィルター名を検索することを視覚的に移動します。 (ただし、リストの並べ替え位相的。)この例では、右向きの矢印は、以下の対応するピンを検索する一覧で、このエントリを検索する必要があることを示します。 スプリッター フィルター 0xFFA0C660 はすぐ下に。

4.  フィルター暗証番号 (pin) のインスタンスの一覧に暗証番号 (pin) の宛先アドレスを検索します。 この場合、このアドレスは 0xFFA8B008 です。

次のグラフ: コマンドが停止しているグラフからも、指定した開始点を分析することもできます。 これを行うには、指定の 4、*フラグ*パラメーター。

```dbgcmd
kd> !graph 812567c0 7 4

Attempting a graph build on 812567c0...  Please be patient...

Graph With Starting Point 812567c0:

"emu10k" Filter ff9ebb98, Child Factories 5
    Output Factory 0:
        Pin 812567c0 (File 811c6630, -> "splitter" 811df960) Irps(q/p) = 8, 0
"splitter" Filter ffb18890, Child Factories 2
    Output Factory 0:
        Pin 811df430 (File ffa55f90) Irps(q/p) = 10, 0
    Input Factory 1:
        Pin 811df960 (File 81187820, <- "emu10k" 812567c0) Irps(q/p) = 0, 8

Analyzing a Hung Graph From 812567c0:

Suspect Filters (For a Hung Graph):
    "emu10k" Filter ff9ebb98 or class "PortCls Wave Cyclic" is suspect.
        Reasons For This Analysis:
            - No critical pin has less than 8 queued Irps
            - Downstream "splitter" pin 811df960 is starved
        Irps to check:
            81255418 811df008 81252008 81255280 81250b30 ffa1fe70 81252e70 ffa01d98

NOTE: The above is based on heuristic analysis.  It is not designed to be a
      replacement for an actual developer looking at this particular hang!  The
      filters listed as suspects may or may not be the actual cause of the
      stall!
```

このような出力では"%sort%"一覧を確認します。 これらの問題のあるフィルターでは、グラフの進行のクリティカル パスにいるものです。 停止のアナライザーによって生成された理由に基づいて、その時点からデバッグを開始します。

**注**  この機能は、停止しているグラフ上でのみ使用する必要があります。 アナライザーには、どのくらいの時間グラフはこの状態になってするが知る方法はありません。 デバッガーに分割し、分析を停止しているグラフとして実行されているグラフは、問題のあるフィルターを引き続き表示されます。

 

 

 





