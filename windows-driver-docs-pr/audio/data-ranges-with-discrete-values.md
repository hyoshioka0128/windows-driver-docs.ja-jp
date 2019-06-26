---
title: 離散値を含むデータ範囲
description: 離散値を含むデータ範囲
ms.assetid: 330edd60-0469-4351-bfb1-29b29e133c1a
keywords:
- 交差部分のデータ ハンドラー WDK オーディオ、不連続値のデータの範囲
- WDK のオーディオの範囲は不連続値のデータ
- WDK のオーディオ、不連続値の範囲のデータ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2c207abc3f09aeeef005d546c46f96557bfc18b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359085"
---
# <a name="data-ranges-with-discrete-values"></a>離散値を含むデータ範囲


## <span id="data_ranges_with_discrete_values"></span><span id="DATA_RANGES_WITH_DISCRETE_VALUES"></span>


オーディオ デバイスは、たとえば 11、22、44 kHz の場合は、サンプル周波数をサポートする場合は、11 から 44 kHz の 1 つの範囲として 3 つすべての出現頻度を指定できます[ **KSDATARANGE\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)構造体. この手法では、簡潔というメリットがあります。 潜在的な欠点は、バグのあるデータの積集合のハンドラーが、範囲内にある無効なパラメーター値 (たとえば、27 kHz) を選択可能性があります。 この場合、アダプターのドライバーに失敗するが、オプションはありません、 **NewStream**を呼び出す (たとえばを参照してください[ **IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)) を使用して pin を作成しようとしている、形式が無効です。

別の方法では、各パラメーターの値の範囲ではなく、各データ範囲が不連続の値を指定するデータ範囲の一覧を指定します。 たとえば、44 kHz 11 からサンプル周波数の範囲を指定する 1 つのデータ範囲を指定するには、代わりに、データ範囲の配列は 11、22、および 44 kHz の 3 つの個別の要素を含めることができます。 これらの要素ごとに、最大と最小サンプル周波数が同じ値に設定されます (11、22、または 44 kHz)。 このアプローチの利点は、サポートされている正確な値のあいまいさがなくなることです。 またを 1 つの不連続値が優先場合は、この値を含むデータ範囲は他の値を含むデータ範囲は、配列内の位置に移動できます。 不連続値のマイナーの欠点は、これらのデータ範囲の配列のサイズを向上させることです。

 

 




