---
title: DMA 使用時の考慮点
description: DMA 使用時の考慮点
ms.assetid: 7bbd11d2-858c-4ed6-81a4-74ba003e7dcd
keywords:
- バス マスターの DMA WDK ビデオのミニポート、考慮事項
- DMA バス マスター WDK ビデオのミニポート、考慮事項
- 同時実行の DMA WDK ビデオのミニポート
- VideoPortStartDma
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe26c24fa604001e8db28b8b6230e2c7063e7bff
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365695"
---
# <a name="points-to-consider-when-using-dma"></a>DMA 使用時の考慮点


## <span id="ddk_points_to_consider_when_using_dma_gg"></span><span id="DDK_POINTS_TO_CONSIDER_WHEN_USING_DMA_GG"></span>


このセクションでは、ミニポート ドライバーで DMA 操作を使用する場合に考慮すべき重要な点を提供します。

### <a name="span-idadditionalnotesonvideoportstartdmaspanspan-idadditionalnotesonvideoportstartdmaspanadditional-notes-on-videoportstartdma"></a><span id="additional_notes_on_videoportstartdma"></span><span id="ADDITIONAL_NOTES_ON_VIDEOPORTSTARTDMA"></span>VideoPortStartDma についての注意事項

通常、ディスプレイ ドライバーは、実際には、DMA の転送を実行するミニポート ドライバーに転送要求を送信します。 ディスプレイ ドライバーの DMA エンジンがアイドル状態のためだけの転送要求のすべてのデータが転送されたこととは限りません。 これは、ミニポート ドライバーを呼び出す必要があるため[ **VideoPortStartDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportstartdma)と[ **VideoPortCompleteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nf-video-videoportcompletedma)複数回の大規模転送要求。 ハードウェアの DMA エンジンはこのような 2 つの DMA 操作間のアイドル状態も転送する追加のデータがある可能性があります。 譲渡要求は完全に実現されている場合は、ディスプレイ ドライバーを通知するために、ミニポート ドライバーの役目です。

*コンテキスト*パラメーターの**VideoPortStartDma**ハードウェア拡張機能でメモリなどの非ページ メモリを指す必要があります。 このパラメーターは、ミニポート ドライバーに渡す[ **HwVidExecuteDma** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pexecute_dma) IRQL ディスパッチで実行されるコールバック ルーチン\_レベル。

### <a name="span-iddmaandinterruptsspanspan-iddmaandinterruptsspandma-and-interrupts"></a><span id="dma_and_interrupts"></span><span id="DMA_AND_INTERRUPTS"></span>DMA と割り込み

多くのデバイスのハードウェア DMA 操作が完了すると、割り込みが生成されます。 ビデオのミニポート ドライバーの割り込みサービス ルーチン (ISR) DPC ルーチン タスクをさらに DMA 関連のキューに入れる必要があります。 ビデオ ポート ドライバーの DMA 関数の呼び出しません ISR のみ呼び出すことができます IRQL ディスパッチ以下であるため\_レベル。

前述の DPC ルーチンで転送されるサイズを確認するには、安全では場合でも、 **VideoPortStartDma**関数がまだ返って、変数がによって示されるため、 *pLength*の引数**VideoPortStartDma**時に既に更新されて*HwVidExecuteDma*が呼び出されました。

### <a name="span-idlogicaladdressesversusphysicaladdressesspanspan-idlogicaladdressesversusphysicaladdressesspanlogical-addresses-versus-physical-addresses"></a><span id="logical_addresses_versus_physical_addresses"></span><span id="LOGICAL_ADDRESSES_VERSUS_PHYSICAL_ADDRESSES"></span>論理アドレスと物理アドレス

ビデオ ポート ドライバーの DMA の実装では、論理アドレスは、DMA ハードウェアで使用されるアドレスの概念を使用します。 論理アドレスは、物理アドレスを異なっていてもかまいません。 ビデオ ポート ドライバー提供の DMA 関数では、プラットフォーム固有のメモリ制限を考慮します。 このためなどのカーネル モードの機能ではなくビデオ ポート ドライバー DMA 関数を使用する重要な[ **MmGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmgetphysicaladdress)します。 参照してください[アダプター オブジェクトと DMA](https://docs.microsoft.com/windows-hardware/drivers/kernel/adapter-objects-and-dma)論理アドレスの詳細についてはします。

### <a name="span-idconcurrentdmaspanspan-idconcurrentdmaspanconcurrent-dma"></a><span id="concurrent_dma"></span><span id="CONCURRENT_DMA"></span>同時実行の DMA

デバイス同時 DMA の転送をサポートしている場合、同時読み取りと書き込みをサポートする DMA コント ローラーか、または 2 つの個別 DMA コント ローラーのミニポート ドライバーが同時実行のパスごとに個別の DMA アダプター オブジェクトを取得します。 たとえば、デバイスに並列で動作する 2 つの DMA コント ローラーがある場合は、ミニポート ドライバーように 2 つの呼び出し**VideoPortGetDmaAdapter**ため、2 つの副社長へのポインターを取得する\_DMA\_アダプター構造体。 その後、ミニポート ドライバーが特定の DMA コント ローラーの DMA 転送要求を行うたびに使用する適切なポインター要求にします。

 

 





