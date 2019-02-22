---
title: MIDI トランスポート
description: MIDI トランスポート
ms.assetid: ce9ec589-0aea-4ed9-a60d-50f2ddfb0c13
keywords:
- ポート ドライバー WDK のオーディオ、シンセサイザー
- ミニポート ドライバー WDK のオーディオ、シンセサイザー
- MIDI トランスポート WDK オーディオ
- wave オーディオ、MIDI トランスポートの WDK をシンクします。
- シンセサイザー WDK オーディオ、MIDI トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9b9dfaed609b57ed9070c597bab95108505b433
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552175"
---
# <a name="midi-transport"></a>MIDI トランスポート


## <span id="midi_transport"></span><span id="MIDI_TRANSPORT"></span>


Dmu ポート ドライバーは、Dmu ミニポート ドライバーのシンセサイザーの作業のフロント エンドとバックエンドの辺に関与します。 ポート ドライバーでは、MIDI データのタイムスタンプ付きで構成され、sequencer をストリームをルーティングする MIDI ストリームを入力します。 Sequencer は、タイムスタンプを削除し、そのタイムスタンプが期限、ミニポート ドライバーに生 MIDI メッセージを渡します。 (DLS 通過したデータの右ポート ドライバーなしの前処理のミニポート ドライバーにします。)

Dmu ミニポート ドライバー MIDI 入力ストリームは、wave データに変換を取得するときは、その出力が (「シンセサイザー シンク」または「レンダリング シンク」とも呼ばれます)、wave シンクによって管理されます。

Dmu ポート ドライバーでは、DirectMusic ユーザー モード コンポーネントから DirectMusic データを受け取る入力ピンとカーネル ストリーミング フィルター dmusic.dll します。 ポートのドライバーでは、合成されたオーディオ ストリームに出力を wave 出力ピンもあります。 Wave シンクは、この暗証番号 (pin) を管理し、そのデータを記述するためのメモリ内、シンセサイザーを指示します。 この配置では、カーネルのストリーミングの詳細をシンセサイザー切り離しています。 Dmu ミニポート ドライバーでは、のみ、MIDI の入力ストリームからデータを wave を合成することの詳細を処理する必要があります。 ポート ドライバーをシステムに、波形データを送信して、SysAudio のフィルターのグラフに接続するすべてのフィルター正しくフローします。 次の図に示すように、MIDI データは Dmu ポート ドライバーにし、シーケンス処理には、Dmu ミニポート ドライバーに渡されます。

![portdmus ドライバーを通じて midi と dl のデータの流れを示す図](images/dmportmi.png)

ミニポート ドライバーに MIDI データ ポート ドライバーの別の部分で指定されているバッファーにレンダリングされるは、wave 形式に変換します。 wave シンク。 、DirectSound へとユーザー モードでは、出て、ではなく wave 出力に移動して、オーディオ ハードウェア、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)します。 DirectSound は実際には、KMixer を公開する API と DirectSound アクセラレータは、KMixer によってハードウェアでエミュレートされたソフトウェアではなく高速化されているミキサー関数で構成されています。

[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)、Dmu ポート ドライバー、オーディオ フィルター グラフでは、どのビルドのハードウェアに接続します。 ポート ドライバーのウェーブ シンク部分では、ハードウェア デバイスに接続できる SysAudio wave アウト pin を取得するには、使用データを渡します。 (かどうかがハードウェアまたはソフトウェアのシンセサイザー) に関係なく Dmu ミニポート ドライバーから wave データをプルし、すべてのタイミングの問題を処理します。 ユーザー モードと比較して、ミニポート ドライバーに似ています、シンセサイザー wave シンクは同じポート ドライバーの一部です。

Wave pin KSPIN のデータ方向の公開 Dmu のミニポート ドライバーでは、ホストにその出力を提供できる場合、\_データフロー\_OUT (を参照してください[ **KSPIN**](https://msdn.microsoft.com/library/windows/hardware/ff563483))、どの SysAudio認識して KMixer に接続します。

Wave シンクの詳細については、次を参照してください。[カーネル モードのソフトウェアのシンセサイザーの A Wave シンク](a-wave-sink-for-kernel-mode-software-synthesizers.md)します。

このセクションが含まれています。

[IMXF インターフェイス](imxf-interfaces.md)

[アロケーター](allocator.md)

 

 




