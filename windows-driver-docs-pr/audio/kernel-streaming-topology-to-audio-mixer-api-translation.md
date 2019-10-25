---
title: カーネル ストリーミング トポロジからオーディオ ミキサー API への変換
description: カーネル ストリーミング トポロジからオーディオ ミキサー API への変換
ms.assetid: ee89dc67-c9f3-41cd-8a09-0c46d636fe64
keywords:
- ミキサー API WDK オーディオ
- カーネルストリーミング WDK オーディオ
- オーディオミキサーライン WDK オーディオ
- ソースミキサーライン WDK オーディオ
- 宛先ミキサーの線 WDK オーディオ
- KS トポロジからミキサーラインの WDK オーディオへの変換
- ミキサーの線 WDK オーディオ
- KS WDK audio との混合ストリーム
- KS トポロジ WDK オーディオ
- シンクが WDK オーディオをピン留めする
- ソースピン WDK オーディオ
- KS WDK audio をピン留めし、翻訳する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac47a44751cfe58dcc851fe2c76c3c8fabd91a47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833167"
---
# <a name="kernel-streaming-topology-to-audio-mixer-api-translation"></a>カーネル ストリーミング トポロジからオーディオ ミキサー API への変換


## <span id="kernel_streaming_topology_to_audio_mixer_api_translation"></span><span id="KERNEL_STREAMING_TOPOLOGY_TO_AUDIO_MIXER_API_TRANSLATION"></span>


**ミキサー** API は、オーディオミキサーデバイスに関する情報を取得するために使用される一連の Windows マルチメディア機能です。 **ミキサー** API は、オーディオミキサーの線を変換元と変換先の線として分類します。 *ソース行*は、オーディオカードへの入力 (CD、マイク、ライン入力、wave など) です。 *宛先行*はカードからの出力 (たとえば、スピーカー、ヘッドホン、電話回線、wave) です。 ソース行が有効であるためには、変換元から変換先への一意のパスを持つ必要があります。 1つのソース行が複数の変換先にマップされる場合がありますが、1つのパスでコピー先の行にソース行を接続することはできません。 **ミキサ**API の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

オーディオアダプター用の WDM ドライバーは、ハードウェアおよびそれらのパスで使用できる機能を通じて、データパスを表す KS フィルタートポロジを公開します。 [WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver) (Wdmaud および WDMAud ファイル内) は、KS フィルタートポロジを解釈し、**ミキサー** API を介して公開されている、対応するソースとターゲットのミキサ線を生成する必要があります。 また、WDMAud は、**ミキサー** API 呼び出しを処理し、アダプタードライバーによって管理されるフィルターのピンとノードに対する同等のプロパティ呼び出しに変換します。

[KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver) (KMixer) と[swmidi システムドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver) (swmidi) は、カーネルオーディオスタックの不可欠なコンポーネントです。 KMixer は、システム全体のオーディオミックス、ビット深度の変換、サンプルレートの変換、および PCM オーディオストリームのチャネルからスピーカーへの構成 (スーパーミックス) 変換を提供します。 SWMidi は、MIDI ストリームの高品質なソフトウェア合成機能を提供します。 システムオーディオドライバー、SysAudio (Sysaudio .sys、「 [Sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)」を参照) は、KMixer と swmidi の機能を、インストールされているオーディオアダプタードライバーと組み合わせて、機能強化された[仮想オーディオデバイス](virtual-audio-devices.md)を形成します。

WDMAud は、KS 部分と、オーディオスタックのレガシ ( [Winmm.dll システムコンポーネント](user-mode-wdm-audio-components.md#winmm_system_component)を参照) 部分の間のインターフェイスを管理します。 WDMAud は、SysAudio で仮想化されたフィルターのピンを、SndVol32 などのアプリケーションで提供されている従来のミキサーラインに変換します。 KS トポロジからミキサー行への変換は、次のように実行されます。

-   KS トポロジでのソースピン (KSPIN\_データフロー\_OUT) は、ターゲットミキサーラインとして公開されます (MIXERLINE\_COMPONENTTYPE\_DST\_*XXX*)。

-   KS トポロジ内のシンクピン (KSPIN\_データフロー\_) は、ソースミキサー行 (MIXERLINE\_COMPONENTTYPE\_SRC\_*XXX*) として公開されます。

-   WDMAud は、フィルターグラフのエンドポイントにあるソースピンから始まる KS フィルターグラフをウォークし、シンクピンに到達するまでデータフローと反対の方向にグラフを走査します。

-   トラバーサル中に検出された各 KS ノードでサポートされているプロパティは、ソースミキサーライン上のコントロールとして公開されます。

上記の最初の2つの項目では、用語の違いによって、KS のソースピンとシンク pin をターゲットとソースのミキサー行にマッピングすることが混乱する可能性があります。 KS では、デバイスは、シンク (入力) ピンとソース (出力) ピンを持つフィルターにラップされます。 "シンク" と "ソース" という用語は、フィルターではなく、2つのフィルター間で (通常はバッファーされる) 接続を指します。

-   上流フィルターのソースピンは、接続に入るデータストリームのソースです。

-   データストリームは、下流のフィルターのシンクピンを介して接続を終了します。

対照的に、ミキサーラインの用語はデバイス中心です。

-   ソースミキサーの線は、デバイスに入ってくるストリームのソースです。

-   ターゲットミキサーの線は、デバイスを終了するストリームの宛先です。

また、KS の用語は、KS フィルターのピンに割り当てられるストリームフローの方向に多少一貫性がありません。 ピン記述子は、 [**Kspin\_データフロー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-kspin_dataflow)列挙値を使用して方向を指定します。

-   シンク pin を介してフィルターに入るストリームには、の KSPIN\_データフロー\_の方向があります。

-   ソースピンを介してフィルターを終了するストリームには、KSPIN\_データフロー\_の方向があります。

"In" と "out" の方向は明確にフィルター処理を行いますが、"シンク" と "ソース" という用語は接続中心です。

WDMAud によって使用されるトポロジ解析アルゴリズムの詳細については、「 [WDMAud topology の解析](wdmaud-topology-parsing.md)」を参照してください。

このセクションには次のものも含まれます。

[トポロジの Pin](topology-pins.md)

[トポロジノード](topology-nodes.md)

[SysTray と SndVol32](systray-and-sndvol32.md)

[フィルタートポロジの公開](exposing-filter-topology.md)

 

 




