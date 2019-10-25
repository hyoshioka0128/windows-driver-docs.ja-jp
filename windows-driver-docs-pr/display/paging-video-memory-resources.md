---
title: ビデオ メモリ リソースのページング
description: ビデオ メモリ リソースのページング
ms.assetid: e9734db6-3ad0-4c64-a9c6-15ba956b2dce
keywords:
- DMA バッファー WDK 表示、ビデオメモリリソースのページング
- ビデオメモリリソースのページングの WDK 表示
- ビデオメモリリソースのページ WDK の表示
- ページングバッファーの WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d48be7e68def75aec05dd45884454bc871f2d0c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826064"
---
# <a name="paging-video-memory-resources"></a>ビデオ メモリ リソースのページング


## <span id="ddk_paging_video_memory_resources_gg"></span><span id="DDK_PAGING_VIDEO_MEMORY_RESOURCES_GG"></span>


Microsoft [windows 2000 Display Driver モデル](windows-2000-display-driver-model-design-guide.md)とは異なり、windows Vista display driver model では、使用可能な物理ビデオメモリの総量よりも多くのビデオメモリリソースを作成できます。これにより、次のようにビデオメモリがページングされます。いる。 つまり、すべてのビデオメモリリソースが同時にビデオメモリに存在するわけではありません。

GPU には、パイプライン内に複数の DMA バッファーを含めることができます。 これらのアクティブな DMA バッファーによって参照されるビデオメモリリソースは、ビデオメモリ内に存在する必要があります。 その他のアイドル状態のビデオメモリリソースは、システムメモリにページアウトできます。

GPU スケジューラがディスプレイミニポートドライバーの[**DxgkDdiSubmitCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_submitcommand)関数を呼び出して、GPU に dma バッファーを送信する前に、スケジューラは dma バッファーで使用されるすべてのビデオメモリリソースが実際にビデオメモリ内にあることを確認する必要があります。 ビデオメモリにないリソースがある場合は、システムメモリからページングされている必要があります。 GPU スケジューラはビデオメモリマネージャーに対してを呼び出し、必要なビデオメモリリソースデータをシステムメモリからビデオメモリに転送するためにビデオメモリ内の領域を検出する必要があります。 ビデオメモリの需要が高い場合、GPU スケジューラはビデオメモリマネージャーでを呼び出して、アイドル状態のビデオメモリリソースデータをシステムメモリに転送し、必要なビデオメモリリソースデータ用の領域を確保する必要があります。 ビデオとシステムメモリ間でデータを転送するためのコマンドを含む特殊な目的の DMA バッファーは、ページングバッファーと呼ばれます。 ビデオメモリマネージャーは、ディスプレイミニポートドライバーの[**DxgkDdiBuildPagingBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)関数を呼び出して、ドライバーがハードウェア固有のデータ転送コマンドを書き込むためのページングバッファーを作成します。

 

 





