---
title: オーディオ ストリーム オブジェクトのインターフェイス
description: オーディオ ストリーム オブジェクトのインターフェイス
ms.assetid: 9d68016a-ddb1-4fbb-b6cc-384f8c76552c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64c8200d748100332562c16a2382edbd53c4ad60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331542"
---
# <a name="audio-stream-object-interfaces"></a>オーディオ ストリーム オブジェクトのインターフェイス


## <span id="ddk_audio_stream_object_interfaces_ks"></span><span id="DDK_AUDIO_STREAM_OBJECT_INTERFACES_KS"></span>


このセクションでは、オーディオ ストリーム オブジェクトのインターフェイスについて説明します。 これらのインターフェイスを wave に関連付けられた MIDI ストリームのウェーブ、MIDI、ピンの間で、そのフローと DirectMusic をフィルター処理します。 これらのインターフェイスの一部、ミニポート ドライバーによって実装される、ポート ドライバーに公開します。 ポート ドライバによって実装され、ミニポート ドライバーに公開されている他のユーザーがします。

このセクションでは、次のオーディオ ストリーム オブジェクトのインターフェイスについて説明します。

DirectMusic ストリームのバッファーのストレージを管理します。 Dmu ポート ドライバーによって実装されます。

割り当てます[デジタル著作権管理 (DRM)](https://msdn.microsoft.com/library/windows/hardware/ff536260)デジタル オーディオ ストリームのコンテンツを保護します。 WaveCyclic、WavePci、または WaveRT ミニポート ドライバーによって実装されます。

MIDI フィルターで pin を流れる MIDI ストリームを表します。 MIDI ミニポート ドライバーによって実装されます。

WaveCyclic フィルターで pin を流れる wave ストリームを表します。 WaveCyclic ミニポート ドライバーによって実装されます。

フィルターで pin を流れる wave ストリームを表します。 WavePci ミニポート ドライバーによって実装されます。

WaveRT フィルターで pin を流れる wave ストリームを表します。 WaveRT のミニポート dirver によって実装されます。

**IMiniportWaveRTStream** DMA ドライバーのイベント通知の追加方法を提供するインターフェイス。

MIDI または DirectMusic DirectMusic フィルターで pin を流れる MIDI ストリームを表します。 Dmu のミニポート ドライバーによって実装されます。

WavePci ミニポート ドライバーのストリーム オブジェクトへのマッピング サービスを提供します。 WavePci ポート ドライバーによって実装されます。

DirectMusic シンセサイザー デバイス wave 出力を処理します。 Dmu のミニポート ドライバーによって実装され、Dmu ポート ドライバーのウェーブ シンクによって使用されます。

[IAllocatorMXF](https://msdn.microsoft.com/library/windows/hardware/ff536491)

[IDrmAudioStream](https://msdn.microsoft.com/library/windows/hardware/ff536568)

[IMiniportMidiStream](https://msdn.microsoft.com/library/windows/hardware/ff536704)

[IMiniportWaveCyclicStream](https://msdn.microsoft.com/library/windows/hardware/ff536715)

[IMiniportWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536725)

[IMiniportWaveRTStream](https://msdn.microsoft.com/library/windows/hardware/ff536738)

[IMiniportWaveRTStreamNotofication](https://msdn.microsoft.com/library/windows/hardware/ff536739)

[IMXF](https://msdn.microsoft.com/library/windows/hardware/ff536782)

[IPortWavePciStream](https://msdn.microsoft.com/library/windows/hardware/ff536907)

[ISynthSinkDMus](https://msdn.microsoft.com/library/windows/hardware/ff537011)

 

 





