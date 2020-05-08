---
title: カーネル モード WDM オーディオ コンポーネント
description: カーネル モード WDM オーディオ コンポーネント
ms.assetid: 827997e2-6f07-4635-ac35-4ad026b82eae
keywords:
- カーネルモードコンポーネント WDK オーディオ
- WDMAud システムドライバー WDK オーディオ
- SysAudio システムドライバー WDK オーディオ
- KMixer システムドライバー WDK オーディオ
- Redbook システムドライバー WDK オーディオ
- SBEmul システムドライバー WDK オーディオ
- SWMidi システムドライバー WDK オーディオ
- DMusic システムドライバー WDK オーディオ
- AEC WDK オーディオ
- DRMK システムドライバー WDK オーディオ
- スプリッターシステムドライバー WDK オーディオ
- ポートクラスアダプタードライバー WDK オーディオ
- USBAudio クラスシステムドライバー WDK オーディオ
- AVCAudio クラスシステムドライバー WDK audio
- 1394 WDK オーディオ
- KMixer システムドライバー WDK audio、KMixer システムドライバーについて
- IEEE 1394 WDK オーディオ
- WDM オーディオコンポーネント WDK
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9aa1ef986683bd43247e3e27f99d4becbce29cec
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925557"
---
# <a name="kernel-mode-wdm-audio-components"></a>カーネル モード WDM オーディオ コンポーネント


## <span id="kernel_mode_wdm_audio_components"></span><span id="KERNEL_MODE_WDM_AUDIO_COMPONENTS"></span>


カーネルモードの Microsoft Windows Driver Model (WDM) オーディオコンポーネントは次のとおりです。

WDMAud システムドライバー

SysAudio システムドライバー

KMixer システムドライバー

Redbook システムドライバー

SBEmul システムドライバー

SWMidi システムドライバー

DMusic システムドライバー

AEC システムドライバー

DRMK システムドライバー

スプリッターシステムドライバー

Port クラス Adapter Driver and PortCls System Driver

USB オーディオ クラス システム ドライバー (Usbaudio.sys)

AVCAudio クラスシステムドライバー

### <a name="span-idkm_wdmaud_system_driverspanspan-idkm_wdmaud_system_driverspanwdmaud-system-driver"></a><span id="km_wdmaud_system_driver"></span><span id="KM_WDMAUD_SYSTEM_DRIVER"></span>WDMAud システムドライバー

カーネルモードの WDMAud システムドライバー (Wdmaud) は、ユーザーモードの WDMAud システムドライバー (Wdmaud) とペアになっています。 WDMAud ドライバーのペアは、ユーザーモードの Microsoft Windows マルチメディアシステム呼び出しとカーネルストリーミング i/o 要求を変換します。 WDMAud は、 **waveIn**、 **waveOut**、 **midiin**、 **midiin**、 **mixer**、 **aux** (Microsoft Windows SDK のドキュメントで説明) の api に対して i/o を実行します。 カーネルモードの WDMAud ドライバーは、カーネルストリーミング (KS) フィルターおよび SysAudio システムドライバーのクライアントです。

### <a name="span-idsysaudio_system_driverspanspan-idsysaudio_system_driverspansysaudio-system-driver"></a><span id="sysaudio_system_driver"></span><span id="SYSAUDIO_SYSTEM_DRIVER"></span>SysAudio システムドライバー

SysAudio システムドライバー (Sysaudio .sys) は、オーディオコンテンツを表示およびキャプチャするフィルターグラフを作成します。 SysAudio ドライバーは、[仮想オーディオデバイス](virtual-audio-devices.md)としてのオーディオフィルターグラフを表し、各仮想オーディオデバイスを KSCATEGORY\_オーディオ\_デバイスデバイスインターフェイスのインスタンスとして登録します。 (アダプタードライバーは、SysAudio 専用に予約されているこのカテゴリに自身を登録しないでください)。たとえば、仮想 MIDI デバイスは、SWMidi ドライバー、KMixer ドライバー、およびポート/ミニポートドライバーを接続することによって作成されるフィルターグラフを表す場合があります。 クライアントは、仮想オーディオデバイスを構成する個々のデバイスではなく、仮想オーディオデバイスとのみ通信します。 クライアントに対して透過的に、SysAudio ドライバーは、接続されているフィルターグラフ内のすべての KS フィルターを構成して、仮想オーディオデバイスを形成します。 次のオーディオストリームソースは、SysAudio がビルドするグラフを使用します。

