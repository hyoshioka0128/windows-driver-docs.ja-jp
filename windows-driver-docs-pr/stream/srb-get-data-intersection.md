---
title: SRB\_\_データ\_共通部分を取得する
description: SRB\_\_データ\_共通部分を取得する
ms.assetid: 67100c7f-dbca-4f75-b884-52e25a666190
keywords:
- SRB_GET_DATA_INTERSECTION ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- SRB_GET_DATA_INTERSECTION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d65552fd031ce679f793cd090d43d2c4dd2f744f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843307"
---
# <a name="srb_get_data_intersection"></a>SRB\_\_データ\_共通部分を取得する


## <span id="ddk_srb_get_data_intersection_ks"></span><span id="DDK_SRB_GET_DATA_INTERSECTION_KS"></span>


クラスドライバーは、この要求を送信して、データ範囲内の最も一致するデータ形式のミニドライバーを照会します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状態\_成功  
一致が見つかったことを示します。

### <a name="comments"></a>コメント

*pSrb*-**commanddata**&gt;ます。**IntersectInfo**は、一致を検索するデータ範囲と形式を返すバッファーの両方を指定します。 *PSrb*ポインターは、 [ **\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)構造体を指す HW\_ストリームを指します。 ( **IntersectInfo**メンバーは、\_INFO 構造体と[**交差するデータ\_\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/ns-strmini-_stream_data_intersect_info)へのポインター型です)。

クラスドライバーは、この要求を使用して、 [ **\_DATAINTERSECTION**](ksproperty-pin-dataintersection.md)プロパティ要求を\_に ksk プロパティを満たします。 クラスドライバーは、ミニドライバーが*pSrb*&gt;-を持つ要求を返すまで、一度に1つの[**ksk**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))の再指定をミニドライバーにフィードし、status\_SUCCESS という状態**の値を**返します。 ミニドライバーは、指定子の値に一致するかどうかを確認します。

一般に、結果のデータ形式は、その形式でストリームを開くためにすぐに使用されます。 データ形式とデータ範囲の詳細については、「 [AVStream のデータ範囲の交差](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)部分」を参照してください。

 

 





