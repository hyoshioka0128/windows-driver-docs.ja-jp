---
title: 遅延の時計
description: 遅延の時計
ms.assetid: 3cdd4c69-d99d-48bc-a1d9-9da2a2511e94
keywords:
- シンセサイザー WDK オーディオ、待機時間クロック
- 待機時間 WDK オーディオ、クロック
- クロック WDK オーディオ、待機時間
- 待機時間 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d785389606d4b2a2c4b21c89c5ed928f657cb3a3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832661"
---
# <a name="latency-clocks"></a>遅延の時計


## <span id="latency_clocks"></span><span id="LATENCY_CLOCKS"></span>


シンセサイザーミニポートドライバーモデルは、複数のデバイス間でオーディオ出力を同期できるように設計されています。 そのため、純粋な UART デバイスによって提供されるよりも複雑なタイミングモデルが含まれています。

イベントは、関連付けられたタイムスタンプを使用してミニポートドライバーに配信 (およびキャプチャ) されます。 このタイムスタンプは、[マスタークロック](https://docs.microsoft.com/windows-hardware/drivers/stream/master-clocks)を基準としています。 マスタークロックは、システム全体のすべてのシーケンス処理で使用されるクロックと同じです。 マスタークロック時間は、100ナノ秒単位で計測されます。

ミニポートドライバーは、 [**Imasterclock:: GetTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-imasterclock-gettime)を呼び出すことによって、マスタークロックから現在の時刻を取得します。 Pin の作成時に、ポートドライバーは、 [**IMiniportDMus:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)メソッドへの入力パラメーターの1つとして、カーネルモードの[imasterclock](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imasterclock)インターフェイスをミニポートドライバーに渡します。 現在、マスタークロックはシステムのリアルタイムクロックをラップします。 *実行*状態にする必要がある pin がある場合、マスタークロックは変更されません。 これは、一時停止しない一定の速度のクロックです。

すべてのレンダリングデバイスは、イベントが受理されてからイベントが発生するまでの間に一定の待機時間があります。 この待機時間は、定数または変数にすることができます (ソフトウェアシンセサイザーの場合と同様に、待機時間はオーディオバッファーの現在の再生位置に依存します)。 この待機時間は、次のものによって補正されます。

-   デバイスの待機時間に関係なく、時間どおりに再生できるように、DMus ミニポートドライバーが事前に十分な量のイベントを受信できるようにします。 イベントは、DMus ポートドライバーの sequencer エンジンによってミニポートドライバー用にシーケンス処理されます。

    Pin の作成時に、ポートドライバーはミニポートドライバーに100ナノ秒単位のデルタ時間を照会します。 この差分時間は、ミニポートドライバーがイベントを受信しようとしている各イベントのプレゼンテーション時間の前までの時間です。 ポートドライバーを使用すると、このようなイベントを事前に配信することができます。 このデルタに非常に大きな値 ( [**IMiniportDMus:: NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nf-dmusicks-iminiportdmus-newstream)の*scheduleprefetch フェッチ*パラメーターで指定) を指定すると、ユーザーモードからポートドライバーに配信されるとすぐに、ポートドライバーによってイベントがミニポートドライバーに渡されます。

-   アプリケーションにイベントをスケジュールするまでの時間を通知します。 この場合、最大待機時間を使用することは望ましくありません。 イベントが送信された後にキャンセルすることはできないため、イベントがプレゼンテーション時間に近いほど、アプリケーションとシンセサイザーが対話できる応答性が増えます。 この要件に対応するために、DirectMusic では待機時間クロックの概念が導入されました。

    待機時間の時計は、イベントを再生するようにスケジュールすることができ、時間どおりに再生できるようにするための最も近い時間を提供します。 つまり、待機時間の時刻に従って、現在の時刻より前に再生されるイベントをアプリケーションがスケジュールした場合、イベントは遅延して再生されます。 シンセサイザーミニポートドライバーは、 [**Ksk プロパティ\_シンセサイザー\_LATENCYCLOCK**](https://docs.microsoft.com/previous-versions/ff537402(v=vs.85))プロパティ項目に応答することによって、待機時間クロックを提供します。

    Ksk\_LATENCYCLOCK に対して、 [Kspropsetid\_シンセサイザー](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)および ksプロパティ\_のミニポートドライバーが照会されます。 ミニポートドライバーのプロパティハンドラーは、次回データを時間にレンダリングするときに、マスタークロックの観点から指定する待機時間クロックを返す必要があります。 たとえば、マスタークロックが現在50を読み取り、現在25単位の待機時間がある場合、待機時間クロックは75を読み取ります。 このようにクロックが実装される理由は、待機時間を一定にする必要がなく、返される値がデルタだけでなくアプリケーションにも使用されることです。

 

 




