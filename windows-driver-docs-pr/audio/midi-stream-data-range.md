---
title: MIDI ストリームのデータ範囲
description: MIDI ストリームのデータ範囲
ms.assetid: 392eadf7-9c6e-4527-bc84-a2916623c154
keywords:
- MIDI ストリームデータ範囲 WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aee90488778740f6354679527315bd223081ec0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832581"
---
# <a name="midi-stream-data-range"></a>MIDI ストリームのデータ範囲


## <span id="midi_stream_data_range"></span><span id="MIDI_STREAM_DATA_RANGE"></span>


この例では、 [**ksk の\_ミュージック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)構造体を使用して、MIDI ストリームのデータ範囲を記述します。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_MUSIC);
 DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
 DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_MIDI);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
  Technology            = STATICGUIDOF(KSMUSIC_TECHNOLOGY_PORT);
  Channels              = 0;
  Notes                 = 0;
  ChannelMask           = 0xFFFF;
```

 

 




