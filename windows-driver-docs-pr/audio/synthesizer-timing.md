---
title: シンセサイザーのタイミング
description: シンセサイザーのタイミング
ms.assetid: 38aca8b7-f895-4b16-aaac-5a13973cf976
keywords:
- シンセサイザー WDK のオーディオ、タイミング
- 時間の WDK オーディオ
- 参照クロック WDK オーディオ
- サンプルのクロックの WDK オーディオ
- WDK のオーディオ、シンセサイザーをクロックします。
- ユーザー モード シンセサイザー WDK オーディオ、シンセサイザー タイミング
- カスタムのシンセサイザー WDK のオーディオ、シンセサイザーのタイミング
- DirectMusic カスタム レンダリング WDK オーディオ、シンセサイザー タイミング
- ユーザー モードの WDK オーディオ、シンセサイザー タイミングでカスタムの表示
- DirectMusic WDK オーディオ、シンセサイザー
- タイマーの WDK オーディオ
- クロックの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c24bbbe6e8a43b49b8126e6cfe87b34db548f3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354209"
---
# <a name="synthesizer-timing"></a>シンセサイザーのタイミング


## <span id="synthesizer_timing"></span><span id="SYNTHESIZER_TIMING"></span>


シンセサイザーは、時間の 2 つの異なるシステムで動作します。

-   参照の時刻

-   サンプル時間

参照はメッセージのシーケンスを再生するには、絶対時間 (マスター クロック単位) です。 渡されるユーザー モードの実装では、 [ **IDirectMusicSynth::PlayBuffer** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-playbuffer)メソッドをシンセサイザー MIDI メッセージが送られるときにします。 シンセサイザー、wave シンク、および DirectMusic の残りの部分の実装によってシンセサイザーに関連付けられている同じマスター時計の下のすべての作業をする必要があります、 [ **IDirectMusicSynth::SetMasterClock** ](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynth-setmasterclock)メソッドを wave シンクと[ **IDirectMusicSynthSink::SetMasterClock**](https://docs.microsoft.com/windows/desktop/api/dmusics/nf-dmusics-idirectmusicsynthsink-setmasterclock)します。

シンセサイザーの出力バッファーにオフセットを測定するサンプルの時間が使用されます。 このバッファーは、サンプリング レートを基準としたため、サンプル時間ウェーブのサンプルが入力されます。 たとえば、22.1 kHz のサンプリング レート、毎秒の時間は等価です 22,100 サンプルまたは 44,200 バイト (16 ビットの mono 形式) の場合。

Wave サンプル バッファーの再生がマスター クロックよりも、異なるタイミング crystal で制御する可能性が高いために、参照の時刻とサンプルを複数傾向があります。 Wave シンクに、手順でそのフェーズ ロックされているループを実装することでに保持します。 このクロックの同期については、「[クロックの同期](clock-synchronization.md)します。

このセクションが含まれています。

[シンセサイザーの待機時間](synthesizer-latency.md)

[イベントのタイムスタンプ](time-stamped-events.md)

 

 




