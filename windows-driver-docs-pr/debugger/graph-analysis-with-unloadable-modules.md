---
title: アンロード可能なモジュールを使用したグラフ分析
description: アンロード可能なモジュールを使用したグラフ分析
ms.assetid: 12441fa1-3d19-4485-815c-546367f31567
keywords:
- カーネル デバッグを読み込めないモジュールのストリーミング
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22993d158783a7661bb55bf0c24dc275b2a390c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342076"
---
# <a name="graph-analysis-with-unloadable-modules"></a>アンロード可能なモジュールを使用したグラフ分析


このセクションでは、KMixer など読み込めないモジュールを使用する場合に影響する可能性があるシナリオについて説明します。

ロードした後は最初のコマンドの使用方法で拡張モジュールを初期化します。 初期化では、拡張機能モジュールは、すべてのモジュールが読み込まれ、シンボルが正しいかどうかをチェックします。 任意の個別のモジュールはアンロードされてまたはが正しくないシンボルが読み込まれて、拡張機能には、識別、ダンプのモジュールなどを処理するライブラリの拡張機能が無効にします。 この場合、手動で無効になっているモジュールを再度有効にする必要があります。

上記のような状況は、ブート時に、拡張機能を読み込む場合に発生する可能性があります。 Ks.dll をロードし、発行する場合にこのシナリオが発生する可能性がありますが具体的を[ **.reboot** ](-reboot--reboot-target-computer-.md)コマンド。 または、起動中にデバッガーを中断および、その時点で Ks.dll をロードする場合に発生する可能性があります。

次の例では、テレックス USB マイクからの 2 つのストリーム (sndrec32) を取得します。 上の重大な**スプリッター!FilterProcess**を実行していると[ **! ks.graph** ](-ks-graph.md)スプリッターのフィルターが生成されます。

```dbgcmd
kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
"splitter" Filter ffa0c660, Child Factories 2
    Output Factory 0:
        Pin 81250008 (File ffb10028) Irps(q/p) = 3, 0
        Pin 811df9c0 (File ffaaf2f0) Irps(q/p) = 3, 0
    Input Factory 1:
        Pin ffa8b008 (File ffb26d68, <- "usbaudio" ffb1caf0) Irps(q/p) = 1, 7
```

この例では、KMixer が読み込まれ、スプリッターに接続されているが、Kmixer がグラフに表示されません。 Irp が分割の出力ピン、キューに登録が、まだ **! ks.graph** KMixer を見つけてコマンドをバック トレースできません。 問題を[ **! ks.libexts 詳細**](-ks-libexts.md)さらに詳しく調査するコマンド。

```dbgcmd
kd> !libexts details
## LibExt Details:
--------------------------------------------------
LibExt "portcls!" :
    Status :  ACTIVE
    This is the port class library extension to the KS DLL.  It supports
    dumping wave cyclic, wave pci, irp streams, and several other upper
    level structures.
    Commands Exported: pciaudio
    Help : pchelp
    Hooks : dump dumpqueue dumpcircuit conv(file) conv(device) graph
LibExt "STREAM!" :
    Status :  ACTIVE
    This is the stream class library extension to the KS DLL.  It supports
    dumping device extensions, filters, streams, and SRBs.
    Hooks : dump enumdevobj graph
LibExt "kmixer!" :
    Status :  INACTIVE
    This is the KMIXER extension to the KS DLL.  It supports
    virtually nothing at this point!
    Hooks : dump graph
```

上記の出力に基づいて、拡張機能の KMixer セクションは現在無効 (状態。非アクティブな) にします。 拡張機能モジュールは、KMixer が読み込まれていないコンテキストで最初に使用した、ため Ks.dll にアンロードのモジュールに時間がかかる参照を防ぐために拡張機能の KMixer セクションが無効にします。

KMixer を明示的に有効にするを使用することができます[ **! ks.libexts** ](-ks-libexts.md)で、**を有効にする**パラメーターは、次のようにします。

```dbgcmd
kd> !libexts enable kmixer
LibExt "kmixer" has been enabled.

kd> !graph ffa0c6d4 7
Attempting a graph build on ffa0c6d4...  Please be patient...
Graph With Starting Point ffa0c6d4:
"usbaudio" Filter ffaaa768, Child Factories 2
    Output Factory 0:
        Pin ffb1caf0 (File 811deeb8, -> "splitter" ffa8b008) Irps(q/p) = 7, 1
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

KMixer はキャプチャ グラフで想定どおりに表示されます。

 

 





