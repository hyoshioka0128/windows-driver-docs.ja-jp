---
title: ビデオ メモリ リソースのページング
description: ビデオ メモリ リソースのページング
ms.assetid: e9734db6-3ad0-4c64-a9c6-15ba956b2dce
keywords:
- DMA バッファー WDK 表示、ビデオ メモリ リソースのページング
- WDK の表示、ビデオ メモリ リソースのページング
- ビデオ メモリ リソースの WDK 表示のページング
- ページング バッファー WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aef9f641abacceea0526c8ec03a7ed5c7e950d00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377357"
---
# <a name="paging-video-memory-resources"></a>ビデオ メモリ リソースのページング


## <span id="ddk_paging_video_memory_resources_gg"></span><span id="DDK_PAGING_VIDEO_MEMORY_RESOURCES_GG"></span>


Microsoft とは異なり[Windows 2000 Display Driver Model](windows-2000-display-driver-model-design-guide.md)、Windows Vista のディスプレイ ドライバー モデルでは、サインアウトし、ページングが使用可能な物理のビデオ メモリの合計量よりも作成するその他のビデオ メモリ リソース必要に応じてビデオ メモリ。 つまり、すべてビデオ メモリ リソースは、ビデオ メモリで同時に。

GPU では、そのパイプラインで複数の DMA バッファーをことができます。 これらのアクティブな DMA バッファーによって参照されているビデオ メモリ リソースは、ビデオ メモリでなければなりません。 その他のアイドル状態のビデオ メモリ リソースは、システム メモリにページ アウトできます。

GPU の前に、スケジューラがディスプレイのミニポート ドライバーを呼び出すことができます[ **DxgkDdiSubmitCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand) GPU、スケジューラに DMA バッファーを送信する関数では、すべてビデオ メモリ リソースがによって使用されるようにする必要があります、DMA バッファーは、ビデオ メモリに実際に存在します。 ビデオ メモリ リソースの一部でない場合する必要がありますページング システム メモリから。 GPU のスケジューラは、ビデオ メモリ マネージャーは、ビデオ メモリをシステム メモリから必要なビデオ メモリ リソースのデータを転送するビデオ メモリ内の領域の検索時に呼び出す必要があります。 ビデオ メモリの需要が高いとき、GPU のスケジューラは、ビデオ メモリ マネージャーは、必要なビデオ メモリ リソースのデータを確保するためにシステム メモリへのアイドル状態のビデオ メモリ リソースのデータの転送時に呼び出す必要があります。 ビデオとシステムのメモリの間でデータを転送するためのコマンドを含んでいる特殊な目的の DMA バッファーは、ページング バッファーと呼ばれます。 ビデオ メモリ マネージャーには、ディスプレイのミニポート ドライバーの[ **DxgkDdiBuildPagingBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)をドライバーがハードウェアに固有のデータ転送のコマンドを書き込むページング バッファーを作成する関数。

 

 





