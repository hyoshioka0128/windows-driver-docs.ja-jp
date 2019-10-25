---
title: 共通バッファー バス マスター DMA
description: 共通バッファー バス マスター DMA
ms.assetid: 4758e084-1d9e-4e17-8627-05edc6b664ba
keywords:
- バスマスタ DMA WDK ビデオミニポート、共通バッファー
- DMA バス-マスタ WDK ビデオミニポート、共通バッファー
- 共通バッファー DMA WDK ビデオミニポート、説明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0076fd8238bb9f254222d35265a77468c21388e0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839799"
---
# <a name="common-buffer-bus-master-dma"></a>共通バッファー バス マスター DMA


## <span id="ddk_common_buffer_bus_master_dma_gg"></span><span id="DDK_COMMON_BUFFER_BUS_MASTER_DMA_GG"></span>


ミニポートドライバーは、共通バッファー DMA を使用するために次の一連の操作を実行します。

1.  アダプターオブジェクトを取得します。

    ミニポートドライバーは、通常はミニポートドライバーの[*HwVidFindAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter)ルーチン内でビデオポートドライバーの[**VideoPortGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdmaadapter)関数を呼び出して、 [**VP\_DMA\_アダプター**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))構造体へのポインターを取得します。 ミニポートドライバーは、後続の DMA 操作にこのポインターを使用します。

2.  共通バッファーを割り当てます。

    ミニポートドライバーは、前の手順で取得したポインターを使用して、ビデオポートドライバーの[**VideoPortAllocateCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportallocatecommonbuffer)関数を呼び出します。

3.  共通バッファーを解放します。

    ミニポートドライバーは、共通のバッファーを必要としなくなったときに、ビデオポートドライバーの[**VideoPortReleaseCommonBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportreleasecommonbuffer)関数を呼び出します。

4.  アダプターオブジェクトを破棄します。

    この手順は省略可能です。 何らかの理由で、その有効期間の残りの DMA 操作がないことがミニポートドライバーによって判断された場合、ビデオポートドライバーの[**VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportputdmaadapter)関数を呼び出すことによって、dma アダプターオブジェクトを破棄する必要があります。

 

 





