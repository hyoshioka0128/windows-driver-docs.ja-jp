---
title: オーディオ データ形式とデータの範囲
description: オーディオ データ形式とデータの範囲
ms.assetid: 85aa74b4-8e33-49f4-82e7-561baa55c265
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 413b512db5aa7b82e3acee7d71c5198bdfc6ef0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550093"
---
# <a name="audio-data-formats-and-data-ranges"></a>オーディオ データ形式とデータの範囲


## <span id="audio_data_formats_and_data_ranges"></span><span id="AUDIO_DATA_FORMATS_AND_DATA_RANGES"></span>


オーディオ ドライバーを使用して、 [ **KSDATAFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff561656)と[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)ストリーム形式のオーディオを指定する構造体。

-   KS データ ストリームのデジタル形式は、KSDATAFORMAT 構造で始まる KS 形式記述子によって指定されます。

-   KS 暗証番号 (pin) をサポートするストリーム形式の範囲が KS データ範囲の配列で指定されました。配列の各要素は、KSDATARANGE 構造で始まる範囲記述子です。

これら 2 つの構造の詳細については、次を参照してください。 [KS データ形式とデータ範囲](https://msdn.microsoft.com/library/windows/hardware/ff567632)します。 KS データ範囲の詳細については、次を参照してください。 [AVStream のデータ範囲の交差部分](https://msdn.microsoft.com/library/windows/hardware/ff558680)します。

このセクションの残りの部分では、次のトピックについて説明します。

[オーディオ データの形式](audio-data-formats.md)

[オーディオ データの範囲](audio-data-ranges.md)

[Wave 形式の拡張可能な記述子](extensible-wave-format-descriptors.md)

[ホーム シアター システム用のマルチ チャネルの形式](multichannel-formats-for-home-theater-systems.md)

[オーディオ データ形式とデータの範囲の例](examples-of-audio-data-formats-and-data-ranges.md)

 

 




