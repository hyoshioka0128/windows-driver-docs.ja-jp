---
title: DirectMusic ストリームのデータ範囲
description: DirectMusic ストリームのデータ範囲
ms.assetid: e3423901-330e-4a86-a921-6678e1c45a97
keywords:
- DirectMusic WDK audio、stream データ範囲
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8138c0512d78d59aff47210b22fad2bee1bf8928
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833506"
---
# <a name="directmusic-stream-data-range"></a>DirectMusic ストリームのデータ範囲


## <span id="directmusic_stream_data_range"></span><span id="DIRECTMUSIC_STREAM_DATA_RANGE"></span>


この例では、 [ **\_ミュージック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_music)構造体を使用して、DirectMusic ストリームのデータ範囲を記述します。

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

 

 




