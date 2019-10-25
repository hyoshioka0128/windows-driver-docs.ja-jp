---
title: DirectSound ストリームのデータ範囲
description: DirectSound ストリームのデータ範囲
ms.assetid: cc31eb2d-7421-4748-b14c-f4d3d15f9884
keywords:
- DirectSound WDK audio、stream データ範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e00d726afbe86cce035adcbd9ed946a1c444d955
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833474"
---
# <a name="directsound-stream-data-range"></a>DirectSound ストリームのデータ範囲


## <span id="directsound_stream_data_range"></span><span id="DIRECTSOUND_STREAM_DATA_RANGE"></span>


この例では、 [**Ksk datar\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造を使用して、DirectSound ストリームのデータ範囲を記述します。

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

この例のメンバー値は、 [PCM マルチチャネルストリームデータ範囲](pcm-multichannel-stream-data-range.md)の例と似ていますが、 **MaximumBitsPerSample**値は例外です。 この値は、サンプルのコンテナーサイズに設定されており、8の倍数である必要があります。 たとえば、デバイスが24ビットのコンテナーで20ビットの有効なオーディオデータをサポートしている場合、 **MaximumBitsPerSample**の値は24に設定する必要があります。

 

 




