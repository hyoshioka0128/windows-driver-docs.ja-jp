---
title: 離散値を含むデータ範囲
description: 離散値を含むデータ範囲
ms.assetid: 330edd60-0469-4351-bfb1-29b29e133c1a
keywords:
- データの交差ハンドラー WDK オーディオ、不連続値のデータ範囲
- 離散値データ範囲 WDK オーディオ
- データ範囲 WDK オーディオ、不連続値
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cc9d96992c82e03460c397da612ea00ae8e1bfe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833574"
---
# <a name="data-ranges-with-discrete-values"></a>離散値を含むデータ範囲


## <span id="data_ranges_with_discrete_values"></span><span id="DATA_RANGES_WITH_DISCRETE_VALUES"></span>


たとえば、オーディオデバイスでサンプル周波数の11、22、および 44 kHz がサポートされている場合、1つの[**Ksk datar\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)構造で、3つのすべての周波数を 11 ~ 44 kHz の範囲として指定できます。 この手法には、簡潔であるという利点があります。 欠点としては、バグのあるデータの交差ハンドラーが範囲内にある無効なパラメーター値 (27 kHz など) を選択することがあります。 この場合、アダプタードライバーにはオプションがありませんが、無効な形式の pin を作成しようとする**newstream**呼び出し (例[ **: IMiniportWavePci:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)) に失敗します。

もう1つの方法は、各データ範囲に、各パラメーターの値の範囲ではなく不連続値を指定するデータ範囲の一覧を提供することです。 たとえば、1つのデータ範囲でサンプル周波数の範囲を 11 ~ 44 kHz に指定するのではなく、データ範囲配列に11、22、44 kHz の3つの独立した要素を含めることができます。 これらの各要素で、最大と最小のサンプル周波数は同じ値 (11、22、または 44 kHz) に設定されます。 この方法の利点は、サポートされている正確な値についてあいまいさが解消されることです。 また、1つの不連続値が別の不連続値よりも優先される場合、この値を含むデータ範囲は、他の値を含むデータ範囲の前の配列内の位置に移動できます。 不連続値の小さな欠点は、データ範囲配列のサイズを増やすことができることです。

 

 




