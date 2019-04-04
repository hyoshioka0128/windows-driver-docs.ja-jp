---
title: カーネル モード WDM オーディオ コンポーネント
description: カーネル モード WDM オーディオ コンポーネント
ms.assetid: 827997e2-6f07-4635-ac35-4ad026b82eae
keywords:
- カーネル モード コンポーネント WDK オーディオ
- WDMAud システム ドライバー WDK オーディオ
- SysAudio システム ドライバー WDK オーディオ
- KMixer システム ドライバー WDK オーディオ
- Redbook システム ドライバー WDK オーディオ
- SBEmul システム ドライバー WDK オーディオ
- SWMidi システム ドライバー WDK オーディオ
- DMusic システム ドライバー WDK オーディオ
- AEC WDK オーディオ
- DRMK システム ドライバー WDK オーディオ
- システム ドライバー WDK オーディオの分割
- ポート クラス アダプター ドライバー WDK オーディオ
- USBAudio クラス システム ドライバー WDK オーディオ
- AVCAudio クラス システム ドライバー WDK オーディオ
- 1394 WDK オーディオ
- KMixer システム ドライバー WDK オーディオ、KMixer システム ドライバーについて
- IEEE 1394 WDK オーディオ
- WDM オーディオ コンポーネント WDK
ms.date: 05/08/2018
ms.localizationpriority: medium
ms.openlocfilehash: 239c968d82da525c03967408201b73f5a8e9cb37
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558738"
---
# <a name="kernel-mode-wdm-audio-components"></a>カーネル モード WDM オーディオ コンポーネント


## <span id="kernel_mode_wdm_audio_components"></span><span id="KERNEL_MODE_WDM_AUDIO_COMPONENTS"></span>


カーネル モードの Microsoft Windows Driver Model (WDM) オーディオ コンポーネントは次のとおりです。

WDMAud システム ドライバー

SysAudio システム ドライバー

KMixer システム ドライバー

Redbook システム ドライバー

SBEmul システム ドライバー

SWMidi システム ドライバー

DMusic システム ドライバー

AEC システム ドライバー

DRMK システム ドライバー

スプリッター システム ドライバー

ポート クラスのアダプターのドライバーと PortCls システム ドライバー

USB オーディオ クラス システム ドライバー (Usbaudio.sys)

AVCAudio クラスのシステム ドライバー

### <a name="span-idkmwdmaudsystemdriverspanspan-idkmwdmaudsystemdriverspanwdmaud-system-driver"></a><span id="km_wdmaud_system_driver"></span><span id="KM_WDMAUD_SYSTEM_DRIVER"></span>WDMAud システム ドライバー

カーネル モード WDMAud システム ドライバー (Wdmaud.sys) は、ユーザー モード WDMAud システム ドライバー (Wdmaud.drv) と組み合わせて使用します。 WDMAud ドライバーのペアは、ユーザー モードの Microsoft Windows のマルチ メディアのシステム呼び出しとカーネル ストリーミング I/O 要求間で変換します。 WDMAud は、次の Api の I/O を実行します: **waveIn**、 **waveOut**、 **midiIn**、 **midiOut**、**ミキサー**、および**aux** (Microsoft Windows SDK のドキュメントで説明)。 カーネル モード WDMAud ドライバーは、(KS) フィルターと SysAudio システム ドライバーのクライアントにストリーミング カーネルです。

### <a name="span-idsysaudiosystemdriverspanspan-idsysaudiosystemdriverspansysaudio-system-driver"></a><span id="sysaudio_system_driver"></span><span id="SYSAUDIO_SYSTEM_DRIVER"></span>SysAudio システム ドライバー

SysAudio システム ドライバー (Sysaudio.sys) は、レンダリングし、オーディオ コンテンツをキャプチャするフィルター グラフを作成します。 SysAudio ドライバーとしてオーディオ フィルター グラフを表す[仮想のオーディオ デバイス](virtual-audio-devices.md)、KSCATEGORY のインスタンスとして各仮想のオーディオ デバイスを登録および\_オーディオ\_デバイスのデバイスのインターフェイス。 (アダプターのドライバーは登録自体は SysAudio 専用として予約されていますが、このカテゴリで)たとえば、仮想 MIDI デバイスでは、SWMidi ドライバー、KMixer ドライバー、およびポート/ミニポート ドライバーに接続することによって作成されるフィルター グラフを表すことができます。 クライアントは、仮想のオーディオ デバイスを構成する個々 のデバイスではなく、仮想のオーディオ デバイスでのみ通信します。 クライアントに対して透過的に、SysAudio ドライバーを構成します KS のすべてのフィルターで仮想のオーディオ デバイスを形成する相互接続されているフィルター グラフ。 次のオーディオ ストリーム ソースは、SysAudio を構築するグラフを使用します。

