---
title: PCM Stream データ範囲
description: PCM Stream データ範囲
ms.assetid: e8a9b681-3bd2-46ed-970f-5217dbfb2e4e
keywords:
- PCM のストリーム データ範囲 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38557a6373eb1f3c07a711c14eef4299f54cbb4b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528425"
---
# <a name="pcm-stream-data-range"></a>PCM Stream データ範囲


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

 

 




