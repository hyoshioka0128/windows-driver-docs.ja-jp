---
title: ドライバー実装の詳細
description: このトピックでは、ハードウェアオフロードオーディオストリームを処理できるオーディオアダプター用に開発されたオーディオドライバーの実装の詳細について説明します。
ms.assetid: FB17FADD-D683-4ECC-95F9-86DF7A289C63
ms.date: 04/17/2020
ms.localizationpriority: medium
ms.openlocfilehash: 59c0cd9df0297332529ceaab111da5a2d1262b20
ms.sourcegitcommit: 8f27122409dea11ef0635afbbe5788a648066a1a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2020
ms.locfileid: "81772731"
---
# <a name="driver-implementation-details"></a>ドライバー実装の詳細


このトピックでは、ハードウェアオフロードオーディオストリームを処理できるオーディオアダプター用に開発されたオーディオドライバーの実装の詳細について説明します。

つまり、このトピックでは、ハードウェアオフロードオーディオを処理できるオーディオアダプターで動作するドライバーをサポートするために Microsoft が (Windows 8 以降) どのように実行したかについて説明します。 次のセクションでは、このようなアダプターをサポートするためにドライバーが対応する必要がある内容についても説明します。

## <a name="span-ida__new_type_guid_for_node_descriptorsspanspan-ida__new_type_guid_for_node_descriptorsspanspan-ida__new_type_guid_for_node_descriptorsspana-new-type-guid-for-node-descriptors"></a><span id="A__new_Type_GUID_for_node_descriptors"></span><span id="a__new_type_guid_for_node_descriptors"></span><span id="A__NEW_TYPE_GUID_FOR_NODE_DESCRIPTORS"></span>ノード記述子の新しい*型*GUID


オーディオアダプターがオフロードされたオーディオストリームを処理できる場合、アダプターのオーディオドライバーは、アダプターの KS フィルターで新しく導入されたノードを使用してこの機能を公開します。

オーディオストリームのパス内の各ノードにはノード記述子があるため、この新しいノードでは、ドライバーは*Type* GUID を[**KSNODETYPE\_audio\_ENGINE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-audio-engine)に設定する必要があります。 ドライバーがこの新しいノードのノード記述子を構成する方法の例を次に示します。

```ManagedCPlusPlus
typedef struct _KSNODE_DESCRIPTOR {
  const KSAUTOMATION_TABLE *AutomationTable;    // drv specific
  const GUID               *Type;       // must be set to KSNODETYPE_AUDIO_ENGINE
  const GUID               *Name;       // drv specific (KSNODETYPE_AUDIO_ENGINE?)  
} KSNODE_DESCRIPTOR, *PKSNODE_DESCRIPTOR;
```

名前 GUID が**\_KSNODETYPE AUDIO\_ENGINE**に設定されている場合は、このノードの既定の名前文字列を作成する必要があります。 次に、その文字列を*ks*に追加して\_、ドライバーのインストール時に、文字列を使用して HKEY LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\MediaCategories レジストリキーを設定できるようにします。

新しいノードタイプ**\_KSNODETYPE AUDIO\_ENGINE**の GUID の定義は次のとおりです。

```ManagedCPlusPlus
Code style
#define STATIC_KSNODETYPE_AUDIO_ENGINE\
    0x35caf6e4, 0xf3b3, 0x4168, 0xbb, 0x4b, 0x55, 0xe7, 0x7a, 0x46, 0x1c, 0x7e
DEFINE_GUIDSTRUCT("35CAF6E4-F3B3-4168-BB4B-55E77A461C7E", KSNODETYPE_AUDIO_ENGINE);
#define KSNODETYPE_AUDIO_ENGINE DEFINE_GUIDNAMED(KSNODETYPE_AUDIO_ENGINE)
```

詳細については、「 *ksmedia .h*ヘッダーファイル」を参照してください。

また、上記の情報に基づいて、ミニポートノードの記述子は次のようになります。

```ManagedCPlusPlus
PCNODE_DESCRIPTOR MiniportNodes[] =
{
    // KSNODE_WAVE_AUDIO_ENGINE
    {
        0,                          // Flags
        NULL,                       // AutomationTable
        &KSNODETYPE_AUDIO_ENGINE,   // Type  KSNODETYPE_AUDIO_ENGINE
        NULL                        // Name
    }
};
```

## <a name="span-ida_new_ks_property_set_for_audio_enginesspanspan-ida_new_ks_property_set_for_audio_enginesspanspan-ida_new_ks_property_set_for_audio_enginesspana-new-ks-property-set-for-audio-engines"></a><span id="A_new_KS_property_set_for_audio_engines"></span><span id="a_new_ks_property_set_for_audio_engines"></span><span id="A_NEW_KS_PROPERTY_SET_FOR_AUDIO_ENGINES"></span>オーディオエンジン用に設定した新しい KS プロパティ


