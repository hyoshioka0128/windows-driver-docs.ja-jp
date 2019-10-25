---
title: KSK プロパティ\_AUDIO\_ミュート
description: KSK プロパティ\_AUDIO\_ミュートプロパティは、ミュートノード (KSNODETYPE\_ミュート) のチャネルがミュートされているかどうかを指定します。
ms.assetid: 3c8d7a09-521d-47fd-8441-866a0d12540f
keywords:
- KSPROPERTY_AUDIO_MUTE オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_MUTE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2221ba8e3d6aaab78fdf19957cdc8fb7c9c0f938
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830987"
---
# <a name="ksproperty_audio_mute"></a>KSK プロパティ\_AUDIO\_ミュート


KSK プロパティ\_AUDIO\_ミュートプロパティは、ミュートノード ([**KSNODETYPE\_ミュート**](ksnodetype-mute.md)) のチャネルがミュートされているかどうかを指定します。

## <span id="ddk_ksproperty_audio_mute_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MUTE_KS"></span>


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
<td align="left"><p>フィルターまたは Pin インスタンスを使用したノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>型</p></td>
</tr>
</tbody>
</table>

 

プロパティ値はブール型で、指定されたストリームのチャネルがミュートされているかどうかを示します。 値が**TRUE の場合**は、チャネルがミュートされていることを示します。 **FALSE**は、ミュートされていないことを示します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_ミュートプロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

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

[**KSNODETYPE\_ミュート**](ksnodetype-mute.md)

 

 