-   DirectSound (Microsoft Windows SDK の「ドキュメント)。

-   Windows のマルチ メディア Api **waveIn**、 **waveOut**、 **midiIn**、 **midiOut**、**ミキサー**、および**aux** (Windows SDK の「ドキュメント).

-   Redbook CD デジタル オーディオ (「Redbook システム ドライバー。)

-   サウンド Blaster エミュレーター (「SBEmul システム ドライバー。)

-   カーネル モード ソフトウェア シンセサイザー (「SWMidi システム ドライバーと DMusic システム ドライバー。)

-   DRMK システム ドライバー

### <a name="span-idkmixersystemdriverspanspan-idkmixersystemdriverspankmixer-system-driver"></a><span id="kmixer_system_driver"></span><span id="KMIXER_SYSTEM_DRIVER"></span>KMixer システム ドライバー

KMixer システム ドライバー (Kmixer.sys) は、KS フィルターには、次を示します。

-   複数の PCM のオーディオ ストリームの混在

-   高品質な形式の変換

-   ビット深度の変換

-   スピーカーの構成とチャネルのマッピング

だけでなく単純な 8 ビットと 16 ビット、mono とステレオのデータ形式、KMixer ドライバーをサポートします。

-   PCM、IEEE 浮動小数点データ

-   ビット深度の 16 ビット、および複数の 2 つのチャネルでマルチ チャネルの形式より大きい

-   頭部伝達関数 (HRTF) 3-D 処理

ボリュームの範囲と、さまざまなバージョンの Windows での既定のボリューム レベルについては、[既定のオーディオ音量設定](default-audio-volume-settings.md)を参照してください。

### <a name="span-idredbooksystemdriverspanspan-idredbooksystemdriverspanredbook-system-driver"></a><span id="redbook_system_driver"></span><span id="REDBOOK_SYSTEM_DRIVER"></span>Redbook システム ドライバー

Redbook システム ドライバー (Redbook.sys) は、デジタル音楽の CD のレンダリングを管理する KS フィルターです。 Redbook ドライバーは、SysAudio システム ドライバーのクライアントです。 システムは、Redbook ドライバー、そして SysAudio ドライバーへのファイル システムからデジタル音楽の CD をルーティングします。 デジタル音楽の CD は、(としてコントロール パネルの マルチ メディアのプロパティ ページで設定) を優先 wave 出力デバイスにレンダリングされます。

### <a name="span-idsbemulsystemdriverspanspan-idsbemulsystemdriverspansbemul-system-driver"></a><span id="sbemul_system_driver"></span><span id="SBEMUL_SYSTEM_DRIVER"></span>SBEmul システム ドライバー

SBEmul システム ドライバー (Sbemul.sys) では、MS-DOS アプリケーションにサウンド Blaster のエミュレーションを提供します。 SBEmul ドライバーは、SysAudio システム ドライバーのクライアントです。 レンダリングし、コンテンツをキャプチャには、SysAudio ドライバーは、(コントロール パネルの マルチ メディアのプロパティ ページで設定した) として優先 wave および MIDI デバイスを使用します。

サウンドの Blaster エミュレーションが Windows 98 でのみサポートされている/me.

### <a name="span-idswmidisystemdriverspanspan-idswmidisystemdriverspanswmidi-system-driver"></a><span id="swmidi_system_driver"></span><span id="SWMIDI_SYSTEM_DRIVER"></span>SWMidi システム ドライバー

