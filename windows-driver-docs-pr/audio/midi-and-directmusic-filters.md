---
title: MIDI と DirectMusic フィルター
description: MIDI と DirectMusic フィルター
ms.assetid: 622aa4ae-c855-4088-bc1a-30dff7a24d23
keywords:
- オーディオ フィルター WDK オーディオ、MIDI
- オーディオ フィルター WDK オーディオ、DirectMusic
- DirectMusic WDK、オーディオ フィルター
- MIDI は、WDK オーディオをフィルター処理します。
- オーディオ デバイス WDK の列挙
- システム提供のミニポート ドライバー WDK オーディオ
- システム指定のポート ドライバー WDK オーディオ
- シンセサイザー WDK のオーディオ、フィルター
- WDK のオーディオ、MIDI をフィルター処理します。
- WDK のオーディオ、DirectMusic をフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaac8459cff2e29ebb2ee8f6bed6beced2629321
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539176"
---
# <a name="midi-and-directmusic-filters"></a>MIDI と DirectMusic フィルター


## <span id="midi_and_directmusic_filters"></span><span id="MIDI_AND_DIRECTMUSIC_FILTERS"></span>


MIDI と DirectMusic フィルターは、合成、出力、または、MIDI 音楽データをキャプチャするデバイスを表します。 アプリケーションが通常 DirectMusic API または Microsoft Windows のマルチ メディアのいずれかにこれらのデバイスの機能がアクセス **midiOut * * * Xxx*と **midiIn * * * Xxx*関数。 これらのインターフェイスの詳細については、Microsoft Windows SDK のドキュメントを参照してください。

MIDI または DirectMusic*シンセサイザー* MIDI イベントのタイムスタンプから成る MIDI ストリーム入力としてフィルターを受け取ります。 フィルターは、次のいずれかを出力します。

-   Wave 形式のデジタル オーディオ ストリーム

-   一組のスピーカーを促進できるアナログのオーディオ信号

MIDI または DirectMusic*出力*MIDI イベントのタイムスタンプから成る MIDI ストリーム入力としてフィルターを受け取ります。 フィルターは、外部の MIDI サウンド モジュールに生の MIDI メッセージを出力します。

MIDI または DirectMusic*キャプチャ*フィルターが MIDI キーボードまたはその他の外部の MIDI デバイスからメッセージを生 MIDI の一連の入力として受け取ります。 フィルターは、MIDI イベントのタイムスタンプから成る MIDI ストリームを出力します。

1 つの MIDI または DirectMusic フィルターは、合成、出力、およびフィルターを表すデバイスの機能によってキャプチャ----3 つの関数の組み合わせを実行できます。 たとえば、純粋なの片方デバイスは、出力とキャプチャがない合成を実行します。

### <a name="span-idmidifilterspanspan-idmidifilterspanspan-idmidifilterspanmidi-filter"></a><span id="MIDI_Filter"></span><span id="midi_filter"></span><span id="MIDI_FILTER"></span>MIDI フィルター

MIDI フィルターは、ポート/ミニポート ドライバーのペアとして実装されます。 MIDI フィルター ファクトリは、次のように、MIDI フィルターを作成します。

-   MIDI のミニポート ドライバー オブジェクトがインスタンス化します。

