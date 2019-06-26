---
title: SRB\_取得\_データ\_積集合
description: SRB\_取得\_データ\_積集合
ms.assetid: 67100c7f-dbca-4f75-b884-52e25a666190
keywords:
- SRB_GET_DATA_INTERSECTION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- SRB_GET_DATA_INTERSECTION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c6d0e92d2298365c56b8d41f823d51e0447bede
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358393"
---
# <a name="srbgetdataintersection"></a>SRB\_取得\_データ\_積集合


## <span id="ddk_srb_get_data_intersection_ks"></span><span id="DDK_SRB_GET_DATA_INTERSECTION_KS"></span>


クラス ドライバーは、データの範囲内の最適な一致するデータ形式のミニドライバーを照会するには、この要求を送信します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

ミニドライバーは、SRB の状態として、次のいずれかを設定する必要があります。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>ステータス\_成功  
一致が見つかったことを示します。

### <a name="comments"></a>コメント

*pSrb*-&gt;**CommandData**.**IntersectInfo**と一致して、バッファーが返されますの形式を検索するデータ範囲を指定します。 *PSrb*ポインターが指す、 [ **HW\_ストリーム\_要求\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_hw_stream_request_block)構造体。 (、 **IntersectInfo**へのポインター型のメンバーを[**ストリーム\_データ\_INTERSECT\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/ns-strmini-_stream_data_intersect_info)構造です)。

クラスのドライバーを満たすためにこの要求を使用して[ **KSPROPERTY\_PIN\_DATAINTERSECTION** ](ksproperty-pin-dataintersection.md)プロパティ要求。 フィードのいずれかのクラス ドライバー [ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))ようにミニドライバーに要求が戻るまでミニドライバーに一度に、 *pSrb* - &gt;**状態**STATUS の値\_成功します。 ミニドライバーは、DataRange.Specifier 値内の一致を確認します。

一般に、その形式でストリームを開く、結果として得られるデータ形式をすぐに使用します。 データ形式とデータの範囲の詳細については、次を参照してください。 [AVStream のデータ範囲の交差部分](https://docs.microsoft.com/windows-hardware/drivers/stream/data-range-intersections-in-avstream)します。

 

 





