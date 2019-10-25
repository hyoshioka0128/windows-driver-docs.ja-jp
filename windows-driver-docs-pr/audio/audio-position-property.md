---
title: オーディオの位置プロパティ
description: オーディオの位置プロパティ
ms.assetid: 893fea84-9136-4107-96d2-8a4e2ab7bd2a
keywords:
- play position WDK audio
- レコード位置 WDK オーディオ
- オーディオプロパティ WDK、ストリーム内の位置
- WDM オーディオプロパティ WDK、stream 内の位置
- 読み取り位置 WDK オーディオ
- 書き込み位置 WDK オーディオ
- クライアントバッファーをループする WDK オーディオ
- 非ループクライアントバッファー WDK オーディオ
- クライアントが WDK オーディオをバッファーする
- ストリーミング位置 WDK オーディオ
- position プロパティ WDK audio
- キャプチャストリームの位置 WDK オーディオ
- ポートドライバー WDK オーディオ、位置プロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2aa7b7f9883ee5748f2c801c81db3c51831d67e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831358"
---
# <a name="audio-position-property"></a>オーディオの位置プロパティ


オーディオドライバーのクライアントは、 [**Ksk プロパティ\_audio\_POSITION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)プロパティを使用して、オーディオストリーム内の現在位置を取得して設定します。 プロパティは、 [**Ksaudio\_position**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_position)構造体を使用して、現在の位置を記述します。 構造体には、 **playoffset**と**writeoffset**の2つのメンバーが含まれています。

**Playoffset**メンバーと**writeoffset**メンバーは、現在オーディオデバイスを排他的に使用するために予約されているクライアントバッファーの領域の境界を定義します。 クライアントは、デバイスが現在このリージョンに含まれるデータにアクセスしている可能性があることを前提としています。 このため、クライアントは、このリージョンの外部にあるバッファーの部分のみにアクセスする必要があります。 ストリームが進むにつれて、領域の境界が移動します。

クライアントバッファーがループしている場合 (つまり、ストリーム型が[**Ksk インターフェイス\_標準\_ループ\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming))、 **Playoffset**と**writeoffset**はバッファー相対オフセットです。 つまり、ループクライアントバッファーの先頭からのバイトオフセットとして指定されます。 オフセットがバッファーの末尾までインクリメントされると、バッファーの先頭に折り返されます。 (バッファーの先頭のオフセットは0です)。したがって、オフセットがバッファーサイズを超えることはありません。

クライアントバッファーが非ループになっている場合 (つまり、ストリームの種類が[**Ksk interface\_STANDARD\_STREAMING**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-streaming))、 **Playoffset**と**writeoffset**はストリーム相対オフセットです。 つまり、ストリームの先頭からのバイトオフセットとして指定されます。 これらのオフセットは、ストリーム全体を格納し、先頭から末尾まで連続している、構成可能なバッファーへのオフセットと考えることができます。

レンダリングストリームの場合、 **Playoffset**メンバーはストリームの再生位置を指定し、 **writeoffset**メンバーはストリームの書き込み位置を指定します。 次の図は、クライアントバッファーの再生位置と書き込み位置を示しています。

![レンダリングストリーム内の再生位置と書き込み位置を示す図](images/playoffset.png)

再生位置は、現在再生されているサンプルのバイトオフセット (つまり、デジタル-アナログコンバーターまたは DAC の入力でラッチされるサンプル) のバイトオフセットです。 書き込み位置は、クライアントがバッファーに安全に書き込むことができる位置を超えています。 ストリームが再生されると、前の図では再生位置と書き込み位置が左から右に移動します。 クライアントの書き込みは、書き込み位置の前に置かれている必要があります。 また、バッファーがループされている場合、クライアントの書き込みで再生位置を overtake することはできません。

WaveCyclic または WavePci ポートドライバーは、再生位置を追跡するためにミニポートドライバーに依存しますが、ポートドライバーは書き込み位置を追跡します。 WaveCyclic および WavePci ポートドライバーは、次のように書き込み位置を更新します。

-   **WaveCyclic**

    WaveCyclic port ドライバーが[**IDmaChannel:: CopyTo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyto)を呼び出して、新しいデータブロックを循環バッファー (クライアントバッファーから) にコピーするたびに、書き込み位置はデータブロックの最後のバイトの (クライアントバッファー内の) 位置に進みます。

-   **WavePci**

    既定では、WavePci ミニポートドライバーが[**Iportwavepcistream:: GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)を呼び出して新しいマッピング (クライアントバッファーの一部) を取得し、呼び出しが成功するたびに、書き込み位置がの最後のバイトの (クライアントバッファー内の) 場所に進みます。新しいマッピング。

    WavePci ミニポートドライバーが、ポートドライバーへのプリフェッチオフセットを指定することによって既定の動作を上書きする場合、現在の書き込み位置は常に現在の再生位置とプリフェッチオフセットの合計と等しくなります。 詳細については、「[プリフェッチオフセット](prefetch-offsets.md)」を参照してください。

キャプチャストリームの場合、 **Playoffset**メンバーはストリームのレコード位置を指定し、 **writeoffset**メンバーはストリームの読み取り位置を指定します。 次の図は、クライアントバッファーのレコードと読み取り位置を示しています。

![キャプチャストリーム内のレコードの位置と読み取り位置を示す図](images/recordoffset.png)

