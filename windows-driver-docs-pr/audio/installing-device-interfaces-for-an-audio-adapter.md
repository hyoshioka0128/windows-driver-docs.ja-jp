---
title: オーディオ アダプター用のデバイス インターフェイスのインストール
description: オーディオ アダプター用のデバイス インターフェイスのインストール
ms.assetid: 824cc6a2-702a-4e51-91b1-ab776b1babf1
keywords:
- オーディオ アダプター WDK、デバイス インターフェイス
- アダプターのドライバー WDK、オーディオ デバイス インターフェイス
- クラスのオーディオ アダプター WDK、デバイス インターフェイスをポートします。
- デバイス インターフェイスの WDK オーディオ
- サブデバイス WDK オーディオ
- WDK のオーディオ デバイス インターフェイス
ms.date: 10/27/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d4c605303bd01c42bf76ac9da26cbcdee1d4342
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359875"
---
# <a name="installing-device-interfaces-for-an-audio-adapter"></a>オーディオ アダプター用のデバイス インターフェイスのインストール


## <span id="installing_device_interfaces_for_an_audio_adapter"></span><span id="INSTALLING_DEVICE_INTERFACES_FOR_AN_AUDIO_ADAPTER"></span>


クライアントによる一連のオーディオ デバイスにアクセスする*デバイス インターフェイス*アダプターの INF ファイルの仕入先を指定します。 アダプターのドライバーを作成、デバイスの初期化時にサブデバイスで一対一に対応している INF ファイルで指定されたデバイス インターフェイス (を参照してください[サブデバイス作成](subdevice-creation.md))。 各デバイス インターフェイスに対して、INF ファイルを指定します、 **FriendlyName**インターフェイスのレジストリ キーの下のユーザー モードでアクセスできるエントリの値。

カーネル ストリーミング アーキテクチャ、トポロジのカテゴリ (を参照してください[ **KSPROPERTY\_トポロジ\_カテゴリ**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-topology-categories)) はデバイスのインターフェイス クラスを表します。

次の表に、トポロジ カテゴリ オーディオ アダプターを使用して、サブデバイスの機能を説明する最も可能性があります。

|カテゴリ|説明|
|--- |--- |
|KSCATEGORY_ACOUSTIC_ECHO_CANCEL|アコースティック エコー キャンセルを実行できるオーディオ デバイス (を参照してください[DirectSound キャプチャ効果](directsound-capture-effects.md)) このカテゴリに自らを登録します。|
|KSCATEGORY_AUDIO|すべてのオーディオ デバイスは、このカテゴリで自分自身を登録します。|
|KSCATEGORY_CAPTURE|データ ストリームを取得できるオーディオ デバイスは、このカテゴリで、自身を登録します。|
|KSCATEGORY_DATATRANSFORM|ストリームのデータ変換を実行するオーディオ デバイスは、このカテゴリで、自身を登録します。|
|KSCATEGORY_MIXER|データ ストリームを混在させることができますのオーディオ デバイスは、このカテゴリで、自身を登録します。|
|KSCATEGORY_RENDER|データ ストリームをレンダリングするオーディオ デバイスは、このカテゴリで、自身を登録します。|
|KSCATEGORY_SYNTHESIZER|オーディオ サンプルを wave にメッセージを MIDI を変換できるオーディオ デバイスまたはアナログ出力シグナルはこのカテゴリで登録します (を参照してください[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md))。|
|KSCATEGORY_TOPOLOGY|デバイスの[トポロジ ミニポート ドライバー](topology-miniport-driver.md)自身をこのカテゴリに登録します。|
|KSCATEGORY_DRM_DESCRAMBLE|Wave の DRM で保護されたストリームにスクランブルを解除するオーディオ デバイスはこのカテゴリで登録します (を参照してください[デジタル著作権管理](digital-rights-management.md))。|


トポロジのカテゴリの完全な一覧を参照してください、KSCATEGORY\_*XXX* Ks.h と Ksmedia.h ヘッダー ファイルで定義されている Guid。

すべてのオーディオ デバイスに分類されます KSCATEGORY\_KSCATEGORY などの他のカテゴリの下で、オーディオがオーディオ デバイスを分類することがありますも\_(オーディオのレンダリング デバイス) のレンダリングまたは KSCATEGORY\_シンセサイザー(のシンセサイザー)。 デバイスの INF ファイルを指定するカテゴリごとに、Windows インストーラーがそのデバイス カテゴリ名の下のレジストリ エントリのセットをビルド (を参照してください[フィルター ファクトリ](filter-factories.md))。

カテゴリ KSCATEGORY 自体組み込みシンセサイザーを保持するデバイスを登録する必要がありますのみ\_シンセサイザーします。 このカテゴリが純粋な片方デバイスを除外することに注意してください。 出力または生 MIDI UART との間の入力、純粋な片方デバイスは、これらのカテゴリに自体を登録する必要があります。

-   KSCATEGORY\_オーディオ

-   KSCATEGORY\_レンダリング

-   KSCATEGORY\_キャプチャ

