---
title: パケットベース バス マスター DMA
description: パケットベース バス マスター DMA
ms.assetid: f94b9ca9-6e29-4801-a092-30af19345f6d
keywords:
- バスマスタ DMA WDK ビデオミニポート、パケットベース
- DMA バス-マスタ WDK ビデオミニポート、パケットベース
- パケットベースの DMA WDK ビデオミニポート、説明
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b84201c0c01738ef9865796fdc04a4d43164276
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826062"
---
# <a name="packet-based-bus-master-dma"></a>パケットベース バス マスター DMA


## <span id="ddk_packet_based_bus_master_dma_gg"></span><span id="DDK_PACKET_BASED_BUS_MASTER_DMA_GG"></span>


通常、ディスプレイドライバーは、ミニポートドライバーに転送要求を送信して、DMA 操作を開始します。 パケットベースの DMA 操作をサポートするミニポートドライバーは、このような要求を受信すると、まずデータ転送に含まれるバッファーをロックします。 次に、ミニポートドライバーはビデオポートドライバーの[**Videoportstartdma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)関数を呼び出して転送を開始します。この関数は、データ転送を実行するためにミニポートドライバーの[**HwVidExecuteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pexecute_dma)コールバックルーチンを呼び出します。 この DMA 操作は非同期的に処理されます。 **Videoportstartdma**は dma 操作が完了するのを待たずに、コントロールをミニポートドライバーに返します。

転送要求のサイズとアダプターに割り当てられているシステムリソースの数によっては、ドライバーが1つの DMA 操作ですべてのデータを転送できない場合があります。 ミニポートドライバーは、転送されるデータが多いかどうかを調べるために返される実際の転送サイズを調べる必要があります。 DMA ハードウェアが現在の転送を完了するとすぐに、ミニポートドライバーはビデオポートドライバーの[**Videoportcompletedma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcompletedma)関数を呼び出して、現在の DMA 操作を完了する必要があります。 転送されるデータが残っている場合、ミニポートドライバーは、データが転送されなくなるまで、ビデオポートドライバーの**Videoportstartdma**関数と**videoportstartdma**関数を繰り返し呼び出すプロセスを繰り返します。 すべてのデータが転送されると、ミニポートドライバーによってバッファーのロックが解除されます。

ミニポートドライバーは、次の一連の操作を実行して、パケットベースの DMA を使用します。

1.  ハードウェアの機能をシステムに報告し、アダプタオブジェクトを取得します。

    ミニポートドライバーは、ビデオポートドライバーの[**VideoPortGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdmaadapter)関数を呼び出します。この関数は、 [**VP\_DMA\_アダプター**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))構造体へのポインターを返します。 通常、この処理は初期化時に行われ、通常はミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)ルーチン内で実行されます。 ミニポートドライバーは、後続の DMA 操作にこのポインターを使用します。

2.  ホストメモリをロックします。

    ミニポートドライバーは、ビデオポートドライバーの[**Videoportlockbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportlockbuffer)関数を呼び出します。この関数は、バッファーをプローブし、メモリページを常駐させて、ロックします。

3.  DMA 転送を開始します。

    ミニポートドライバーは、ビデオポートドライバーの[**Videoportstartdma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)関数を呼び出します。この関数は、ホストのプロセッサメモリキャッシュをフラッシュし、スキャッター/ギャザーリストを構築し、ミニポートドライバーの[**HwVidExecuteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pexecute_dma)コールバックルーチンを呼び出して、DMA 操作を非同期に実行します。 **Videoportstartdma**は、dma 操作の完了を待たずに、ミニポートドライバーに制御を返します。

4.  DMA 転送を完了します。

    ミニポートドライバーは、ハードウェアが DMA 操作を完了するとすぐにビデオポートドライバーの[**Videoportcompletedma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcompletedma)関数を呼び出す必要があります。 多くのビデオアダプターは、DMA 操作の完了時に割り込みを生成します。 たとえば、この種類のアダプターを使用するシステムは、次のように割り込みに応答する可能性があります。 ハードウェアが割り込みを生成して、DMA 操作が完了したことをミニポートドライバーに通知すると、ミニポートドライバーの割り込みサービスルーチン (ISR) は、DPC ルーチンをキューに記録するために、ビデオポートドライバーの[**VideoPortQueueDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportqueuedpc)関数を呼び出します。ビデオポートドライバーの**Videoportcompletedma**関数を呼び出します。 このビデオポートドライバー関数は IRQL ディスパッチ\_レベル以下で呼び出される必要があるため、ISR は**Videoportcompletedma**を直接呼び出すことができません。

    **Videoportcompletedma**は、バスマスターアダプターの内部キャッシュに残っているすべてのデータをフラッシュし、未使用のリソース ( **Videoportcompletedma**によって作成されたスキャッター/ギャザーリストを含む) を解放します。

    データの一部のみが転送された場合 (たとえば、使用可能なマップレジスタの数に制限があるため)、すべてのデータが次のようになるまで、ミニポートドライバーは**Videoportstartdma**と**videoportstartdma**を繰り返し呼び出す必要があります。支払.

5.  ホストメモリのロックを解除します。

    すべてのデータが転送されると、ミニポートドライバーはビデオポートドライバーの[**Videoportunlockbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportunlockbuffer)関数を呼び出して、2番目の手順で取得したデータバッファーのロックを解除する必要があります。

6.  アダプターオブジェクトを破棄します。

    *この手順は省略可能*です。 何らかの理由で、その有効期間の残りの DMA 操作がないことがミニポートドライバーによって判断された場合、ビデオポートドライバーの[**VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportputdmaadapter)関数を呼び出すことによって、dma アダプターオブジェクトを破棄する必要があります。

 

 





