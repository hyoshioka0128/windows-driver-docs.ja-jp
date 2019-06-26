---
title: オーディオ ストリーム オブジェクトのインターフェイス
description: オーディオ ストリーム オブジェクトのインターフェイス
ms.assetid: 9d68016a-ddb1-4fbb-b6cc-384f8c76552c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e05d2cfaf56eab015e6ad9c3fc08a07db8e6b71e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355643"
---
# <a name="audio-stream-object-interfaces"></a>オーディオ ストリーム オブジェクトのインターフェイス


## <span id="ddk_audio_stream_object_interfaces_ks"></span><span id="DDK_AUDIO_STREAM_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオ ストリーム オブジェクトのインターフェイスについて説明します。 これらのインターフェイスを wave に関連付けられた MIDI ストリームのウェーブ、MIDI、ピンの間で、そのフローと DirectMusic をフィルター処理します。 これらのインターフェイスの一部、ミニポート ドライバーによって実装される、ポート ドライバーに公開します。 ポート ドライバによって実装され、ミニポート ドライバーに公開されている他のユーザーがします。

このセクションでは、次のオーディオ ストリーム オブジェクトのインターフェイスについて説明します。

DirectMusic ストリームのバッファーのストレージを管理します。 Dmu ポート ドライバーによって実装されます。

割り当てます[デジタル著作権管理 (DRM)](https://docs.microsoft.com/windows-hardware/drivers/audio/digital-rights-management)デジタル オーディオ ストリームのコンテンツを保護します。 WaveCyclic、WavePci、または WaveRT ミニポート ドライバーによって実装されます。

MIDI フィルターで pin を流れる MIDI ストリームを表します。 MIDI ミニポート ドライバーによって実装されます。

WaveCyclic フィルターで pin を流れる wave ストリームを表します。 WaveCyclic ミニポート ドライバーによって実装されます。

フィルターで pin を流れる wave ストリームを表します。 WavePci ミニポート ドライバーによって実装されます。

WaveRT フィルターで pin を流れる wave ストリームを表します。 WaveRT のミニポート dirver によって実装されます。

**IMiniportWaveRTStream** DMA ドライバーのイベント通知の追加方法を提供するインターフェイス。

MIDI または DirectMusic DirectMusic フィルターで pin を流れる MIDI ストリームを表します。 Dmu のミニポート ドライバーによって実装されます。

WavePci ミニポート ドライバーのストリーム オブジェクトへのマッピング サービスを提供します。 WavePci ポート ドライバーによって実装されます。

DirectMusic シンセサイザー デバイス wave 出力を処理します。 Dmu のミニポート ドライバーによって実装され、Dmu ポート ドライバーのウェーブ シンクによって使用されます。

[IAllocatorMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-iallocatormxf)

[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nn-drmk-idrmaudiostream)

[IMiniportMidiStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportmidistream)

[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)

[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)

[IMiniportWaveRTStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstream)

[IMiniportWaveRTStreamNotofication](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavertstreamnotification)

[IMXF](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-imxf)

[IPortWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iportwavepcistream)

[ISynthSinkDMus](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dmusicks/nn-dmusicks-isynthsinkdmus)

 

 





