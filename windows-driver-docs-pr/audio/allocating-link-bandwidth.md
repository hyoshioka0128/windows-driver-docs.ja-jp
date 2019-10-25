---
title: リンク帯域幅の割り当て
description: リンク帯域幅の割り当て
ms.assetid: 7a5d5364-d869-4f6a-a7c3-9326ec347150
keywords:
- HD オーディオ、帯域幅
- High Definition Audio (HD audio)、帯域幅
- バス帯域幅 WDK オーディオ
- 帯域幅 WDK オーディオ
- 帯域幅の割り当て
- リンク帯域幅 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3b597c8a7682493a1455d6dcc8cb209a8e765a8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831582"
---
# <a name="allocating-link-bandwidth"></a>リンク帯域幅の割り当て


HD audio リンクには、レンダーおよびキャプチャストリームで使用できるバス帯域幅が限られています。 Glitchless オーディオを確実にするために、HD オーディオバスドライバーは共有リソースとしてバス帯域幅を管理します。 関数ドライバーは DMA エンジンを割り当てるときに、DMA エンジンのレンダーストリームまたはキャプチャストリームが使用できるように、使用可能なバス帯域幅の一部も割り当てる必要があります。

固定量のバス帯域幅は、HD オーディオリンクのシリアルデータ (SDI) ラインおよび serial data out (SDO) 行で使用できます。 HD オーディオバスドライバーは、SDI と SDO の線で個別に帯域幅の消費を監視します。 入力または出力バスの帯域幅を割り当てる要求が使用可能な帯域幅を超えると、バスドライバーは要求に失敗します。

関数ドライバーがバスドライバーの[**Allocatecapturedmaengine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_capture_dma_engine)ルーチンと[**AllocateRenderDmaEngine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pallocate_render_dma_engine)ルーチンを呼び出すと、ストリーム形式が指定されます。 ストリーム形式は、ストリームのサンプル速度、サンプルサイズ、およびチャネル数を指定します。 この情報から、Allocate*Xxx*DmaEngine ルーチンによって、ストリームのバス帯域幅の要件が決定されます。 十分な帯域幅が使用可能な場合、このルーチンは DMA エンジンが使用するために必要な帯域幅を割り当てます。 それ以外の場合、*Xxx*DmaEngine を割り当てる呼び出しは失敗します。

関数ドライバーは、 [**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)を呼び出して、既存の DMA エンジン割り当ての帯域幅割り当ての変更を要求することができます。

Allocate*Xxx*DmaEngine および[**ChangeBandwidthAllocation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pchange_bandwidth_allocation)ルーチンは、HD audio DDI の両方のバージョンで使用できます。

 

 




