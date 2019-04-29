---
title: PCM 高ビットデプス ストリームのデータ範囲
description: PCM 高ビットデプス ストリームのデータ範囲
ms.assetid: 4f3d48ff-e01d-4c80-b493-253afdba6fd7
keywords:
- PCM 高深さストリーム データ範囲 WDK
- ストリーム データを高深さの範囲は WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42628b45256d8b1ec85d9599fd3a7118815b8e6f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332240"
---
# <a name="pcm-high-bitdepth-stream-data-range"></a>PCM 高ビットデプス ストリームのデータ範囲


## <span id="pcm_high_bitdepth_stream_data_range"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096) PCM 高深さストリームのデータ範囲を記述する構造体。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_AUDIO);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  MaximumChannels        = 4;   // max number of channels, or -1 for unlimited
  MinimumBitsPerSample   = 2;
  MaximumBitsPerSample   = 24;  // 24, 32, etc.
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

この例ではメンバーの値と同様に、 [PCM マルチ チャネル Stream データ範囲](pcm-multichannel-stream-data-range.md)の例外は、例、`MaximumBitsPerSample`が 16 より大きい値。 この値は、サポートの有効なビットの最大数に設定されます。 たとえば、デバイスは、24 ビットのコンテナーの値に 20 bits の有効なオーディオ データをサポートしている場合`MaximumBitsPerSample`20 に設定する必要があります。

 

 




