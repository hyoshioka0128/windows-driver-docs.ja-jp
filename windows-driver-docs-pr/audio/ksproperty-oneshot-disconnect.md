---
title: KSPROPERTY \_ ONESHOT \_ DISCONNECT
description: KSK プロパティ \_ ONESHOT \_ disconnect プロパティは、Bluetooth オーディオデバイスからの切断をオーディオドライバーに要求するために使用されます。
ms.assetid: B79B3B1E-A34A-4FF9-852A-938C0D5202E9
keywords:
- KSPROPERTY_ONESHOT_DISCONNECT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ONESHOT_DISCONNECT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 084817a07e1d94908182a5e4a3dedaa6e64febee
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851283"
---
# <a name="ksproperty_oneshot_disconnect"></a>KSPROPERTY \_ ONESHOT \_ DISCONNECT


**Ksk プロパティ \_ ONESHOT \_ disconnect**プロパティは、Bluetooth オーディオデバイスからの切断をオーディオドライバーに要求するために使用されます。

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
<th align="left">オン</th>
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
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>NULL</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は、このプロパティの要求と共に送信されません。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**Ksk プロパティ \_ ONESHOT \_ DISCONNECT**プロパティは、 \_ 要求が成功した場合に STATUS SUCCESS を返します。

> [!NOTE]
> 要求が成功した場合、ドライバーは Bluetooth オーディオデバイスとの接続を切断しようとしましたが、必ずしも試行が成功したことを意味するわけではありません。

 

<a name="remarks"></a>コメント
-------

ドライバーに[**Ksk プロパティジャックの \_ \_ 説明**](ksproperty-jack-description.md)ピンプロパティを実装できます。 この実装では、 **Ksk プロパティ \_ ONESHOT \_ DISCONNECT**プロパティ要求を行った後に、エンドポイントの接続状態を確認できます。

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
<td align="left"><p>Windows 7 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSK プロパティ \_ ジャックの \_ 説明**](ksproperty-jack-description.md)

 

 






