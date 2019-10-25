---
title: DMA 使用時の考慮点
description: DMA 使用時の考慮点
ms.assetid: 7bbd11d2-858c-4ed6-81a4-74ba003e7dcd
keywords:
- バスマスタ DMA WDK ビデオミニポート、考慮事項
- DMA バス-マスタ WDK ビデオミニポート、考慮事項
- 同時 DMA WDK ビデオミニポート
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 234bc4662132c5aeb654f24f7d3b8144905b8d61
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829749"
---
# <a name="points-to-consider-when-using-dma"></a>DMA 使用時の考慮点


## <span id="ddk_points_to_consider_when_using_dma_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_USING_DMA_GG"></span>


このセクションでは、ミニポートドライバーで DMA 操作を使用する予定の場合に考慮すべき重要な点について説明します。

### <a name="span-idadditional_notes_on_videoportstartdmaspanspan-idadditional_notes_on_videoportstartdmaspanadditional-notes-on-videoportstartdma"></a><span id="additional_notes_on_videoportstartdma"></span><span id="ADDITIONAL_NOTES_ON_VIDEOPORTSTARTDMA"></span>VideoPortStartDma に関するその他の注意事項

通常、表示ドライバーは、転送要求をミニポートドライバーに送信します。この場合、実際には、これらの DMA 転送が行われます。 ディスプレイドライバーは、その DMA エンジンがアイドル状態であるために、転送要求のすべてのデータが転送されたことを想定できません。 これは、サイズの大きい転送要求では、ミニポートドライバーが[**Videoportstartdma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportstartdma)と[**videoportstartdma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportcompletedma)を複数回呼び出す必要があるためです。 ハードウェアの DMA エンジンは、転送する追加データがある場合でも、2つの DMA 操作の間にアイドル状態になります。 転送要求が完全に完了したことを表示ドライバーに通知するのは、ミニポートドライバーの役割です。

**Videoportstartdma**の*コンテキスト*パラメーターは、ハードウェア拡張機能のメモリなど、非ページメモリを指している必要があります。 このパラメーターは、IRQL ディスパッチ\_レベルで実行されるミニポートドライバーの[**HwVidExecuteDma**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pexecute_dma)コールバックルーチンに渡されます。

### <a name="span-iddma_and_interruptsspanspan-iddma_and_interruptsspandma-and-interrupts"></a><span id="dma_and_interrupts"></span><span id="DMA_AND_INTERRUPTS"></span>DMA と割り込み

多くのデバイスでは、ハードウェア DMA 操作の完了時に割り込みが生成されます。 ビデオミニポートドライバーの割り込みサービスルーチン (ISR) は、さらに DMA 関連のタスクを行うために DPC ルーチンをキューに追加する必要があります。 ISR でビデオポートドライバーの DMA 機能を呼び出すことはできません。これらは、IRQL ディスパッチ\_レベル以下でのみ呼び出すことができるためです。

Videoportstartdma 関数がまだ返されていない場合でも、この DPCルーチンで転送されるサイズを確認するのは安全です。これは、 **videoportstartdma**の*pLength*引数が指す変数が既にあるためです。*HwVidExecuteDma*が呼び出された時点で更新されました。

### <a name="span-idlogical_addresses_versus_physical_addressesspanspan-idlogical_addresses_versus_physical_addressesspanlogical-addresses-versus-physical-addresses"></a><span id="logical_addresses_versus_physical_addresses"></span><span id="LOGICAL_ADDRESSES_VERSUS_PHYSICAL_ADDRESSES"></span>論理アドレスと物理アドレス

ビデオポートドライバーの DMA 実装では、DMA ハードウェアによって使用されるアドレスである論理アドレスの概念が使用されます。 論理アドレスは、物理アドレスとは異なる場合があります。 ビデオポートドライバーが提供する DMA 機能では、プラットフォーム固有のメモリ制限が考慮されます。 このため、このようなカーネルモード関数を[**MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)として使用するのではなく、ビデオポートドライバーの DMA 機能を使用することが重要です。 論理アドレスの詳細については[、「アダプターオブジェクトと DMA](https://docs.microsoft.com/windows-hardware/drivers/kernel/adapter-objects-and-dma) 」を参照してください。

### <a name="span-idconcurrent_dmaspanspan-idconcurrent_dmaspanconcurrent-dma"></a><span id="concurrent_dma"></span><span id="CONCURRENT_DMA"></span>同時 DMA

同時読み取りと書き込みをサポートする DMA コントローラーで、または2つの異なる DMA コントローラーで同時 DMA 転送をサポートするデバイスの場合、ミニポートドライバーは、同時パスごとに個別の DMA アダプターオブジェクトを取得する必要があります。 たとえば、並列で動作する2つの DMA コントローラーがデバイスにある場合、ミニポートドライバーは2つの**VideoPortGetDmaAdapter**呼び出しを行う必要があります。これにより、2つの VP\_DMA\_アダプターの構造体へのポインターを取得します。 その後、ミニポートドライバーが特定の DMA コントローラーの DMA 転送要求を行うたびに、その要求で適切なポインターを使用する必要があります。

 

 





