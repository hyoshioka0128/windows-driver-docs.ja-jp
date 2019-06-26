---
title: オーディオ データ形式とデータ範囲
description: オーディオ データ形式とデータ範囲
ms.assetid: 85aa74b4-8e33-49f4-82e7-561baa55c265
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7077af609883bb89035c4edd001f1538fbd3a065
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355745"
---
# <a name="audio-data-formats-and-data-ranges"></a>オーディオ データ形式とデータ範囲


## <span id="audio_data_formats_and_data_ranges"></span><span id="AUDIO_DATA_FORMATS_AND_DATA_RANGES"></span>


オーディオ ドライバーを使用して、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)と[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))ストリーム形式のオーディオを指定する構造体。

-   KS データ ストリームのデジタル形式は、KSDATAFORMAT 構造で始まる KS 形式記述子によって指定されます。

-   KS 暗証番号 (pin) をサポートするストリーム形式の範囲が KS データ範囲の配列で指定されました。配列の各要素は、KSDATARANGE 構造で始まる範囲記述子です。

これら 2 つの構造の詳細については、次を参照してください。 [KS データ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)します。 KS データ範囲の詳細については、次を参照してください。 [AVStream のデータ範囲の交差部分](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)します。

このセクションの残りの部分では、次のトピックについて説明します。

[オーディオ データの形式](audio-data-formats.md)

[オーディオ データの範囲](audio-data-ranges.md)

[Wave 形式の拡張可能な記述子](extensible-wave-format-descriptors.md)

[ホーム シアター システム用のマルチ チャネルの形式](multichannel-formats-for-home-theater-systems.md)

[オーディオ データ形式とデータの範囲の例](examples-of-audio-data-formats-and-data-ranges.md)

 

 




