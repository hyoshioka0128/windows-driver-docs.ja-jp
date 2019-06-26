---
title: 2 つ以上のストリームの同期
description: 2 つ以上のストリームの同期
ms.assetid: c25f4ca2-8a9f-43bc-a1bf-b71826b446ff
keywords:
- HD オーディオ、ストリームの同期
- 高解像度オーディオ (HD オーディオ) のストリームの同期
- WDK オーディオのストリームの同期
- ストリームの同期の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e11d64b1a78cf796e43116aae18b52d356d03ec
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354218"
---
# <a name="synchronizing-two-or-more-streams"></a>2 つ以上のストリームの同期


[ **SetDmaEngineState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)ルーチンは、次のいずれか 1 つまたは複数の DMA エンジンの状態を設定: 実行を一時停止、停止、またはリセットします。 このルーチンの呼び出しでは、1 つ以上の DMA エンジンを指定する場合、すべて DMA エンジンの状態遷移同期的にします。

ストリームのグループを同期する機能は、オーディオ アプリケーションによって必要があります。 たとえば、オーディオ ドライバーは、2 つのオーディオ コーデックを結合する論理サラウンド サウンド オーディオ デバイスを作成するコーデック結合を使用可能性があります。 1 つのコーデックが前面のスピーカーをドライブや 2 つ目のオーディオ コーデックがバック スピーカーをドライブ。 コーデックの機能、によって、オーディオ ドライバーに各コーデックの 1 つ、2 つのストリームの元のサラウンド サウンド オーディオ ストリームを分割する必要があります。 使用して、 [ **SetDmaEngineState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)ルーチンの開始し、同時にストリームを停止する、2 つのストリームは同期を維持します。

同期にもいくつかのサンプルでは、2 つのストリームを許可すると、各オーディオ成果物の望ましくない可能性があります。

[ **SetDmaEngineState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/nc-hdaudio-pset_dma_engine_state)ルーチンは、HD オーディオ DDI の両方のバージョンで使用できます。

UAA HD オーディオ クラス ドライバーは、コーデック結合を実行しません。

 

 




