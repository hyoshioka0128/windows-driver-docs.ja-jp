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
ms.openlocfilehash: ed2bab09b323bf012e42c809671421bc6720ed40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328570"
---
# <a name="synthesizer-timing"></a>シンセサイザーのタイミング


## <span id="synthesizer_timing"></span><span id="SYNTHESIZER_TIMING"></span>


シンセサイザーは、時間の 2 つの異なるシステムで動作します。

-   参照の時刻

-   サンプル時間

参照はメッセージのシーケンスを再生するには、絶対時間 (マスター クロック単位) です。 渡されるユーザー モードの実装では、 [ **IDirectMusicSynth::PlayBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536540)メソッドをシンセサイザー MIDI メッセージが送られるときにします。 シンセサイザー、wave シンク、および DirectMusic の残りの部分の実装によってシンセサイザーに関連付けられている同じマスター時計の下のすべての作業をする必要があります、 [ **IDirectMusicSynth::SetMasterClock** ](https://msdn.microsoft.com/library/windows/hardware/ff536543)メソッドを wave シンクと[ **IDirectMusicSynthSink::SetMasterClock**](https://msdn.microsoft.com/library/windows/hardware/ff536528)します。

シンセサイザーの出力バッファーにオフセットを測定するサンプルの時間が使用されます。 このバッファーは、サンプリング レートを基準としたため、サンプル時間ウェーブのサンプルが入力されます。 たとえば、22.1 kHz のサンプリング レート、毎秒の時間は等価です 22,100 サンプルまたは 44,200 バイト (16 ビットの mono 形式) の場合。

Wave サンプル バッファーの再生がマスター クロックよりも、異なるタイミング crystal で制御する可能性が高いために、参照の時刻とサンプルを複数傾向があります。 Wave シンクに、手順でそのフェーズ ロックされているループを実装することでに保持します。 このクロックの同期については、「[クロックの同期](clock-synchronization.md)します。

このセクションが含まれています。

[シンセサイザーの待機時間](synthesizer-latency.md)

[イベントのタイムスタンプ](time-stamped-events.md)

 

 