-   DirectSound (Microsoft Windows SDK のドキュメントを参照してください。)

-   Windows マルチメディア Api **waveIn**、 **waveOut**、 **midiin**、 **midiin**、**ミキサー**、 **aux** (Windows SDK のドキュメントを参照)。

-   Redbook CD digital audio (Redbook システムドライバーを参照してください。)

-   Sound Blaster emulator (「SBEmul System Driver」を参照してください)。

-   カーネルモードソフトウェアシンセサイザー (「SWMidi システムドライバーと DMusic システムドライバー」を参照してください)。

-   DRMK システムドライバー

### <a name="span-idkmixer_system_driverspanspan-idkmixer_system_driverspankmixer-system-driver"></a><span id="kmixer_system_driver"></span><span id="KMIXER_SYSTEM_DRIVER"></span>KMixer システムドライバー

KMixer システムドライバー (Kmixer) は、次の処理を実行する KS フィルターです。

-   複数の PCM オーディオストリームの混合

-   高品質形式の変換

-   ビット深度変換

-   スピーカーの構成とチャネルのマッピング

KMixer ドライバーでは、単純な8ビットおよび16ビットの mono およびステレオデータ形式に加えて、次の機能をサポートしています。

-   PCM と IEEE の浮動小数点データ

-   16ビットを超えるビット深度と、3つ以上のチャネルを持つマルチチャネル形式

-   Head 関連の転送関数 (HRTF) の3-d 処理

さまざまなバージョンの Windows でのボリューム範囲と既定のボリュームレベルの詳細については、「[既定のオーディオボリューム設定](default-audio-volume-settings.md)」を参照してください。

### <a name="span-idredbook_system_driverspanspan-idredbook_system_driverspanredbook-system-driver"></a><span id="redbook_system_driver"></span><span id="REDBOOK_SYSTEM_DRIVER"></span>Redbook システムドライバー

Redbook システムドライバー (Redbook) は、CD デジタルオーディオのレンダリングを管理する KS フィルターです。 Redbook ドライバーは、SysAudio システムドライバーのクライアントです。 システムは、ファイルシステムを介して Redbook ドライバーに CD デジタルオーディオをルーティングし、次に SysAudio ドライバーにルーティングします。 CD デジタルオーディオは、(コントロールパネルのマルチメディアプロパティページで設定されている) 優先 wave 出力デバイスでレンダリングされます。

### <a name="span-idsbemul_system_driverspanspan-idsbemul_system_driverspansbemul-system-driver"></a><span id="sbemul_system_driver"></span><span id="SBEMUL_SYSTEM_DRIVER"></span>SBEmul システムドライバー

SBEmul システムドライバー (Sbemul) は、MS-DOS アプリケーション用のサウンドブラスターエミュレーションを提供します。 SBEmul ドライバーは、SysAudio システムドライバーのクライアントです。 コンテンツをレンダリングしてキャプチャするために、SysAudio ドライバーは、(コントロールパネルのマルチメディアプロパティページで設定されている) 優先 wave デバイスと MIDI デバイスを使用します。

サウンドブラスターエミュレーションは、Windows 98/Me でのみサポートされています。

### <a name="span-idswmidi_system_driverspanspan-idswmidi_system_driverspanswmidi-system-driver"></a><span id="swmidi_system_driver"></span><span id="SWMIDI_SYSTEM_DRIVER"></span>SWMidi システムドライバー

