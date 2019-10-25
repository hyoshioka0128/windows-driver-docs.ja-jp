---
title: PCM 高ビットデプス ストリームのデータの形式
description: PCM 高ビットデプス ストリームのデータの形式
ms.assetid: 0ad63f01-4fcf-4eca-b8d6-b0b65f384455
keywords:
- PCM 高ビット深度ストリームデータ形式 WDK
- 高ビット深度ストリームデータ形式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42edce9421649c3103b32d1c7625b49deec9ecd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832549"
---
# <a name="pcm-high-bitdepth-stream-data-format"></a>PCM 高ビットデプス ストリームのデータの形式


## <span id="pcm_high_bitdepth_stream_data_format"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_FORMAT"></span>


この例では、 [**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体の拡張バージョンを使用して、PCM ハイビット深度ストリームのデータ形式を記述します。 これは、次に示す `Format.wBitsPerSample` と `Format.wValidBitsPerSample` の値を除き、PCM マルチチャネルの例と似ています。

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

 

 




