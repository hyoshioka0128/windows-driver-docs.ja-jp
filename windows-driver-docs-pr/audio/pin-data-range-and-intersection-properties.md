---
title: ピンのデータ範囲と交差のプロパティ
description: ピンのデータ範囲と交差のプロパティ
ms.assetid: 55a749b2-1f54-42f8-876c-f391112d7bab
keywords:
- WDK、ピンのオーディオのプロパティ
- WDM オーディオ プロパティ WDK、ピン
- ピン WDK オーディオでは、データを形式します。
- データ範囲の形式の WDK オーディオ
- WDK のオーディオ、ピンを書式設定します。
- 交差部分を WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5914c94adc546c08ddd5fd82b67a2e7ab027b30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355306"
---
# <a name="pin-data-range-and-intersection-properties"></a>ピンのデータ範囲と交差のプロパティ


## <span id="pin_data_range_and_intersection_properties"></span><span id="PIN_DATA_RANGE_AND_INTERSECTION_PROPERTIES"></span>


プロパティに複数の要求では、オーディオ デバイスがその入力と出力ピンで処理できるオーディオ ストリームのデータ形式に関する情報を提供します。

Pin がサポートできるオーディオ ストリームのデータ形式がで表現される、 [ **KSMULTIPLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksmultiple_item)の配列[ **KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))-構造体を派生します。 暗証番号 (pin) のデータ範囲のサポートは、次の 3 つを介して公開される[KSPROPSETID\_Pin](https://docs.microsoft.com/windows-hardware/drivers/stream/kspropsetid-pin)フィルター プロパティ。

[**KSPROPERTY\_PIN\_DATARANGES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataranges)このプロパティは、静的なサポートされているすべての可能な形式を表すデータ範囲を報告します。 通常、データの範囲は、アダプターのドライバーで静的配列内に格納されます。
[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-constraineddataranges)このプロパティは動的であり、プロパティの要求時にサポートされる形式のサブセットを表すデータの範囲を報告します。 プロパティ ハンドラーは、どの形式、暗証番号 (pin) が実行時にサポートできるかを判断するためのロジックを含める必要があります。 たとえば、ハードウェアの実装では、特定の形式の組み合わせでは、全二重のサポートを許可しない DMA 制約可能性があります。
[**KSPROPERTY\_PIN\_DATAINTERSECTION** ](https://docs.microsoft.com/windows-hardware/drivers/stream/ksproperty-pin-dataintersection)このプロパティは、データ範囲の一覧からデータ形式を選択します。 選択範囲は動的な機能に基づいており、形式は、ドライバーは、プロパティの要求時にサポートできる形式のサブセットから取得されます。 このプロパティを使用して、呼び出し元は、データ範囲の配列を提供します。 現在サポート可能であるデータの範囲が見つかるまで、配列の検索をプロパティ ハンドラー以降の最初の要素では、します。 かどうか成功すると、ハンドラーは出力データ形式は、そのデータの範囲から取得し、ステータスを返しますを\_成功します。 ハンドラーが状態を返しますそれ以外の場合、\_いいえ\_一致します。
オーディオ システム コンポーネントの使用、KSPROPERTY\_暗証番号 (pin)\_DATARANGES と KSPROPERTY\_PIN\_DATAINTERSECTION プロパティ。 ミニポート ドライバーでは、これらのプロパティをサポートする必要があります。 KSPROPERTY サポート\_PIN\_CONSTRAINEDDATARANGES は省略可能です。

詳細については、次を参照してください。[オーディオ データ形式とデータ範囲](audio-data-formats-and-data-ranges.md)します。

**注**   、KSPROPERTY\_PIN\_DATARANGES と KSPROPERTY\_暗証番号 (pin)\_各 CONSTRAINEDDATARANGES が 8 バイト固定アドレスで開始します。

 

 

 




