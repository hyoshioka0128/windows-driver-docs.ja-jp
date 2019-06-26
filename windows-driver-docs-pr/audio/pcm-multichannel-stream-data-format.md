---
title: PCM マルチチャンネル ストリームのデータ形式
description: PCM マルチチャンネル ストリームのデータ形式
ms.assetid: cab528a7-5db4-4e37-89c4-35dfc472f0ae
keywords:
- WDK の PCM マルチ チャネル ストリームのデータ形式します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c23db0237d10294e5c91577c98675fd11d5c9847
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355323"
---
# <a name="pcm-multichannel-stream-data-format"></a>PCM マルチチャンネル ストリームのデータ形式


## <span id="pcm_multichannel_stream_data_format"></span><span id="PCM_MULTICHANNEL_STREAM_DATA_FORMAT"></span>


この例の拡張バージョンを使用して、 [ **KSDATAFORMAT\_WAVEFORMATEX** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdataformat_waveformatex) PCM マルチ チャネル ストリームのデータ形式を記述する構造体。

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

 

 




