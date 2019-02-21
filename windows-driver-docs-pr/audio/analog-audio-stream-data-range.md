---
title: アナログ オーディオ Stream データ範囲
description: アナログ オーディオ Stream データ範囲
ms.assetid: e4503ace-1e96-401e-b410-18ee6b07a37b
keywords:
- アナログのオーディオ WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c15f3ceab899ca3c3d4c965df5aa85a08da507c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532208"
---
# <a name="analog-audio-stream-data-range"></a>アナログ オーディオ Stream データ範囲


## <span id="analog_audio_stream_data_range"></span><span id="ANALOG_AUDIO_STREAM_DATA_RANGE"></span>


この例では、 [ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)アナログのオーディオ ストリームのデータ範囲を記述する構造体。

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

 

 




