---
title: オーディオ ドライバーのプロパティ セット
description: オーディオ ドライバーのプロパティ セット
ms.assetid: bac74ad5-3a9b-40b1-ae49-c86558c34e94
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 661e29d53d64a01521d0ee891d9f931950ff0ad3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550032"
---
# <a name="audio-drivers-property-sets"></a>オーディオ ドライバーのプロパティ セット


## <span id="ddk_audio_drivers_property_sets_ks"></span><span id="DDK_AUDIO_DRIVERS_PROPERTY_SETS_KS"></span>


このセクションでは、WDM カーネル ストリーミング サービス Microsoft Windows 2000 以降を使用するオーディオ ドライバー、および Windows Millennium Edition (me) および Windows 98 で使用可能なオーディオ固有のプロパティ セットについて説明します。

各プロパティのリファレンス ページには、次の列見出しのテーブルが含まれています。


| 取得 | 設定 | 対象 | プロパティ記述子の型 | プロパティ値の型 |
|-----|-----|--------|--------------------------|---------------------|
|     |     |        |                          |                     |

これらの見出しには、次の意味があります。

-   **取得**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_プロパティの GET 要求ですか? (Yes または no を指定します。)

-   **設定**

    KS ターゲット オブジェクトのサポート、KSPROPERTY\_型\_セット プロパティ要求でしょうか。 (Yes または no を指定します。)

-   **ターゲット**

    要求のターゲットは、プロパティの要求に送信される KS オブジェクトです。 オーディオのプロパティの対象は、フィルターまたは pin のいずれかです。 (プロパティ要求を指定します、ターゲット オブジェクトがカーネル ハンドルによって。)

-   **プロパティ記述子の型**

    プロパティ記述子には、プロパティとそのプロパティに対して実行する操作を指定します。 記述子が常に始まり、 [ **KSPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff564262)構造がいくつかの型記述子の追加情報を格納します。 たとえば、 [ **KSNODEPROPERTY** ](https://msdn.microsoft.com/library/windows/hardware/ff537143)構造体は、プロパティ記述子を KSPROPERTY 構造で始まりますが、ノード ID も含まれています

-   **プロパティ値の型**

    プロパティは通常の値を持つし、この値の型は、プロパティによって異なります。 たとえば、オンまたはオフ----だけ 2 つの状態のいずれかの可能性のあるプロパティには、ブール値通常があります。 ULONG 値 0 の整数値を 0 xffffffff にことが前提としているプロパティがあります。 複雑なプロパティは、配列や構造体の値があります。

上記のプロパティ記述子とプロパティの値は、記載されているインスタンス仕様および操作データのバッファーのプロパティに固有のバージョン[KS プロパティ、イベント、およびメソッド](https://msdn.microsoft.com/library/windows/hardware/ff567673)します。

プロパティ要求は、次のフラグのいずれかの関数を使用して、プロパティに対して実行される操作を指定します。

-   KSPROPERTY\_型\_BASICSUPPORT

-   KSPROPERTY\_型\_取得

-   KSPROPERTY\_型\_設定

フィルターと暗証番号 (pin) のすべてのオブジェクトは、それらのプロパティを basic サポート操作をサポートします。 Get をサポートし、操作を設定するかどうかは、プロパティによって異なります。 フィルターまたは pin オブジェクトの固有の機能を表すプロパティは、get 操作のみを必要とする可能性があります。 構成可能な設定を表すプロパティは、取得操作が現在の設定を読み取るために役立つ可能性もが、設定操作のみを必要があります。 オーディオのプロパティで、get、セット、および操作を basic サポートを使用する方法の詳細については、[オーディオ エンドポイント、プロパティおよびイベント](https://msdn.microsoft.com/library/windows/hardware/ff536199)を参照してください。

オーディオ ドライバーには、次のプロパティのセットが定義されています。

[KSPROPSETID\_AC3](kspropsetid-ac3.md)

[KSPROPSETID\_音響\_エコー\_キャンセル](kspropsetid-acoustic-echo-cancel.md)

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

[KSPROPSETID\_SoundDetector](kspropsetid-sounddetector.md)

[KSPROPSETID\_シンセサイザー](kspropsetid-synth.md)

[KSPROPSETID\_SynthClock](kspropsetid-synthclock.md)

[KSPROPSETID\_シンセサイザー\_Dls](kspropsetid-synth-dls.md)

[KSPROPSETID\_Sysaudio](kspropsetid-sysaudio.md)

[KSPROPSETID\_Sysaudio\_暗証番号 (pin)](kspropsetid-sysaudio-pin.md)

[KSPROPSETID\_TelephonyControl](kspropsetid-telephonycontrol.md)

[KSPROPSETID\_TelephonyTopology](kspropsetid-telephonytopology.md)

[KSPROPSETID\_TopologyNode](kspropsetid-topologynode.md)

 

 





