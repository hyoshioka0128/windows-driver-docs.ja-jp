---
title: KSPROPERTY\_オーディオ\_混在\_レベル\_キャップ
description: KSPROPERTY\_オーディオ\_混在\_レベル\_CAPS プロパティ supermixer ノードのミックス レベル機能を指定します (KSNODETYPE\_SUPERMIX)。 1 つのプロパティの get 要求では、入力と出力チャネルのすべての組み合わせの情報を取得します。
ms.assetid: ab7a5dfb-8975-41bb-9347-953406701804
keywords:
- KSPROPERTY_AUDIO_MIX_LEVEL_CAPS オーディオ デバイス
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
ms.openlocfilehash: d88bfa48565a330f244d0c70eaa98fc969418675
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332990"
---
# <a name="kspropertyaudiomixlevelcaps"></a>KSPROPERTY\_オーディオ\_混在\_レベル\_キャップ


KSPROPERTY\_オーディオ\_混在\_レベル\_CAPS プロパティ supermixer ノードのミックス レベル機能を指定します ([**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)). 1 つ*取得*-要求のプロパティは、入力と出力チャネルのすべての組み合わせの情報を取得します。

## <span id="ddk_ksproperty_audio_mix_level_caps_ks"></span><span id="DDK_KSPROPERTY_AUDIO_MIX_LEVEL_CAPS_KS"></span>


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
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537088" data-raw-source="[&lt;strong&gt;KSAUDIO_MIXCAP_TABLE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537088)"><strong>KSAUDIO_MIXCAP_TABLE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は型 KSAUDIO の構造体\_MIXCAP\_テーブルで、すべての機能を指定します*m*\**n*入出力経路を持つ supermixer ノードで*m*チャネルを入力し、 *n*出力チャネル。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_混在\_レベル\_CAPS プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

[**KSAUDIO\_MIXCAP\_テーブル**](https://msdn.microsoft.com/library/windows/hardware/ff537088)

[**KSNODETYPE\_SUPERMIX**](ksnodetype-supermix.md)

 

 






