---
title: KSK プロパティ\_オーディオ\_混合\_レベル\_キャップ
description: KSK プロパティ\_AUDIO\_ミックス\_LEVEL\_CAPS プロパティは、スーパーミキサーノード (KSNODETYPE\_スーパーミックス) の混合レベル機能を指定します。 1つの get プロパティ要求は、入力チャネルと出力チャネルのすべての組み合わせに関する情報を取得します。
ms.assetid: ab7a5dfb-8975-41bb-9347-953406701804
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a93904ae67b79c7196806ae2e67170059abc4394
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831015"
---
# <a name="ksproperty_audio_mix_level_caps"></a>KSK プロパティ\_オーディオ\_混合\_レベル\_キャップ


KSK プロパティ\_AUDIO\_ミックス\_LEVEL\_CAPS プロパティは、スーパーミキサーノード ([**KSNODETYPE\_スーパーミックス**](ksnodetype-supermix.md)) の混合レベル機能を指定します。 1つの*get*プロパティ要求は、入力チャネルと出力チャネルのすべての組み合わせに関する情報を取得します。

## <span id="ddk_ksproperty_audio_mix_level_caps_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_CAPS_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXCAP_TABLE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksaudio_mixcap_table)"><strong>KSAUDIO_MIXCAP_TABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、KSAUDIO\_MIXCAP\_TABLE 型の構造体で、 *m*入力チャネルと n を使用してスーパーミキサーノード内のすべての*m*\**n*入力出力経路の機能を指定します。出力チャネル。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

\_\_レベル CAPS プロパティ要求で\_は、\_が正常に完了したことを示すステータス\_SUCCESS が返されます。 それ以外の場合、要求は適切なエラー状態コードを返します。

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

[**KSNODETYPE\_スーパーミックス**](ksnodetype-supermix.md)

 

 






