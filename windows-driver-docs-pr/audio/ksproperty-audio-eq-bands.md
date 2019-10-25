---
title: KSK プロパティ\_AUDIO\_EQ\_バンド
description: KSK プロパティ\_AUDIO\_EQ\_バンドプロパティは、イコライゼーションテーブルからの周波数バンドのセットを指定します。 これは、EQ ノード (KSNODETYPE\_イコライザー) のチャネルの取得専用プロパティです。
ms.assetid: 64304cad-cf07-4bdb-96d5-7dd594380725
keywords:
- KSPROPERTY_AUDIO_EQ_BANDS オーディオデバイス
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
ms.openlocfilehash: 9e74286a26dc1696d10cbf6789d3b208b27f8351
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831038"
---
# <a name="ksproperty_audio_eq_bands"></a>KSK プロパティ\_AUDIO\_EQ\_バンド


KSK プロパティ\_AUDIO\_EQ\_バンドプロパティは、イコライゼーションテーブルからの周波数バンドのセットを指定します。 これは、EQ ノード ([**KSNODETYPE\_イコライザー**](ksnodetype-equalizer.md)) のチャネルの取得専用プロパティです。

## <span id="ddk_ksproperty_audio_eq_bands_ks"></span><span id="DDK_KSPROPERTY_AUDIO_EQ_BANDS_KS"></span>


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
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></p></td>
<td align="left"><p>ULONG 配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、ULONG 要素の配列です。

```cpp
  ULONG  CenterFreqVal[N];
```

チャネルのイコライゼーションテーブルに N 周波数バンドのエントリが含まれている場合、配列には N 個の要素が含まれ、各配列要素は対応するバンドの中心周波数を指定します。 ミニポートドライバーは、各要素に、ヘルツ (Hz) で表される整数の頻度値を書き込みます。 次の表に、配列要素へのイコライゼーションバンドの割り当てを示します。

配列要素の説明センター Freqval\[0\]

イコライゼーションバンド0のセンター周波数 (Hz)。

中央 Freqval\[1\]

イコライゼーションバンド1のセンター周波数 (Hz)。

...

中央 Freqval\[N-1\]

イコライゼーションバンド N-1 のセンター周波数 (Hz)。

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_EQ\_バンドプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

イコライゼーションバンドの数を決定するには、最初に[**Ksk プロパティ\_AUDIO\_NUM\_EQ\_バンド**](ksproperty-audio-num-eq-bands.md)要求を送信します。

周波数バンドのイコライゼーションレベルは、 [**Ksk プロパティ\_AUDIO\_EQ\_LEVEL**](ksproperty-audio-eq-level.md)プロパティによって指定されます。

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

[**KSK プロパティ\_AUDIO\_EQ\_レベル**](ksproperty-audio-eq-level.md)

 

 