レコード位置は、アナログ-デジタルコンバーター (ADC) の出力でラッチされる最新のサンプルのバイトオフセットです。 (この位置によって、オーディオデバイスの DMA エンジンが最終的にサンプルを書き込むバッファー位置が指定されます)。読み取り位置は、クライアントがバッファーから安全に読み取ることができない位置です。 ストリームの記録が進むにつれて、前の図では、読み取り位置とレコード位置が左から右に進みます。 クライアントの読み取りは、読み取り位置を記録する必要があります。 また、バッファーがループされている場合は、クライアントの読み取りがレコードの位置を超えている必要があります。

WaveCyclic または WavePci ポートドライバーは、レコードの位置を追跡するためにミニポートドライバーに依存しますが、ポートドライバーは読み取り位置を追跡します。 WaveCyclic および WavePci port ドライバーは、次のように読み取り位置を更新します。

-   **WaveCyclic**

    WaveCyclic port ドライバーが[**IDmaChannel:: CopyFrom**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idmachannel-copyfrom)を呼び出して、循環バッファー (クライアントバッファー) から新しいデータブロックをコピーするたびに、読み取り位置はデータブロックの最後のバイトの (クライアントバッファー内の) 位置に進みます。

-   **WavePci**

    WavePci ミニポートドライバーが[**Iportwavepcistream:: ReleaseMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-releasemapping)を呼び出して、以前に取得したマッピング (クライアントバッファーの一部) を解放するたびに、読み取り位置は、の最後のバイトの (クライアントバッファー内の) 場所に進みます。解放されたマッピング。

ミニポートドライバーは、KSK プロパティ\_AUDIO\_POSITION プロパティ要求のハンドラールーチンを実装する必要はありません。 代わりに、WaveCyclic および WavePci ポートドライバーは、ミニポートドライバーに代わってこれらの要求を処理します。 Get property 要求を処理する場合、WaveCyclic または WavePci port ドライバーは**writeoffset**値を計算するために必要なすべての情報を既に持っていますが、それでも、 **playoffset**値を計算するためにミニポートドライバーからの情報が必要です。 この情報を取得するために、ポートドライバーは、ミニポートドライバーの[**IMiniportWaveCyclicStream:: GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavecyclicstream-getposition)メソッドまたは[**IMiniportWavePciStream:: GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)メソッドを呼び出します。

レンダリングストリームの場合、 **GetPosition**メソッドは、再生位置 (DAC を通じて現在再生されているサンプルのバイトオフセット) を取得します。 キャプチャストリームの場合、 **GetPosition**メソッドは、レコードの位置を取得します。これは、ADC によってキャプチャされる最新のサンプルのバイトオフセットです。

**GetPosition**呼び出しによって取得されるオフセット値は、現在、スピーカージャックを介して送信されている信号に対応する再生位置か、またはマイクのジャック。 これは DMA の位置ではありません。 (DMA 位置は、オーディオデバイスの DMA エンジンが DMA バッファーとの間で現在やり取りしているサンプルのバイトオフセットです)。

一部のオーディオハードウェアには、現在各 DAC または ADC にあるサンプルのバイトオフセットを追跡する位置登録が含まれています。この場合、 **GetPosition**メソッドは、適切なストリームの位置レジスタの内容を取得するだけです。 その他のオーディオハードウェアでは、DMA 位置でのみドライバーを提供できます。その場合、現在の DMA の位置とバッファリングの遅延を考慮して、DAC または ADC 内のサンプルのバイトオフセットの最大の推定値を**GetPosition**メソッドで提供する必要があります。デバイスの内部。

WaveCyclic または WavePci port ドライバーのプロパティハンドラーは、ループバッファーと非ループバッファーを区別して、ストリーム相対またはバッファー相対のバイトオフセットを提供するかどうかを決定する必要がありますが、この詳細 (つまり、バッファーがループされているかどうかを判断します。非ループ) はミニポートドライバーに対して透過的です。

**IMiniportWaveCyclicStream:: GetPosition**メソッドは、クライアントバッファーがループされているかどうかに関係なく、常にバッファー相対再生またはレコード位置を報告します。 クライアントバッファーがループされている場合、プロパティハンドラーはミニポートドライバーによって報告されたバッファー相対位置を変換します。これは、循環バッファーへのオフセットとして表され、クライアントバッファーへのオフセットとして表されます。この位置は、ハンドラーによって次の**ように書き込まれます。PlayOffset**メンバー。 クライアントバッファーがループされていない場合、プロパティハンドラーは、再生**オフセット**メンバーに書き込む前に、バッファー相対再生位置をストリーム相対再生位置に変換します。

**IMiniportWavePciStream:: GetPosition**メソッドは、クライアントバッファーがループされているかどうかに関係なく、常にストリーム相対再生またはレコード位置を報告します。 クライアントバッファーがループしている場合、プロパティハンドラーは、KSK オーディオの**Playoffset**メンバーに書き込む前に、ストリーム相対再生位置をバッファー相対再生位置 (クライアントバッファーへのオフセットとして表現) に変換し\_プロパティ要求の位置構造。 クライアントバッファーがループ処理されない場合、プロパティハンドラーは、ストリーム相対位置を**Playoffset**メンバーに書き込みます。

再生またはレコードの位置は、ストリームの初期化直後にゼロになります。 KSK 状態への遷移\_停止状態 ( [**Ksk 状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ne-ks-ksstate)を参照) は、位置をゼロにリセットします。 \_KSK 状態からの遷移によってストリームが停止されると、\_一時停止または KSSTATE\_取得した場合、位置がフリーズします。 この unfreezes は、ストリームが KSK 状態\_PAUSE または KSSTATE から遷移して、\_KSK 状態\_実行された場合に発生します。

WaveCyclic および WavePci ミニポートドライバーの**GetPosition**メソッドの実装例については、「Windows Driver KIT (WDK) のオーディオドライバーの例」を参照してください。

 

 




