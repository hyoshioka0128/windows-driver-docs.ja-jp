---
title: 遅延の時計
description: 遅延の時計
ms.assetid: 3cdd4c69-d99d-48bc-a1d9-9da2a2511e94
keywords:
- シンセサイザー WDK のオーディオ、待機時間の時計
- WDK オーディオ、時計の待機時間
- WDK のオーディオ、待機時間をクロックします。
- 待機時間の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6ed612864e2436c2bdc57a077f2dd44867f02fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360461"
---
# <a name="latency-clocks"></a>遅延の時計


## <span id="latency_clocks"></span><span id="LATENCY_CLOCKS"></span>


シンセサイザーのミニポート ドライバー モデルは、複数のデバイス間でのオーディオ出力の同期を許可する設計されています。 そのため、純粋な UART デバイスで提供されるよりさらに複雑なタイミング モデルが含まれています。

イベントが配信を (されからキャプチャされた) 関連付けられているタイムスタンプを持つミニポート ドライバー。 このタイムスタンプが関連して、[マスター クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/master-clocks)します。 マスターのクロックは、システム全体ですべてのシーケンス処理で使用される同じクロックです。 マスター クロック時間は 100 ナノ秒タイマー刻み単位で測定されます。

ミニポート ドライバー マスター クロックから呼び出すことによって、現在の時刻を取得する[ **IMasterClock::GetTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-imasterclock-gettime)します。 Pin の作成時に、ポート ドライバーはカーネル モードを渡します[IMasterClock](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imasterclock)インターフェイスへの入力パラメーターの 1 つとして、ミニポート ドライバーを、 [ **IMiniportDMus::NewStream** 。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-newstream)メソッド。 現時点では、マスターのクロックは、システムのリアルタイム クロックをラップします。 マスターのクロックが変化しないにする必要がある pin がある場合に、*実行*状態。 一時停止することはありませんが一定の割合のクロックになります。

すべてのレンダリング デバイスでは、一定のイベントを承諾する時間と、イベントが聞こえる時刻間の待機時間があります。 この待機時間は、定数または (待機時間がオーディオのバッファーの現在の再生位置には依存シンセサイザー ソフトウェアの場合) のように変数を指定できます。 この待機時間は、ことで補正は。

-   Dmu のミニポート ドライバー、デバイスの待機時間に関係なく、時間で再生できるように、事前に十分なイベントを受信することができます。 イベントは、Dmu ポート ドライバー sequencer エンジンによってミニポート ドライバーのシーケンス処理します。

    Pin の作成時に、ポート ドライバーは 100 ナノ秒単位のデルタ時間のミニポート ドライバーを照会します。 このデルタ時間は、どの程度ミニポート ドライバーが、イベントを受信する各イベントのプレゼンテーション時間います。 ポート ドライバーにより、最も効果的にこのイベントを配信するまでに先行します。 この差分の非常に大きな値を指定 (で指定された*SchedulePreFetch*のパラメーター [ **IMiniportDMus::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nf-dmusicks-iminiportdmus-newstream)) にイベントを渡すポート ドライバーにより、ミニポート ドライバーがユーザー モードからポート ドライバーに配信されるとすぐにします。

-   アプリケーションをどの程度進んでイベントのスケジュールをお知らせいたします。 最大待機時間の使用が望ましくないこの場合です。 自分が送信した後、イベントをキャンセルすることはできませんので、近いこと送信できるイベントのプレゼンテーション時間にアプリケーションとシンセサイザーを操作できるより応答性が向上します。 この要件を処理するには、DirectMusic には、待機時間の時計の概念が導入されています。

    待機時間の時計は、最も近い将来の時刻に再生し、再生時間にスケジュールできるイベントを提供します。 つまり、アプリケーションのスケジュールを待機時間の時計に準じた現在時刻の前に再生できるイベントは場合、イベントが再生される遅延します。 シンセサイザーのミニポート ドライバーに応答して待機時間の時計を提供する、 [ **KSPROPERTY\_シンセサイザー\_LATENCYCLOCK** ](https://docs.microsoft.com/previous-versions/ff537402(v=vs.85))プロパティ項目。

    ミニポート ドライバーが照会されます[KSPROPSETID\_シンセサイザー](https://docs.microsoft.com/windows-hardware/drivers/audio/kspropsetid-synth)と KSPROPERTY\_シンセサイザー\_LATENCYCLOCK します。 ミニポート ドライバーのプロパティのハンドラーは、次回の時間にデータを表示することができますが、マスターのクロックの観点からを指定する待機時間の時計を返す必要があります。 たとえば、マスターのクロックが現在、50 を読み取り、現在 25 の単位の待機時間は、75 読み取り待機時間の時計にします。 クロックがこの方法で実装されている理由は、待機時間が一定である必要はありません、返される値はデルタだけよりもアプリケーションに複数の使用のことです。

 

 




