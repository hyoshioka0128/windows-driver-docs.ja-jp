---
title: KSPROPERTY\_AC3\_ダイアログ\_レベル
description: KSPROPERTY\_AC3\_ダイアログ\_レベル プロパティは、AC で 3 でエンコードされたストリームにオーディオのプログラム内で音声のダイアログ ボックスの平均ボリューム レベルを指定します。
ms.assetid: 8b88b631-abf7-4407-a7c1-ddacf849a81e
keywords:
- KSPROPERTY_AC3_DIALOGUE_LEVEL オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AC3_DIALOGUE_LEVEL
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35a4e592f2201cd2150e446a1e5a1506f3715472
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560527"
---
# <a name="kspropertyac3dialoguelevel"></a>KSPROPERTY\_AC3\_ダイアログ\_レベル


KSPROPERTY\_AC3\_ダイアログ\_レベル プロパティは、AC で 3 でエンコードされたストリームにオーディオのプログラム内で音声のダイアログ ボックスの平均ボリューム レベルを指定します。

## <span id="ddk_ksproperty_ac3_dialogue_level_ks"></span><span id="DDK_KSPROPERTY_AC3_DIALOGUE_LEVEL_KS"></span>


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
<td align="left"><p>X</p></td>
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff537078" data-raw-source="[&lt;strong&gt;KSAC3_DIALOGUE_LEVEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff537078)"><strong>KSAC3_DIALOGUE_LEVEL</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KSAC3\_ダイアログ\_平均ダイアログ レベルを指定するレベルの構造体。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_AC3\_ダイアログ\_レベル プロパティ要求がステータスを返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

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


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSAC3\_ダイアログ\_レベル**](https://msdn.microsoft.com/library/windows/hardware/ff537078)

 

 






