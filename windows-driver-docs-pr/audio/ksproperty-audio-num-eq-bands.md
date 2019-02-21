---
title: KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド
description: KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド プロパティを使用して、イコライゼーション テーブル内の周波数のバンドの数を取得します。 これは EQ ノード内のチャネルの取得専用プロパティ (KSNODETYPE\_イコライザー)。
ms.assetid: b7bb9f05-0b27-4b41-aa38-efb87fc1beee
keywords:
- KSPROPERTY_AUDIO_NUM_EQ_BANDS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_NUM_EQ_BANDS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f67ba732e22f69e63155a406330ea03e5149a3b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537747"
---
# <a name="kspropertyaudionumeqbands"></a>KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド


KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド プロパティを使用して、イコライゼーション テーブル内の周波数のバンドの数を取得します。 これは EQ ノード内のチャネルの取得専用プロパティ ([**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md))。

## <span id="ddk_ksproperty_audio_num_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_NUM_EQ_BANDS_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型のノードのイコライゼーション テーブルで頻度のバンドの数を指定します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

組み合わせてこのプロパティが使用される、 [ **KSPROPERTY\_オーディオ\_EQ\_バンド**](ksproperty-audio-eq-bands.md)と[ **KSPROPERTY\_オーディオ\_EQ\_レベル**](ksproperty-audio-eq-level.md)プロパティをこれらのプロパティの値を格納する配列の長さを確認します。

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


[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

 

 






