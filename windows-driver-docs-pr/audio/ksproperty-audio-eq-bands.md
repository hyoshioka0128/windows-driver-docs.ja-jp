---
title: KSPROPERTY\_オーディオ\_EQ\_バンド
description: KSPROPERTY\_オーディオ\_EQ\_バンド プロパティ イコライゼーション テーブルからの周波数のバンドのセットを指定します。 これは EQ ノード内のチャネルの取得専用プロパティ (KSNODETYPE\_イコライザー)。
ms.assetid: 64304cad-cf07-4bdb-96d5-7dd594380725
keywords:
- KSPROPERTY_AUDIO_EQ_BANDS オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_EQ_BANDS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88aa0389e8f92d3aadfc2edf91488c81b29df84c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360622"
---
# <a name="kspropertyaudioeqbands"></a>KSPROPERTY\_オーディオ\_EQ\_バンド


KSPROPERTY\_オーディオ\_EQ\_バンド プロパティ イコライゼーション テーブルからの周波数のバンドのセットを指定します。 これは EQ ノード内のチャネルの取得専用プロパティ ([**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md))。

## <span id="ddk_ksproperty_audio_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_BANDS_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>ULONG 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) には、ULONG 要素の配列です。

```cpp
  ULONG  CenterFreqVal[N];
```

チャネルのイコライゼーション テーブルに N 周波数のバンドのエントリが含まれている場合は、配列には、n 個の要素が含まれています。 を配列の各要素が、対応するバンドの中心周波数を指定します。 ミニポート ドライバーは、各要素にヘルツ (Hz) で表される整数の頻度の値を書き込みます。 イコライゼーション バンドの配列要素への割り当ては、次の表に示します。

配列の要素の説明 CenterFreqVal\[0\]

イコライゼーション バンド 0 の中心周波数 (Hz) で。

CenterFreqVal\[1\]

イコライゼーション バンド 1 の (Hz) の中心周波数。

...

CenterFreqVal\[N-1\]

イコライゼーション バンド N-1 の中心周波数 (Hz) で。

 

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_EQ\_バンド プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

最初の送信でイコライゼーション バンドの数を決定できます、 [ **KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド**](ksproperty-audio-num-eq-bands.md)要求。

頻度のバンドのイコライゼーション レベルがで指定された、 [ **KSPROPERTY\_オーディオ\_EQ\_レベル**](ksproperty-audio-eq-level.md)プロパティ。

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


[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md)

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)

 

 






