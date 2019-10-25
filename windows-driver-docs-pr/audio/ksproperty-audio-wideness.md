---
title: KSK プロパティ\_AUDIO\_WIDENESS
description: KSK プロパティ\_AUDIO\_WIDENESS プロパティは、ステレオ画像の WIDENESS (見かけ上の幅) を指定します。
ms.assetid: 56b18337-c29b-437f-b52f-8d804d857729
keywords:
- KSPROPERTY_AUDIO_WIDENESS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WIDENESS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b478ab06e023429c69996408f6d60f9afdd0467
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832898"
---
# <a name="ksproperty_audio_wideness"></a>KSK プロパティ\_AUDIO\_WIDENESS


KSK プロパティ\_AUDIO\_WIDENESS プロパティは、ステレオ画像の WIDENESS (見かけ上の幅) を指定します。

## <span id="ddk_ksproperty_audio_wideness_ks"></span><span id="DDK_KSPROPERTY_AUDIO_WIDENESS_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) の型は ULONG で、wideness を指定します。 Wideness は、16ビット分の符号なし固定小数点値として表現されます。 Wideness 値は、0から0xFFFFFFFF までの線形範囲に従います。

-   値0x00010000 は unity (100%) を表します。これは、ステレオイメージの幅が、左右のスピーカーによってフレームされた領域と一致する必要があることを示します。

-   Unity よりも大きい値の場合、ステレオ画像は、左右のスピーカーで囲まれた領域の外側に拡大表示されます。

-   Unity より小さい値の場合、ステレオイメージの認識される幅は、左右のスピーカー間のスペースよりも小さくする必要があります。

-   値が0の場合は、サウンドが左と右のスピーカーの中間の位置からのものであることを示します。

ステレオイメージの見かけ上の幅は、wideness 値の直線的な増加に比例して増加します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_WIDENESS property 要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

これは、wideness ノード ([**KSNODETYPE\_ステレオ\_ワイド**](ksnodetype-stereo-wide.md)) のプロパティです。 Wideness ノードでは、既存のステレオ (2 チャネル) ストリームに spaciousness を追加できます。 この効果を実現するために、ノードはストリームを処理して、左右のスピーカーで囲まれた領域の外側の位置から音が出てくるように見えます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE\_ステレオ\_ワイド**](ksnodetype-stereo-wide.md)

 

 






