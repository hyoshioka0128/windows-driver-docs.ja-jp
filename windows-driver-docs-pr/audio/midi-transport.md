---
title: MIDI トランスポート
description: MIDI トランスポート
ms.assetid: ce9ec589-0aea-4ed9-a60d-50f2ddfb0c13
keywords:
- ポートドライバー WDK オーディオ、シンセサイザー
- ミニポートドライバー WDK オーディオ、シンセサイザー
- MIDI トランスポート WDK オーディオ
- wave シンク WDK オーディオ、MIDI トランスポート
- シンセサイザー WDK オーディオ、MIDI トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c7093218d39a15842028a8d58ae132ee1e52e83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830359"
---
# <a name="midi-transport"></a>MIDI トランスポート


## <span id="midi_transport"></span><span id="MIDI_TRANSPORT"></span>


DMus ポートドライバーは、DMus ミニポートドライバーのシンセサイザー作業の前後に関係しています。 ポートドライバーは、タイムスタンプ付きの MIDI データで構成される MIDI ストリームを入力し、そのストリームを sequencer にルーティングします。 Sequencer はタイムスタンプを削除し、タイムスタンプが期限切れになったときに未処理の MIDI メッセージをミニポートドライバーに渡します。 (DLS データは、ポートドライバーを使用して、前処理を行わずにミニポートドライバーに渡されます)。

DMus ミニポートドライバーの MIDI 入力ストリームが wave データに変換されると、その出力は wave シンク ("シンセサイザーシンク" または "レンダーシンク" とも呼ばれます) によって管理されます。

DMus ポートドライバーは、DirectMusic ユーザーモードコンポーネント (dmusic .dll) からの DirectMusic データを受け付ける入力ピンを持つカーネルストリーミングフィルタを実装します。 ポートドライバーには、合成されたオーディオストリームを出力する wave 出力ピンもあります。 Wave シンクはこの pin を管理し、メモリ内でデータを書き込む場所をシンセに指示します。 このようにすることで、カーネルストリーミングの詳細からシンセを分離できます。 DMus ミニポートドライバーは、入力 MIDI ストリームからのから wave データの詳細を処理するためだけに必要です。 ポートドライバーは wave データをシステムに送信し、SysAudio のフィルターグラフは、すべてのフローが正しくなるようにフィルターに接続します。 次の図に示すように、MIDI データは DMus ポートドライバーにあり、シーケンス処理後に DMus ミニポートドライバーに渡されます。

![portdmus ドライバーを使用した midi と dls データのフローを示す図](images/dmportmi.png)

ミニポートドライバーは、MIDI データを wave 形式に変換します。これは、ポートドライバーの別の部分 (wave シンク) で指定されたバッファーにレンダリングされます。 次に、ユーザーモードでの動作と同じように DirectSound に移動するのではなく、 [KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)を使用してオーディオハードウェアに出力します。 DirectSound は、KMixer を公開する API にすぎません。 DirectSound アクセラレーションは、KMixer によってソフトウェアでエミュレートされるのではなく、ハードウェアで加速するミキサー関数で構成されています。

オーディオフィルターグラフを構築する[sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)は、dmus ポートドライバーをハードウェアに接続します。 ポートドライバーの wave シンク部分では、SysAudio がハードウェアデバイスに接続できる、wave out pin を使用してデータを送信します。 これは、(ハードウェアまたはソフトウェアのシンセサイザーであるかどうかに関係なく) DMus ミニポートドライバーからウェーブデータをプルし、すべてのタイミングの問題を処理します。 ユーザーモードと比較すると、ミニポートドライバーは、シンセに似ています。一方、wave シンクはポートドライバーの一部にすぎません。

DMus ミニポートドライバーが出力をホストに渡すことができる場合、その出力は KSPIN\_データフロー\_のデータの方向を持つ wave ピンを公開します (「 [**kspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)」を参照)。 sysaudio は、KMixer を認識して接続します。

Wave シンクの詳細については、「[カーネルモードのソフトウェアシンセサイザーの Wave シンク](a-wave-sink-for-kernel-mode-software-synthesizers.md)」を参照してください。

このセクションには次のものも含まれます。

[IMXF インターフェイス](imxf-interfaces.md)

[アロケーター](allocator.md)

 

 