SWMidi システム ドライバー (Swmidi.sys) は、ソフトウェアをエミュレート全般 MIDI (GM) と高品質な Roland GS ウェーブの音声合成を提供する KS フィルターです。 A **midiOut * * * Xxx*ハードウェア シンセサイザーが利用できない場合、アプリケーションが SWMidi を使用します。 SWMidi フィルターは WDMAud システム ドライバーからの入力として MIDI タイムスタンプ付きストリームを受信し、KMixer システム ドライバーに PCM wave ストリームを出力します。 SWMidi は、すべての PCM の wave 形式の 2 チャンネルの 1 つの出力ストリームを形成するには、内部的には、音声合成します。

### <a name="span-iddmusicsystemdriverspanspan-iddmusicsystemdriverspandmusic-system-driver"></a><span id="dmusic_system_driver"></span><span id="DMUSIC_SYSTEM_DRIVER"></span>DMusic システム ドライバー

DMusic システム ドライバー (Dmusic.sys) は、ソフトウェア、高品質、ダウンロード可能なサウンド (DL) 合成をサポートする KS フィルターです。 DMusic ドライバーは、システムが指定したポート クラス ミニポート ドライバーです。 公開をサポートする 1 つの DirectMusic pin、 [DirectMusic ストリーム データ範囲](directmusic-stream-data-range.md)します。 DMusic フィルターは DirectMusic システム コンポーネントからの入力として MIDI タイムスタンプ付きストリームを受信し、KMixer システム ドライバーに PCM wave ストリームを出力します。 DMusic ドライバーは、すべての PCM の wave 形式の 2 チャンネルの 1 つの出力ストリームを形成するには、内部的には、音声合成します。 DirectMusic アプリケーションでは、カーネル モードのソフトウェア シンセサイザー DirectMusic の既定では、ユーザー モードのシンセサイザーの代わりに使用する、Dmusic.sys を明示的に選択する必要があります。

### <a name="span-idaecsystemdriverspanspan-idaecsystemdriverspanaec-system-driver"></a><span id="aec_system_driver"></span><span id="AEC_SYSTEM_DRIVER"></span>AEC システム ドライバー

AEC システム ドライバー (Aec.sys) では、ソフトウェアの AEC (アコースティック エコー キャンセル) とノイズ抑制アルゴリズムを実装することで、全二重 DirectSound アプリケーションをサポートします。 詳細については、[DirectSound キャプチャ効果](directsound-capture-effects.md)を参照してください。

### <a name="span-iddrmksystemdriverspanspan-iddrmksystemdriverspandrmk-system-driver"></a><span id="drmk_system_driver"></span><span id="DRMK_SYSTEM_DRIVER"></span>DRMK システム ドライバー

DRMK システム ドライバー (Drmk.sys) は、DRM で保護されたコンテンツを格納しているオーディオ ストリームの復号化する KS フィルターです。 詳細については、[デジタル著作権管理](digital-rights-management.md)を参照してください。

### <a name="span-idsplittersystemdriverspanspan-idsplittersystemdriverspansplitter-system-driver"></a><span id="splitter_system_driver"></span><span id="SPLITTER_SYSTEM_DRIVER"></span>スプリッター システム ドライバー

スプリッター システム ドライバー (Splitter.sys) は 2 つ作成される KS フィルターまたは以上の出力を 1 つの入力キャプチャ ストリームからストリームします。 スプリッター ドライバーは、入力ストリームの形式とは無関係に 2 つの詳細出力ストリームに入力ストリームを透過的にコピーします。

