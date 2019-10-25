---
title: ピンのデータ範囲と交差のプロパティ
description: ピンのデータ範囲と交差のプロパティ
ms.assetid: 55a749b2-1f54-42f8-876c-f391112d7bab
keywords:
- オーディオプロパティ WDK、pin
- WDM オーディオプロパティ WDK、pin
- WDK オーディオ、データ形式をピン留めする
- データ範囲形式 WDK オーディオ
- WDK オーディオ、pin をフォーマットします
- WDK オーディオの共通部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 491cc55f5b49a878765ffc80f120826d2ae8030a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832501"
---
# <a name="pin-data-range-and-intersection-properties"></a>ピンのデータ範囲と交差のプロパティ


## <span id="pin_data_range_and_intersection_properties"></span><span id="PIN_DATA_RANGE_AND_INTERSECTION_PROPERTIES"></span>


いくつかのプロパティ要求では、入力ピンと出力ピンでオーディオデバイスが処理できるオーディオストリームのデータ形式に関する情報が提供されます。

Pin がサポートできるオーディオストリームのデータ形式は、ksk の[**複数\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)の配列である[**ksk**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))によって表されます。 ピンデータ範囲のサポートは、次の3つの[Ksk Propsetid\_](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)によって公開され、フィルターのプロパティをピン留めします。

[**Ksk プロパティ\_PIN\_DATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)このプロパティは、静的なデータ範囲を報告し、サポートされるすべての形式を表します。 通常、データ範囲は、アダプタードライバーの静的配列に格納されます。
[**Ksk プロパティ\_PIN\_CONSTRAINEDDATARANGES**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)このプロパティは、動的なデータ範囲を報告し、プロパティ要求時にサポートされる形式のサブセットを表します。 プロパティハンドラーには、pin が実行時にサポートできる形式を決定するためのロジックが含まれている必要があります。 たとえば、ハードウェア実装には、特定の形式の組み合わせで全二重のサポートを許可しない DMA 制約がある場合があります。
[**Ksk プロパティ\_ピン\_DATAINTERSECTION 集合**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)このプロパティは、データ範囲の一覧からデータ形式を選択します。 選択は動的な機能に基づいており、形式は、プロパティ要求時にドライバーがサポートできる形式のサブセットから取得されます。 このプロパティを使用するために、呼び出し元はデータ範囲の配列を提供します。 最初の要素から、現在サポートできるデータ範囲が見つかるまで、プロパティハンドラーは配列を検索します。 成功した場合、ハンドラーはそのデータ範囲から取得されたデータ形式を出力し、STATUS\_SUCCESS を返します。 それ以外の場合、ハンドラーは状態\_返し\_一致しません。
オーディオシステムコンポーネントでは、KSK プロパティを使用して、DATARANGES および KSPROPERTY\_ピン留め\_DATAINTERSECTION プロパティ\_\_します。 ミニポートドライバーは、これらのプロパティをサポートする必要があります。 CONSTRAINEDDATARANGES を使用した KSK プロパティ\_PIN\_のサポートは省略可能です。

詳細については、「[オーディオデータ形式とデータ範囲](audio-data-formats-and-data-ranges.md)」を参照してください。

**   KSK**プロパティ\_ピン留め\_DATARANGES と ksk プロパティ\_\_ピン留めすると、8バイトでアラインされたアドレスで開始されます。

 

 

 




