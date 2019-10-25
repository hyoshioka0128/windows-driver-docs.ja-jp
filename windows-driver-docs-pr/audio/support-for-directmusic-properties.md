---
title: DirectMusic プロパティのサポート
description: DirectMusic プロパティのサポート
ms.assetid: f44cf9a9-bdfc-4794-b064-4d1126fb83aa
keywords:
- ハードウェア高速化の WDK オーディオ
- ミニポートドライバー WDK オーディオ、カーネルモードハードウェアアクセラレーション
- シンセサイザー WDK オーディオ、カーネルモードハードウェアアクセラレーション
- シンセサイザー WDK audio、プロパティのサポート
- IKsControl インターフェイス
- プロパティセット Guid WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79eedcd1d98a356d89aa1a6412bd0bdf6b17a801
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832350"
---
# <a name="support-for-directmusic-properties"></a>DirectMusic プロパティのサポート


## <span id="support_for_directmusic_properties"></span><span id="SUPPORT_FOR_DIRECTMUSIC_PROPERTIES"></span>


DirectMusic 合成ミニポートドライバーは、プロパティ項目の配列の形式でハードウェア機能を指定します。 各プロパティ項目は、次の項目を含む[**Pcproperty\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcproperty_item)構造体です。

-   DirectMusic によって定義される特定のハードウェア機能を定義するプロパティセット GUID。

-   ドライバー内に実装されているプロパティハンドラーメソッドへのポインター。

-   ハンドラーがプロパティを取得し、プロパティを設定し、プロパティの基本サポートを示すことができるかどうかを指定するフラグのセット。

### <a name="span-idproperty_set_guidsspanspan-idproperty_set_guidsspanproperty-set-guids"></a><span id="property_set_guids"></span><span id="PROPERTY_SET_GUIDS"></span>プロパティセット Guid

次のプロパティセット Guid は、DirectMusic によって定義されます。

-   \_\_PROP\_DLS1 の GUID

-   \_\_PROP\_DLS2 の GUID

-   \_DMUS\_PROP\_効果の GUID

-   \_DMUS\_PROP\_GM\_ハードウェアの GUID

-   \_DMUS\_PROP\_GS\_可能な GUID

-   GUID\_DMUS\_PROP\_GS\_ハードウェア

-   \_\_PROP\_INSTRUMENT2 の GUID

-   \_\_PROP\_LegacyCaps の GUID

-   \_DMUS\_PROP\_MemorySize の GUID

-   \_\_PROP\_SampleMemorySize の GUID

-   \_DMUS\_PROP\_SamplePlaybackRate の GUID

-   \_DMUS\_PROP\_SetSynthSink の GUID

-   \_DMUS\_PROP\_SynthSink\_DSOUND の GUID

-   \_DMUS\_PROP\_SynthSink\_WAVE の GUID

-   \_\_PROP\_ボリュームの GUID

-   \_\_PROP\_WavesReverb の GUID

-   \_PROP\_の\_の GUID

-   \_DMUS\_PROP\_WritePeriod の GUID

-   \_DMUS\_PROP\_XG\_対応する GUID

-   \_PROP\_XG\_ハードウェアの GUID\_DMUS

前のプロパティセット Guid の定義については、Microsoft Windows SDK の「DirectX 8.0 プログラマーリファレンス」にある[**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体の説明を参照してください。 上記の Guid のそれぞれに対して設定されるプロパティは、0のインデックスによって識別される1つの要素で構成されます。

### <a name="span-idikscontrol_interfacespanspan-idikscontrol_interfacespanikscontrol-interface"></a><span id="ikscontrol_interface"></span><span id="IKSCONTROL_INTERFACE"></span>IKsControl インターフェイス

[Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)インターフェイスは、プロパティ、イベント、およびメソッドの基本サポートを取得、設定、または照会するために使用されます。 このインターフェイスは、WDM カーネルストリーミング (KS) アーキテクチャの一部ですが、directmusic が DirectMusic ポートのプロパティを公開するためにも使用されます。 このインターフェイスを取得するには、Windows SDK ドキュメントで説明されているように、 **IDirectMusicPort:: QueryInterface**メソッドを呼び出します。このメソッドは、 *Riid*パラメーターを**IID\_iksk コントロール**に設定したものです。

[Iksk コントロール](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nn-ksproxy-ikscontrol)インターフェイスには、 [**ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksproperty)、 [**KsEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksevent)、および[**ksk メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-ikscontrol-ksmethod)の3つのメソッドがあります。 現時点では、 **"ksk" プロパティ**のみが DirectMusic でサポートされています。

[**Ikscontrol:: Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ikscontrol-ksproperty)メソッドは、プロパティの値を取得または設定します。 プロパティ項目要求が特定の DirectMusic ポートにルーティングされる方法は、ポートの実装方法によって異なります。

-   Microsoft Win32 ハンドルベースのマルチメディア呼び出し (midiOut Api と Midiout Api) 上で DirectMusic エミュレーションを表すポートでは、プロパティはサポートされません。 **Guid\_DMUS\_PROP\_LegacyCaps**プロパティセット guid を使用して、Win32 マルチメディア呼び出しで実装されているかどうかをポートに照会します。

-   プラグ可能なソフトウェアシンセサイザーを表すポートに対するプロパティ項目要求は、ユーザーモードで完全に処理されます。 この種類のポートのトポロジは、シンクノード ( [IDirectMusicSynthSink](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynthsink)インターフェイス) に接続されているシンセサイザー ( [IDirectMusicSynth](https://docs.microsoft.com/windows/desktop/api/dmusics/nn-dmusics-idirectmusicsynth)インターフェイスによって表されます) です。 プロパティ要求は、最初にシンセサイザーノードに与えられ、次にシンセサイザーによって認識されない場合はシンクノードに渡されます。

 

 




