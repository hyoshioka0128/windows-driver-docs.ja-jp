---
title: PCM マルチチャンネル ストリームのデータ範囲
description: PCM マルチチャンネル ストリームのデータ範囲
ms.assetid: b7e1a5d9-fb8a-46ed-932b-d667e470d4ab
keywords:
- PCM マルチチャネルストリームデータ範囲 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19e648b0719c7c83e820cd435a4b082e7184c487
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830255"
---
# <a name="pcm-multichannel-stream-data-range"></a>PCM マルチチャンネル ストリームのデータ範囲


## <span id="pcm_multichannel_stream_data_range"></span><span id="PCM_MULTICHANNEL_STREAM_DATA_RANGE"></span>


この例では、 [**ksk の\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造体を使用して、PCM マルチチャネルストリームのデータ範囲を記述します。

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
  MaximumBitsPerSample   = 16;
  MinimumSampleFrequency = 5000;
  MaximumSampleFrequency = 48000;
```

 

 