-   呼び出すことによって、MIDI ポート ドライバー オブジェクトをインスタンス化[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値**CLSID\_PortMidi**します。

-   ポート ドライバーの呼び出す[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)ポート ドライバーに、ミニポート ドライバーをバインドするメソッド。

コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。 ポートおよびミニポートのドライバーがを介して相互に通信、 [IPortMidi](https://msdn.microsoft.com/library/windows/hardware/ff536891)と[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)インターフェイス。

MIDI 出力とシンセサイザーをサポートするためには、デバイス、MIDI ポート ドライバーには 1 ミリ秒のタイマー精度のミニポート ドライバーに生の MIDI メッセージを出力するソフトウェア sequencer が含まれています。

### <a name="span-iddirectmusicfilterspanspan-iddirectmusicfilterspanspan-iddirectmusicfilterspandirectmusic-filter"></a><span id="DirectMusic_Filter"></span><span id="directmusic_filter"></span><span id="DIRECTMUSIC_FILTER"></span>DirectMusic フィルター

DirectMusic フィルターは、MIDI フィルターの機能のスーパー セットを提供します。 スーパー セットには、これらの追加機能が含まれます。

-   MIDI instruments を示す波形とアーティキュレーションのデータが含まれているリソースを DLS (ダウンロード可能なサウンド)。 A [ **KSPROPERTY\_シンセサイザー\_DLS\_ダウンロード**](https://msdn.microsoft.com/library/windows/hardware/ff537396)プロパティの設定要求は、フィルターに DLS リソースをダウンロードします。

-   選択可能な instruments の数を拡張するためのチャネル グループ。 [ **DMU\_カーネル\_イベント**](https://msdn.microsoft.com/library/windows/hardware/ff536340) MIDI ストリーム内の各タイムスタンプ MIDI メッセージをパッケージ化に使用される、構造体がそのメッセージを使用するには、どのチャネル グループを指定します。

-   ハードウェア MIDI シーケンス処理をサポートするための 100 ナノ秒の解像度の 64 ビットの時刻スタンプ。 DMU\_カーネル\_イベントの構造が高解像度 MIDI メッセージのタイムスタンプを指定します。

チャネル グループでは、同時に再生できるメモの数は元 MIDI 仕様の 16 のチャネルに限定ではありません。 音声シンセサイザーで使用できる数によってのみ制限されます。

DirectMusic フィルターは、ポート/ミニポート ドライバーのペアとして実装されます。 DirectMusic フィルター ファクトリは、次のように DirectMusic フィルターを作成します。

-   Dmu (DirectMusic) のミニポート ドライバー オブジェクトがインスタンス化します。

-   呼び出すことによって、Dmu ポート ドライバー オブジェクトをインスタンス化[ **PcNewPort** ](https://msdn.microsoft.com/library/windows/hardware/ff537715)の GUID 値**CLSID\_PortDMus**します。

-   ポート ドライバーの呼び出す[ **iport::init** ](https://msdn.microsoft.com/library/windows/hardware/ff536943)ポート ドライバーに、ミニポート ドライバーをバインドするメソッド。

コード例で[サブデバイス作成](subdevice-creation.md)このプロセスを示しています。 ポートおよびミニポートのドライバーがを介して相互に通信、 [IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)と[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)インターフェイス。

DirectMusic シンセサイザー デバイスをサポートするためには、Dmu ポート ドライバーには、MIDI イベントを再生できるようにスケジュールされているときに前のハードウェア sequencer のバッファーにタイムスタンプを出力できるは、低解像度 (1 ミリ秒) ソフトウェア sequencer が含まれています。 DirectMusic 出力デバイスをサポートするためには、ポート ドライバーのソフトウェアの sequencer で再生するには、生の MIDI メッセージを出力する構成もできます。

### <a name="span-idenumeratingmidianddirectmusicdevicesspanspan-idenumeratingmidianddirectmusicdevicesspanspan-idenumeratingmidianddirectmusicdevicesspanenumerating-midi-and-directmusic-devices"></a><span id="Enumerating_MIDI_and_DirectMusic_Devices"></span><span id="enumerating_midi_and_directmusic_devices"></span><span id="ENUMERATING_MIDI_AND_DIRECTMUSIC_DEVICES"></span>MIDI と DirectMusic デバイスを列挙します。

MIDI 入力または出力を列挙する場合、Windows のマルチ メディアを使用してデバイスを**midiInXxx**または**midiOutXxx**関数、アプリケーションはミニポート ドライバーが公開WDMデバイスのみを参照できます*MIDI ピン*します。 これらは、DL とチャネルのグループなどの高度な機能のサポートが不足しているが、生の MIDI ストリームを管理する pin です。 ただし、DirectMusic を介してデバイスを列挙する場合、アプリケーション、デバイスが表示されます WDM MIDI ピンの両方と*DirectMusic ピン*します。 DirectMusic ピンは、MIDI ストリームのタイムスタンプを管理し、配布リストとチャンネルのグループをサポートします。

カスタム ミニポート ドライバーを実装する場合は、ハードウェア ベンダーによって、MIDI ミニポート ドライバーまたは Dmu のミニポート ドライバーの両方ではなくいずれかが通常書き込みます。 MIDI ミニポート ドライバーでは、MIDI ピンのみを公開できます。 ただし、Dmu のミニポート ドライバーを公開できます MIDI と DirectMusic pin では、個別の MIDI ミニポート ドライバーを記述する必要があります。 DirectMusic フィルター MIDI 暗証番号 (pin) の例は、Dmusuart サンプル オーディオ ドライバー、Windows Driver Kit (WDK) でを参照してください。

MIDI または Dmu のミニポート ドライバーが型 KSDATAFORMAT の主要な形式を指定して MIDI または DirectMusic 暗証番号 (pin) のデータ範囲を指定するときに\_型\_音楽およびのサブフォーマット型 KSDATARANGE\_サブタイプ\_の MIDI、MIDI pin または KSDATARANGE\_サブタイプ\_DirectMusic pin の DIRECTMUSIC します。 MIDI と DirectMusic ピンのデータ範囲の記述子の例が記載[MIDI Stream データ範囲](midi-stream-data-range.md)と[DirectMusic Stream データ範囲](directmusic-stream-data-range.md)、それぞれします。

MIDI フィルター MIDI 暗証番号 (pin) のインスタンスを公開、 [IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)インターフェイス。 DirectMusic フィルター MIDI または DirectMusic の暗証番号 (pin) インスタンスを公開、 [IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)インターフェイス。

Windows Me、98/DirectMusic で同じの片方のデバイスを 2 回列挙場合があります。 理由は、一部のハードウェア ベンダーが、片方デバイスのレガシ、プレ WDM MIDI デバイスと WDM デバイスの両方を公開することです。 レガシ デバイスの場合は、DirectMusic は DMusic.dll から Ihvaudio.dll への直接パスを表す片方デバイスを列挙します。 WDM デバイスの場合は、DirectMusic は、次の一連のコンポーネントで構成される circuitous パスを使用して同じ片方デバイスを列挙します。

1.  DMusic.dll

2.  DMusic16.dll

3.  MMSystem.dll

4.  WDMAud.drv

5.  WDMAud.sys

6.  ベンダーのミニポート ドライバー

MIDI シンセサイザーに表示される、Windows マルチ メディア コントロール パネル (Mmsys.cpl) WDM デバイスと同じ名前になります。

### <a name="span-idsystem-suppliedportandminiportdriversspanspan-idsystem-suppliedportandminiportdriversspanspan-idsystem-suppliedportandminiportdriversspansystem-supplied-port-and-miniport-drivers"></a><span id="System-Supplied_Port_and_Miniport_Drivers"></span><span id="system-supplied_port_and_miniport_drivers"></span><span id="SYSTEM-SUPPLIED_PORT_AND_MINIPORT_DRIVERS"></span>システム指定のポートおよびミニポート ドライバー

PortCls システム ドライバーには、いくつかシステム提供 MIDI と Dmu ミニポート ドライバーが組み込まれています。

-   FMSynth ミニポート ドライバーは、MIDI デバイス OPL3 スタイル FM の合成を実装するインターフェイスを提供します。

-   UART ミニポート ドライバーは、片方のハードウェア インターフェイスでは、MIDI デバイスをサポートしていますが、このドライバー (Windows 98 金) した後は廃止されており既存のアダプターのドライバーに対してのみサポートされます。 新しいアダプターのドライバー コードには、UART を置き換え、その機能のスーパー セットを実装する DMusUART ミニポート ドライバー (Windows 98 SE、および Windows Me と Windows 2000 以降)、代わりに使用する必要があります。

アダプターのドライバーは、システム提供のミニポート ドライバーを呼び出すことによってアクセスできる、 [ **PcNewMiniport** ](https://msdn.microsoft.com/library/windows/hardware/ff537714)関数。 FMSynth と DMusUART ミニポート ドライバーも Windows Driver Kit (WDK) でのサンプル オーディオ ドライバーとして含まれています。 これらのサンプルのソース コードを変更すると、ハードウェア ベンダーが独自の機能を自分のデバイスを管理するドライバーを拡張できます。

DMusUART は、MIDI と DirectMusic の両方のピンを公開しますが、DLS ダウンロードまたはハードウェアのシーケンス処理はサポートされない Dmu ミニポート ドライバーの例に示します。 シンセサイザー ノードがある、ミニポート ドライバーの DirectMusic レンダリング pin ([**KSNODETYPE\_シンセサイザー**](https://msdn.microsoft.com/library/windows/hardware/ff537203)) いくつかサポートしている[KSPROPSETID\_シンセサイザー](https://msdn.microsoft.com/library/windows/hardware/ff537486)プロパティ。 ミニポート ドライバーは KSCATEGORY のカテゴリに含まれます\_レンダリングと KSCATEGORY\_キャプチャが含まれない KSCATEGORY\_シンセサイザー (ため、内部のシンセサイザーは含まれません)。 詳細については、WDK の DMusUART サンプル オーディオ ドライバーを参照してください。

Windows XP 以降では、MIDI、Dmu ポート ドライバーが、同じ内部ソフトウェア実装を使用することに注意してください。 つまり、 **CLSID\_PortMidi**と**CLSID\_PortDMus**を呼び出すときに、Guid が等しい**PcNewPort**します。 Windows の以前のバージョン用に記述されたアプリケーションを MIDI、Dmu ポート ドライバーの統合の結果の動作の変更を確認できません。

 

 




