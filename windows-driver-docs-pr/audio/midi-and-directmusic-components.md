---
title: MIDI と DirectMusic のコンポーネント
description: MIDI と DirectMusic のコンポーネント
ms.assetid: 6334f332-31ba-4daf-aad1-94bb65d25153
keywords:
- WDM オーディオコンポーネント WDK
- ユーザーモードコンポーネント WDK オーディオ
- カーネルモードコンポーネント WDK オーディオ
- コンポーネントのキャプチャ WDK オーディオ
- MIDI コンポーネント WDK オーディオ
- DirectMusic WDK audio, コンポーネント
- WDK オーディオの再生
- タイムスタンプ付き MIDI WDK オーディオ
- メモ-イベントの WDK オーディオ
- メモオフイベント WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22546ede83dc9a6eb09ddb44670741b5fa15cd2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832626"
---
# <a name="midi-and-directmusic-components"></a>MIDI と DirectMusic のコンポーネント


## <span id="midi_and_directmusic_components"></span><span id="MIDI_AND_DIRECTMUSIC_COMPONENTS"></span>


アプリケーションプログラムは、ユーザーとカーネルモードのコンポーネントを組み合わせて、MIDI と DirectMusic のストリームをキャプチャして再生します。

アプリケーションでは、次のいずれかのソフトウェアインターフェイスを使用して、MIDI の再生とキャプチャを行うことができます。

-   Microsoft Windows マルチメディア **Midiout * * * xxx*および **midiout ** * * xxx 関数

-   DirectMusic API

**Midiout ** * * xxx 関数と **midiout * * * xxx*関数の動作は、従来の MIDI ドライバーとデバイスの機能に基づいています。 Windows 98 以降、 [WDMAud システムドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver)は、これらの関数の呼び出しを、WDM オーディオドライバーへのコマンドに変換します。 ただし、古いソフトウェアやハードウェアの動作をエミュレートすることで、**Midiout * * * xxx*および **midiout * * * xxx 関数に*よって、DirectMusic API で使用できるようになった有効桁数と拡張機能が犠牲になります。 DirectMusic と Windows マルチメディア MIDI 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

DirectMusic と Windows マルチメディア MIDI 関数は、MIDI および DirectMusic ストリームを処理するオーディオフィルターグラフを構築する[sysaudio システムドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)のクライアントです。 グラフの作成は、これらのソフトウェアインターフェイスを使用するアプリケーションに対して透過的です。

### <a name="span-idmidi_componentsspanspan-idmidi_componentsspanspan-idmidi_componentsspanmidi-components"></a><span id="MIDI_Components"></span><span id="midi_components"></span><span id="MIDI_COMPONENTS"></span>MIDI コンポーネント

