---
title: KSPROPERTY\_AUDIOENGINE\_GFXENABLE
description: KSPROPERTY\_AUDIOENGINE\_GFXENABLE プロパティ要求により、オーディオ ドライバーを取得またはそのグローバル効果の処理能力に関する、オーディオ エンジン ノードの状態を変更します。
ms.assetid: 313A5919-FA92-484D-B5AB-A1417A0A2076
keywords:
- KSPROPERTY_AUDIOENGINE_GFXENABLE オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIOENGINE_GFXENABLE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0079e23a6a5c9ad702c99dc394fe4b8f6157ee1d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332853"
---
# <a name="kspropertyaudioenginegfxenable"></a>KSPROPERTY\_AUDIOENGINE\_GFXENABLE


**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**プロパティ要求により、オーディオ ドライバーを取得またはそのグローバル効果の処理能力に関する、オーディオ エンジン ノードの状態を変更します。

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
<td align="left"><p>〇</p></td>
<td align="left"><p>フィルターを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

プロパティ値が型**BOOL**オーディオ エンジン ノードでの処理全体の効果が有効になっているかどうかを示します。 値**TRUE**処理が有効になっていることを示します。 **FALSE**は無効になっていることを示します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**プロパティ要求を返します**状態\_成功**を正常に完了したことを示します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 8</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY\_AUDIOENGINE**](ksproperty-audioengine.md)

[**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**](ksproperty-audioengine-lfx-enable.md)

 

 






