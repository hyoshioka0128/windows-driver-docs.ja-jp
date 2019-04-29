---
title: KSPROPERTY\_オーディオ\_サラウンド\_エンコード
description: KSPROPERTY\_オーディオ\_囲む\_エンコード プロパティは、フィルターのブロックの挿入のエンコーダーが有効になっているかどうかを指定します。 ブロックの挿入エンコーダー ノード (KSNODETYPE\_PROLOGIC\_エンコーダー) ドルビー サラウンド Pro ロジックのエンコードを実行します。
ms.assetid: 249ee13f-a986-4cb1-906f-55062274df45
keywords:
- KSPROPERTY_AUDIO_SURROUND_ENCODE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_SURROUND_ENCODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d245231dba1c26eb58b808f332229154b63db621
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332914"
---
# <a name="kspropertyaudiosurroundencode"></a>KSPROPERTY\_オーディオ\_サラウンド\_エンコード


KSPROPERTY\_オーディオ\_囲む\_エンコード プロパティは、フィルターのブロックの挿入のエンコーダーが有効になっているかどうかを指定します。 ブロックの挿入エンコーダー ノード ([**KSNODETYPE\_PROLOGIC\_エンコーダー**](ksnodetype-prologic-encoder.md)) ドルビー サラウンド Pro ロジックのエンコードを実行します。

## <span id="ddk_ksproperty_audio_surround_encode_ks"></span><span id="DDK_KSPROPERTY_AUDIO_SURROUND_ENCODE_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は BOOL 型のブロックの挿入エンコーダー ノードが有効か無効かどうかを示します。 値**TRUE**サラウンド エンコーダー ノードが有効になっていることを示します。 **FALSE**は無効になっていることを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_サラウンド\_エンコード プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

Microsoft Windows XP 以降では、 [KMixer システム ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537039#kmixer-system-driver)サポート、KSPROPERTY\_オーディオ\_サラウンド\_エンコード プロパティ。

有効な場合、ブロックの挿入エンコーダー ノードはサラウンドでエンコードされたステレオ出力ストリームに (左、右、センター、およびバック スピーカーのチャネル) を持つ 4 チャネル入力ストリームをエンコードします。 この出力ストリームでデコードできます、 [ **KSNODETYPE\_PROLOGIC\_デコーダー** ](ksnodetype-prologic-decoder.md)例については、ノード。 これは、オーディオ デバイスのアナログ ステレオ出力を直接左、右、センターを駆動する外部サラウンド デコーダーに接続することができますし、スピーカーのバックアップを再生できます。

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

[**KSNODETYPE\_PROLOGIC\_エンコーダー**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE\_PROLOGIC\_デコーダー**](ksnodetype-prologic-decoder.md)

 

 






