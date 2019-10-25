---
title: ビデオミニポートドライバーのバスマスタ DMA
description: ビデオミニポートドライバーのバスマスタ DMA
ms.assetid: fe6c2e16-d222-4948-b1df-34ed8d57d9d8
keywords:
- ビデオミニポートドライバー WDK Windows 2000、バスマスタ DMA
- バスマスタ DMA WDK ビデオミニポート
- DMA バス-マスタ WDK ビデオミニポート
- 共通バッファー DMA WDK ビデオミニポート
- 共通バッファー DMA WDK ビデオミニポート、概要
- パケットベースの DMA WDK ビデオミニポート
- パケットベースの DMA WDK ビデオミニポート、概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6992915d543f886e4ba23d7a2355078a6262d7a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839821"
---
# <a name="bus-master-dma-in-video-miniport-drivers"></a>ビデオミニポートドライバーのバスマスタ DMA


## <span id="ddk_bus_master_dma_in_video_miniport_drivers_gg"></span><span id="DDK_BUS_MASTER_DMA_IN_VIDEO_MINIPORT_DRIVERS_GG"></span>


Windows XP 以降では、オペレーティングシステムグラフィックスインターフェイスは PCI バスマスタデバイスで DMA をサポートしています。 PCI バスマスタデバイスのビデオミニポートドライバーは、ビデオポートドライバーによって提供されるヘルパー関数を使用して、次の種類の DMA サポートを実装できます。

-   **パケットベースの DMA**

    パケットベースの DMA では、データは、要求元のスペースとデバイスの間で直接転送されます。 要求元の領域が連続していない可能性があるため、ハードウェアのスキャッター/ギャザーがサポートされているデバイスでは、パケットベースの DMA の方が効率的です。 パケットベースの DMA は、ユーザー領域とデバイス間で大量の任意のデータを移動する場合に最適な選択肢です。

-   **共通バッファー DMA**

    共通バッファー DMA では、バッファーは (したがって共通の) 間で共有され、DMA 操作を繰り返すためにホストとデバイスの両方で使用されます。 一部のドライバーでは、共通バッファー DMA を使用して、一連のコマンドなどのドライバーで操作されたデータをグラフィックスエンジンにアップロードします。 共通バッファーは連続しており、デバイスとホストの両方の CPU に常にアクセスできます。

    一般的なバッファーは貴重なシステムリソースです。 ドライバーとシステムの全体的なパフォーマンスを向上させるために、ドライバーはできるだけ経済的に共通バッファー DMA を使用する必要があります。

バスマスタアダプターの性質によっては、一部のミニポートドライバーがパケットベースの DMA を排他的に使用し、他のデバイスが共通バッファー DMA だけを使用し、その両方を使用します。

使用する DMA の種類にかかわらず、ミニポートドライバーは[**VideoPortGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportgetdmaadapter)を呼び出して、 [**VP\_dma\_アダプター**](https://docs.microsoft.com/previous-versions/ff570570(v=vs.85))構造へのポインターを取得し、それを後続の DMA 関数呼び出しに使用します。 継続的な DMA 操作が不要になった場合、ミニポートドライバーは[**VideoPortPutDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportputdmaadapter)を呼び出して、アダプターオブジェクトを破棄する必要があります。

次のサブセクションでは、ビデオポートドライバーによって提供されるパケットベースおよび共通バッファー DMA のサポートを使用する方法について説明します。

[パケットベースのバスマスタ DMA](packet-based-bus-master-dma.md)

[共通バッファーバスマスタ DMA](common-buffer-bus-master-dma.md)

[DMA を使用する場合の考慮事項](points-to-consider-when-using-dma.md)

 

 





