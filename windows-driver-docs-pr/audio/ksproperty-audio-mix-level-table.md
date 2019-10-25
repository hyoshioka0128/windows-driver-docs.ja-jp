---
title: KSK プロパティ\_オーディオ\_混合\_レベル\_テーブル
description: KSK プロパティ\_AUDIO\_ミックス\_レベル\_テーブルプロパティは、supermixer ノード (KSNODETYPE\_SUPERMIXER) のミックスレベルを指定します。 すべての入力チャネルと出力チャネルに関する情報を提供します。
ms.assetid: 1a1b486b-06e4-462b-8fe9-9d3581c82d06
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_TABLE オーディオデバイス
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
ms.openlocfilehash: f932fd125f2d99e8daf5686224957a72f9e38444
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832978"
---
# <a name="ksproperty_audio_mix_level_table"></a>KSK プロパティ\_オーディオ\_混合\_レベル\_テーブル


KSK プロパティ\_AUDIO\_ミックス\_レベル\_テーブルプロパティは、supermixer ノード ([**KSNODETYPE\_supermixer**](ksnodetype-supermix.md)) のミックスレベルを指定します。 すべての入力チャネルと出力チャネルに関する情報を提供します。

## <span id="ddk_ksproperty_audio_mix_level_table_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_TABLE_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXLEVEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)"><strong>KSAUDIO_MIXLEVEL</strong></a>構造体の配列</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (operation data) は、KSK オーディオ\_MIXLEVEL 構造体の配列であり、M 入力チャネルと N 出力チャネルを持つ supermixer ノードのすべての M\*N 入力出力パスのミックスレベルを指定します。 この配列には、M\*N 個の要素が含まれています。

```cpp
  KSAUDIO_MIXLEVEL  MixLevel[M*N];
```

次の表は、配列要素とスーパーミキサーノード M\*N の入力出力パスとのマッピングを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Array 要素</th>
<th align="left">入力-出力パス</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>MixLevel [0]</p></td>
<td align="left"><p>チャネル0を出力するための入力チャネル0</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel [1]</p></td>
<td align="left"><p>チャネル1を出力するための入力チャネル0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel [N-1]</p></td>
<td align="left"><p>チャネルを出力するための入力チャネル 0-1</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel [N]</p></td>
<td align="left"><p>入力チャネル1から出力チャネル0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel [N + 1]</p></td>
<td align="left"><p>入力チャネル1から出力チャネル1</p></td>
</tr>
<tr class="even">
<td align="left"><p>MixLevel [2N-1]</p></td>
<td align="left"><p>チャネルを出力するための入力チャネル 1 N-1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MixLevel [M * N-1]</p></td>
<td align="left"><p>チャネルを出力するための入力チャネル (M-1) N-1</p></td>
</tr>
</tbody>
</table>

 

次の図は、MixLevel 配列要素を入力出力パスにマッピングする方法を示しています。 各入力出力パスを制御する MixLevel array 要素のインデックスは、角かっこで示されています。

![スーパーミキサーノードの mixlevel array 要素のマッピングを示す図](images/supermix.png)

入力チャネル*i*を出力チャネル*j*に接続するパスがない場合、フィルターでは、配列要素 MixLevel の**ミュート**メンバー\[*i*\*N +*j*\] を**TRUE**に設定する必要があります。

Ksaudio\_MIXLEVEL 配列のサイズは、 [**ksaudio\_MIXCAP\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)構造から計算されます。この構造体は、 [**KSK プロパティ\_オーディオ\_混合\_レベル\_キャップ**](ksproperty-audio-mix-level-caps.md)から取得されます。 構造体の**Inputchannels**と**outputchannels**のメンバーに*m*と*n*の値が含まれている場合、配列のサイズはです。

*m* \* *n* \* **SIZEOF**(ksaudio\_MIXLEVEL)

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_レベル\_テーブルのプロパティを\_\_KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

フィルターは KSK プロパティ\_AUDIO\_ミックス\_レベル\_テーブルセットプロパティの要求に成功します。これは、フィルターの範囲を超える混合レベルの値 (KSK AUDIO\_MIXLEVEL の**レベル**メンバー) を指定しますが (警告なし) は、サポートされている範囲に値をクランプします。 ただし、このプロパティを取得するための後続の要求では、フィルターは実際に使用された値を出力します。

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

[**KSAUDIO\_MIXCAP\_テーブル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)

[**KSK プロパティ\_オーディオ\_混合\_レベル\_キャップ**](ksproperty-audio-mix-level-caps.md)

[**KSAUDIO\_MIXLEVEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixlevel)

[**KSNODETYPE\_スーパーミックス**](ksnodetype-supermix.md)

 

 






