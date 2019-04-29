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
ms.openlocfilehash: 58663f51a46861d3228298335e228f97df7fcde0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332968"
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
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は BOOL 型の指定したストリームのチャネルがミュートされているかどうかを示します。 値**TRUE**チャネルがミュートされていることを示します。 **FALSE**ミュートされていないことを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_ミュート プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODEPROPERTY\_オーディオ\_チャネル**](https://msdn.microsoft.com/library/windows/hardware/ff537145)

[**KSNODETYPE\_ミュート**](ksnodetype-mute.md)

 

 






