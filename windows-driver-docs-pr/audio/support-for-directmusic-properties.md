---
title: DirectMusic プロパティのサポート
description: DirectMusic プロパティのサポート
ms.assetid: f44cf9a9-bdfc-4794-b064-4d1126fb83aa
keywords:
- ハードウェア アクセラレータ WDK オーディオ
- ミニポート ドライバー WDK オーディオ、カーネル モード ハードウェア アクセラレーション
- シンセサイザー WDK オーディオ、カーネル モードのハードウェア アクセラレーション
- シンセサイザー WDK のオーディオ、プロパティのサポート
- IKsControl インターフェイス
- プロパティ セット Guid の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 854c1a876db2cd3f71fc8582558d3dc9b69c3e20
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354243"
---
# <a name="support-for-directmusic-properties"></a>DirectMusic プロパティのサポート


## <span id="support_for_directmusic_properties"></span><span id="SUPPORT_FOR_DIRECTMUSIC_PROPERTIES"></span>


DirectMusic 合成ミニポート ドライバーでは、プロパティ項目の配列の形式でそのハードウェアの機能を指定します。 プロパティの各項目は、 [ **PCPROPERTY\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/ns-portcls-pcproperty_item)次を含む構造体。

-   プロパティは、DirectMusic で定義されている特定のハードウェア機能を定義する GUID を設定します。

-   ドライバー内で実装されているプロパティ ハンドラー メソッドへのポインター。

-   ハンドラーが、プロパティを取得するかどうかを指定するフラグのセットは、プロパティの設定し、プロパティの基本的なサポートを示します。

### <a name="span-idpropertysetguidsspanspan-idpropertysetguidsspanproperty-set-guids"></a><span id="property_set_guids"></span><span id="PROPERTY_SET_GUIDS"></span>プロパティ セット Guid

DirectMusic では、次のプロパティ セット Guid が定義されています。

-   GUID\_DMU\_PROP\_DLS1

-   GUID\_DMU\_PROP\_DLS2

-   GUID\_DMU\_PROP\_効果

-   GUID\_DMU\_PROP\_GM\_ハードウェア

-   GUID\_DMU\_PROP\_GS\_対応

-   GUID\_DMU\_PROP\_GS\_ハードウェア

-   GUID\_DMU\_PROP\_INSTRUMENT2

-   GUID\_DMU\_PROP\_LegacyCaps

-   GUID\_DMU\_PROP\_%memorysize

-   GUID\_DMU\_PROP\_SampleMemorySize

-   GUID\_DMU\_PROP\_SamplePlaybackRate

-   GUID\_DMU\_PROP\_SetSynthSink

-   GUID\_DMU\_PROP\_SynthSink\_DSOUND

-   GUID\_DMUS\_PROP\_SynthSink\_WAVE

-   GUID\_DMU\_PROP\_ボリューム

-   GUID\_DMU\_PROP\_WavesReverb

-   GUID\_DMU\_PROP\_WriteLatency

-   GUID\_DMU\_PROP\_WritePeriod

-   GUID\_DMU\_PROP\_XG\_対応

-   GUID\_DMU\_PROP\_XG\_ハードウェア

上記のプロパティの定義セット Guid は、の説明を参照してください。、 [ **KSPROPERTY** ](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)) DirectX 8.0 プログラマーズ リファレンス、Microsoft Windows sdk で構造体。 上記の Guid のそれぞれのプロパティの設定は、インデックスはゼロで識別される 1 つの要素で構成されます。

### <a name="span-idikscontrolinterfacespanspan-idikscontrolinterfacespanikscontrol-interface"></a><span id="ikscontrol_interface"></span><span id="IKSCONTROL_INTERFACE"></span>IKsControl インターフェイス

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)インターフェイスを取得し、設定、または、プロパティ、イベント、およびメソッドの基本的なサポートのクエリに使用されます。 このインターフェイスでは、(KS) アーキテクチャでは、ストリーミング WDM カーネルの一部ですが、DirectMusic ポートのプロパティを公開する DirectMusic でも使用されます。 このインターフェイスを取得する、 **IDirectMusicPort::QueryInterface**メソッド (Windows SDK のドキュメントで説明) を*riid*パラメーターに設定**IID\_IKsControl**します。

[IKsControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nn-ksproxy-ikscontrol)インターフェイスが 3 つのメソッドには。[**KsProperty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksproperty)、 [ **KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksevent)、および[ **KsMethod**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-ikscontrol-ksmethod)します。 現在、のみ**KsProperty** DirectMusic でサポートされています。

[ **IKsControl::KsProperty** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ikscontrol-ksproperty)メソッドを取得またはプロパティの値を設定します。 特定の DirectMusic ポートにプロパティ項目要求をルーティングする方法は、ポートの実装方法によって異なります。

-   Microsoft Win32 ハンドルに基づくマルチ メディアの呼び出し (midiOut および midiIn Api) の上に DirectMusic エミュレーションを表すポートでプロパティがサポートされていません。 使用して、 **GUID\_DMU\_PROP\_LegacyCaps**プロパティ セット GUID を Win32 マルチ メディアの呼び出しで実装されているかどうかのポートを照会します。

-   プロパティ項目の要求を表すプラグ可能なソフトウェアのシンセサイザーのポートには、ユーザー モードで完全処理されます。 ポートの種類のトポロジはシンセサイザー (によって表される、 [IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)インターフェイス) シンク ノードに接続されている (、 [IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)インターフェイス)。 プロパティ要求が与えられます最初シンセサイザーのノードにシンク ノードにし、シンセサイザーでが認識されない場合。

 

 




