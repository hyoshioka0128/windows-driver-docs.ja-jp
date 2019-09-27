---
title: KSPROPERTY\_SOUNDDETECTOR\_のリセット
description: Ksproperty\_sounddetector\_RESET プロパティは、パターンが設定されていない状態で検出機能を unarmed 状態にリセットします。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664D
keywords:
- KSPROPERTY_SOUNDDETECTOR_RESET オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_RESET
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/25/2019
ms.localizationpriority: medium
ms.openlocfilehash: 0e6d1d3277ee404a2dd3795de0f0d7eb8de2519d
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71329458"
---
# <a name="ksproperty_sounddetector_reset"></a>KSPROPERTY\_SOUNDDETECTOR\_のリセット

**Ksproperty\_\_sounddetector RESET**プロパティは、パターンが設定されていない状態で検出機能を unarmed 状態にリセットします。

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
<th align="left">取得</th>
<th align="left">Set</th>
<th align="left">移行先</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>いいえ</p></td>
<td align="left"><p>はい</p></td>
<td align="left"><p>Assert</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティ値はブール値です。 True はリセットすることを示し、false は無視されます。

<a name="remarks"></a>コメント
-------

OS は、次のような場合に true の値を設定して reset を呼び出します。

- キーワード検出機能をアン arm します。
- 設定されている[**ksk\_プロパティ\_の sounddetector パターン**](ksproperty-sounddetector-patterns.md)をすべてクリアします。

キーワードパターンが設定されていないときにこの true を設定した場合 ([**ksk プロパティ\_\_sounddetector パターン**](ksproperty-sounddetector-patterns.md)が空の場合)、効果はありません。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 10 バージョン1903</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[**KSK プロパティ\_の SOUNDDETECTOR\_パターン**](ksproperty-sounddetector-patterns.md)

[**KSSOUNDDETECTORPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/)
