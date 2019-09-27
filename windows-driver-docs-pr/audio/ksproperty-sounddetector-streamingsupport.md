---
title: KSK プロパティ\_SOUNDDETECTOR\_の STREAMINGSUPPORT
description: Ksk プロパティ\_sounddetector\_streamingsupport プロパティは、ストリーミングがサポートされているかどうかを示します。
ms.assetid: 3B9B43C0-31EE-4490-AD29-98DA81D1664E
keywords:
- KSPROPERTY_SOUNDDETECTOR_STREAMINGSUPPORT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SOUNDDETECTOR_STREAMINGSUPPORT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 09/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7792fd58d77e3d481dba0b27520be4cf835c66a2
ms.sourcegitcommit: 8295a2b59212972b0f7457a748cc904b5417ad67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71329456"
---
# <a name="ksproperty_sounddetector_streamingsupport"></a>KSK プロパティ\_SOUNDDETECTOR\_の STREAMINGSUPPORT

**Ksk プロパティ\_sounddetector\_streamingsupport**プロパティは、ストリーミングがサポートされているかどうかを示します。

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
<td align="left"><p>はい</p></td>
<td align="left"><p>いいえ</p></td>
<td align="left"><p>Assert</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty" data-raw-source="[&lt;strong&gt;KSSOUNDDETECTORPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kssounddetectorproperty"><strong>KSSOUNDDETECTORPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

プロパティ値は、ストリーミングがサポートされているかどうかを示すブール値です。

この読み取りプロパティをサポートし、false を返すドライバーは、関連付けられたバーストオーディオストリームを使用せずに音声認識がサポートされることを示します。

このプロパティをサポートしていないドライバー、またはこのプロパティをサポートしていて true を返すドライバーは、キーワード検出をトリガーしたオーディオデータのバースティングをサポートしていることを示しています。

すべての検出機能では、ハードウェアのキーワード検出をトリガーしたオーディオデータのバッファリングとバーストストリーミングをサポートし、この要求を失敗させるか、この値を true に設定する必要があります。

<a name="remarks"></a>コメント
-------
このプロパティは将来使用するためのものです。 現在、音声認識のみを行う検出機能の OS サポートはありません。

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
