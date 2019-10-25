---
title: PCM ストリームのデータ範囲
description: PCM ストリームのデータ範囲
ms.assetid: e8a9b681-3bd2-46ed-970f-5217dbfb2e4e
keywords:
- PCM ストリームデータ範囲 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abc5efafc6c94de751b1064085dc15e760bed4fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830249"
---
# <a name="pcm-stream-data-range"></a>PCM ストリームのデータ範囲


## <span id="pcm_stream_data_range"></span><span id="PCM_STREAM_DATA_RANGE"></span>


この例では、 [**ksk の\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体を使用して、PCM ストリームのデータ範囲を記述します。

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

 

 




