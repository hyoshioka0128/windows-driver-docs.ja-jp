---
title: PCM ストリームのデータ範囲
description: PCM ストリームのデータ範囲
ms.assetid: e8a9b681-3bd2-46ed-970f-5217dbfb2e4e
keywords:
- PCM のストリーム データ範囲 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38557a6373eb1f3c07a711c14eef4299f54cbb4b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332234"
---
# <a name="pcm-stream-data-range"></a>PCM ストリームのデータ範囲


## <span id="pcm_stream_data_range"></span><span id="PCM_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096) PCM ストリームのデータ範囲を記述する構造体。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_AUDIO);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  MaximumChannels        = 2;
  MinimumBitsPerSample   = 2;
  MaximumBitsPerSample   = 16;
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

 

 




