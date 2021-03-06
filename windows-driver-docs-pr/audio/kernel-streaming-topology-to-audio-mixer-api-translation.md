---
title: カーネル ストリーミング トポロジからオーディオ ミキサー API への変換
description: カーネル ストリーミング トポロジからオーディオ ミキサー API への変換
ms.assetid: ee89dc67-c9f3-41cd-8a09-0c46d636fe64
keywords:
- API の WDK オーディオ ミキサー
- WDK オーディオのストリーミング カーネル
- オーディオ ミキサー行 WDK オーディオ
- ソース ミキサー行 WDK オーディオ
- 移行先ミキサー行 WDK オーディオ
- ミキサー行 WDK オーディオを KS トポロジを翻訳します。
- ミキサー行 WDK オーディオ
- KS ミキシング WDK オーディオをストリーミングします。
- KS トポロジ WDK オーディオ
- シンク ピン WDK オーディオ
- ソース ピン WDK オーディオ
- KS WDK のピンのオーディオ、翻訳します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2fb11d4223749d342f0bb0b07cdbbb63016bad2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359830"
---
# <a name="kernel-streaming-topology-to-audio-mixer-api-translation"></a>カーネル ストリーミング トポロジからオーディオ ミキサー API への変換


## <span id="kernel_streaming_topology_to_audio_mixer_api_translation"></span><span id="KERNEL_STREAMING_TOPOLOGY_TO_AUDIO_MIXER_API_TRANSLATION"></span>


**ミキサー** API は、一連の Windows のマルチ メディア関数オーディオ ミキサー デバイスに関する情報を取得するために使用します。 **ミキサー** API は、オーディオ ミキサー行元とコピー先の行として分類します。 *ソース行*(たとえば、CD、マイク、行で、および wave) は、オーディオ カードへの入力します。 *出力先の行*(たとえば、スピーカー、ヘッドホン、電話回線、および wave) カードからの出力します。 有効にするソース行、先に、元の一意のパスが必要です。 1 つのソース行が 1 つ以上の変換先にマップ可能性がありますが、パスを 1 つ以上が接続できないソースの行出力先の行。 詳細については、**ミキサー** API、Microsoft Windows SDK のドキュメントを参照してください。

オーディオのアダプターの WDM ドライバーでは、ハードウェアとそれらのパスで使用できる関数を介したデータ パスを表す KS フィルター トポロジを公開します。 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver) (Wdmaud.sys と Wdmaud.drv ファイル) 内、KS フィルター トポロジを解釈し、対応するソースとを通じて公開されている変換先ミキサー線を生成する必要があります、**ミキサー**API です。 WDMAud も処理、**ミキサー** API を呼び出すし、フィルターのピンとアダプターのドライバーによって管理されているノードで同等のプロパティの呼び出しに変換します。

[KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver) (Kmixer.sys) と[SWMidi システム ドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver) (Swmidi.sys) はカーネル オーディオ スタックの不可欠なコンポーネントです。 KMixer は、システム全体のオーディオ ミキシング、ビット数の変換、サンプル速度変換、および PCM のオーディオ ストリームのチャネルのスピーカーの構成 (supermix) 翻訳を提供します。 SWMidi は、MIDI ストリームの合成を高品質なソフトウェアを提供します。 システム オーディオ ドライバー、SysAudio (Sysaudio.sys; を参照してください[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver))、フォームの拡張機能にインストールされているオーディオ アダプター ドライバー KMixer SWMidi の機能を組み合わせて[仮想オーディオデバイス](virtual-audio-devices.md)します。

WDMAud KS 部分と、従来の間のインターフェイスを管理する (を参照してください[WinMM システム コンポーネント](user-mode-wdm-audio-components.md#winmm_system_component))、オーディオ スタックの一部です。 WDMAud は、SysAudio 仮想化されたフィルターのピンを SndVol32 などのアプリケーションで説明されているレガシ ミキサーの行に変換します。 KS トポロジからミキサー行への変換は、次のように実行されます。

-   ピンのソース (KSPIN\_データフロー\_アウト)、KS トポロジが出力先ミキサーの行として公開されます (MIXERLINE\_COMPONENTTYPE\_DST\_*XXX*)。

-   ピンのシンク (KSPIN\_データフロー\_IN)、KS トポロジがソース ミキサーの行として公開されます (MIXERLINE\_COMPONENTTYPE\_SRC\_*XXX*)。

-   WDMAud には、フィルターのグラフのエンドポイントであるし、シンク暗証番号 (pin) に達するまで、データ フローとは反対方向にあるグラフを走査するソース ピン KS フィルター グラフの先頭がについて説明します。

-   移動中に検出される各 KS ノードでサポートされているプロパティは、ミキサーのソース行上のコントロールとして公開されます。

KS のマップ上の最初の 2 つの項目をミキサー行の送信先と送信元にソースとシンクのピンは用語で違いがあるため混乱を招く可能性があります。 KS、デバイスがシンク (入力) ピンとソース (出力) ピンを持つフィルターでラップされます。 用語「シンク」と「ソース」は、フィルターにありませんが、2 つのフィルター間 (通常はバッファーされている) の接続にではなくを参照してください。

-   アップ ストリームのフィルターのソースの暗証番号 (pin) は、接続が入力したデータ ストリームのソースです。

-   データ ストリームは、ダウン ストリームのフィルターのシンクの暗証番号 (pin) 経由の接続を終了します。

これに対し、ミキサー行の用語はデバイス中心です。

-   ソース ミキサーの行は、デバイスの入力ストリームのソースです。

-   移行先ミキサー線は、デバイスに存在するストリームの転送先です。

また、KS 用語では、このストリーム フロー方向を KS フィルターで pin を割り当てることでやや一貫性がありません。 暗証番号 (pin) の記述子を使用して、 [ **KSPIN\_データフロー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-kspin_dataflow)方向を指定する列挙値。

-   シンクの暗証番号 (pin) を使用して、フィルターを入力するストリームが KSPIN 方向を\_データフロー\_in です。

-   ソースの暗証番号 (pin) を使用して、フィルターを終了するストリームが KSPIN 方向を\_データフロー\_アウトします。

用語「シンク」と"source"では、接続を中心とした"in"、"out"方向は明確にフィルターを中心とした、です。

WDMAud で使用されるアルゴリズムの解析中のトポロジの詳細については、次を参照してください。 [WDMAud トポロジ解析](wdmaud-topology-parsing.md)します。

このセクションが含まれています。

[トポロジのピン](topology-pins.md)

[トポロジのノード](topology-nodes.md)

[システム トレイと SndVol32](systray-and-sndvol32.md)

[フィルターのトポロジを公開します。](exposing-filter-topology.md)

 

 