次の図は、midi アプリケーションが midi データを*再生*するために使用するユーザーモードとカーネルモードのコンポーネントを示しています。 このアプリケーションは、 [winmm.dll システムコンポーネント](user-mode-wdm-audio-components.md#winmm_system_component)である winmm.dll に実装されている **midiout * * * Xxx*関数を使用して、WDM オーディオドライバーに対してインターフェイスを行います。

![midi 再生コンポーネントを示す図](images/midiplay.png)

上の図の MIDI アプリケーションは、タイムスタンプ付きの MIDI イベントを MIDI ファイルから読み取り、再生します。 MIDI および DMus ミニポートドライバーは、ベンダーが提供するコンポーネントであることを示すために、暗いボックスとして表示されます。 必要に応じて、ベンダーは、システムが提供するミニポートドライバー (FMSynth、UART、または Dマス目の Uart) のいずれかを使用することを選択できます。これは、カスタムミニポートドライバーを記述する代わりに使用します。 図内の他のすべてのコンポーネントは、システムによって提供されます。

一般的な MIDI 再生アプリケーションのメインループは、 **timeSetEvent**を呼び出して、次のノートオンイベントまたはノートオフイベントをスケジュールします。 この呼び出しは、そのパラメーターの1つとして、アプリケーションのコールバックルーチンへの関数ポインターを受け取ります。 イベントが発生し、オペレーティングシステムがコールバックルーチンを呼び出すと、このルーチンは**Midiout短縮メッセージ**を呼び出して、1つまたは複数のスケジュールされたメモをオンまたはオフにします。 **Midiout短縮 msg**関数は、ページロックされたデータバッファーに MIDI メッセージを格納し、呼び出し中にこのメモリをページに記録する必要がないようにします。 **TimeSetEvent**と**Midiout短縮メッセージ**の呼び出しの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

WDMAud は、ユーザーとカーネルモードの両方のコンポーネント (Wdmaud と Wdmaud) で構成され、 **Midiout短縮メッセージ**からの未加工の MIDI メッセージが到着した時刻を記録します。 WDMAud は、これらのタイムスタンプを MIDI メッセージと組み合わせて、図の WDMAud の下に表示されるカーネルモードコンポーネントのいずれかに送信する MIDI ストリームを生成します。

MIDI アプリケーションのオーディオフィルターグラフを構築する場合、SysAudio は、3つの可能な接続 (SWMidi、MIDI ポート、または DMus ポートドライバー) のいずれか1つだけを選択します。これは、前の図に示されています。 アプリケーションで既定の MIDI デバイスを選択すると、まず、midi または DMus ミニポートドライバーに MIDI ピンがあるシンセサイザーデバイスが、SysAudio によって検索されます。 そのようなデバイスがレジストリに見つからない場合、SysAudio は[swmidi システムドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver) (swmidi .sys) を代わりに使用します。 SWMidi は、ソフトウェアで wavetable シンセサイザーを実装する KS フィルターであり、wave オーディオストリームをレンダリングできるデバイスのみを必要とします。

SWMidi は、すべての音声を組み合わせて1つの wave PCM ストリームを生成し、 [KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)に出力します。 KMixer は、PCM 形式の wave ストリームを WaveCyclic または WavePci デバイスに渡します。このデバイスのポートとミニポートドライバーは、図の左下隅に表示されます。 また、KMixer は、 [usbaudio クラスシステムドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver)によって制御される USB オーディオデバイスに出力ストリームを渡すことができます (図には示されていません)。

上の図では、MIDI ポートドライバーは WDMAud からタイムスタンプ付きの MIDI ストリームを受け取り、それを未加工の MIDI メッセージに変換します。これは、MIDI ミニポートドライバーがシンセサイザーデバイスを経由して再生します。 MIDI ポートドライバーには、ソフトウェアで実装され、タイマー精度1ミリ秒で未加工の MIDI メッセージをスケジュールすることができる sequencer が含まれています。

DMus ポートドライバーは、シンセサイザーデバイスにハードウェア sequencer が搭載されている場合、MIDI ポートドライバーよりもはるかに高いタイミングの精度を実現できます。 この場合、DMus ミニポートドライバーでは、Isr (割り込みサービスルーチン) およびその他の高優先度操作を使用した CPU 時間の競合によって生じるジッターを吸収するのに十分な大きさのハードウェアバッファーを指定する必要があります。 DMus ポートドライバーがミニポートドライバーに出力する MIDI ストリーム内のタイムスタンプは、100ナノ秒解像度の64ビット値です。

DMusic シンセがハードウェアシーケンサーを搭載していない場合は、DMus ポートドライバーのソフトウェア sequencer に依存する必要があります。これは、MIDI ポートドライバーの場合と同様に、1ミリ秒のタイマー精度を持ちます。

アダプタードライバーは、GUID 値が**clsid\_PortMidi**または**Clsid\_Portdmus**で[**PCNEWPORT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出して、MIDI または dmus のポートドライバーを作成します。 Windows XP 以降では、MIDI および DMus ポートドライバーは同じソフトウェア実装を共有します。

前の図の下部に表示されるのは、Portcls に含まれるシステム指定のミニポートドライバー FMSynth、UART、および Dマス Uart です。 アダプタードライバーは、 [**Pcnewminiport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)を呼び出すことによって、これらのミニポートドライバーのいずれかを作成します。 FMSynth と UART は[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)インターフェイスを提供し、Dマス Uart は[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)インターフェイスを提供します。 UART は現在互換性のために残されています (Windows 98 Gold の後)。また、既存のドライバーに対してのみサポートされています。 新しいアダプタードライバーでは、代わりに、UART の機能のスーパーセットを実装する Dマス Uart (Windows 98 SE 以降、Windows 2000 以降) を使用する必要があります。 Dマス Uart は、DLS ダウンロードもハードウェアシーケンスもサポートしない DMus ミニポートドライバーの一例です。 Windows Driver Kit (WDK) のサンプルオーディオドライバーでは、FMSynth ドライバーと Dマスの Uart ミニポートドライバーのソースコードを使用できます。

次の図は、midi アプリケーションプログラムが midi データを*キャプチャ*するために使用するユーザーモードとカーネルモードのコンポーネントを示しています。 このアプリケーションは、**Midiin * * * Xxx*関数を介して、WDM オーディオドライバーに対してインターフェイスを行います。

![midi キャプチャコンポーネントを示す図](images/midicapt.png)

上の図では、MIDI および DMus ミニポートドライバーが、ベンダーが提供するコンポーネントであることを示すために、暗くなったボックスとして表示されています。 必要に応じて、ベンダーはシステムが提供するミニポートドライバー、UART または Dマス目のキャプチャを使用することを選択できます。 図内の他のすべてのコンポーネントは、システムによって提供されます。

MIDI データのソースは通常、MPU-401 デバイスです。 **Pcnewminiport ポート**を呼び出すことにより、アダプタードライバーはシステムが提供するミニポートドライバー、UART または dマス目のキャプチャを作成し、MPU-401 デバイスから MIDI データをキャプチャできます。 ここでも、UART は互換性のために残されています。代わりに、新しいドライバーで Dマスの Uartcapture を使用する必要があります (Windows 98 SE 以降、Windows 2000 以降)。

Midi ノートオンまたはノートオフイベントが発生するたびに、midi または DMusic キャプチャミニポートドライバー (前の図の下部) は、midi メッセージにタイムスタンプを追加してから、midi または DMus ポートドライバーにフローする MIDI ストリームに追加します。

MIDI または DMusic キャプチャポートドライバーは、タイムスタンプ付きの MIDI ストリームを Wdmaud に出力します。これは、WDMAud システムドライバーのカーネルモードの半分です。 ユーザーモードの半分 (Wdmaud) は、Winmm.dll に実装されている **Midiin * * * Xxx*関数を使用して、タイムスタンプ付きの MIDI ストリームをアプリケーションプログラムに出力します。

図の上部にある MIDI アプリケーションは、タイムスタンプ付きの MIDI イベントを MIDI ファイルに書き込みます。 アプリケーションが**Midiinopen**を呼び出して MIDI 入力ストリームを開くと、関数ポインターがコールバックルーチンに渡されます。 ノートオンまたは終了イベントが発生すると、オペレーティングシステムは、1つまたは複数のタイムスタンプ付き MIDI メッセージを含むデータブロックを使用してコールバックルーチンを呼び出します。 これらのメッセージのタイムスタンプは、MIDI または DMus ミニポートドライバーによって最初に生成されたものと基本的に同じです。

### <a name="span-iddirectmusic_componentsspanspan-iddirectmusic_componentsspanspan-iddirectmusic_componentsspandirectmusic-components"></a><span id="DirectMusic_Components"></span><span id="directmusic_components"></span><span id="DIRECTMUSIC_COMPONENTS"></span>DirectMusic コンポーネント

次の図は、DirectMusic アプリケーションプログラムが MIDI データを*再生*または*キャプチャ*するために使用するユーザーおよびカーネルモードのコンポーネントを示しています。

![directmusic の再生とキャプチャのコンポーネントを示す図](images/dmusplay.png)

再生コンポーネントは、前の図の左半分に表示され、キャプチャコンポーネントは右側に表示されます。 DMus ミニポートドライバーは、ベンダーが提供するコンポーネントであることを示すために、暗いボックスとして表示されます。 必要に応じて、ベンダーはシステムが提供するミニポートドライバー、Dマス目または Dマス目のキャプチャを使用することもできます。 図のその他のコンポーネントはシステムによって提供されます。

図の左上隅にある DirectMusic アプリケーションは、タイムスタンプ付きの MIDI ストリームをファイルからユーザーモードの[DirectMusic システムコンポーネント](user-mode-wdm-audio-components.md#directmusic_system_component)(dmusic .dll) に送信します。これにより、ストリームが dmus ポートドライバーに送信されます。 このドライバーは、DirectMusic シンセサイザーまたは MPU-401 デバイス (使用可能な場合) のミニポートドライバーにバインドできます。 または、ポートドライバーを[dmusic システムドライバー](kernel-mode-wdm-audio-components.md#dmusic_system_driver) (dmusic .sys) にバインドすることもできます。これは、ソフトウェアで DLS 対応 wavetable シンセサイザーを実装し、wave オーディオをレンダリングできるデバイスのみを必要とする、システムによって提供される dmus ミニポートドライバーです。一連.

SWMidi と同様に、dmusic ドライバー (Dmusic) は、すべての音声を組み合わせて1つの PCM 形式の wave ストリームを生成し、KMixer に出力します。 KMixer は、wave ストリームを wave デバイスに渡すことができます。この場合、ポートとミニポートドライバーは、図の左下隅に表示されます。また、この図には表示されない USBAudio システムドライバーによって制御される USB オーディオデバイスに渡すこともできます。

DirectMusic キャプチャコンポーネントは、前の図の右側半分に表示されます。 図の右下隅にある DMusic capture ミニポートドライバーは、キャプチャハードウェアを制御し、記録する各 MIDI メッセージにタイムスタンプを設定します。 DMus ポートドライバーは、タイムスタンプ付きの MIDI ストリームをユーザーモードの DirectMusic コンポーネント (DMusic .dll) に送信します。 アプリケーションは、このストリームに DirectMusic API 経由でアクセスし、タイムスタンプ付きの MIDI データをファイルに書き込みます。

アダプタードライバーでは、システムによって提供される Dマス間キャプチャミニポートドライバーを使用して、MPU-401 キャプチャデバイスを制御できます。 アダプタードライバーは、このミニポートドライバーを作成します。これは、GUID 値の**CLSID\_Dマス**を持つ**pcnewminiport ポート**を呼び出します。 結果として得られるミニポートドライバーオブジェクトは、 **IMiniportDMus**インターフェイスをサポートします。 Dマスソースコードは、Windows Driver Kit (WDK) のサンプルオーディオドライバーに含まれています。

DirectMusic アプリケーションは、(SWMidi (Swmidi) などの **Midiout * * * Xxx*デバイスを選択した場合にも実行できます。 わかりやすくするために、前の図ではこのパスを省略しています。 正常に動作させるには、DMusic ドライバー (Dmusic .sys) に最初の DLS ダウンロードが必要です。SWMidi を使用すると、この要件を回避できます。

 

 




