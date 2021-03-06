---
title: データのコピーおよびキャッシュのポリシー
description: データのコピーおよびキャッシュのポリシー
ms.assetid: 1867f2bd-240c-4525-9f02-98b8f1d54b17
keywords:
- キャッシュの HD オーディオ
- 高解像度オーディオ (HD オーディオ) キャッシュ
- キャッシュの WDK オーディオ
- バス スヌーピング WDK オーディオ
- 覗き見 WDK オーディオ
- メモリの WDK オーディオ
- オーディオ データのコピー
- データ コピーの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39cd87a109a7bc51daf0aff7ba420fbd64181b15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359102"
---
# <a name="data-copying-and-caching-policy"></a>データのコピーおよびキャッシュのポリシー


WaveCyclic ミニポート ドライバーでは、HD オーディオ コント ローラーのハードウェアにアクセスする、DMA バッファーとユーザー モードのオーディオ アプリケーションにアクセスするクライアント バッファー間でのオーディオ データをコピーします。

-   データ ストリームの再生は、ドライバーは、DMA バッファーに、クライアント バッファーからデータをコピーします。

-   キャプチャのデータ ストリームの場合は、ドライバーは、クライアントのバッファーに、DMA バッファーからデータをコピーします。

ストリームの再生とキャプチャの両方で、ドライバーは、DMA バッファー メモリのキャッシュを有効にすると、最適なパフォーマンスを実現できます (キャッシュの種類**MmCached**) と、キャッシュを保証する PCI コント ローラーのバス スヌーピング メカニズムに依存一貫性。 ただし、PCI Express コント ローラーのいくつかの実装は、Intel の初期 PCI Express チップセット) など、HD オーディオ コント ローラーのアイソクロナス データ転送を覗きされません。

PCI コント ローラーのハードウェアが DMA バッファー転送スヌーピング (のぞき見) をサポートしていますまたはアイソクロナス データ転送を実行するかどうか関数ドライバーを検出できません。 潜在的なキャッシュの一貫性の問題を回避するために、ドライバーは無効としてそのメモリのキャッシュの種類を指定することによって、DMA バッファー メモリのキャッシュ**MmWriteCombined**します。 (**MmNonCached**も機能しますがも実行しない可能性があります)。サンプル関数のドライバーに基づいているカスタム アダプターのドライバーを記述すること、PCI コント ローラーは DMA バッファー転送スヌーピング (のぞき見) 実際にサポートを確認する場合を除きに、WaveCyclic ミニポート ドライバー同様に動作する必要があります。

デバイスとスヌーピング (のぞき見) バスを実行しないシステムをサポートするには、カスタム関数のドライバーはこれらの規則に従う必要があります。

-   再生ストリーム、として、DMA バッファーのキャッシュの種類を指定**MmWriteCombined**します。 クライアント バッファーからデータのブロックを DMA バッファーにコピーした後、 [ **KeMemoryBarrier** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kememorybarrier) DMA エンジンにデータを見やすく関数。 **KeMemoryBarrier**プロセッサのデータ キャッシュを大きく耐性が効率的な方法でコピーしたデータをメモリにフラッシュします。

-   キャプチャ ストリームでは、いずれかとして、DMA バッファーのキャッシュの種類を指定**MmWriteCombined**または**MmNonCached**します。 さらに、関数のドライバーでは、DMA バッファーへの書き込みを避ける必要があります。 オーディオ サンプルの一括処理を実行する必要がある場合、最初にデータを別の場所をコピーする必要があります。

関数ドライバーまたは DMA バッファーからコピーしたデータのブロックが開始または書き込み結合バッファーの境界で終了する必要はありませんし、そのサイズは書き込み結合バッファー サイズ (通常、32 ビットまたは 64 バイト) の倍数である必要はありません。

使用するコーデック関数ドライバー、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl) DDI のバージョン、 [ **AllocateContiguousDmaBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_contiguous_dma_buffer) DMA バッファー メモリの割り当てと割り当てルーチンを実行します。 ルーチンが常に、バッファーのキャッシュの種類を設定**MmWriteCombined**します。

書き込み結合の詳細についてで、ia-32 Intel アーキテクチャ ソフトウェア ・ デベロッパーズ マニュアルを参照してください、 [Intel](https://go.microsoft.com/fwlink/p/?linkid=38518) web サイト。

 

 




