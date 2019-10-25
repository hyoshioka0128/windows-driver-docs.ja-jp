---
title: オーディオ ドライバーのプロパティ セット
description: オーディオ ドライバーのプロパティ セット
ms.assetid: bac74ad5-3a9b-40b1-ae49-c86558c34e94
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbd279a2b5bfeec24d975a837d5068c3377f768d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831359"
---
# <a name="audio-drivers-property-sets"></a>オーディオ ドライバーのプロパティ セット


## <span id="ddk_audio_drivers_property_sets_ks"></span><span id="DDK_AUDIO_DRIVERS_PROPERTY_SETS_KS"></span>


このセクションでは、Microsoft Windows 2000 以降、および Windows Millennium Edition (Me) および Windows 98 で WDM カーネルストリーミングサービスを使用するオーディオドライバーで使用できるオーディオ固有のプロパティセットについて説明します。

各プロパティの参照ページには、次の列見出しを持つテーブルが含まれています。


| [購入] | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しの意味は次のとおりです。

-   **取得**

    ターゲットの KS オブジェクトは、プロパティの取得\_\_型の KSK プロパティをサポートしていますか? ("Yes" または "no" を指定します)。

-   **一連**

    ターゲットの KS オブジェクトでは、プロパティ\_型\_SET プロパティがサポートされているかどうかを確認できます。 ("Yes" または "no" を指定します)。

-   **接続**

    要求のターゲットは、プロパティ要求の送信先となる KS オブジェクトです。 オーディオプロパティのターゲットは、フィルターまたはピンです。 (プロパティ要求では、カーネルハンドルによってターゲットオブジェクトが指定されます)。

-   **プロパティ記述子の型**

    プロパティ記述子は、プロパティと、そのプロパティに対して実行する操作を指定します。 記述子は常に[**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造で始まりますが、一部の種類の記述子には追加情報が含まれています。 たとえば、 [**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)構造体は、ksk プロパティ構造体で始まるプロパティ記述子ですが、ノード ID も含まれています。

-   **プロパティ値の型**

    通常、プロパティには値があり、この値の型はプロパティによって異なります。 たとえば、2つの状態 (on または off) のいずれかであるプロパティは、通常、ブール値を持ちます。 0から0xFFFFFFFF の整数値を想定できるプロパティは、ULONG 値を持つ場合があります。 より複雑なプロパティには、配列または構造体の値が含まれる場合があります。

前のプロパティ記述子とプロパティ値は、 [「KS プロパティ、イベント、およびメソッド](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-properties--events--and-methods)」で説明されている、インスタンス仕様および操作データバッファーのプロパティ固有バージョンです。

プロパティ要求では、次のいずれかのフラグを使用して、プロパティに対して実行する操作を指定します。

-   KSPROPERTY\_TYPE\_BASICSUPPORT

-   KSK プロパティ\_TYPE\_GET

-   KSK プロパティ\_TYPE\_SET

すべてのフィルターオブジェクトとピンオブジェクトは、そのプロパティに対する基本サポート操作をサポートしています。 Get 操作と set 操作をサポートするかどうかは、プロパティによって異なります。 Filter オブジェクトまたは pin オブジェクトの固有の機能を表すプロパティは、get 操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティは、設定操作のみを必要とする場合がありますが、get 操作は現在の設定の読み取りにも便利な場合があります。 オーディオプロパティでの get、set、および basic サポート操作の使用の詳細については、「[オーディオエンドポイント、プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-endpoints--properties-and-events)、およびイベント」を参照してください。

オーディオドライバーには、次のプロパティセットが定義されています。

[KSPROPSETID\_AC3](kspropsetid-ac3.md)

[KSPROPSETID\_音響\_Echo\_キャンセル](kspropsetid-acoustic-echo-cancel.md)

[KSPROPSETID\_オーディオ](kspropsetid-audio.md)

[KSPROPSETID\_AudioEngine](kspropsetid-audioengine.md)

[KSPROPSETID\_AudioGfx](kspropsetid-audiogfx.md)

[KSPROPSETID\_DirectSound3DBuffer](kspropsetid-directsound3dbuffer.md)

[KSPROPSETID\_DirectSound3DListener](kspropsetid-directsound3dlistener.md)

[KSPROPSETID\_DrmAudioStream](kspropsetid-drmaudiostream.md)

[KSPROPSETID\_FMRXTopology](kspropsetid-fmrxtopology.md)

[KSPROPSETID\_Hrtf3d](kspropsetid-hrtf3d.md)

[KSPROPSETID\_Itd3d](kspropsetid-itd3d.md)

[KSPROPSETID\_ジャック](kspropsetid-jack.md)

[KSPROPSETID\_RTAudio](kspropsetid-rtaudio.md)

[KSPROPSETID\_SoundDetector 器](kspropsetid-sounddetector.md)

[KSPROPSETID\_シンセサイザー](kspropsetid-synth.md)

[KSPROPSETID\_SynthClock](kspropsetid-synthclock.md)

[KSPROPSETID\_シンセサイザー\_Dls](kspropsetid-synth-dls.md)

[KSPROPSETID\_Sysaudio](kspropsetid-sysaudio.md)

[KSPROPSETID\_Sysaudio\_Pin](kspropsetid-sysaudio-pin.md)

[KSPROPSETID\_TelephonyControl](kspropsetid-telephonycontrol.md)

[KSPROPSETID\_TelephonyTopology](kspropsetid-telephonytopology.md)

[KSPROPSETID\_TopologyNode](kspropsetid-topologynode.md)

 

 





