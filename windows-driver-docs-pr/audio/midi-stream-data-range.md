---
title: MIDI ストリームのデータ範囲
description: MIDI ストリームのデータ範囲
ms.assetid: 392eadf7-9c6e-4527-bc84-a2916623c154
keywords:
- MIDI ストリーム データの範囲の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46113bbf2f5771b1f49e2eb5df72a99d7abfa5cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578742"
---
# <a name="midi-stream-data-range"></a>MIDI ストリームのデータ範囲


## <span id="midi_stream_data_range"></span><span id="MIDI_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097) MIDI ストリームのデータ範囲を記述する構造体。

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

 

 




