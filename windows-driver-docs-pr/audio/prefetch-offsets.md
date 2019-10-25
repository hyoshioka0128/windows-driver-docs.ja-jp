---
title: プリフェッチ オフセット
description: プリフェッチ オフセット
ms.assetid: 92a0163f-29b1-4e15-88ab-67e1097d015e
keywords:
- ハードウェア高速化 WDK DirectSound、プリフェッチオフセット
- プリフェッチオフセット WDK オーディオ
- 書き込みカーソルオフセット WDK オーディオ
- カーソルオフセット WDK オーディオを再生する
- WDK オーディオをオフセットする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d34d23a8348617dc93fdcfef6e8a39253eac6614
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830227"
---
# <a name="prefetch-offsets"></a>プリフェッチ オフセット


## <span id="prefetch_offsets"></span><span id="PREFETCH_OFFSETS"></span>


WavePci ミニポートドライバーは、 [**Iprefetchoffset:: setprefetchoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)メソッドを呼び出して、ハードウェアアクセラレータによる DirectSound 出力ストリームのプリフェッチオフセットを指定します。 このオフセットは、オーディオデバイスのハードウェアバッファー内の再生カーソルから書き込みカーソルを分離するデータのバイト数です。 書き込みカーソルは、DirectSound アプリケーションが次のサウンドサンプルを安全に書き込むことができるバッファー位置を指定します。 Play カーソルは、オーディオデバイスによって現在再生されているサウンドサンプルのバッファー位置を指定します。

DirectSound は、 [**Ksk プロパティ\_AUDIO\_POSITION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)プロパティ要求を送信することにより、再生および書き込みカーソルの現在の位置を WavePci port ドライバーに照会します。 この要求に応答して、ポートドライバーは[**IMiniportWavePciStream:: GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-getposition)を呼び出すことによって、ミニポートドライバーから現在の再生位置を取得します。 ポートドライバーが書き込み位置を決定する方法は、 [**Setprefetchoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)が呼び出されたかどうかによって異なります。

既定では、ポートドライバーは、ミニポートドライバーによって要求された最後のマッピングに書き込みカーソルを位置付けます。 [**Iportwavepcistream:: GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavepcistream-getmapping)を呼び出すたびに、既定のプリフェッチオフセットが大きくなります。 WavePci ミニポートドライバーが大量のマッピングを取得すると、既定のオフセットが非常に大きくなる可能性があります。

[**Setprefetchoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)を呼び出すと、既定値がオーバーライドされます。 この呼び出しの後、ポートドライバーは、指定されたプリフェッチオフセットを再生位置に追加することによって書き込み位置を計算します (DirectSound バッファーの最後にあるラップアラウンドを考慮します)。

ミニポートドライバーでは、いくつかの理由により、多数のマッピングが割り当てられる場合があります。 1つは、システムプロセッサに対するオーディオ操作のオーバーヘッドを軽減することです。 多くのマッピングでは、オーディオデバイスを継続的にデータと共に提供するために、ドライバーの割り込み回数が少なくて済みます。 もう1つの理由は、複数のマッピングを割り当てることによって、デバイスドライバーが正しく動作しないと、システムが短時間実行される場合に、オーディオ再生が悪影響を受ける可能性が低下することです。

プリフェッチオフセットが大きい場合の問題の1つは、一部の DirectSound アプリケーションが再生カーソルと書き込みカーソルの相対的な位置を混同する可能性があることです。 Windows 95/98 では、オーディオ Vxd は比較的小さいプリフェッチオフセットを維持します。これらのオペレーティングシステム用に作成された DirectSound アプリケーションは、オフセットが予想よりも大きい場合に正しく動作しない可能性があります。

たとえば、アプリケーションで DirectSound バッファーを上半分に分割してから半分にし、その後、アプリケーションとデバイスの2つの部分を "ping を" します。 書き込みカーソルは、バッファーの上限または下限を最初に入力したときに、バッファーの半分に分のデータを書き込みます。 このスキームは、再生カーソルが常にバッファーの残りの半分に配置されていることを前提としています。つまり、書き込まれていない半分です。 プリフェッチオフセットがバッファーサイズの半分を超える場合、この想定は正しくないことに注意してください。 この場合、書き込みカーソルは DirectSound バッファーの最後に到達し、バッファーの先頭をラップすると、再生カーソルと同じ半分のバッファーに配置されます。 アプリケーションでは、バッファーの残りのデータを新しい書き込みカーソルの位置に書き込むときに、再生カーソルの位置を上書きし、まだ再生されていないデータを破棄します。

アプリケーション自体はこの種の障害に対してなりになる可能性がありますが、WavePci ミニポートドライバーでは、 [**Setprefetchoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)を呼び出してプリフェッチオフセットをより小さい値に設定するだけで、エラーモードを排除できます。

プリフェッチオフセットを小さい値に設定すると、結果として得られる書き込みカーソルが再生カーソルの近くに移動します。 プリフェッチオフセットは、ハードウェアの FIFO サイズに設定する必要があります。 一般的なプリフェッチオフセットは、DMA エンジンのハードウェア設計によって異なり、約64のサンプルです。

特定の古い DirectSound アプリケーションとの互換性を維持するために、DirectSound は現在、ハードウェアアクセラレータのピンの書き込みカーソルを10ミリ秒間隔で埋め込みます。 埋め込みの量は今後変わる可能性があることに注意してください。

ドライバーレベルでカーソルの書き込みと再生カーソルを管理する方法の詳細については、「 [Audio Position プロパティ](audio-position-property.md)」を参照してください。

 

 




