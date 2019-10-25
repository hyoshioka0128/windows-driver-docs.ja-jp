---
title: MIDI フィルターと DirectMusic フィルター
description: MIDI フィルターと DirectMusic フィルター
ms.assetid: 622aa4ae-c855-4088-bc1a-30dff7a24d23
keywords:
- オーディオフィルター WDK audio、MIDI
- オーディオフィルター WDK audio、DirectMusic
- DirectMusic WDK audio, フィルター
- MIDI フィルター WDK オーディオ
- オーディオデバイスの列挙 (WDK)
- システムが提供するミニポートドライバー WDK オーディオ
- システム指定のポートドライバー WDK オーディオ
- シンセサイザー WDK オーディオ、フィルター
- WDK オーディオ、MIDI をフィルター処理します
- WDK オーディオ、DirectMusic をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b3e4ef561585c986eefcb50836b946a11724a44
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830369"
---
# <a name="midi-and-directmusic-filters"></a>MIDI フィルターと DirectMusic フィルター


## <span id="midi_and_directmusic_filters"></span><span id="MIDI_AND_DIRECTMUSIC_FILTERS"></span>


MIDI と DirectMusic のフィルターは、MIDI 音楽データを合成、出力、またはキャプチャするデバイスを表します。 通常、アプリケーションは、DirectMusic API または Microsoft Windows マルチメディア **Midiout * * * xxx*および **midiout * * * xxx*関数を使用して、これらのデバイスの機能にアクセスします。 これらのインターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

MIDI または DirectMusic*シンセサイザー*フィルターは、タイムスタンプ付きの midi イベントで構成される midi ストリームを入力として受け取ります。 このフィルターは、次のいずれかを出力します。

-   Wave 形式のデジタルオーディオストリーム

-   スピーカーのセットを駆動できるアナログオーディオ信号

MIDI または DirectMusic の*出力*フィルターは、タイムスタンプ付きの midi イベントで構成される midi ストリームを入力として受け取ります。 フィルターは、未加工の MIDI メッセージを外部 MIDI サウンドモジュールに出力します。

MIDI または DirectMusic*キャプチャ*フィルターは、midi キーボードまたはその他の外部 midi デバイスから一連の未加工の midi メッセージを入力として受け取ります。 このフィルターは、タイムスタンプ付きの MIDI イベントで構成される MIDI ストリームを出力します。

1つの MIDI または DirectMusic フィルターは、フィルターが表すデバイスの機能に応じて、合成、出力、キャプチャという3つの機能を組み合わせて実行できます。 たとえば、純粋 MPU-401 デバイスは出力とキャプチャを実行しますが、合成は実行しません。

### <a name="span-idmidi_filterspanspan-idmidi_filterspanspan-idmidi_filterspanmidi-filter"></a><span id="MIDI_Filter"></span><span id="midi_filter"></span><span id="MIDI_FILTER"></span>MIDI フィルター

MIDI フィルターは、ポート/ミニポートドライバーのペアとして実装されます。 MIDI フィルターファクトリは、次のように MIDI フィルターを作成します。

-   このメソッドは、MIDI ミニポートドライバーオブジェクトをインスタンス化します。