SWMidi システムドライバー (Swmidi .sys) は、ソフトウェアによってエミュレートされた一般的な MIDI (GM) と高品質のローランド GS wavetable 合成を提供する KS フィルターです。 **Midiout * * * Xxx*アプリケーションは、ハードウェアシンセサイザーが使用できないときに swmidi を使用します。 SWMidi フィルターは、WDMAud システムドライバーからタイムスタンプ付きの MIDI ストリームを入力として受信し、PCM wave ストリームを KMixer システムドライバーに出力します。 SWMidi は、すべての音声を内部的にミックスして、PCM wave 形式の単一の2チャネル出力ストリームを形成します。

### <a name="span-iddmusic_system_driverspanspan-iddmusic_system_driverspandmusic-system-driver"></a><span id="dmusic_system_driver"></span><span id="DMUSIC_SYSTEM_DRIVER"></span>DMusic システムドライバー

DMusic システムドライバー (Dmusic .sys) は、ソフトウェアでエミュレートされた高品質のダウンロード可能なサウンド (DLS) 合成をサポートする KS フィルターです。 DMusic ドライバーは、システムによって提供されるポートクラスのミニポートドライバーです。 [Directmusic ストリームのデータ範囲](directmusic-stream-data-range.md)をサポートする単一の directmusic pin を公開します。 DMusic フィルターは、DirectMusic システムコンポーネントからタイムスタンプ付きの MIDI ストリームを入力として受信し、PCM wave ストリームを KMixer システムドライバーに出力します。 DMusic ドライバーは、すべての音声を内部的にミックスして、PCM wave 形式の単一の2チャネル出力ストリームを形成します。 DirectMusic アプリケーションでは、DirectMusic の既定のユーザーモードのシンセサイザーの代わりに使用するために、カーネルモードのソフトウェアシンセサイザー (Dmusic .sys) を明示的に選択する必要があります。

### <a name="span-idaec_system_driverspanspan-idaec_system_driverspanaec-system-driver"></a><span id="aec_system_driver"></span><span id="AEC_SYSTEM_DRIVER"></span>AEC システムドライバー

Aec システムドライバー (Aec) は、ソフトウェアに AEC (音響エコー取り消し) とノイズ抑制アルゴリズムを実装することによって、全二重 DirectSound アプリケーションをサポートしています。 詳細については、「 [DirectSound キャプチャの効果](directsound-capture-effects.md)」を参照してください。

### <a name="span-iddrmk_system_driverspanspan-iddrmk_system_driverspandrmk-system-driver"></a><span id="drmk_system_driver"></span><span id="DRMK_SYSTEM_DRIVER"></span>DRMK システムドライバー

DRMK システムドライバー (Drmk .sys) は、DRM で保護されたコンテンツを含むオーディオストリームを復号化する KS フィルターです。 詳細については、「 [Digital Rights Management](digital-rights-management.md)」を参照してください。

### <a name="span-idsplitter_system_driverspanspan-idsplitter_system_driverspansplitter-system-driver"></a><span id="splitter_system_driver"></span><span id="SPLITTER_SYSTEM_DRIVER"></span>スプリッターシステムドライバー

スプリッターシステムドライバー (スプリッター) は、1つの入力キャプチャストリームから2つ以上の出力ストリームを作成する KS フィルターです。 スプリッタードライバーは、入力ストリームの形式に関係なく、入力ストリームをさらに2つの出力ストリームに透過的にコピーします。

スプリッタードライバーは、Windows Me および Microsoft Windows XP 以降でサポートされています。 詳細については、「 [Avstream スプリッター](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-splitters)」を参照してください。

### <a name="span-idport_class_adapter_driver_and_portcls_system_driverspanspan-idport_class_adapter_driver_and_portcls_system_driverspanport-class-adapter-driver-and-portcls-system-driver"></a><span id="port_class_adapter_driver_and_portcls_system_driver"></span><span id="PORT_CLASS_ADAPTER_DRIVER_AND_PORTCLS_SYSTEM_DRIVER"></span>Port クラス Adapter Driver and PortCls System Driver

