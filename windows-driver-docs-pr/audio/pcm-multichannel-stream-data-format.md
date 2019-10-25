---
title: PCM マルチチャンネル ストリームのデータ形式
description: PCM マルチチャンネル ストリームのデータ形式
ms.assetid: cab528a7-5db4-4e37-89c4-35dfc472f0ae
keywords:
- PCM マルチチャネルストリームデータ形式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ddf9d080fec872157e4c947a3ecd6d8c241eeef
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832546"
---
# <a name="pcm-multichannel-stream-data-format"></a>PCM マルチチャンネル ストリームのデータ形式


## <span id="pcm_multichannel_stream_data_format"></span><span id="PCM_MULTICHANNEL_STREAM_DATA_FORMAT"></span>


この例では、 [**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体の拡張バージョンを使用して、PCM マルチチャネルストリームのデータ形式を記述します。

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
  Format.nAvgBytesPerSec = 352800;
  Format.nBlockAlign     = 8;
  Format.wBitsPerSample  = 16;
  Format.cbSize          = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
  Format.wValidBitsPerSample = 16;
  Format.dwChannelMask   = KSAUDIO_SPEAKER_SURROUND;
  Format.SubFormat       = KSDATAFORMAT_SUBTYPE_PCM;
```

 

 