なお、 [SysAudio システム ドライバー](kernel-mode-wdm-audio-components.md#sysaudio_system_driver)レジストリ カテゴリ KSCATEGORY を予約\_オーディオ\_の専用デバイスその[仮想のオーディオ デバイス](virtual-audio-devices.md)します。 アダプターのドライバーがする必要がありますこのカテゴリで自身を登録していません。

次の例では、アダプターは通常、オーディオ デバイスをサポートする 4 つの一般的なデバイスのシステム定義インターフェイスをインストールします。

### <a name="span-idexampleinstallingaudiodeviceinterfacesspanspan-idexampleinstallingaudiodeviceinterfacesspanexample-installing-audio-device-interfaces"></a><span id="example__installing_audio_device_interfaces"></span><span id="EXAMPLE__INSTALLING_AUDIO_DEVICE_INTERFACES"></span>例: オーディオ デバイス インターフェイスのインストール

XYZ オーディオ デバイスのデバイス インストールのセクションを使用して、この例では、 [ **INF AddInterface ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addinterface-directive) 4 つのオーディオのアダプター インターフェイスをインストールします。 以下では、アダプターのドライバーは各インターフェイス クラスのインスタンス間で区別するために使用できるインターフェイスに一意の参照文字列を割り当てますそれぞれ 4 つのディレクティブの。

```inf
  [XYZ-Audio-Device.Interfaces]
  AddInterface=%KSCATEGORY_AUDIO%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_RENDER%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_CAPTURE%,%KSName_Wave%,XYZ-Audio-Device.Wave
  AddInterface=%KSCATEGORY_TOPOLOGY%,%KSName_Topology%,XYZ-Audio-Device.Topology
```

最初の 3 つ**AddInterface**ディレクティブは、add インターフェイス セクション Device.Wave-XYZ-オーディオをという名前を指定します。 最後には、XYZ-オーディオ-Device.Topology をという名前を add インターフェイスのセクションを指定します。 各追加インターフェイス セクションの下のユーザー モードでアクセス可能なデバイス インターフェイスのサブキーに、次のレジストリ エントリを追加します、 \\DeviceClasses\\&lt;*InterfaceGUID* &gt;レジストリ キー。

-   FriendlyName レジストリ エントリには、各デバイス インターフェイスのフレンドリ名を指定します。

-   Microsoft DirectShow には、プロキシをアダプターのアクセスし、KSProxy システム ドライバーによって制御されることを示す GUID 値に設定されて、CLSID のレジストリ エントリが必要です。

次の例では、各インターフェイスの FriendlyName と CLSID をレジストリに追加する INF ファイルのエントリが含まれています、2 つの追加インターフェイス セクションが表示されます。

```inf
  [XYZ-Audio-Device.Wave]
  AddReg=XYZ-Audio-Device.Wave.AddReg
  [XYZ-Audio-Device.Wave.AddReg]
  HKR,,FriendlyName,,%WaveDeviceName%
  HKR,,CLSID,,%Proxy.CLSID%

  [XYZ-Audio-Device.Topology]
  AddReg=XYZ-Audio-Device.Topology.AddReg
  [XYZ-Audio-Device.Topology.AddReg]
  HKR,,FriendlyName,,%WaveDeviceMixerName%
  HKR,,CLSID,,%Proxy.CLSID%
```

この例では、キーワード HKR では、デバイスのシステム提供のレジストリ パスを表します。 詳細については、次を参照してください。 [ **INF AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)します。

この例は、文字列のセクションを次に示します。

```inf
  [Strings]
  KSCATEGORY_AUDIO="{6994AD04-93EF-11D0-A3CC-00A0C9223196}"
  KSCATEGORY_RENDER="{65E8773E-8F56-11D0-A3B9-00A0C9223196}"
  KSCATEGORY_CAPTURE="{65E8773D-8F56-11D0-A3B9-00A0C9223196}"
  KSCATEGORY_TOPOLOGY="{DDA54A40-1E4C-11D1-A050-405705C10000}"
  Proxy.CLSID="{17CCA71B-ECD7-11D0-B908-00A0C9223196}"
  WaveDeviceName="XYZ Audio Device"
  WaveDeviceMixerName="XYZ Audio Device Super Mixer"
```

文字列名を**AddInterface**を KSCATEGORY のディレクティブを指定\_*XXX*アダプター ドライバーを使用するため、同じ名前内部的に文字列として、デバイス インターフェイスをローカライズすることはできません定数。 サンプル アダプター ドライバー、Windows Driver Kit (WDK) では、次の文字列、オーディオ デバイス インターフェイスの名前を使用します。

```inf
  KSNAME_Wave="Wave"
  KSNAME_UART="UART"
  KSNAME_FMSynth="FMSynth"
  KSNAME_Topology="Topology"
  KSNAME_Wavetable="Wavetable"
  KSNAME_DMusic="DMusic"
```

、統一性のために、独自のドライバーは、その対応するデバイス インターフェイスへこれらの同じ名前を割り当てる必要があります。 ドライバーは、ベンダーがその他のデバイスのインターフェイスをサポートする場合は、これらのインターフェイスの独自の独自の名前を在庫ことができます。 ドライバーを使用する名前が一致、INF ファイルを確認します。 文字列が一致しない場合、システムのセットアップはそのドライバーを読み込むことができません。

