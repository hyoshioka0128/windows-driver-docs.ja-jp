---
title: カーネル モードのソフトウェア シンセサイザーのウェーブ シンク
description: カーネル モードのソフトウェア シンセサイザーのウェーブ シンク
ms.assetid: 37ba9ad5-8b35-4252-a6fd-46dead924294
keywords:
- wave シンク WDK オーディオ、カーネルモードソフトウェアシンセサイザー
- MIDI トランスポート WDK オーディオ
- wave シンク WDK オーディオ、MIDI トランスポート
- シンセサイザー WDK オーディオ、MIDI トランスポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85cbbce59c9e0398e49499c04f2fffe10f4c1146
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831423"
---
# <a name="a-wave-sink-for-kernel-mode-software-synthesizers"></a>カーネル モードのソフトウェア シンセサイザーのウェーブ シンク


## <span id="a_wave_sink_for_kernel_mode_software_synthesizers"></span><span id="A_WAVE_SINK_FOR_KERNEL_MODE_SOFTWARE_SYNTHESIZERS"></span>


「[シンセサイザーと Wave シンク](synthesizers-and-wave-sinks.md)」で説明されているように、dmus ポートドライバーは、カーネルモードで動作するソフトウェアシンセサイザーの Wave シンクを実装します。 シンセサイザーのミニポートドライバーは、ポートドライバーへの[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)インターフェイスを公開します。 ポートドライバーの wave シンクは、このインターフェイスを使用して、シンセサイザーによって生成される wave データを読み取ります。

DMus ポートドライバーの wave シンクを使用するには、DMus ミニポートドライバーで2種類の pin を使用して DirectMusic フィルターを定義する必要があります。

-   DirectMusic 入力ピンまたは MIDI 入力ピン。 この pin は、MIDI メッセージを含むレンダーストリームのシンクです。

-   波の出力ピン。 この pin は、PCM サンプルを含むレンダーストリームのソースです。

次の図は、シンセサイザーノード ([**KSNODETYPE\_シンセサイザー**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-synthesizer)) を含む DirectMusic フィルターを示しています。 このフィルターは、DirectMusic 入力ピンと wave 出力ピンを提供することで、カーネルモードのソフトウェアシンセサイザーの前述の要件を満たしています。 (また、従来の MIDI 合成をサポートする DMus ミニポートドライバーは、MIDI 入力ピンを提供できます)。

![カーネルモードソフトウェアシンセサイザーの directmusic フィルターを示す図](images/wavesink.png)

図の左側では、MIDI ストリームが DirectMusic 入力ピンを使用してフィルターに入ります。 この pin には、ポートドライバーに公開される[Imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)インターフェイスがあります。 ポートドライバーは、 [**IMiniportDMus:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)メソッドを呼び出すことによって、このインターフェイスを取得します。 ポートドライバーは、 [**Imxf::P utMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)メソッドを呼び出すことにより、MIDI メッセージをピンにフィードします。

図の右側では、wave ストリームは wave 出力ピンを介してフィルターを終了し、ポートドライバーの wave シンクにフローします。 ポートドライバーは、 **ISynthSinkDMus**インターフェイスを通じてピンと通信します。 このインターフェイスを取得するには、まず**IMiniportDMus:: NewStream**を呼び出して**imxf**インターフェイスを持つストリームオブジェクトを取得し、次にその**ISynthSinkDMus**インターフェイスのオブジェクトを照会します。 Wave シンクは、 [**ISynthSinkDMus:: Render**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-render)メソッドを呼び出すことによって、ピンから wave データをプルします。

ハードウェアシンセサイザーは、レンダリングのためにポートドライバーの wave シンクに依存していることもありますが、 **ISynthSinkDMus:: Render**を呼び出すと、多数の対話型アプリケーションの魅力的を実現するために、MIDI ストリームに十分な待機時間が追加されます。 ストリームの待機時間を減らすために、ハードウェアシンセサイザーは、ポートドライバーの wave シンクを使用する代わりに、ミックスおよび wave レンダリングハードウェアへの内部接続を備えている可能性があります。 この種類のシンセサイザーは、前の図の右側にある wave 出力ピンを、ハードウェアミキサーに配線された接続 (*ブリッジ pin*として表現) で置き換えます。

**ISynthSinkDMus**インターフェイスには、wave シンクを使用して wave データをレンダリングするメソッド、参照時刻からサンプル時刻への変換、およびマスタークロックとの同期を行うメソッドが用意されています。

[**ISynthSinkDMus::RefTimeToSample**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-reftimetosample)

[**ISynthSinkDMus:: Render**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-render)

[**ISynthSinkDMus:: SampleToRefTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-sampletoreftime)

[**ISynthSinkDMus:: SyncToMaster**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-isynthsinkdmus-synctomaster)

**ISynthSinkDMus**は、 **imxf**インターフェイスから継承します。 詳細については、「 [ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)」を参照してください。

上の図の DMus ミニポートドライバーは、次のように DirectMusic 入力ピンと wave 出力ピンを識別します。

-   DirectMusic 入力ピンを識別するために、ミニポートドライバーは、pin のデータ範囲を定義します。これは、種類が KSDATAFORMAT\_type\_MUSIC のメジャー形式と、種類が KSDATAFORMAT\_SUBTYPE\_DIRECTMUSIC のサブ形式です。 この組み合わせは、pin がタイムスタンプ付きの MIDI ストリームを受け入れることを示します。 データ範囲記述子は、 [**Ksdatarange MUSIC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)型の構造体です。 (例については、「 [DirectMusic ストリームのデータ範囲](directmusic-stream-data-range.md)」を参照してください)。ミニポートドライバーでは、のデータフロー\_\_、ピンのデータフロー方向を定義します。 ( [**Pcpin\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/ns-portcls-pcpin_descriptor)の構造体の**KsPinDescriptor**。データフローメンバーは、データフローの方向を示します)。**IMiniportDMus:: NewStream**を呼び出してこのピンのストリームオブジェクトを作成すると、ポートドライバーは、 *streamtype*パラメーターを dmus\_ストリーム\_MIDI\_RENDER に設定します。

-   ミニポートドライバーは、wave 出力ピンを識別するために、ピンのデータ範囲を定義します。これは、種類が KSDATAFORMAT\_TYPE\_AUDIO のメジャー形式と、KSDATAFORMAT\_サブタイプ\_PCM のサブ形式です。 この組み合わせは、ピンが PCM サンプルを含む wave オーディオストリームを出力することを示します。 データ範囲記述子は、 [**Ksdatarange AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)型の構造体です。 ( [PCM ストリームのデータ範囲](pcm-stream-data-range.md)の例を参照してください)。ミニポートドライバーは、ピンのデータフローの方向を定義して、データフロー\_\_します。 **IMiniportDMus:: NewStream**を呼び出してこのピンのストリームオブジェクトを作成すると、ポートドライバーによって*streamtype*パラメーターが dmus\_ストリーム\_WAVE\_SINK に設定されます。

さらに、ドライバーがシンセサイザーの MIDI 入力ピンをサポートする場合、その定義は DirectMusic 入力ピンの定義と似ていますが、pin 定義では、KSDATAFORMAT\_サブタイプのサブ形式\_MIDI を指定します。ピンは、タイムスタンプが付けられた MIDI ストリームではなく、未加工の MIDI ストリームを受け入れます。

 

 




