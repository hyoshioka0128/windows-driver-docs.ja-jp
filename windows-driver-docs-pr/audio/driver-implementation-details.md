---
title: ドライバーの実装の詳細
description: このトピックでは、ハードウェア オフロードされたオーディオ ストリームを処理できるオーディオのアダプターを開発したオーディオ ドライバーの実装の詳細を表示します。
ms.assetid: FB17FADD-D683-4ECC-95F9-86DF7A289C63
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11d7c2a0dbde495b6eeb27d30522445a84ba2c63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553309"
---
# <a name="driver-implementation-details"></a>ドライバーの実装の詳細


このトピックでは、ハードウェア オフロードされたオーディオ ストリームを処理できるオーディオのアダプターを開発したオーディオ ドライバーの実装の詳細を表示します。

つまり、このトピックでは、Microsoft が何 (Windows 8 以降) がハードウェア オフロードされたオーディオを処理できるオーディオのアダプターで動作するドライバーをサポートするについて説明します。 次のセクションでこのトピックでもは、ドライバーに必要なそのようなアダプターをサポートするためにできます。

## <a name="span-idanewtypeguidfornodedescriptorsspanspan-idanewtypeguidfornodedescriptorsspanspan-idanewtypeguidfornodedescriptorsspana-new-type-guid-for-node-descriptors"></a><span id="A__new_Type_GUID_for_node_descriptors"></span><span id="a__new_type_guid_for_node_descriptors"></span><span id="A__NEW_TYPE_GUID_FOR_NODE_DESCRIPTORS"></span>新しい*型*ノード記述子の GUID


オーディオのアダプターができる場合は、オフロードされたオーディオ ストリームの処理、オーディオ ドライバーのアダプターのアダプターの KS フィルターで新しく導入されたノードを使用して、この機能を公開します。

