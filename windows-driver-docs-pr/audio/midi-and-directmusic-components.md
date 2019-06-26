---
title: MIDI と DirectMusic のコンポーネント
description: MIDI と DirectMusic のコンポーネント
ms.assetid: 6334f332-31ba-4daf-aad1-94bb65d25153
keywords:
- WDM オーディオ コンポーネント WDK
- ユーザー モード コンポーネント WDK オーディオ
- カーネル モード コンポーネント WDK オーディオ
- コンポーネントの WDK オーディオをキャプチャします。
- MIDI コンポーネント WDK オーディオ
- DirectMusic WDK オーディオ、コンポーネント
- WDK オーディオを再生
- MIDI WDK オーディオのタイムスタンプ
- 注上のイベントの WDK オーディオ
- 注オフ イベント WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 808313dd844ef120261f58f03988b993eaff336e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363256"
---
# <a name="midi-and-directmusic-components"></a>MIDI と DirectMusic のコンポーネント


## <span id="midi_and_directmusic_components"></span><span id="MIDI_AND_DIRECTMUSIC_COMPONENTS"></span>


アプリケーション プログラムは、キャプチャし、再生 MIDI と DirectMusic ストリームを行うユーザー モードとカーネル モード コンポーネントとの組み合わせに依存します。

アプリケーションは、次のいずれかを使用できます MIDI の再生とキャプチャ ソフトウェア インターフェイス。

-   Microsoft Windows のマルチ メディア **midiOut * * * Xxx*と **midiIn * * * Xxx*関数

-   DirectMusic API