ポートクラスアダプタードライバーは、オーディオデバイスをサポートするために、ポート/ミニポートドライバーアーキテクチャを使用します。 PortCls ドライバーには、ISA および PCI オーディオデバイス用のドライバーサポートが組み込まれています。 PortCls システムドライバー (Portcls) は、ベンダーが提供するポートクラスアダプタードライバーのフレームワークも提供しますが、Microsoft では、ベンダーが ISA および PCI オーディオデバイスをサポートするために、システム提供のポートクラスアダプタードライバーを使用することをお勧めします。 PortCls フレームワークは、他のハードウェアバスまたはソフトウェア専用デバイスのオーディオデバイス用のドライバーを構築する場合にも役立ちます。 詳しくは、[ポート クラスの概要に関するページ](introduction-to-port-class.md)をご覧ください。

### <a name="span-idusbaudio_class_system_driverspanspan-idusbaudio_class_system_driverspanusb-audio-class-system-driver-usbaudiosys"></a><span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>USB オーディオクラスシステムドライバー (Usbaudio .sys)

USBAudio クラスシステムドライバー (Usbaudio .sys) は、オーディオデバイスのユニバーサルシリアルバスデバイスクラス定義に準拠する USB オーディオデバイスのドライバーサポートを提供します。 このクラスのシステムドライバーの詳細については、「 [USB オーディオクラスシステムドライバー (usbaudio .sys)](usb-audio-class-system-driver--usbaudio-sys-.md)」を参照してください。

### <a name="span-idavcaudio_class_system_driverspanspan-idavcaudio_class_system_driverspanavcaudio-class-system-driver"></a><span id="avcaudio_class_system_driver"></span><span id="AVCAUDIO_CLASS_SYSTEM_DRIVER"></span>AVCAudio クラスシステムドライバー

AVCAudio クラスシステムドライバー (Avcaudio .sys) は、IEEE 1394 バス上に存在するオーディオデバイスのドライバーサポートを提供する AVStream ミニドライバーです。 Windows XP 以降では、AVCAudio ドライバーおよび IEEE 1394 オーディオデバイスの関連するサポートを利用できます。

システム提供のドライバーを使用するには、ハードウェアベンダーが、次の仕様の適切なセクションに準拠するようにオーディオデバイスを設計する必要があります。

-   Iec 61883-1 および IEC 61883-6 (IEC 60958)

-   AV/C デジタルインターフェイスコマンドセットの汎用仕様 Ver。 3.0

-   AV/C オーディオサブユニットの仕様1.0

-   接続と互換性管理の仕様1.0

-   AV/C メディアストリーム形式の情報とネゴシエーション

-   現在処理中の AV/C オーディオサブユニット仕様に対する更新

これらの仕様は、 [1394 貿易 Association](https://1394ta.org/) web サイトから入手できます。 AVCAudio ドライバーは、これらの仕様で説明されている機能のサブセットをサポートしています。

オーディオデバイスがプラグアンドプレイデバイスの列挙中に IEEE 1394 準拠のオーディオデバイスとして識別すると、システムは AVCAudio ドライバーを自動的に読み込み、デバイスをドライブにします。 AVCAudio は、専用のアダプタードライバーを使用せずに、デバイスを直接ドライブにします。 これは、適切な IEEE 1394 仕様に準拠しているデバイスには、専用のアダプタードライバーが必要ないことを意味します。

ハードウェアベンダーは、独自のアダプタードライバーを記述する代わりに、IEEE 1394 オーディオデバイスに AVCAudio ドライバーを使用することをお勧めします。

次の図は、Windows XP の IEEE 1394 オーディオデバイスのドライバー階層を示しています。 Windows XP 以降では、この図に示されているすべてのドライバーコンポーネントが、Microsoft によってオペレーティングシステムと共に提供されています。

![1394オーディオデバイスのドライバー階層を示す図](images/avcaudio.png)

図のドライバーコンポーネントの詳細については、次のセクションを参照してください。

[AVStream の概要](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-overview)

[AV/C クライアント ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)

[IEEE 1394 バス](https://developer.microsoft.com/windows/hardware)

 

 




