---
title: DirectMusic ストリームのデータ範囲
description: DirectMusic ストリームのデータ範囲
ms.assetid: e3423901-330e-4a86-a921-6678e1c45a97
keywords:
- DirectMusic WDK、オーディオ ストリームのデータ範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad971162c43bced5fafb190b65dc5ed3ad5f0e53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333892"
---
# <a name="directmusic-stream-data-range"></a>DirectMusic ストリームのデータ範囲


## <span id="directmusic_stream_data_range"></span><span id="DIRECTMUSIC_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE\_音楽**](https://msdn.microsoft.com/library/windows/hardware/ff537097) DirectMusic ストリームのデータ範囲を記述する構造体。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE_MUSIC);
 DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
 DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_MUSIC);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DIRECTMUSIC);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
  Technology            = STATICGUIDOF(KSMUSIC_TECHNOLOGY_WAVETABLE);
  Channels              = 0;
  Notes                 = 0;
  ChannelMask           = 0xFFFF;
```

 

 




