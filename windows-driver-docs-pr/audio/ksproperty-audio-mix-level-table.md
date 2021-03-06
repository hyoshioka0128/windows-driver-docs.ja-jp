---
title: KSPROPERTY\_オーディオ\_混在\_レベル\_テーブル
description: KSPROPERTY\_オーディオ\_混在\_レベル\_テーブル プロパティを supermixer ノードのミックス レベルを指定します (KSNODETYPE\_SUPERMIX)。 すべての入力と出力チャネルの情報を提供します。
ms.assetid: 1a1b486b-06e4-462b-8fe9-9d3581c82d06
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_TABLE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIX_LEVEL_TABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e05e4e922e08ee31a90b535a7f80923a7b18459
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358912"
---
# <a name="kspropertyaudiomixleveltable"></a>KSPROPERTY\_オーディオ\_混在\_レベル\_テーブル


KSPROPERTY\_オーディオ\_混在\_レベル\_テーブル プロパティを supermixer ノードのミックス レベルを指定します ([**KSNODETYPE\_SUPERMIX** ](ksnodetype-supermix.md)). すべての入力と出力チャネルの情報を提供します。

## <span id="ddk_ksproperty_audio_mix_level_table_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_TABLE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>配列<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXLEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel)"> <strong>KSAUDIO_MIXLEVEL</strong> </a>構造体</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) が KSAUDIO の配列\_ミキシング レベル構造体のすべての M ミックス レベルを指定する\*m supermixer ノード内の N 入力出力パスが出力チャネルのチャネルと N を入力します。 配列には、M が含まれています。\*n 個の要素。

```cpp
  KSAUDIO_MIXLEVEL  MixLevel[M*N];
```

次の表では、配列要素のマッピングを示します supermixer ノードの m\*N 入力出力パス。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">配列要素</th>
<th align="left">入力-出力パス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ミキシング レベル [0]</p></td>
<td align="left"><p>0 の出力チャネルにチャネル 0 を入力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミキシング レベル [1]</p></td>
<td align="left"><p>1 の出力チャネルにチャネル 0 を入力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミキシング レベル [N-1]</p></td>
<td align="left"><p>N-1 の出力チャネルにチャネル 0 を入力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミキシング レベル [N]</p></td>
<td align="left"><p>0 の出力チャネルにチャネル 1 を入力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ミキシング レベル [n+1]</p></td>
<td align="left"><p>1 の出力チャネルにチャネル 1 を入力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ミキシング レベル 2 n-1</p></td>
<td align="left"><p>N-1 の出力チャネルにチャネル 1 の入力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>[1 M N *] ミキシング レベル</p></td>
<td align="left"><p>N-1 の出力チャネルにチャネル M-1 の入力します。</p></td>
</tr>
</tbody>
</table>

 

次の図は、入力、出力パスの配列要素のミキシング レベルのマッピングを示します。 各入力出力パスを制御するミキシング レベルの配列要素のインデックスは、角かっこで表示されます。

![supermixer ノードのミキシング レベルの配列要素のマッピングを示す図](images/supermix.png)

入力チャネルに接続するパスがない場合*は*出力チャネルに*j*、フィルターを設定する必要があります、**ミュート**ミキシング レベルの配列要素のメンバー\[*しました* \*N +*j* \]に**TRUE**します。

KSAUDIO サイズ\_ミキシング レベルの配列はから計算されます、 [ **KSAUDIO\_MIXCAP\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixcap_table)構造体から取得した[ **KSPROPERTY\_オーディオ\_混在\_レベル\_CAP**](ksproperty-audio-mix-level-caps.md)します。 場合、構造体の**InputChannels**と**OutputChannels**メンバーが値を含む*m*と*n*配列のサイズが

*m* \* *n* \* **sizeof**(KSAUDIO\_ミキシング レベル)

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_混在\_レベル\_テーブル プロパティの要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

フィルターは、KSPROPERTY を成功\_オーディオ\_混在\_レベル\_ミックス レベル値を指定するテーブルのプロパティの設定要求 (**レベル**KSAUDIO のメンバー\_ミキシング レベル) では取り上げませんが、フィルターの範囲 (サイレント) 値をサポートされている範囲にクランプします。 このプロパティを取得する後続の要求でただし、フィルターの出力は、実際の値を使用します。

<a name="requirements"></a>必要条件
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


[**KSNODEPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSAUDIO\_MIXCAP\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSPROPERTY\_オーディオ\_混在\_レベル\_キャップ**](ksproperty-audio-mix-level-caps.md)

[**KSAUDIO\_ミキシング レベル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

 

 






