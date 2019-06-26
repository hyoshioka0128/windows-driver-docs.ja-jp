---
title: オーディオの位置プロパティ
description: オーディオの位置プロパティ
ms.assetid: 893fea84-9136-4107-96d2-8a4e2ab7bd2a
keywords:
- 位置の WDK オーディオを再生します。
- WDK のオーディオのレコードの位置
- WDK、ストリーム内の位置のオーディオのプロパティ
- WDM オーディオ プロパティ WDK、ストリーム内の位置
- WDK オーディオの位置を読み取る
- WDK オーディオの位置を書き込む
- ループのクライアント側のバッファーの WDK オーディオ
- nonlooped クライアント バッファー WDK オーディオ
- クライアント バッファー WDK オーディオ
- ストリームの位置の WDK オーディオ
- 位置プロパティ WDK オーディオ
- ストリームの位置の WDK オーディオをキャプチャします。
- ポート ドライバー WDK オーディオの位置プロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e84e529ff08ec81a265cfad712276f314c04ba19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355679"
---
# <a name="audio-position-property"></a>オーディオの位置プロパティ


オーディオ ドライバーのクライアントを使用して、 [ **KSPROPERTY\_オーディオ\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)プロパティを取得およびオーディオ ストリーム内の現在位置を設定します。 プロパティで使用する[ **KSAUDIO\_位置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_position)現在位置を表す構造体。 構造体には、2 つのメンバーが含まれています。**PlayOffset**と**WriteOffset**します。

**PlayOffset**と**WriteOffset**メンバーが排他的に使用するオーディオ デバイス用に予約されているクライアントのバッファーの領域の境界を定義します。 クライアントは、あるデバイスが現在にアクセスするこのリージョン内のデータのいずれかを想定する必要があります。 そのため、このリージョンの外にあるバッファーの部分のみをクライアントにアクセスする必要があります。 ストリームが進むと、領域の境界が移動します。

クライアント バッファーをループ処理している場合 (つまり、ストリームの種類が[ **KSINTERFACE\_標準\_るーぷさいせいぼたん\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-looped-streaming))、 **PlayOffset**と**WriteOffset**バッファーの相対オフセットします。 つまり、これらはループ クライアント バッファーの先頭からのバイト オフセットとして指定します。 バッファーの末尾にインクリメントをオフセットするか、バッファーの先頭にラップします。 (バッファーの先頭オフセットは 0 です)。したがって、どちらのオフセットには、バッファー サイズは、これまで超えています。

クライアント バッファーが場合 nonlooped (つまり、ストリームの種類が[ **KSINTERFACE\_標準\_ストリーミング**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksinterface-standard-streaming))、 **PlayOffset**と**WriteOffset**ストリームの相対オフセットします。 つまり、これらはストリームの先頭からのバイト オフセットとして指定します。 これらのオフセットはストリーム全体が含まれており、最初から最後までの連続する理想的なバッファーにオフセットとしての考えることができます。

レンダリング ストリームの場合、 **PlayOffset**メンバーは、ストリームの再生位置を指定し、 **WriteOffset**メンバーが、ストリームの書き込み位置を指定します。 次の図は、クライアント バッファー内の再生、書き込み位置を示します。

![再生位置とレンダリングのストリームに書き込み位置を示す図](images/playoffset.png)

再生位置が現在再生中のサンプルのバイト オフセット (アナログ デジタル コンバーター、または DAC の入力はラッチ サンプル)。 書き込み位置は、これを超えるクライアントは安全にバッファーに書き込む位置です。 再生、書き込み位置左から右に移動、ストリームの再生中、上記の図。 クライアントの書き込みは、書き込み位置を行く必要があります。 さらに、バッファーをループすると、クライアントの書き込みに再生位置が登場しない必要があります。

WaveCyclic または WavePci ポート ドライバーがの再生位置を追跡するミニポート ドライバーに依存していますが、ポート ドライバーの追跡、書き込み位置。 WaveCyclic と WavePci ポート ドライバーは、次のような書き込み位置を更新します。

-   **WaveCyclic**

    WaveCyclic ポート ドライバーの呼び出しごとに[ **IDmaChannel::CopyTo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyto) (クライアントの場所に書き込み位置を進めます (クライアントのバッファー) からに循環バッファーを新しいデータのブロックをコピーするにはバッファー) のデータ ブロックの最後のバイト。

-   **WavePci**

    既定では、毎回 WavePci のミニポート ドライバー呼び出し[ **IPortWavePciStream::GetMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping) (クライアント バッファーの一部) の新しいマッピングと呼び出しの取得に成功すると、書き込み位置の進歩新しいマッピングの最後のバイトの (クライアントのバッファー) の場所。

    WavePci ミニポート ドライバーでは、プリフェッチ ポート ドライバーにオフセットを指定することで、既定の動作をオーバーライドする場合は常に、現在の書き込み位置を現在の再生位置とプリフェッチ オフセットの合計を等しくします。 詳細については、次を参照してください。[プリフェッチ オフセット](prefetch-offsets.md)します。

キャプチャのストリームの場合、 **PlayOffset**メンバーは、ストリームのレコードの位置を指定し、 **WriteOffset**メンバーが、ストリームの読み取り位置を指定します。 次の図は、レコードを表示し、クライアント バッファー内の位置を読み取る。

![キャプチャ ストリーム内の位置を読んで、レコードの位置を示す図](images/recordoffset.png)

レコードの位置は、アナログ/デジタル変換、または ADC の出力にラッチを最新のサンプルのバイト オフセットです。 (この位置は、オーディオ デバイスの DMA エンジンが、サンプルを書かなければ先バッファーの場所を指定します)。読み取り位置が、位置を超えると、クライアントは、バッファーから読み取り安全にことはできません。 ストリームの進行状況の記録として、読み取りレコードの位置を進めると左から右に上記の図。 クライアントの読み取りには、読み取り位置を記録する必要があります。 さらに、バッファーをループすると、クライアントの読み取りが、レコードの位置の前ままする必要があります。

