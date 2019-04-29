---
title: MIDI ストリームのデータ形式
description: MIDI ストリームのデータ形式
ms.assetid: c179cf74-7493-4c27-97bd-5eb4d0dffbe6
keywords:
- MIDI ストリームのデータ形式の WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1edb84cf06c56e713dc9f41d3297e68a25efa447
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332346"
---
# <a name="midi-stream-data-format"></a>MIDI ストリームのデータ形式


## <span id="midi_stream_data_format"></span><span id="MIDI_STREAM_DATA_FORMAT"></span>


この例では、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656) MIDI ストリームのデータ形式を記述する構造体。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT);
  DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
 DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_MIDI);
  DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

 

 