Windows 8 以降では、ハードウェアオーディオエンジンとハードウェアオフロードオーディオ処理をサポートするために、 [Kspropsetid\_audioengine](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audioengine)プロパティセットが導入されました。 そのため、オフロードされたオーディオストリームを処理できるアダプターのドライバーは、この新しいプロパティセットのプロパティをサポートしている必要があります。

新しいプロパティである**Ksk Propsetid\_audioengine**は、次のように定義されています。

```ManagedCPlusPlus
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

この新しいプロパティセット内のプロパティの名前は、 [**Ksk プロパティ\_audioengine**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine)列挙型で定義され、ドライバーはこれらの名前をサポートする必要があります。

次に、 **Kspropsetid\_audioengine**プロパティセットの新しいプロパティを示します。

[**KSK プロパティ\_AUDIOENGINE\_の\_バッファー\_サイズの範囲**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-buffer-size-limits)

[**KSK プロパティ\_AUDIOENGINE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-descriptor)

[**KSK プロパティ\_AUDIOENGINE\_の DEVICEFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-deviceformat)

[**KSK プロパティ\_AUDIOENGINE\_GFXENABLE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-gfx-enable)

[**KSK プロパティ\_AUDIOENGINE\_LFXENABLE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-lfx-enable)

[**KSK プロパティ\_AUDIOENGINE\_ループバック\_保護**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-loopback-protection)

[**KSK プロパティ\_AUDIOENGINE\_MIXFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-mixformat)

[**KSK プロパティ\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-supporteddeviceformats)

[**KSK プロパティ\_AUDIOENGINE\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audioengine-volumelevel)

## <a name="span-idupdates_to_the_kspropsetid__audio_property_setspanspan-idupdates_to_the_kspropsetid__audio_property_setspanspan-idupdates_to_the_kspropsetid__audio_property_setspanupdates-to-the-kspropsetid_-audio-property-set"></a><span id="Updates_to_the_KSPROPSETID__Audio_property_set"></span><span id="updates_to_the_kspropsetid__audio_property_set"></span><span id="UPDATES_TO_THE_KSPROPSETID__AUDIO_PROPERTY_SET"></span>KSPROPSETID\_オーディオプロパティセットの更新


新しい**kspropsetid\_audioengine**プロパティセットのプロパティをサポートするだけでなく、ドライバーは、 [ksk propsetid\_オーディオ](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-audio)プロパティセット内の次の既存のプロパティもサポートする必要があります。

[**KSK プロパティ\_オーディオ\_ミュート**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mute)

[**KSK プロパティ\_AUDIO\_PEAKMETER2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-peakmeter2)

[**KSK プロパティ\_AUDIO\_VOLUMELEVEL**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)

また、ハードウェアオフロードオーディオ処理のドライバーサポートの実装を完了するために、 **Kspropsetid\_オーディオ**プロパティセットに新しいプロパティが追加されました。

新しい**Ksk Propsetid\_オーディオ**プロパティを次に示します。

[**KSK プロパティ\_オーディオ\_リニア\_バッファー\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-linear-buffer-position)

[**KSPROPERTY\_オーディオ\_プレゼンテーション\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-presentation-position)

[**KSK プロパティ\_AUDIO\_\_WALASTCURRENT\_書き込み\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-wavert-current-write-position)

## <a name="span-idport-class_driver_updates_and_glitch_reportingspanspan-idport-class_driver_updates_and_glitch_reportingspanspan-idport-class_driver_updates_and_glitch_reportingspanport-class-driver-updates-and-glitch-reporting"></a><span id="Port-class_driver_updates_and_glitch_reporting"></span><span id="port-class_driver_updates_and_glitch_reporting"></span><span id="PORT-CLASS_DRIVER_UPDATES_AND_GLITCH_REPORTING"></span>ポートクラスのドライバーの更新とエラーの報告


前のセクションで説明したハードウェアオフロードオーディオ処理のサポートに加えて、Windows ポートクラスドライバーも "ヘルパーインターフェイス" によって更新され、オフロードオーディオストリームで動作するドライバーを簡単に開発できるようになりました。 このようなドライバーが異常を検出すると、ドライバーがエラーを報告できるようにするメカニズムが用意されています。 次のトピックでは、ヘルパーインターフェイスとエラー報告の詳細について説明します。

[オフロードされたオーディオ処理のためのヘルパー インターフェイス](helper-interfaces-for-offloaded-audio-processing.md)

[オフロードされたオーディオに関するグリッチ レポート](glitch-reporting-for-offloaded-audio.md)

 

 




