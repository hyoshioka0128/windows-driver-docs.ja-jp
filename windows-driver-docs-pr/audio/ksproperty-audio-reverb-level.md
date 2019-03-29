---
title: KSPROPERTY\_オーディオ\_リバーブ\_レベル
description: KSPROPERTY\_オーディオ\_リバーブ\_レベル プロパティは、現在リバーブ レベルを指定します。 これはリバーブ ノードのプロパティ (KSNODETYPE\_リバーブ)。
ms.assetid: f38396a2-5528-4085-a051-fcfb73e9c1d1
keywords:
- KSPROPERTY_AUDIO_REVERB_LEVEL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_REVERB_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cda5187366a13beb15eb338827bc800b65155cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571363"
---
# <a name="kspropertyaudioreverblevel"></a>KSPROPERTY\_オーディオ\_リバーブ\_レベル


KSPROPERTY\_オーディオ\_リバーブ\_レベル プロパティは、現在リバーブ レベルを指定します。 これはリバーブ ノードのプロパティ ([**KSNODETYPE\_リバーブ**](ksnodetype-reverb.md))。

## <span id="ddk_ksproperty_audio_reverb_level_ks"></span><span id="DDK_KSPROPERTY_AUDIO_REVERB_LEVEL_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537143" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537143)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は ULONG 型で、リバーブ レベルを指定します。 リバーブ値は 0 から 100 に線形範囲に従います\*(65536-1/65536) %。

-   0x00010000 の値は、100% を表します。

-   100 を表す値が 0 xffffffff\*(65536-1/65536) % です。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_リバーブ\_レベル プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSNODETYPE\_リバーブ**](ksnodetype-reverb.md)

[**KSNODEPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff537143)

 

 






