---
title: KSPROPERTY\_オーディオ\_EQ\_レベル
description: KSPROPERTY\_オーディオ\_EQ\_レベル プロパティは、n の頻度のバンドのエントリを含むイコライゼーション テーブル イコライゼーション レベルを指定します。 これは EQ ノード内のチャネルのプロパティ (KSNODETYPE\_イコライザー)。
ms.assetid: 17c34af2-dbeb-472c-9825-9dc64f7f96bd
keywords:
- KSPROPERTY_AUDIO_EQ_LEVEL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_EQ_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5eab82a27885f5f1358b96ebade163399bff7b0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333047"
---
# <a name="kspropertyaudioeqlevel"></a>KSPROPERTY\_オーディオ\_EQ\_レベル


KSPROPERTY\_オーディオ\_EQ\_レベル プロパティのエントリを含むイコライゼーション テーブル イコライゼーション レベルを指定する*n*周波数バンド。 これは EQ ノード内のチャネルのプロパティ ([**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md))。

## <span id="ddk_ksproperty_audio_eq_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_LEVEL_KS"></span>


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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>Long 型の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) には、長い要素の配列です。

```cpp
  LONG  Level[N];
```

チャネルのイコライゼーション テーブルに N 周波数のバンドのエントリが含まれている場合は、配列には、n 個の要素が含まれています。 し、各要素がイコライゼーションの表にバンドのいずれかのレベルを指定します。 バンドの配列要素への割り当ては、次の表に示します。

レベルを説明する要素を配列\[0\]

バンド 0 のレベル。

レベル\[1\]

バンド 1 のレベル。

...

レベル\[N-1\]

バンド N-1 のレベル。

 

レベルの値は、次のスケールを使用します。

無限大デシベル (減衰) は-2147483648

-2147483647 は-32767.99998474 デシベル (減衰) と

+ 2147483647 までは、+32767.99998474 デシベル (向上です)。

整数値、比較的によって表されるデシベル範囲場所

このスケールでは、1/65536 デシベル精度があります。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_EQ\_レベル プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

フィルターは、KSPROPERTY を成功\_オーディオ\_EQ\_レベルのプロパティの設定要求フィルターの範囲を超えてはサポートされている範囲に値が固定される値を指定します。 ただし、このプロパティを取得する後続の要求には、使用される実際の値を出力にされます。

最初の送信でイコライゼーション バンドの数を決定できます、 [ **KSPROPERTY\_オーディオ\_NUM\_EQ\_バンド**](ksproperty-audio-num-eq-bands.md)要求。

イコライゼーションのバンドの中心周波数がで指定された、 [ **KSPROPERTY\_オーディオ\_EQ\_バンド**](ksproperty-audio-eq-bands.md)プロパティ。

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

[**KSPROPERTY\_AUDIO\_NUM\_EQ\_BANDS**](ksproperty-audio-num-eq-bands.md)

[**KSPROPERTY\_AUDIO\_EQ\_BANDS**](ksproperty-audio-eq-bands.md)

 

 






