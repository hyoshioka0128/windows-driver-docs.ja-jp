---
title: DirectSound Stream データ範囲
description: DirectSound Stream データ範囲
ms.assetid: cc31eb2d-7421-4748-b14c-f4d3d15f9884
keywords:
- DirectSound WDK、オーディオ ストリームのデータ範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12eebfffc9b53a3770eaeb47247fb9dda58ea38a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537858"
---
# <a name="directsound-stream-data-range"></a>DirectSound Stream データ範囲


## <span id="directsound_stream_data_range"></span><span id="DIRECTSOUND_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096) DirectSound ストリームのデータ範囲を記述する構造体。

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

 

 