オーディオ ストリームのパス内の各ノードがノード記述子を持つため、この新しいノードのドライバーを設定する必要があります、*型*GUID [ **KSNODETYPE\_オーディオ\_エンジン**](https://msdn.microsoft.com/library/windows/hardware/hh450866). ドライバーがこの新しいノードのノードの記述子を構成する方法の例を次に示します。

```ManagedCPlusPlus
typedef struct _KSNODE_DESCRIPTOR {
  const KSAUTOMATION_TABLE *AutomationTable;    // drv specific
  const GUID               *Type;       // must be set to KSNODETYPE_AUDIO_ENGINE
  const GUID               *Name;       // drv specific (KSNODETYPE_AUDIO_ENGINE?)  
} KSNODE_DESCRIPTOR, *PKSNODE_DESCRIPTOR;
```

名前の GUID に設定されている場合**KSNODETYPE\_オーディオ\_エンジン**、し、このノードの既定の名前文字列を作成する必要があります。 その文字列を追加して*ks.inf*ドライバーのインストール中、文字列を使用して、HKEY を設定するように、\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\MediaCategories レジストリ キー。

新しいノード タイプの GUID の定義**KSNODETYPE\_オーディオ\_エンジン**、次に示します。

```ManagedCPlusPlus
Code style
#define STATIC_KSNODETYPE_AUDIO_ENGINE\
    0x35caf6e4, 0xf3b3, 0x4168, 0xbb, 0x4b, 0x55, 0xe7, 0x7a, 0x46, 0x1c, 0x7e
DEFINE_GUIDSTRUCT("35CAF6E4-F3B3-4168-BB4B-55E77A461C7E", KSNODETYPE_AUDIO_ENGINE);
#define KSNODETYPE_AUDIO_ENGINE DEFINE_GUIDNAMED(KSNODETYPE_AUDIO_ENGINE)
```

詳細については、次を参照してください。、 *ksmedia.h*ヘッダー ファイル。

上記の情報に基づき、ミニポート ノードの記述子に次のようになります。

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

## <a name="span-idanewkspropertysetforaudioenginesspanspan-idanewkspropertysetforaudioenginesspanspan-idanewkspropertysetforaudioenginesspana-new-ks-property-set-for-audio-engines"></a><span id="A_new_KS_property_set_for_audio_engines"></span><span id="a_new_ks_property_set_for_audio_engines"></span><span id="A_NEW_KS_PROPERTY_SET_FOR_AUDIO_ENGINES"></span>オーディオ エンジンの設定の新しい KS プロパティ


Windows 8 では、以降では、 [KSPROPSETID\_AudioEngine](https://msdn.microsoft.com/library/windows/hardware/hh450902)オーディオ エンジンのハードウェアおよびハードウェア オフロードされたオーディオ処理をサポートするプロパティ セットが導入されています。 処理できるアダプターのドライバーがオフロードできるようにオーディオ ストリームはこの新しいプロパティを設定でプロパティをサポートする必要があります。

新しいプロパティを設定した**KSPROPSETID\_AudioEngine**、次のように定義されています。

```ManagedCPlusPlus
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

この新しいプロパティ セット内のプロパティの名前が定義されている、 [ **KSPROPERTY\_AUDIOENGINE** ](https://msdn.microsoft.com/library/windows/hardware/hh450867)列挙型、およびドライバーは、これらの名前をサポートする必要があります。

内の新しいプロパティをここでは、 **KSPROPSETID\_AudioEngine**プロパティ セット。

[**KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**](https://msdn.microsoft.com/library/windows/hardware/hh450868)

[**KSPROPERTY\_AUDIOENGINE\_記述子**](https://msdn.microsoft.com/library/windows/hardware/hh450870)

[**KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT**](https://msdn.microsoft.com/library/windows/hardware/hh450872)

[**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**](https://msdn.microsoft.com/library/windows/hardware/hh450874)

[**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**](https://msdn.microsoft.com/library/windows/hardware/hh450876)

[**KSPROPERTY\_AUDIOENGINE\_ループバック\_保護**](https://msdn.microsoft.com/library/windows/hardware/hh450878)

[**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**](https://msdn.microsoft.com/library/windows/hardware/hh450880)

[**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](https://msdn.microsoft.com/library/windows/hardware/hh450884)

[**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/hh831855)

## <a name="span-idupdatestothekspropsetidaudiopropertysetspanspan-idupdatestothekspropsetidaudiopropertysetspanspan-idupdatestothekspropsetidaudiopropertysetspanupdates-to-the-kspropsetid-audio-property-set"></a><span id="Updates_to_the_KSPROPSETID__Audio_property_set"></span><span id="updates_to_the_kspropsetid__audio_property_set"></span><span id="UPDATES_TO_THE_KSPROPSETID__AUDIO_PROPERTY_SET"></span>更新プログラム、KSPROPSETID\_オーディオ プロパティ セット


新しいプロパティをサポートしているだけでなく**KSPROPSETID\_AudioEngine**プロパティを設定するドライバーはで、次の既存のプロパティをサポートする必要がありますも、 [KSPROPSETID\_オーディオ](https://msdn.microsoft.com/library/windows/hardware/ff537440)プロパティ セット。

[**KSPROPERTY\_オーディオ\_ミュート**](https://msdn.microsoft.com/library/windows/hardware/ff537293)

[**KSPROPERTY\_AUDIO\_PEAKMETER**](https://msdn.microsoft.com/library/windows/hardware/ff537296)

[**KSPROPERTY\_オーディオ\_VOLUMELEVEL**](https://msdn.microsoft.com/library/windows/hardware/ff537309)

新しいプロパティが追加されましたによるハードウェア オフロードされたオーディオ処理用のドライバー サポートの実装を完了して、 **KSPROPSETID\_オーディオ**プロパティ セット。

ここでは、新しい**KSPROPSETID\_オーディオ**プロパティ。

[**KSPROPERTY\_オーディオ\_線形\_バッファー\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450894)

[**KSPROPERTY\_オーディオ\_プレゼンテーション\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450895)

[**KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_位置**](https://msdn.microsoft.com/library/windows/hardware/hh450896)

## <a name="span-idport-classdriverupdatesandglitchreportingspanspan-idport-classdriverupdatesandglitchreportingspanspan-idport-classdriverupdatesandglitchreportingspanport-class-driver-updates-and-glitch-reporting"></a><span id="Port-class_driver_updates_and_glitch_reporting"></span><span id="port-class_driver_updates_and_glitch_reporting"></span><span id="PORT-CLASS_DRIVER_UPDATES_AND_GLITCH_REPORTING"></span>ポート クラス ドライバーの更新プログラムとの不具合の報告


によるハードウェア オフロードされたオーディオ処理の前のセクションで説明されている、サポートに加え、Windows ポート クラス ドライバーも更新されています「ヘルパー インターフェイス」で動作するドライバーの開発を簡略化するオーディオ ストリームをオフロードします。 異常が検出されると、このようなドライバーに不具合エラーを報告するドライバーを許可するメカニズムがあります。 ヘルパー インターフェイスとの不具合の報告の詳細については、以下のトピックです。

[オフロードされたオーディオ処理のためのヘルパー インターフェイス](helper-interfaces-for-offloaded-audio-processing.md)

[オフロードされたオーディオのレポートの不具合](glitch-reporting-for-offloaded-audio.md)

 

 




