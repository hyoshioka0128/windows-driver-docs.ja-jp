---
title: KSPROPERTY\_オーディオ\_ワイドかどうか
description: KSPROPERTY\_オーディオ\_ワイドかどうかのプロパティは、ステレオのイメージのワイドかどうか (明らかな幅) を指定します。
ms.assetid: 56b18337-c29b-437f-b52f-8d804d857729
keywords:
- KSPROPERTY_AUDIO_WIDENESS オーディオ デバイス
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
ms.openlocfilehash: 500c4b3f263b567fd8886973f2425b310bd7eb40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332902"
---
# <a name="kspropertyaudiowideness"></a>KSPROPERTY\_オーディオ\_ワイドかどうか


KSPROPERTY\_オーディオ\_ワイドかどうかのプロパティは、ステレオのイメージのワイドかどうか (明らかな幅) を指定します。

## <span id="ddk_ksproperty_audio_wideness_ks"></span><span id="DDK_KSPROPERTY_AUDIO_WIDENESS_KS"></span>


### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>〇</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、ワイドかどうかを指定します。 ワイドかどうかは、16 ビットの分数で署名されていない固定小数点の値として表されます。 ワイドかどうかの値では、0 から 0 xffffffff に線形範囲に従います。

-   0x00010000 の値は、ステレオの画像の幅が、左右のスピーカーで囲まれているリージョンと一致する必要があることを示します unity (100%) を表します。

-   値が unity よりも大きい場合、左右のスピーカーで囲まれている領域の外側を拡張するステレオの画像が表示されます。

-   Unity よりも小さいか、値は、ステレオの画像の見かけ上の幅が左右のスピーカーの領域よりも小さい必要があります。

-   値 0 は、左右のスピーカー位置の途中からサウンドが表示されることを示します。

ワイドかどうかの値の線形増加とステレオの画像の明らかな幅が直線的に増やす必要があります。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_ワイドかどうかのプロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

これは、ワイドかどうかのノードのプロパティ ([**KSNODETYPE\_ステレオ\_ワイド**](ksnodetype-stereo-wide.md))。 ワイドかどうかのノードでは、既存のステレオ (2 つのチャネル) ストリームに広がりを追加できます。 この効果を実現するためには、ノードは、左右のスピーカーで囲まれている領域の外側の位置から出ているようにいくつかの音を鳴らすにストリームを処理します。

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
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSNODETYPE\_ステレオ\_ワイド**](ksnodetype-stereo-wide.md)

 

 






