---
title: PCM 高深さ Stream データの形式
description: PCM 高深さ Stream データの形式
ms.assetid: 0ad63f01-4fcf-4eca-b8d6-b0b65f384455
keywords:
- PCM 高深さストリーム データは、WDK を形式します。
- WDK の高深さストリームのデータ形式します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4bcaf4ab83d2e0d5c945240d5de894713fbc7c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560453"
---
# <a name="pcm-high-bitdepth-stream-data-format"></a>PCM 高深さ Stream データの形式


## <span id="pcm_high_bitdepth_stream_data_format"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_FORMAT"></span>


この例の拡張バージョンを使用して、 [ **KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095) PCM 高深さストリームのデータ形式を記述する構造体。 これは、値を除く、PCM のマルチ チャンネル例のような`Format.wBitsPerSample`と`Format.wValidBitsPerSample`を下に表示されます。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT) + sizeof(WAVEFORMATEXTENSIBLE);
 DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
  DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
 DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  Format.wFormatTag      = WAVE_FORMAT_EXTENSIBLE;
  Format.nChannels       = 4;
  Format.nSamplesPerSec  = 44100;
  Format.nAvgBytesPerSec = 529200;
  Format.nBlockAlign     = 8;
  Format.wBitsPerSample  = 24;
  Format.cbSize          = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
  Format.wValidBitsPerSample = 20;
  Format.dwChannelMask   = KSAUDIO_SPEAKER_SURROUND;
  Format.SubFormat       = KSDATAFORMAT_SUBTYPE_PCM;
```

 

 