動作、**midiOut * * * Xxx*と **midiIn * * * Xxx*関数はレガシ MIDI ドライバーとデバイスの機能に基づいています。 Windows 98 以降、 [WDMAud システム ドライバー](user-mode-wdm-audio-components.md#wdmaud_system_driver) WDM オーディオ ドライバーをコマンドにこれらの関数の呼び出しを変換します。 ソフトウェアとハードウェアの以前の動作をエミュレートすることにより、ただし、**midiOut * * * Xxx*と **midiIn * * * Xxx*関数犠牲の有効桁数のタイミングと拡張機能を使用できますを通じて、DirectMusic API。 DirectMusic と Windows のマルチ メディア MIDI 関数の詳細については、Microsoft Windows SDK のドキュメントを参照してください。

DirectMusic と Windows のマルチ メディア MIDI 関数は、クライアントの[SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)MIDI と DirectMusic ストリームを処理できるオーディオ フィルター グラフをビルドします。 グラフの構築は、これらのソフトウェアのインターフェイスを使用するアプリケーションに対して透過的です。

### <a name="span-idmidicomponentsspanspan-idmidicomponentsspanspan-idmidicomponentsspanmidi-components"></a><span id="MIDI_Components"></span><span id="midi_components"></span><span id="MIDI_COMPONENTS"></span>MIDI コンポーネント

次の図は、ユーザー モードおよびカーネル モード コンポーネント、MIDI アプリケーションを使用している*再生*MIDI データ。 このアプリケーションのインターフェイスを通じて WDM オーディオ ドライバーを **midiOut * * * Xxx*で実装される、関数、 [WinMM システム コンポーネント](user-mode-wdm-audio-components.md#winmm_system_component)、Winmm.dll します。

![midi 再生コンポーネントを示す図](images/midiplay.png)

前の図に MIDI アプリケーションでは、MIDI ファイルから MIDI イベントのタイムスタンプを読み取るし、再生されます。 MIDI と Dmu ミニポート ドライバーは、コンポーネントのベンダーが提供できることを示すために暗いボックスとして表示されます。 該当する場合は、仕入先のカスタムのミニポート ドライバーを記述する代わりに、システム提供のミニポート ドライバー--FMSynth、UART、または DMusUART--のいずれかを使用こともできます。 すべての他のコンポーネントの図には、システム提供します。

一般的な MIDI 再生アプリケーション呼び出しのメイン ループ**timeSetEvent**次のメモまたは注オフ イベントがスケジュールされます。 この呼び出しはそのパラメーターの 1 つとして、アプリケーションのコールバック ルーチンへの関数ポインターを受け取ります。 このルーチンを呼び出すイベントが発生するし、オペレーティング システムは、コールバック ルーチンを呼び出し、 **midiOutShortMsg**を 1 つまたは複数のスケジュールされたノート有効または無効にします。 **MidiOutShortMsg**関数は、ページにこのメモリの呼び出し中に不要にページ ロックされたデータ バッファーで MIDI メッセージを格納します。 詳細については、 **timeSetEvent**と**midiOutShortMsg**呼び出しは、Microsoft Windows SDK ドキュメントを参照してください。

WDMAud、両方のユーザー モードとカーネル モード コンポーネント (Wdmaud.drv および Wdmaud.sys) から成る、位置からメッセージを生 MIDI 時刻を記録しますが、 **midiOutShortMsg**呼び出しが到着します。 WDMAud は、WDMAud 下の図に表示されるカーネル モード コンポーネントの 1 つに送られる MIDI ストリームを生成する MIDI メッセージをこれらのタイムスタンプを結合します。

MIDI アプリケーションのオーディオ フィルター グラフを作成するときに、次の 3 つ考えられるへの接続の--SWMidi、MIDI ポート、または Dmu ポート ドライバー - 前の図に表示される 1 つだけ SysAudio を選択します。 アプリケーションでは、既定の MIDI デバイスを選択した場合は、SysAudio は最初にシンセサイザー デバイスが MIDI または Dmu ミニポート ドライバーには、MIDI 暗証番号 (pin) が含まれています。 SysAudio は代わりに、レジストリでこのようなデバイスが見つからない場合、 [SWMidi システム ドライバー](kernel-mode-wdm-audio-components.md#swmidi_system_driver) (Swmidi.sys)。 SWMidi はソフトウェアでは、ウェーブ シンセサイザーを実装する KS フィルターと wave オーディオ ストリームをレンダリングするデバイスのみが必要です。

SWMidi ミックスへの出力が 1 つのウェーブ PCM のストリームを生成するには、その音声はすべて、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)します。 さらに、KMixer は、図の左下隅にあるポートおよびミニポート ドライバーが表示される、WaveCyclic または WavePci デバイスに PCM でフォーマットされた wave ストリームを渡します。 または、KMixer はによって制御される USB オーディオ デバイスにその出力ストリームを渡すことができます、 [USBAudio クラスのシステム ドライバー](kernel-mode-wdm-audio-components.md#usbaudio_class_system_driver) (図に示されていません)。

上記の図では、MIDI ポート ドライバーは WDMAud から MIDI のタイムスタンプ付きストリームを受け取るし、シンセサイザー デバイスを介して、MIDI ミニポート ドライバーを再生する生の MIDI メッセージに変換します。 MIDI ポート ドライバーには、シーケンサー、ソフトウェアに実装され、生 MIDI メッセージ 1 ミリ秒のタイマー精度のスケジュールを設定することはこれが含まれています。

Dmu ポート ドライバーはシンセサイザー デバイスには、ハードウェア sequencer が含まれている場合は、MIDI ポート ドライバーよりもはるかに高いタイミング精度を実現できます。 この場合は、Dmu のミニポート ドライバーでは、Isr (割り込みサービス ルーチン) での CPU 時間とその他の優先度の高い操作での競合に起因ジッターを緩和するのに十分な大きさであるハードウェア バッファーを指定する必要があります。 Dmu ポート ドライバーに出力するミニポート ドライバー MIDI ストリームのタイムスタンプは、100 ナノ秒単位の精度と 64 ビット値です。

DMusic シンセサイザーでは、ハードウェア sequencer はありません、MIDI ポート ドライバーが 1 ミリ秒のタイマー精度を Dmu ポート ドライバーのソフトウェアの sequencer に依存する必要があります。

アダプタのドライバを呼び出して MIDI または Dmu ポート ドライバーを作成します[ **PcNewPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewport)の GUID 値を持つ**CLSID\_PortMidi**または**CLSID\_PortDMus**、それぞれします。 Windows XP 以降では、MIDI、Dmu ポート ドライバーは、同じソフトウェア実装を共有します。

上記の図の下部に表示されるは、FMSynth、UART、および DMusUART、Portcls.sys に含まれているシステム提供のミニポート ドライバーの名前です。 呼び出して、アダプターのドライバーがこれらのミニポート ドライバーのいずれかに作成します. [ **PcNewMiniport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-pcnewminiport)します。 FMSynth と UART 提供[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidi)インターフェイス、および DMusUART を提供する[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iminiportdmus)インターフェイス。 UART (Windows 98 金) した後は廃止されておりは既存のドライバーに対してのみサポートされていることに注意してください。 新しいアダプターのドライバーでは、DMusUART (Windows 98 se と後で、および Windows 2000 以降)、UART の機能のスーパー セットを実装する代わりに使用する必要があります。 DMusUART は、DLS ダウンロードもハードウェアのシーケンス処理をサポートしている Dmu ミニポート ドライバーの例に示します。 FMSynth と DMusUART ミニポート ドライバーのソース コードは、サンプル オーディオ ドライバーには、Windows Driver Kit (WDK) で使用できます。

次の図は、ユーザー モードおよびカーネル モード コンポーネント、MIDI アプリケーション プログラムを使用している*キャプチャ*MIDI データ。 このアプリケーション インターフェイスを通じて WDM オーディオ ドライバー、**midiIn * * * Xxx*関数。

![midi キャプチャ コンポーネントを示す図](images/midicapt.png)

上記の図では、MIDI、Dmu ミニポート ドライバーは、コンポーネントのベンダーが提供できることを示す暗くなったボックスとして表示されます。 該当する場合は、仕入先は UART または DMusUARTCapture、システム提供のミニポート ドライバーのいずれかを使用する代わりに選択可能性があります。 すべての他のコンポーネントの図には、システム提供します。

MIDI データのソースは、通常、片方デバイスです。 呼び出して**PcNewMiniport**アダプターのドライバーはシステム提供のミニポート ドライバー、MIDI デバイスからデータを片方をキャプチャするには、UART または DMusUARTCapture のいずれかで作成できます。 ここでも、UART は廃止、され、新しいドライバーは代わりに DMusUARTCapture (Windows 98 se と後で、および Windows 2000 以降) を使用する必要があります。

MIDI 注上または注オフ イベントが発生するたび、MIDI または DMusic キャプチャ ミニポート ドライバー (上記の図の下部) MIDI または Dmu ポート ドライバーに流れる MIDI ストリームに追加する前に、MIDI メッセージにタイムスタンプを追加します。

MIDI または DMusic キャプチャ ポート ドライバーは、WDMAud システム ドライバーの半分を Wdmaud.sys、カーネル モードには、タイムスタンプ付き MIDI ストリームに出力します。 ユーザー モードの半分、Wdmaud.drv を通じてアプリケーション プログラムへの出力タイムスタンプ MIDI ストリーム、**midiIn * * * Xxx*関数で、Winmm.dll で実装されます。

図の上部にある MIDI アプリケーションでは、MIDI イベントのタイムスタンプを MIDI ファイルを書き込みます。 アプリケーションの呼び出し時に**midiInOpen** MIDI 入力ストリームを開くには、関数ポインターに渡す、コールバック ルーチン。 注上または注オフ イベントが発生、オペレーティング システムは、1 つ以上のタイムスタンプ付き MIDI メッセージを含むデータ ブロックでコールバック ルーチンを呼び出します。 これらのメッセージのタイムスタンプは基本的に同じものを MIDI または Dmu のミニポート ドライバーが当初生成したです。

### <a name="span-iddirectmusiccomponentsspanspan-iddirectmusiccomponentsspanspan-iddirectmusiccomponentsspandirectmusic-components"></a><span id="DirectMusic_Components"></span><span id="directmusic_components"></span><span id="DIRECTMUSIC_COMPONENTS"></span>DirectMusic コンポーネント

次の図は、DirectMusic アプリケーション プログラムで使用されるユーザー モードとカーネル モード コンポーネントを示しています。*再生*または*キャプチャ*MIDI データ。

![directmusic 再生とキャプチャ コンポーネントを示す図](images/dmusplay.png)

再生コンポーネントは上記の図の左半分に表示され、キャプチャ コンポーネントが、右側に表示されます。 Dmu のミニポート ドライバーは、コンポーネントのベンダーが提供できることを示すために暗いボックスとして表示されます。 必要に応じて、仕入先代わりに使用できます、DMusUART または DMusUARTCapture のシステム提供のミニポート ドライバーのいずれか。 他のコンポーネントの図には、システムが提供します。

図の左上隅で DirectMusic アプリケーションに指示タイムスタンプ MIDI からのストリーム ファイルをユーザー モードに[DirectMusic システム コンポーネント](user-mode-wdm-audio-components.md#directmusic_system_component)(DMusic.dll) を順番に指示 Dmu ポート ドライバーにストリームします。 このドライバーは、1 つが使用可能な場合、DirectMusic シンセサイザーまたは片方のデバイスのミニポート ドライバーにバインドできます。 または、ポート ドライバーにバインドできる、 [DMusic システム ドライバー](kernel-mode-wdm-audio-components.md#dmusic_system_driver) (Dmusic.sys)、これは、システム提供の Dmu ミニポート ドライバー ソフトウェアでは、DL 対応ウェーブ シンセサイザーを実装して、デバイスのみを必要とします。wave オーディオ ストリームを表示できます。

など、SWMidi DMusic ドライバー、Dmusic.sys、KMixer に出力される 1 つの PCM でフォーマットされた wave ストリームを生成するには、その音声のすべてを合成します。 KMixer、さらに、渡すことができます、wave ストリーム ポートおよびミニポート ドライバーが、図の左下隅に現れる場合、wave デバイス、または USB オーディオ デバイスが、図に表示されない、USBAudio システム ドライバーによって制御されます。

DirectMusic キャプチャ コンポーネントは、上記の図の右半分に表示されます。 図の右下隅で DMusic キャプチャ ミニポート ドライバーは、各 MIDI メッセージを記録する、そのキャプチャ ハードウェアとタイムスタンプを制御します。 Dmu ポート ドライバーでは、ユーザー モードの DirectMusic コンポーネント DMusic.dll タイムスタンプ付きの MIDI ストリームを出力します。 アプリケーションでは、DirectMusic API を介してこのストリームにアクセスして、MIDI のタイムスタンプ データをファイルに書き込みます。

アダプターのドライバーでは、片方のキャプチャ デバイスを制御するのにシステム提供の DMusUARTCapture ミニポート ドライバーを使用できます。 アダプタのドライバを呼び出してこのミニポート ドライバーを作成します**PcNewMiniport**の GUID 値**CLSID\_DMusUARTCapture**します。 結果として得られるミニポート ドライバー オブジェクトがサポートする、 **IMiniportDMus**インターフェイス。 DMusUARTCapture ミニポート ドライバーのソース コードは、サンプル オーディオ ドライバーには、Windows Driver Kit (WDK) で使用できます。

DirectMusic アプリケーションも一通り、**midiOut * * * Xxx* SWMidi (Swmidi.sys) を選択した場合などのデバイス。 わかりやすくするため、このパスは、上記の図から省略されます。 DMusic ドライバー (Dmusic.sys) は正しく実行するには、最初の DL ダウンロードが必要です。SWMidi を使用すると、この要件が回避できます。

 

 