-   これは、GUID 値**CLSID\_PortMidi**を持つ[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって、MIDI ポートドライバーオブジェクトをインスタンス化します。

-   ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出して、ミニポートドライバーをポートドライバーにバインドします。

[サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。 ポートとミニポートドライバーは、 [Iportmidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportmidi)インターフェイスと[IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)インターフェイスを介して相互に通信します。

Midi 出力およびシンセサイザーデバイスをサポートするために、MIDI ポートドライバーには、1ミリ秒のタイマー精度で未処理の MIDI メッセージをミニポートドライバーに出力するソフトウェア sequencer が含まれています。

### <a name="span-iddirectmusic_filterspanspan-iddirectmusic_filterspanspan-iddirectmusic_filterspandirectmusic-filter"></a><span id="DirectMusic_Filter"></span><span id="directmusic_filter"></span><span id="DIRECTMUSIC_FILTER"></span>DirectMusic フィルター

DirectMusic フィルターは、MIDI フィルターの機能のスーパーセットを提供します。 スーパーセットには、次の追加機能が含まれます。

-   MIDI 音色を説明する波形および articulation データを含む DLS (ダウンロード可能なサウンド) リソース。 [**Ksk プロパティ\_の\_dls\_download**](https://docs.microsoft.com/previous-versions/ff537396(v=vs.85)) set property 要求は、dls リソースをフィルターにダウンロードします。

-   選択可能な音色の数を増やすためのチャネルグループ。 [**Dmus\_カーネル\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/ns-dmusicks-_dmus_kernel_event)構造は、各タイムスタンプ付き midi メッセージを midi ストリームにパッケージ化するために使用され、そのメッセージに使用するチャネルグループを指定します。

-   ハードウェアの MIDI シーケンス処理をサポートする100ナノ秒の解像度を使用した64ビットタイムスタンプ。 DMUS\_カーネル\_イベント構造では、MIDI メッセージの高解像度タイムスタンプを指定します。

チャネルグループでは、同時に再生できるノートの数は、元の MIDI 仕様の16チャネルに限定されなくなりました。 シンセサイザーで使用できる音声の数によってのみ制限されます。

DirectMusic フィルターは、ポート/ミニポートドライバーのペアとして実装されます。 DirectMusic フィルターファクトリは、次のように DirectMusic フィルターを作成します。

-   このメソッドは、DMus (DirectMusic) ミニポートドライバーオブジェクトをインスタンス化します。

-   このメソッドは、GUID 値**CLSID\_PortDMus**で[**pcnewport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewport)を呼び出すことによって、dmus ポートドライバーオブジェクトをインスタンス化します。

-   ポートドライバーの[**IPort:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iport-init)メソッドを呼び出して、ミニポートドライバーをポートドライバーにバインドします。

[サブデバイス作成](subdevice-creation.md)のコード例では、このプロセスを示しています。 ポートとミニポートドライバーは、 [Iportdmus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)インターフェイスと[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)インターフェイスを介して相互に通信します。

DirectMusic シンセサイザーデバイスをサポートするために、DMus ポートドライバーには低解像度 (1 ミリ秒) のソフトウェア sequencer が含まれています。この sequencer は、再生予定の時点でハードウェアシーケンサーのバッファーにタイムスタンプ付き MIDI イベントを出力できます。 DirectMusic の出力デバイスをサポートするために、ポートドライバーのソフトウェア sequencer は、再生時に未加工の MIDI メッセージを出力するように構成することもできます。

### <a name="span-idenumerating_midi_and_directmusic_devicesspanspan-idenumerating_midi_and_directmusic_devicesspanspan-idenumerating_midi_and_directmusic_devicesspanenumerating-midi-and-directmusic-devices"></a><span id="Enumerating_MIDI_and_DirectMusic_Devices"></span><span id="enumerating_midi_and_directmusic_devices"></span><span id="ENUMERATING_MIDI_AND_DIRECTMUSIC_DEVICES"></span>MIDI と DirectMusic デバイスの列挙

Windows マルチメディア**Midiinxxx**または**midiinxxx**関数を使用して midi 入力デバイスまたは出力デバイスを列挙する場合、アプリケーションは、ミニポートドライバーが*MIDI pin*を公開する WDM デバイスのみを表示できます。 これらは、未加工の MIDI ストリームを管理するが、DLS や channel グループなどの高度な機能はサポートしていないピンです。 ただし、デバイスを DirectMusic で列挙する場合、アプリケーションは MIDI ピンと*DirectMusic pin*の両方を備えた WDM デバイスを表示できます。 DirectMusic ピンは、タイムスタンプ付きの MIDI ストリームを管理し、DLS および channel グループをサポートします。

カスタムミニポートドライバーを実装する場合、ハードウェアベンダーは通常、MIDI ミニポートドライバーまたは DMus ミニポートドライバーのいずれかを書き込みますが、両方を書き込むことはありません。 MIDI ミニポートドライバーは、MIDI ピンのみを公開できます。 ただし、DMus ミニポートドライバーでは、MIDI と DirectMusic の両方の pin を公開できます。これにより、個別の MIDI ミニポートドライバーを作成する必要がなくなります。 DirectMusic フィルターの MIDI pin の例については、Windows Driver Kit (WDK) の Dマス Uart サンプルオーディオドライバーを参照してください。

Midi または DirectMusic のピン留めのデータ範囲を指定するときに、MIDI または DMus のミニポートドライバーは、種類が KSDATAFORMAT\_\_type のメジャー形式を指定します。これは、midi pin または KSK の種類が\_MIDI の場合は種類が "\_KS" になります。DirectMusic pin の\_サブタイプ\_DIRECTMUSIC です。 MIDI と DirectMusic の pin のデータ範囲記述子の例は、それぞれ[Midi ストリームのデータ範囲](midi-stream-data-range.md)と[Directmusic ストリームのデータ範囲](directmusic-stream-data-range.md)に表示されます。

Midi フィルターの MIDI pin インスタンスは、 [IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)インターフェイスを公開します。 DirectMusic フィルターの MIDI または DirectMusic pin インスタンスは、 [Imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)インターフェイスを公開します。

Windows Me/98 では、DirectMusic で同じ MPU-401 デバイスが2回列挙されることがあります。 これは、一部のハードウェアベンダーが、MPU-401 デバイスをレガシ、WDM 前 MIDI デバイス、および WDM デバイスとして公開しているためです。 レガシデバイスの場合、DirectMusic は、Ihvaudio からへの直接パスを表す MPU-401 デバイスを列挙します。 WDM デバイスの場合、DirectMusic は、次の一連のコンポーネントで構成される circuitous パスを使用して、同じ MPU-401 デバイスを列挙します。

1.  DMusic .dll

2.  DMusic16

3.  MMSystem .dll

4.  WDMAud

5.  WDMAud

6.  ベンダーのミニポートドライバー

Windows マルチメディアコントロールパネル (Mmsys. cpl) に表示される MIDI シンセサイザーは、WDM デバイスと同じ名前になります。

### <a name="span-idsystem-supplied_port_and_miniport_driversspanspan-idsystem-supplied_port_and_miniport_driversspanspan-idsystem-supplied_port_and_miniport_driversspansystem-supplied-port-and-miniport-drivers"></a><span id="System-Supplied_Port_and_Miniport_Drivers"></span><span id="system-supplied_port_and_miniport_drivers"></span><span id="SYSTEM-SUPPLIED_PORT_AND_MINIPORT_DRIVERS"></span>システムが提供するポートとミニポートドライバー

システムによって提供される MIDI および DMus ミニポートドライバーは、PortCls システムドライバーに組み込まれています。

-   FMSynth ミニポートドライバーは、OPL3 スタイルの FM 合成を実装する MIDI デバイスへのインターフェイスを提供します。

-   UART ミニポートドライバーは、MPU-401 ハードウェアインターフェイスの MIDI デバイスをサポートしていますが、このドライバーは互換性のために残されています (Windows 98 Gold の後)。また、既存のアダプタードライバーでのみサポートされています。 新しいアダプタードライバーコードでは、代わりに、UART を優先し、その機能のスーパーセットを実装する Dマス Uart ドライバー (Windows 98 SE および Windows Me の場合は windows 2000 以降) を使用する必要があります。

アダプタードライバーは、 [**Pcnewminiport ポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewminiport)関数を呼び出すことによって、システムが提供するミニポートドライバーにアクセスできます。 Windows Driver Kit (WDK) には、FMSynth と Dマスの Uart のミニポートドライバーも含まれています。 これらのサンプルのソースコードを変更することにより、ハードウェアベンダーは、デバイスの独自の機能を管理するためにドライバーを拡張できます。

Dマス Uart は、MIDI ピンと DirectMusic ピンの両方を公開する DMus ミニポートドライバーの一例ですが、DLS ダウンロードやハードウェアシーケンス処理はサポートしていません。 ミニポートドライバーの DirectMusic レンダリング pin には、いくつかの[Ksk Propsetid\_シンセサイザー](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)プロパティをサポートする、シンセサイザーノード ([**KSNODETYPE\_シンセサイザー**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)) があります。 ミニポートドライバー自体は、KSCATEGORY\_RENDER と KSCATEGORY\_CAPTURE のカテゴリに含まれていますが、KSCATEGORY\_シンセサイザー (内部シンセサイザーは含まれていないため) には含まれていません。 詳細については、WDK の Dマス Uart サンプルオーディオドライバーを参照してください。

Windows XP 以降では、MIDI および DMus ポートドライバーが同じ内部ソフトウェア実装を使用することに注意してください。 これは、 **Pcnewport**の呼び出し時に、 **Clsid\_portmidi**と**clsid\_portdmus** guid と同等であることを意味します。 以前のバージョンの Windows 用に作成されたアプリケーションでは、MIDI と DMus のポートドライバーを統合することによって動作が変更されることはありません。

 

 




