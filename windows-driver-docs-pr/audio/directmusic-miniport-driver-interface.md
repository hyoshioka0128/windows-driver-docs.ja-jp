---
title: DirectMusic ミニポート ドライバー インターフェイス
description: DirectMusic ミニポート ドライバー インターフェイス
ms.assetid: a3532993-732a-4a7e-82bc-fc4199ec23dd
keywords:
- ミニポートドライバー WDK オーディオ、シンセサイザー
- シンセサイザー WDK オーディオ、ミニポートドライバー
- wave シンク WDK オーディオ、ミニポートドライバー
- DirectMusic カーネルモード WDK オーディオ、ミニポートドライバー
- カーネルモード synths WDK オーディオ、ミニポートドライバー
- ポートドライバー WDK オーディオ、シンセサイザー
- ハードウェア高速化の WDK オーディオ
- ミニポートドライバー WDK オーディオ、カーネルモードハードウェアアクセラレーション
- シンセサイザー WDK オーディオ、カーネルモードハードウェアアクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dca0a36472226617807c1440af25d6134f99187d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833549"
---
# <a name="directmusic-miniport-driver-interface"></a>DirectMusic ミニポート ドライバー インターフェイス


## <span id="directmusic_miniport_driver_interface"></span><span id="DIRECTMUSIC_MINIPORT_DRIVER_INTERFACE"></span>


DMus ミニポートドライバーのインターフェイスは、MIDI ミニポートドライバーのインターフェイスに基づいていますが、高度なシンセサイザーをサポートするために次の拡張機能が追加されています。

-   1インスタンスあたり16を超えるチャネルをダウンロードする

-   ハードウェアでのノートイベントのシーケンス処理

DMus ミニポートドライバーインターフェイスは、MIDI ミニポートドライバーインターフェイスとはいくつかの点で異なります。 DMus ミニポートドライバーは、 [IMiniportMidi](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidi)ではなく、インターフェイス[IMiniportDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iminiportdmus)を実装します。 このインターフェイスは**IMiniportMidi**に似ていますが、 [**IMiniportDMus:: Newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)メソッドは[imxf](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf) (MIDI 変換フィルター) インターフェイスを作成し、dmus ポートドライバーの[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)インターフェイスに接続します。[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)インターフェイスを実装します。 **IAllocatorMXF**と**imxf**は、標準の**GetMessage**および**putmessage**呼び出しをラップします ( [**IAllocatorMXF:: GetMessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iallocatormxf-getmessage)および[**imxf::P utmessage**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imxf-putmessage)を参照)。 これらの呼び出しは、未加工の MIDI バイトではなく、パッケージ化されたイベントを処理します。

シンセサイザー用の DMus ミニポートドライバーは、一部またはすべての DirectMusic プロパティを実装できます。 これらのプロパティを使用すると、システムはデバイスの DLS ダウンロードとチャネル割り当てを管理できます。 Dマス、.h ヘッダーファイルは、DirectMusic 固有のプロパティアイテムを定義します。 これらのプロパティの一覧については、「 [kspropsetid\_シンセサイザー](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth) 」と「 [kspropsetid\_シンセサイザー\_Dls](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth-dls)」を参照してください。

DMus ミニポートドライバーでは、複数の pin インスタンスを作成できます。 各 pin インスタンスは1つの仮想シンセサイザーとして機能し、他の pin インスタンスとは独立した一連のチャネルと DLS ダウンロードを含みます。

「[オーディオドライバー」プロパティ](https://docs.microsoft.com/windows-hardware/drivers/audio/audio-drivers-property-sets)で説明されている一部のシンセサイザープロパティは、pin インスタンスで動作し、その他はグローバルです。 グローバルプロパティを処理するには、シンセサイザーのトポロジにシンセサイザーノードが必要です。 各プロパティ項目の説明は、その項目がシンセサイザーノードに送信されるか、または pin インスタンスに送信されるかを示します。 合成をサポートするハードウェアの各部分について、次の図に示すように、ポートドライバーオブジェクトとミニポートドライバーオブジェクトが存在します。

![directmusic シンセサイザーのポートとミニポートドライバーを示す図](images/dmkmport.png)

ポートドライバーオブジェクトは、ミニポートドライバーオブジェクトによって保持されている[Iportdmus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iportdmus)インターフェイスの1つのインスタンスを公開します。 ミニポートドライバーは、ポートドライバーによって保持されている**IMiniportDMus**インターフェイスの1つのインスタンスをエクスポートします。 インスタンス化されたすべてのピンについて、ポートドライバーは一致する**Imxf**インターフェイスを要求します。 システムとこのインスタンス間の通信は、ピンに宛てられたプロパティ要求と、 **Imxf** stream インターフェイスとの間でやり取りされるイベントの組み合わせです。

ミニポートドライバーの作成時には、次の2つのオブジェクトをミニポートドライバーに渡す必要があります。

-   時計

-   アロケーターオブジェクト

この時計は、レンダリング操作とキャプチャ操作に非常に重要です。 ミニポートドライバーは、指定された時刻にメモをレンダリングする必要があります。ミニポートドライバーが MIDI データを読み取るときは、カーネルイベントにタイムスタンプをかけることができるように、時間を把握しておく必要があります。 詳細については、「[待機時間クロック](latency-clocks.md)」を参照してください。

**IAllocatorMXF**インターフェイスを持つ[アロケーター](allocator.md)オブジェクトは、メモリプールとして使用され、メモリをリサイクルします。 システム内のすべての MIDI メッセージは、この共通プールから割り当てられます。 個々のメッセージを作成または破棄するには、アロケーターオブジェクトを使用する必要があります。

このセクションの内容:

[MIDI トランスポート](midi-transport.md)

[待機時間のクロック](latency-clocks.md)

[ミニポートドライバーのプロパティ項目の要求](miniport-driver-property-item-requests.md)

[PortDMus を既定の DirectMusic ポートドライバーにする](making-portdmus-the-default-directmusic-port-driver.md)

[従来のデバイスとしてシンセサイザーを公開する](exposing-your-synthesizer-as-a-legacy-device.md)

 

 




