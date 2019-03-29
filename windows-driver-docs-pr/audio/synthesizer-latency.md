---
title: シンセサイザーの待機時間
description: シンセサイザーの待機時間
ms.assetid: a3134024-77b9-463b-959b-3c910f83014d
keywords:
- シンセサイザー WDK のオーディオ、待機時間
- WDK オーディオ、シンセサイザーの待機時間
- MIDI メッセージ待機時間の WDK オーディオ
- IReferenceClock オブジェクト
- wave オーディオ、待機時間の WDK をシンクします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b97f055a5d013fed25ba7dc0d2b2409485a63ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579408"
---
# <a name="synthesizer-latency"></a>シンセサイザーの待機時間


## <span id="synthesizer_latency"></span><span id="SYNTHESIZER_LATENCY"></span>


シンセサイザーのタイミングで別の考慮事項は、待機時間は、現在の時刻とメモを再生できる初めての違いです。 MIDI メッセージをシンセサイザーに送信され、現在のサンプル時に出力バッファーに表示されることはできません。 許容値は、バッファーが既に配置されているが、wave 出力デバイスにストリーミングされていないデータに対して行う必要があります。

Wave シンクはそのためは、待機時間の時計を実装する必要があります、 [ **IReferenceClock** ](https://msdn.microsoft.com/library/windows/desktop/dd743269)オブジェクト (Microsoft Windows SDK のドキュメントで説明)。 待機時間のクロックの[ **IReferenceClock::GetTime** ](https://docs.microsoft.com/en-us/previous-versions//dd551385(v=vs.85))メソッドの取得、サンプリング時間までデータは、バッファーに既に書き込まれているし、これをマスターのクロックの相対時刻の参照に変換します. Wave シンクを参照し、サンプルの時間の間の変換[ **IDirectMusicSynthSink::SampleToRefTime** ](https://msdn.microsoft.com/library/windows/hardware/ff536526)と[ **IDirectMusicSynthSink::RefTimeToSample** ](https://msdn.microsoft.com/library/windows/hardware/ff536525)、ここでは、シンセサイザーを呼び出して**IDirectMusicSynthSink::RefTimeToSample**変換を完了します。

待機時間は、すべて wave シンクによって管理されます。 実装、 [ **IDirectMusicSynthSink::GetLatencyClock** ](https://msdn.microsoft.com/library/windows/hardware/ff536523)メソッドは、待機時間の時計へのポインターを出力して、によってこのポインターを取得する必要がさらに[ **IDirectMusicSynth::GetLatencyClock**](https://msdn.microsoft.com/library/windows/hardware/ff536536)します。 アプリケーションでは、待機時間のクロックを使用して、コンピューターを呼び出すことによって、シンセサイザーに渡されるときに再生するキューを MIDI メッセージの最初のポイントを判断、 [ **IDirectMusicSynth::PlayBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff536540)メソッド。

MIDI メッセージの待機時間の例は、次の図に示します。

![midi メッセージの待機時間を示す図](images/dmclock.png)

上記の図では、待機時間の時計は、メモを再生できる PCM バッファーのループで最初の場所を指します。 マスターのクロックが、あること、22 時間単位で、ポイント、サウンドは、現在再生されてが、時間単位の 22 と 30 日間のスペース wave データが既に追加されていますを記述できなくできますに注意してください。 そのため、新しいタイムスタンプ MIDI イベントを再生するスケジュールできる最初の場所は 30 時間です。 そのため、待機時間の時計が 30 時間単位を読み取ります。

メッセージは、この待機時間を再生、または後に、いつでもスケジュールできます。 そのため、すぐに表示するメッセージのシンセサイザーの入力バッファー内に配置する前に待機時間 (現在の時刻ではない) がスタンプされます。

 

 




