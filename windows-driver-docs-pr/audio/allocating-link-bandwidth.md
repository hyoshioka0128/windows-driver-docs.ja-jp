---
title: リンク帯域幅の割り当て
description: リンク帯域幅の割り当て
ms.assetid: 7a5d5364-d869-4f6a-a7c3-9326ec347150
keywords:
- HD オーディオ、帯域幅
- 高解像度オーディオ (HD オーディオ)、帯域幅
- バスの帯域幅の WDK オーディオ
- 帯域幅の WDK オーディオ
- 帯域幅の割り当てください。
- リンクの帯域幅の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05c0f868594d126e6e977fed6544efd6152b2792
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355765"
---
# <a name="allocating-link-bandwidth"></a>リンク帯域幅の割り当て


HD オーディオのリンクが、一定のバスのレンダリングに使用できる帯域幅と、使用するストリームをキャプチャします。 Glitchless ことを確認するには、オーディオ、HD オーディオ バス ドライバー バスの帯域幅をリソースとして管理共有します。 関数のドライバーが DMA エンジンによって割り当てられるときに、DMA エンジンのレンダリングのバスの使用可能な帯域幅の一部を割り当てるかを使用するストリームをキャプチャする必要があります。

バスの帯域幅の固定量では、HD オーディオ リンクのシリアル (SDI) 行のデータと (SDO) 行をシリアル データがあります。 HD オーディオ バス ドライバーでは、SDI と SDO 行を個別に帯域幅の消費を監視します。 入力の割り当てまたはバスの帯域幅を出力する要求が使用できる帯域幅を超えている場合、バス ドライバーは、要求が失敗します。

関数のドライバーが、バス ドライバーを呼び出すときに[ **AllocateCaptureDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)と[ **AllocateRenderDmaEngine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンの場合、ストリームの形式を指定します。 ストリーム形式は、ストリームのサンプリング レート、サンプル サイズ、およびチャネルの数を指定します。 この情報は、割り当てから*Xxx*DmaEngine ルーチンは、ストリームのバスの帯域幅要件を決定します。 十分な帯域幅を使用できる場合、ルーチンは、DMA エンジンを使用して、必要な帯域幅を割り当てます。 それ以外の場合、割り当てへの呼び出し*Xxx*DmaEngine は失敗します。

関数のドライバーを呼び出すことができます[ **ChangeBandwidthAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)に既存の DMA エンジン割り当ての帯域幅の割り当ての変更を要求します。

割り当て*Xxx*DmaEngine と[ **ChangeBandwidthAllocation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)ルーチンは、HD オーディオ DDI の両方のバージョンで使用できます。

 

 




