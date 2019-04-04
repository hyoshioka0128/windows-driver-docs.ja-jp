---
title: KSPROPERTY\_オーディオ\_低音\_BOOST
description: KSPROPERTY\_オーディオ\_低音\_BOOST プロパティができ、トーン ノードでのチャネルの音を無効にします (KSNODETYPE\_トーン)。
ms.assetid: aa54b88b-e251-4d16-9ced-842fec569914
keywords:
- KSPROPERTY_AUDIO_BASS_BOOST オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_BASS_BOOST
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2ef7e24fdffd88f04a30325d07f81406f318d5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580314"
---
# <a name="kspropertyaudiobassboost"></a>KSPROPERTY\_オーディオ\_低音\_BOOST


KSPROPERTY\_オーディオ\_低音\_BOOST プロパティができ、トーン ノードでのチャネルの音を無効にします ([**KSNODETYPE\_トーン**](ksnodetype-tone.md))。

## <span id="ddk_ksproperty_audio_bass_boost_ks"></span><span id="DDK_KSPROPERTY_AUDIO_BASS_BOOST_KS"></span>


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
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>はい</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><a href="https://msdn.microsoft.com/library/windows/hardware/ff537145" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY_AUDIO_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537145)"><strong>KSNODEPROPERTY_AUDIO_CHANNEL</strong></a></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (データの操作) は BOOL 型の音がオンまたはオフになっているかどうかを示します。 値**TRUE**指定したチャネルの音であることを示します。 **FALSE**オフであることを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_低音\_BOOST プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>コメント
-------

トーン ノードでは、レベル、中間の頻度レベル、低音のレベルおよび音高音を制御するプロパティをサポートできます。 詳細については、[ **KSNODETYPE\_トーン**](ksnodetype-tone.md)を参照してください。

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

[**KSNODETYPE\_トーン**](ksnodetype-tone.md)

 

 






