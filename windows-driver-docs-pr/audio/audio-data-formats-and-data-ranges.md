---
title: オーディオ データ形式とデータ範囲
description: オーディオ データ形式とデータ範囲
ms.assetid: 85aa74b4-8e33-49f4-82e7-561baa55c265
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c99c146709f1f55e544c0a444b6b5394b1e7735b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831921"
---
# <a name="audio-data-formats-and-data-ranges"></a>オーディオ データ形式とデータ範囲


## <span id="audio_data_formats_and_data_ranges"></span><span id="AUDIO_DATA_FORMATS_AND_DATA_RANGES"></span>


オーディオドライバーは、次のように、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)と[**ksk**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))の各構造体を使用して、オーディオストリーム形式を指定します。

-   KS データストリームのデジタル形式は、KSDATAFORMAT 構造体で始まる KS 形式記述子によって指定されます。

-   KS pin がサポートできるストリーム形式の範囲は、KS データ範囲の配列によって指定されます。各配列要素は、KSK の構造体で始まる範囲記述子です。

これらの2つの構造体の詳細については、「 [KS データ形式とデータ範囲](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-data-formats-and-data-ranges)」を参照してください。 KS データ範囲の詳細については、「 [AVStream のデータ範囲の交差](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)部分」を参照してください。

このセクションの残りの部分では、次のトピックについて説明します。

[オーディオデータ形式](audio-data-formats.md)

[オーディオデータの範囲](audio-data-ranges.md)

[拡張可能な Wave 形式の記述子](extensible-wave-format-descriptors.md)

[家庭シアターシステムのマルチチャンネル形式](multichannel-formats-for-home-theater-systems.md)

[オーディオデータ形式とデータ範囲の例](examples-of-audio-data-formats-and-data-ranges.md)

 

 




