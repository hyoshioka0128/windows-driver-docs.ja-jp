---
title: DirectSound ストリームのデータ範囲
description: DirectSound ストリームのデータ範囲
ms.assetid: cc31eb2d-7421-4748-b14c-f4d3d15f9884
keywords:
- DirectSound WDK、オーディオ ストリームのデータ範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beaaa2379e9cf9455b9367c6c8f049dc38677259
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360130"
---
# <a name="directsound-stream-data-range"></a>DirectSound ストリームのデータ範囲


## <span id="directsound_stream_data_range"></span><span id="DIRECTSOUND_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio) DirectSound ストリームのデータ範囲を記述する構造体。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_AUDIO);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_DSOUND);
  MaximumChannels        = 4;   // max number of channels, or -1 for unlimited
  MinimumBitsPerSample   = 2;
  MaximumBitsPerSample   = 16;  // 16, 24, 32, etc.
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

この例ではメンバー値がのと同様、 [PCM マルチ チャネル ストリームのデータ範囲](pcm-multichannel-stream-data-range.md)の例外は、例、 **MaximumBitsPerSample**値。 この値は、サンプル コンテナーのサイズに設定されているため、8 の倍数である必要があります。 たとえば、デバイスは、24 ビットのコンテナーの値に 20 bits の有効なオーディオ データをサポートしている場合**MaximumBitsPerSample** 24 に設定する必要があります。

 

 




