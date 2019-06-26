---
title: DMA バッファーに対するセグメントの指定
description: DMA バッファーに対するセグメントの指定
ms.assetid: 7cd51f22-bf9b-4c45-98f0-e9e0d41dab96
keywords:
- メモリのセグメントの WDK 表示、DMA バッファー
- DMA バッファー メモリ セグメント、WDK の表示
- バッファーの WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f432e4b6f4032d7e3c6cf718fbfe439bb4d5cea7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376078"
---
# <a name="specifying-segments-for-dma-buffers"></a>DMA バッファーに対するセグメントの指定


## <span id="ddk_specifying_segments_for_dma_buffers_gg"></span><span id="DDK_SPECIFYING_SEGMENTS_FOR_DMA_BUFFERS_GG"></span>


ディスプレイのミニポート ドライバーでは、開口部セグメントをどの DMA からバッファーを割り当てることができますを指定できます。 DMA バッファーはロック ダウンされたシステムの連続したメモリとして割り当てることもできます。

ビデオ メモリ マネージャーは、割り当て、アプリケーションで必要な場合は、DMA バッファーを破棄します。 そのため、ビデオ メモリ マネージャーでは、元の DMA バッファーが割り当てられるセグメントのセットが必要です。 1 つだけのセグメントのセグメント セット可能性がありますで構成されることに注意してください。

Microsoft DirectX グラフィックスのカーネルのサブシステムが、表示ミニポート ドライバーを呼び出すときに[ **DxgkDdiCreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_createdevice)ディスプレイのミニポート ドライバーを指定できます、グラフィック コンテキスト デバイスを作成する関数セグメント セット ビデオ メモリ マネージャーが DMA バッファーを割り当てることができます。 ディスプレイのミニポート ドライバーが設定されている場合、 **DmaBufferSegmentSet**のメンバー、 [ **DXGK\_DEVICEINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_deviceinfo)ビデオ メモリ マネージャーは、0、構造体DMA バッファーの連続した非ページ メモリを割り当てるここでは、ディスプレイのミニポート ドライバーは、PCI サイクルを使用して、メモリにアクセスする必要があり、DMA 経由データ送信しなければならないメモリの物理アドレスから直接。 ディスプレイのミニポート ドライバーが設定されている場合**DmaBufferSegmentSet**に 0 以外の場合、ビデオ メモリ マネージャーにページング可能なメモリを割り当てるし、ページを指定した aperture セグメントにマップされます。 呼び出しでディスプレイのミニポート ドライバーに絞りセグメント内でページが明らかになるその[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数。

ローカルのビデオ メモリ内の DMA バッファーは、基本的なビデオ メモリ マネージャー モデルによってサポートされていないことに注意してください。

 

 





