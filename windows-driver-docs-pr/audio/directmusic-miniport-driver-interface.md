---
title: DirectMusic ミニポート ドライバー インターフェイス
description: DirectMusic ミニポート ドライバー インターフェイス
ms.assetid: a3532993-732a-4a7e-82bc-fc4199ec23dd
keywords:
- ミニポート ドライバー WDK のオーディオ、シンセサイザー
- シンセサイザー WDK オーディオ、ミニポート ドライバー
- wave シンク WDK オーディオ、ミニポート ドライバー
- DirectMusic カーネル モードの WDK オーディオ、ミニポート ドライバー
- カーネル モードのシンセサイザー WDK オーディオ、ミニポート ドライバー
- ポート ドライバー WDK のオーディオ、シンセサイザー
- ハードウェア アクセラレータ WDK オーディオ
- ミニポート ドライバー WDK オーディオ、カーネル モード ハードウェア アクセラレーション
- シンセサイザー WDK オーディオ、カーネル モードのハードウェア アクセラレーション
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54820cce4e34f0419b7e0985b9cda5faa920bdb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571353"
---
# <a name="directmusic-miniport-driver-interface"></a>DirectMusic ミニポート ドライバー インターフェイス


## <span id="directmusic_miniport_driver_interface"></span><span id="DIRECTMUSIC_MINIPORT_DRIVER_INTERFACE"></span>


Dmu のミニポート ドライバー インターフェイス、MIDI ミニポート ドライバー インターフェイスに基づいていますが、高度なシンセサイザーをサポートするために次の拡張機能を追加します。

-   インスタンスあたり 16 チャネルより大きい DLS ダウンロード

-   ハードウェアの注イベントのシーケンス処理

Dmu のミニポート ドライバー インターフェイスは、いくつかの方法では、MIDI ミニポート ドライバー インターフェイスによって異なります。 Dmu のミニポート ドライバー インターフェイスを実装する[IMiniportDMus](https://msdn.microsoft.com/library/windows/hardware/ff536699)ではなく[IMiniportMidi](https://msdn.microsoft.com/library/windows/hardware/ff536703)します。 このインターフェイスはのような**IMiniportMidi**が、 [ **IMiniportDMus::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536701)メソッドを作成、 [IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782) (MIDI 変換フィルター) インターフェイスに接続して、 [IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491) Dmu ポート ドライバーの実装ではなく、インターフェイス、 [IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)インターフェイス。 **IAllocatorMXF**と**IMXF** 、標準のラップ**GetMessage**と**PutMessage**呼び出し (を参照してください[ **IAllocatorMXF:。GetMessage** ](https://msdn.microsoft.com/library/windows/hardware/ff536494)と[ **IMXF::PutMessage**](https://msdn.microsoft.com/library/windows/hardware/ff536791))。 これらの呼び出しでは、MIDI の実際のバイト数ではなく、パッケージ化されたイベントを処理します。

シンセサイザーの Dmu ミニポート ドライバーには、DirectMusic プロパティの一部またはすべてを実装できます。 これらのプロパティは、DL のダウンロードとデバイスのチャネルの割り当てを管理するシステムを許可します。 Dmusprop.h ヘッダー ファイルでは、DirectMusic 固有のプロパティ項目を定義します。 これらのプロパティの一覧は、次を参照してください。 [KSPROPSETID\_シンセサイザー](https://msdn.microsoft.com/library/windows/hardware/ff537486)と[KSPROPSETID\_シンセサイザー\_Dls](https://msdn.microsoft.com/library/windows/hardware/ff537488)します。

Dmu のミニポート ドライバーは、複数の暗証番号 (pin) インスタンスの作成を許可する必要があります。 各ピンのインスタンスが 1 つの仮想シンセサイザーとして機能し、チャネルのセットを格納し、DLS ダウンロードの暗証番号 (pin) のインスタンスの独立したします。

説明されているシンセサイザー プロパティの一部[オーディオ ドライバーのプロパティ セット](https://msdn.microsoft.com/library/windows/hardware/ff536197)暗証番号 (pin) のインスタンスで動作させ、他のユーザーはグローバルです。 グローバル プロパティを処理するには、そのトポロジでシンセサイザー ノード シンセサイザーが必要です。 各プロパティ項目の説明では、その項目をシンセサイザー ノードまたは暗証番号 (pin) のインスタンスに送信されるかどうかを示します。 合成をサポートするハードウェアの各部分では、存在ポート ドライバー オブジェクトおよびミニポート ドライバー オブジェクトでは、次の図に示すようにします。

![directmusic シンセサイザーのポートおよびミニポートのドライバーを示す図](images/dmkmport.png)

ポート ドライバー オブジェクトが 1 つのインスタンスを公開、 [IPortDMus](https://msdn.microsoft.com/library/windows/hardware/ff536879)インターフェイスで、ミニポート ドライバー オブジェクトによって保持されます。 ミニポート ドライバーが 1 つのインスタンスをエクスポート、 **IMiniportDMus**インターフェイスで、ポート、ドライバーによって保持されます。 すべてのインスタンス化された pin では、ポート ドライバー要求に対応する**IMXF**インターフェイス。 とこのインスタンスと、システム間の通信は、暗証番号 (pin) とイベントの間をフローに宛てられたプロパティ要求の組み合わせ、 **IMXF**ストリーム インターフェイス。

2 つのオブジェクトは、作成時にそのミニポート ドライバーに渡す必要があります。

-   時計

-   アロケーター オブジェクト

クロックがレンダリングの非常に重要な操作をキャプチャするとします。 指定したノートを表示するために、ミニポート ドライバーが必要な時間です。ミニポート ドライバーは MIDI のデータを読み取り、タイムスタンプのカーネル イベントをできるように時間を把握し、必要があります。 詳細については、次を参照してください。[待機時間のクロック](latency-clocks.md)します。

[アロケーター](allocator.md)を持つオブジェクトを**IAllocatorMXF**インターフェイス、メモリをリサイクルするメモリのプールとして使用されます。 システム内のすべての MIDI メッセージは、この共通のプールから割り当てられます。 作成または個々 のメッセージを破棄するには、アロケーター オブジェクトを使用してください。

このセクションの内容:

[MIDI トランスポート](midi-transport.md)

[クロックの待機時間](latency-clocks.md)

[ミニポート ドライバーのプロパティ項目を要求](miniport-driver-property-item-requests.md)

[PortDMus DirectMusic ポートの既定のドライバーの作成](making-portdmus-the-default-directmusic-port-driver.md)

[レガシ デバイスとして、シンセサイザーを公開します。](exposing-your-synthesizer-as-a-legacy-device.md)

 

 




