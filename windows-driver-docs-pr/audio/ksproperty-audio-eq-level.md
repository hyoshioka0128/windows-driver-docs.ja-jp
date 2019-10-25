---
title: KSK プロパティ\_AUDIO\_EQ\_レベル
description: KSK プロパティ\_AUDIO\_EQ\_LEVEL プロパティは、n 周波数バンドのエントリを含むイコライゼーションテーブルのイコライゼーションレベルを指定します。 これは、EQ ノード (KSNODETYPE\_イコライザー) のチャネルのプロパティです。
ms.assetid: 17c34af2-dbeb-472c-9825-9dc64f7f96bd
keywords:
- KSPROPERTY_AUDIO_EQ_LEVEL オーディオデバイス
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
ms.openlocfilehash: e2a681db2a6e86a503e7c9248e352d207ec46230
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833034"
---
# <a name="ksproperty_audio_eq_level"></a>KSK プロパティ\_AUDIO\_EQ\_レベル


KSK プロパティ\_AUDIO\_EQ\_LEVEL プロパティは、 *n*周波数バンドのエントリを含むイコライゼーションテーブルのイコライゼーションレベルを指定します。 これは、EQ ノード ([**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md)) のチャネルのプロパティです。

## <span id="ddk_ksproperty_audio_eq_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_LEVEL_KS"></span>


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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>LONG 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、長い要素の配列です。

```cpp
  LONG  Level[N];
```

チャネルのイコライゼーションテーブルに N 周波数バンドのエントリが含まれている場合、配列には N 個の要素が含まれ、各要素はイコライゼーションテーブル内のいずれかのバンドのレベルを指定します。 次の表に、配列要素へのバンドの割り当てを示します。

配列要素の説明レベル\[0\]

帯域幅0のレベル。

レベル\[1\]

帯域幅1のレベル。

...

レベル\[N-1\]

帯域幅 N-1 のレベル。

 

レベル値には次のスケールが使用されます。

-2147483648 は-無限大デシベル (減衰),

-2147483647 は-32767.99998474 デシベル (減衰)、および

\+ 2147483647 は + 32767.99998474 デシベル (ゲイン) です。

2147483648 ~ + 2147483647 の整数値で表されるデシベル範囲。ここで、

このスケールの解像度は1/65536 デシベルです。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_EQ\_LEVEL プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

フィルターは、KSK プロパティ\_AUDIO\_EQ\_レベルのセットプロパティ要求に成功します。この要求は、フィルターの範囲を超える値を指定しますが、値はサポートされる範囲にクランプされます。 ただし、このプロパティを取得するための後続の要求では、使用される実際の値が出力されます。

イコライゼーションバンドの数を決定するには、最初に[**Ksk プロパティ\_AUDIO\_NUM\_EQ\_バンド**](ksproperty-audio-num-eq-bands.md)要求を送信します。

イコライゼーションバンドの中心周波数は、 [**Ksk プロパティ\_AUDIO\_EQ\_バンド**](ksproperty-audio-eq-bands.md)プロパティによって指定されます。

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


[**KSNODEPROPERTY\_AUDIO\_CHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)

[**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md)

[**KSK プロパティ\_AUDIO\_NUM\_EQ\_バンド**](ksproperty-audio-num-eq-bands.md)

[**KSK プロパティ\_AUDIO\_EQ\_バンド**](ksproperty-audio-eq-bands.md)

 

 