スプリッター ドライバーは、Microsoft Windows XP と Windows Me でサポートされている以降です。 詳細については、[AVStream スプリッター](https://msdn.microsoft.com/library/windows/hardware/ff554255)を参照してください。

### <a name="span-idportclassadapterdriverandportclssystemdriverspanspan-idportclassadapterdriverandportclssystemdriverspanport-class-adapter-driver-and-portcls-system-driver"></a><span id="port_class_adapter_driver_and_portcls_system_driver"></span><span id="PORT_CLASS_ADAPTER_DRIVER_AND_PORTCLS_SYSTEM_DRIVER"></span>ポート クラスのアダプターのドライバーと PortCls システム ドライバー

ポート クラス ドライバーは、オーディオ デバイスをサポートするためにポート/ミニポート ドライバーのアーキテクチャを使用します。 PortCls ドライバーには、ISA および PCI のオーディオ デバイスの組み込みのドライバー サポートが含まれています。 PortCls システム ドライバー (Portcls.sys) には、ポートのベンダーから提供されたクラスのアダプターのドライバーのフレームワークも用意されていますには、ベンダーが ISA および PCI のオーディオ デバイスをサポートするシステム提供のポートのクラス ドライバーを使用することをお勧めします。 PortCls フレームワークも構築のドライバー ソフトウェア専用デバイスやその他のハードウェア バス上のオーディオ デバイスの便利な場合があります。 詳しくは、[ポート クラスの概要に関するページ](introduction-to-port-class.md)をご覧ください。

### <a name="span-idusbaudioclasssystemdriverspanspan-idusbaudioclasssystemdriverspanusb-audio-class-system-driver-usbaudiosys"></a><span id="usbaudio_class_system_driver"></span><span id="USBAUDIO_CLASS_SYSTEM_DRIVER"></span>USB オーディオ クラス システム ドライバー (Usbaudio.sys)

USBAudio クラスのシステム ドライバー (Usbaudio.sys) では、オーディオ デバイスの場合、ユニバーサル シリアル バス デバイス クラス定義に準拠している USB オーディオ デバイス ドライバーのサポートを提供します。 このクラスのシステム ドライバーの詳細については、[USB オーディオ クラス システム ドライバー (Usbaudio.sys)](usb-audio-class-system-driver--usbaudio-sys-.md)を参照してください。

### <a name="span-idavcaudioclasssystemdriverspanspan-idavcaudioclasssystemdriverspanavcaudio-class-system-driver"></a><span id="avcaudio_class_system_driver"></span><span id="AVCAUDIO_CLASS_SYSTEM_DRIVER"></span>AVCAudio クラスのシステム ドライバー

AVCAudio クラスのシステム ドライバー (Avcaudio.sys) では、IEEE 1394 バス上に存在するオーディオ デバイスのドライバーのサポートを提供する AVStream ミニドライバーです。 AVCAudio ドライバーと IEEE 1394 オーディオ デバイスの関連付けのサポートは、Windows XP で使用できる以降です。

システム提供のドライバーを使用するには、ハードウェア ベンダーは、次の仕様の適切なセクションに準拠するようにオーディオ デバイスをデザインする必要があります。

-   IEC 61883 1 および IEC 61883 6 (IEC 60958)

-   AV/C デジタル インターフェイス コマンドは、一般的な仕様のバージョンを設定します。 3.0

-   AV/C オーディオ サブユニット指定 1.0

-   接続との互換性 Management Specification 1.0

-   AV/C メディア Stream の書式情報、およびネゴシエーション

-   現在処理中には、AV/C オーディオのサブユニット仕様への更新

これらの仕様については、「、 [1394 貿易](https://go.microsoft.com/fwlink/p/?linkid=8728)web サイト。 AVCAudio ドライバーでは、これらの仕様で説明されている機能のサブセットをサポートします。

オーディオ デバイスが識別されるプラグ アンド プレイ デバイスの列挙中に、IEEE 1394 に準拠したオーディオ デバイスとして、ときに、システムは自動的にデバイスのドライブに AVCAudio ドライバーを読み込みます。 AVCAudio は、デバイスを直接、独自のアダプターのドライバーの助けなしドライブします。 これは、適切な IEEE 1394 仕様に準拠しているデバイスには独自のアダプター ドライバーが必要ないことを意味します。

ハードウェア ベンダーが、独自のアダプターのドライバーを記述する代わりに、IEEE 1394 オーディオ デバイスに対する AVCAudio ドライバーを使用することをお勧めします。

次の図は、Windows XP では、IEEE 1394 オーディオ デバイスのドライバーの階層を示します。 Windows XP 以降はすべてこの図に示すように、ドライバー コンポーネントのオペレーティング システムと Microsoft によって提供されます。

![1394 オーディオ デバイスのドライバーの階層を示す図](images/avcaudio.png)

図に、ドライバー コンポーネントに関する詳細については、次のセクションを参照してください。

[AVStream の概要](https://msdn.microsoft.com/library/windows/hardware/ff554240)

[AV/C クライアント ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff556364)

[IEEE 1394 バス](https://msdn.microsoft.com/library/windows/hardware/ff537207)

 

 




