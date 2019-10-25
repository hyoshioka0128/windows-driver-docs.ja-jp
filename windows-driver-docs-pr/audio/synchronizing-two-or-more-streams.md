---
title: 2 つ以上のストリームの同期
description: 2 つ以上のストリームの同期
ms.assetid: c25f4ca2-8a9f-43bc-a1bf-b71826b446ff
keywords:
- HD オーディオ、ストリームの同期
- High Definition Audio (HD audio)、ストリームの同期
- ストリームの同期 WDK オーディオ
- ストリーム同期 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0a3acb484f2d6bebc5e88848068c3c37b18bb6dd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832339"
---
# <a name="synchronizing-two-or-more-streams"></a>2 つ以上のストリームの同期


[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)ルーチンは、1つまたは複数の DMA エンジンの状態を、次のいずれかに設定します。実行中、一時停止、停止、またはリセットします。 このルーチンへの呼び出しで複数の DMA エンジンが指定されている場合は、すべての DMA エンジンによって状態が同期的に移行されます。

一部のオーディオアプリケーションでは、ストリームのグループを同期する機能が必要です。 たとえば、オーディオドライバーは、コーデックの組み合わせを使用して2つのオーディオコーデックを結合する論理サラウンドサウンドオーディオデバイスを作成する場合があります。1つはフロントスピーカーを、もう1つは2番目のオーディオコーデックはバックスピーカーを駆動するコーデックです。 コーデックの機能によっては、元のサラウンドサウンドオーディオストリームを、コーデックごとに1つずつ、2つのストリームに分割することが必要になる場合があります。 [**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)ルーチンを使用してストリームの開始と停止を連携させることで、2つのストリームを同期したままにすることができます。

いくつかのサンプルでも、2つのストリームを同期させることができない場合、望ましくないオーディオアイテムが発生する可能性があります。

[**SetDmaEngineState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pset_dma_engine_state)ルーチンは、HD audio DDI の両方のバージョンで使用できます。

UAA HD オーディオクラスドライバーは、コーデックの組み合わせを実行しません。

 

 




