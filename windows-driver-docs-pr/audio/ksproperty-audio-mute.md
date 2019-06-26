---
title: KSPROPERTY\_オーディオ\_ミュート
description: KSPROPERTY\_オーディオ\_ミュート プロパティを指定するかどうか、ミュート ノード上のチャネル (KSNODETYPE\_ミュート) がミュートされているかどうか。
ms.assetid: 3c8d7a09-521d-47fd-8441-866a0d12540f
keywords:
- KSPROPERTY_AUDIO_MUTE オーディオ デバイス
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
ms.openlocfilehash: 585ace1907ff3539e8d66ad56c005bd9e54ebf9b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360607"
---
# <a name="kspropertyaudiomute"></a>KSPROPERTY\_オーディオ\_ミュート


KSPROPERTY\_オーディオ\_ミュート プロパティを指定するかどうか、ミュート ノード上のチャネル ([**KSNODETYPE\_ミュート**](ksnodetype-mute.md)) がミュートされているかどうか。

## <span id="ddk_ksproperty_audio_mute_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MUTE_KS"></span>


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
<td align="left"><p>はい</p></td>
<td align="left"><p>フィルターまたは暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksnodeproperty_audio_channel)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は BOOL 型の指定したストリームのチャネルがミュートされているかどうかを示します。 値**TRUE**チャネルがミュートされていることを示します。 **FALSE**ミュートされていないことを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_ミュート プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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

[**KSNODETYPE\_ミュート**](ksnodetype-mute.md)

 

 






