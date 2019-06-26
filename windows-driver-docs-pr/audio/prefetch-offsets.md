---
title: プリフェッチ オフセット
description: プリフェッチ オフセット
ms.assetid: 92a0163f-29b1-4e15-88ab-67e1097d015e
keywords:
- ハードウェア アクセラレータ WDK DirectSound、プリフェッチ オフセット
- オフセットの WDK オーディオをプリフェッチします。
- 書き込みカーソル オフセット WDK オーディオ
- カーソル オフセット WDK オーディオを再生します。
- オフセットの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9271059269d2a1b476e16b4498eb23303fe8311
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362538"
---
# <a name="prefetch-offsets"></a>プリフェッチ オフセット


## <span id="prefetch_offsets"></span><span id="PREFETCH_OFFSETS"></span>


WavePci のミニポート ドライバーは呼び出し、 [ **IPreFetchOffset::SetPreFetchOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)ハードウェア アクセラレータによる DirectSound のプリフェッチのオフセットを指定するメソッドの出力ストリーム。 このオフセットには、書き込みカーソルを分離するオーディオ デバイスのハードウェアのバッファーでプレイ カーソルからのデータのバイト数です。 書き込みカーソルでは、先 DirectSound アプリケーションは安全に次のサウンドのサンプルを書き込むバッファーの位置を指定します。 再生のカーソルでは、オーディオ デバイスが現在再生されるサウンドのサンプルのバッファーの位置を指定します。

DirectSound クエリ、WavePci、プレイの現在の位置のドライバーのポートし、送信することによって書き込みカーソルを[ **KSPROPERTY\_オーディオ\_位置**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-position)プロパティ要求。 この要求に応答して、ポート ドライバーを取得、現在の再生位置、ミニポート ドライバーから呼び出すことによって[ **IMiniportWavePciStream::GetPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-getposition)します。 かどうかによって異なりますポート ドライバーが、書き込み位置を決定する方法[ **SetPreFetchOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)が呼び出されました。

既定では、ポート ドライバーは、ミニポート ドライバーによって要求された最後のマッピングで書き込みカーソルを移動します。 呼び出すごとに[ **IPortWavePciStream::GetMapping**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iportwavepcistream-getmapping)既定のプリフェッチのオフセットを大ききます。 WavePci ミニポート ドライバーでは、多数のマッピングを取得、既定のオフセットが非常に大きくなることができます。

呼び出す[ **SetPreFetchOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)既定値よりも優先されます。 この呼び出しでは、次のポートのドライバーは、(を考慮して、周回、DirectSound のバッファーの末尾) の再生位置に指定されたプリフェッチ オフセットを追加することで、書き込み位置を計算します。

ミニポート ドライバーは理由はいくつかの多数のマッピングを割り当てる可能性があります。 システム プロセッサのオーディオの操作のオーバーヘッドを軽減する 1 つです。 詳細マッピングは、ドライバーが少ない割り込み継続的にデータを指定するオーディオ デバイスを保持する必要があります。 別の理由は、複数のマッピングが減少が発生する可能性を割り当てるオーディオの再生が低下故障短期間のシステムの動作が不適切なデバイス ドライバー分け合う場合。

問題の 1 つ大きいプリフェッチ オフセットは、DirectSound アプリケーションによってできますなった、プレイの相対位置について混乱して書き込みカーソル。 Windows 95/98 では、オーディオ Vxd が比較的小さいプリフェッチのオフセットを維持し、オフセットが期待されるよりも大きい場合、これらのオペレーティング システム用に記述された DirectSound アプリケーションが正しく動作しない可能性があります。

たとえば、アプリケーションに分割 DirectSound バッファー上の半分と下半分と、"ping pong"し、アプリケーションとデバイスの 2 つの要素。 書き込みカーソルが最初、バッファーの上限や下限の半分に入ると、その半分のバッファーに、半分のバッファーの分のデータを書き込みます。 このスキームでは、バッファーに書き込まれていないが半分の他の半分でのプレイ カーソルの位置が常に前提としています。 この前提がプリフェッチ オフセットが、バッファー サイズの半分を超えた場合は、正しくないことに注意してください。 その場合は、書き込みカーソルは DirectSound バッファーの最後に達するし、バッファーの先頭に戻って、再生カーソルとして、バッファーの同じ半分のことができます。 アプリケーションでは、新しい書き込みカーソルの位置を半分のバッファーの分のデータを書き込みます、再生のカーソル位置を上書きして、まだ再生されていないデータは破棄を終了します。

WavePci ミニポート ドライバーが呼び出すだけで、障害モードを排除できますが、アプリケーション自体は、この種類の障害を確実に見下すことができます、 [ **SetPreFetchOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iprefetchoffset-setprefetchoffset)プリフェッチを設定するには値を小さくするオフセットします。

値を小さくするプリフェッチ オフセットを設定すると、play カーソルに近い結果として得られる書き込みカーソルが移動します。 ハードウェアの FIFO サイズには、プリフェッチ オフセットを設定する必要があります。 一般的なプリフェッチ オフセットは、DMA エンジンのハードウェアの設計によって、約 64 のサンプルです。

特定の古い DirectSound アプリケーションと互換性を保つ、DirectSound は現在 10 ミリ秒でハードウェア アクセラレータを使用した pin の書き込みカーソルを埋めます。 埋め込みの量が、後で変わる可能性がありますに注意してください。

書き込みカーソルとドライバー レベルでプレイ カーソルの管理に関する詳細については、次を参照してください。[オーディオ位置プロパティ](audio-position-property.md)します。

 

 