WaveCyclic または WavePci ポート ドライバーが、レコードの位置を追跡するミニポート ドライバーに依存していますが、ポート ドライバーの追跡、読み取り位置。 WaveCyclic と WavePci ポート ドライバーは、次のような読み取り位置を更新します。

-   **WaveCyclic**

    WaveCyclic ポート ドライバーの呼び出しごとに[ **IDmaChannel::CopyFrom** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idmachannel-copyfrom) (クライアントの場所に、読み取り位置を進めます (クライアントのバッファー) に、循環バッファーからデータの新しいブロックをコピーバッファー) のデータ ブロックの最後のバイト。

-   **WavePci**

    WavePci ミニポート ドライバーの呼び出しごとに[ **IPortWavePciStream::ReleaseMapping** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-releasemapping)読み取り位置に進めます (クライアント バッファーの一部) の前に取得したマッピングをリリースする、リリースのマッピングでは、最後のバイトの (クライアントのバッファー) 内の位置。

ミニポート ドライバーは KSPROPERTY のハンドラー ルーチンを実装する必要はありません\_オーディオ\_位置プロパティ要求。 代わりに、WaveCyclic と WavePci ポート ドライバーは、ミニポート ドライバーに代わってこれらの要求を処理します。 WaveCyclic または WavePci ポート ドライバーは既に計算に必要なすべての情報プロパティの get 要求を処理する際、 **WriteOffset**値が、を計算するミニポートドライバーからの情報を必要があります。**PlayOffset**値。 この情報を取得するポート ドライバーに呼び出し、ミニポート ドライバーの[ **IMiniportWaveCyclicStream::GetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavecyclicstream-getposition)または[ **IMiniportWavePciStream::GetPosition** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)メソッド。

ストリームについては、レンダリング、 **GetPosition**メソッドは、現在再生中で、DAC を使用するサンプルのバイト オフセットの再生位置を取得します。 ストリームについては、キャプチャ、 **GetPosition**メソッドは、レコードの位置の ADC によってキャプチャされる最新のサンプルのバイト オフセットを取得します。

オフセットの値を取得するメモを**GetPosition**呼び出しは現在、スピーカーのジャックから送信されるシグナルに対応する再生位置または現在シグナルに対応するレコードの位置マイクのジャックから受信しました。 DMA 位置ではありません。 (DMA 位置は、DMA バッファーとの間で、オーディオ デバイス DMA エンジンが転送中のサンプルのバイト オフセットです)。

一部のオーディオ ハードウェアには追跡のサンプルでは、各 DAC または ADC、現在のバイト オフセット後者に位置登録が含まれています、 **GetPosition**メソッドは単の位置のレジスタの内容を取得します適切なストリーム。 その他のオーディオ ハードウェアのみを提供するドライバー、DMA の位置をその場合、 **GetPosition**メソッドは、DMA の現在の位置を考慮して、DAC または ADC でサンプルのバイト オフセットの最適な見積もりを入力する必要があり、デバイスの内部バッファリングの遅延。

WaveCyclic または WavePci ポート ドライバー プロパティ ハンドラーがかどうかストリーム相対スケールまたは相対パスのバッファーのバイトを提供するオフセット、この詳細を確認するループと nonlooped バッファー間で区別する必要がありますが (バッファーをループ処理するかどうか、またはnonlooped) は、ミニポート ドライバーに対して透過的です。

**IMiniportWaveCyclicStream::GetPosition**メソッドは常にバッファーの相対 play またはクライアントのバッファーは、ループまたは nonlooped かどうかに関係なく、レコードの位置を報告します。 クライアント バッファーをループすると、プロパティ ハンドラーは、ハンドラー、へ書き込みますクライアントバッファーへのオフセットを循環バッファーのオフセットとして表現されたミニポートドライバーによって報告されたバッファーの相対位置を変換**PlayOffset**メンバー。 クライアント バッファーが場合 nonlooped、プロパティ ハンドラーに変換バッファーの相対の再生位置プレイのストリームの相対位置に書き込む前に、 **PlayOffset**メンバー。

**IMiniportWavePciStream::GetPosition**メソッドは常に相対ストリーム再生またはクライアントのバッファーは、ループまたは nonlooped かどうかに関係なく、レコードの位置を報告します。 クライアント バッファーをループすると、プロパティ ハンドラー再生のストリームの相対位置に変換 (クライアント バッファーのオフセットとして表されます) の相対パスのバッファーの再生位置に書き込む前に、 **PlayOffset**内のメンバー、KSAUDIO\_プロパティ要求内の位置の構造体。 クライアント バッファーの場合、nonlooped プロパティ ハンドラー書き込みますにストリームの相対位置、 **PlayOffset**メンバー。

Play またはレコードの位置はストリームの次のすぐにゼロ初期化です。 KSSTATE への遷移\_停止状態 (を参照してください[ **KSSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ne-ks-ksstate)) 位置を 0 にリセットします。 KSSTATE からの移行によって、ストリームを停止するときに\_KSSTATE に実行\_を一時停止または KSSTATE\_ACQUIRE、位置がフリーズします。 ストリームが遷移 KSSTATE ときの凍結が\_を一時停止または KSSTATE\_KSSTATE に取得\_を実行します。

実装例**GetPosition** WaveCyclic と WavePci ミニポート ドライバーでは、メソッドは、Windows Driver Kit (WDK) のサンプル オーディオ ドライバーを参照してください。

 

 




