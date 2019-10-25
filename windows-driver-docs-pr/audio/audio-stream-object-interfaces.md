---
title: オーディオ ストリーム オブジェクトのインターフェイス
description: オーディオ ストリーム オブジェクトのインターフェイス
ms.assetid: 9d68016a-ddb1-4fbb-b6cc-384f8c76552c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1507b4056738f299bf969fc72ff61f4a8d6e0eaa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831295"
---
# <a name="audio-stream-object-interfaces"></a>オーディオ ストリーム オブジェクトのインターフェイス


## <span id="ddk_audio_stream_object_interfaces_ks"></span><span id="DDK_AUDIO_STREAM_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオストリームオブジェクトのインターフェイスについて説明します。 これらのインターフェイスは、wave、MIDI、および DirectMusic フィルターのピン間でやり取りされる wave および MIDI ストリームに関連付けられています。 これらのインターフェイスの一部はミニポートドライバーによって実装され、ポートドライバーに公開されます。 その他は、ポートドライバーによって実装され、ミニポートドライバーに公開されます。

このセクションでは、次のオーディオストリームオブジェクトインターフェイスについて説明します。

DirectMusic ストリームのバッファーストレージを管理します。 DMus ポートドライバーによって実装されます。

[デジタル著作権管理 (DRM)](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)保護をオーディオストリームのデジタルコンテンツに割り当てます。 WaveCyclic、WavePci、または WaveRT ミニポートドライバーによって実装されます。

MIDI フィルターのピンを通過する MIDI ストリームを表します。 MIDI ミニポートドライバーによって実装されます。

WaveCyclic フィルターのピンを通過する wave ストリームを表します。 WaveCyclic ミニポートドライバーによって実装されます。

WavePci フィルターのピンを通過する wave ストリームを表します。 WavePci ミニポートドライバーによって実装されます。

WaveRT フィルターのピンを通過する wave ストリームを表します。 WaveRT ミニポートの dirver によって実装されます。

**IMiniportWaveRTStream**インターフェイスを強化し、DMA ドライバーイベント通知用の追加のメソッドを提供します。

DirectMusic フィルターで MIDI または DirectMusic ピンを通過する MIDI ストリームを表します。 DMus ミニポートドライバーによって実装されます。

マップサービスを WavePci ミニポートドライバーのストリームオブジェクトに提供します。 WavePci port ドライバーによって実装されます。

DirectMusic シンセサイザーデバイスの波出力を処理します。 DMus ミニポートドライバーによって実装され、DMus ポートドライバーの wave シンクによって使用されます。

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-iallocatormxf)

[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstream)

[IMiniportWaveRTStreamNotofication](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavertstreamnotification)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavepcistream)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/dmusicks/nn-dmusicks-isynthsinkdmus)

 

 





