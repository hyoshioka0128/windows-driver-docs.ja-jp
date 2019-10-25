---
title: DMA バッファーに対するセグメントの指定
description: DMA バッファーに対するセグメントの指定
ms.assetid: 7cd51f22-bf9b-4c45-98f0-e9e0d41dab96
keywords:
- メモリセグメント WDK ディスプレイ、DMA バッファー
- DMA バッファー WDK ディスプレイ、メモリセグメント
- WDK のバッファーの表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac518fe8cf2c9a09de7165469598a33dc638bf3c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825713"
---
# <a name="specifying-segments-for-dma-buffers"></a>DMA バッファーに対するセグメントの指定


## <span id="ddk_specifying_segments_for_dma_buffers_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_DMA_BUFFERS_GG"></span>


ディスプレイミニポートドライバーでは、DMA バッファーを割り当てることができるアパーチャセグメントを指定できます。 DMA バッファーは、連続してロックダウンされたシステムメモリとして割り当てることもできます。

ビデオメモリマネージャーは、アプリケーションが必要とするときに、DMA バッファーを割り当てて破棄します。 そのため、ビデオメモリマネージャーでは、DMA バッファーを割り当てることができる一連のセグメントが必要です。 セグメントセットは1つのセグメントのみで構成される場合があることに注意してください。

Microsoft DirectX graphics kernel サブシステムがディスプレイミニポートドライバーの[**DxgkDdiCreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)関数を呼び出してグラフィックスコンテキストデバイスを作成すると、ディスプレイミニポートドライバーは、ビデオメモリマネージャーが使用できるセグメントセットを指定できます。DMA バッファーを割り当てます。 ディスプレイミニポートドライバーによって、 [**DXGK\_DEVICEINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo)構造体の**DmaBufferSegmentSet**メンバーが0に設定されている場合、ビデオメモリマネージャーは DMA バッファー用に連続してページングされていないメモリを割り当てます。この場合、ディスプレイミニポートドライバーは PCI サイクルを使用してメモリにアクセスする必要があり、DMA 経由ではメモリの物理アドレスから直接データを送信する必要があります。 ディスプレイミニポートドライバーで**DmaBufferSegmentSet**が0以外に設定されている場合、ビデオメモリマネージャーはページング可能なメモリを割り当て、指定された絞りのセグメントにページをマップします。 [**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数を呼び出すと、アパーチャセグメント内のページがミニポートドライバーに表示されます。

Basic video memory manager モデルは、ローカルビデオメモリの DMA バッファーをサポートしていないことに注意してください。

 

 





