---
title: アナログ オーディオ ストリームのデータ範囲
description: アナログ オーディオ ストリームのデータ範囲
ms.assetid: e4503ace-1e96-401e-b410-18ee6b07a37b
keywords:
- アナログのオーディオ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b27950896163fcaf6819536901ccd22213e0b9c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355769"
---
# <a name="analog-audio-stream-data-range"></a>アナログ オーディオ ストリームのデータ範囲


## <span id="analog_audio_stream_data_range"></span><span id="ANALOG_AUDIO_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))アナログのオーディオ ストリームのデータ範囲を記述する構造体。

```cpp
  DataRange.FormatSize  = sizeof(KSDATARANGE);
  DataRange.Flags       = 0;
  DataRange.SampleSize  = 0;
  DataRange.Reserved    = 0;
  DataRange.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataRange.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_ANALOG);
  DataRange.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_NONE);
```

通常、ミニポート ドライバーが通過アナログ信号を記述するこの種類のデータ範囲を使用、*ブリッジ pin*、オーディオのアダプター カードに有線接続を表します。 ブリッジの pin の詳細については、次を参照してください。[オーディオ フィルター グラフ](audio-filter-graphs.md)します。 またでのコード例を参照してください[フィルター トポロジを公開する](exposing-filter-topology.md)します。

 

 




