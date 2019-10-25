---
title: PCM 高ビットデプス ストリームのデータ範囲
description: PCM 高ビットデプス ストリームのデータ範囲
ms.assetid: 4f3d48ff-e01d-4c80-b493-253afdba6fd7
keywords:
- PCM 高ビット深度ストリームデータ範囲 WDK
- 高ビット深度ストリームデータ範囲 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2852f62f95b0792f8e39583b7da377acdfaddcb2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830263"
---
# <a name="pcm-high-bitdepth-stream-data-range"></a>PCM 高ビットデプス ストリームのデータ範囲


## <span id="pcm_high_bitdepth_stream_data_range"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_RANGE"></span>


この例では、 [**Ksdatarange\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造を使用して、PCM 高ビット深度ストリームのデータ範囲を記述します。

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

この例のメンバー値は、 [PCM マルチチャネルストリームのデータ範囲](pcm-multichannel-stream-data-range.md)の例と似ていますが、`MaximumBitsPerSample` 値は16を超えています。 この値は、サポートされている有効な bits の最大数に設定されます。 たとえば、デバイスが24ビットのコンテナーで20ビットの有効なオーディオデータをサポートしている場合、`MaximumBitsPerSample` の値を20に設定する必要があります。

 

 




