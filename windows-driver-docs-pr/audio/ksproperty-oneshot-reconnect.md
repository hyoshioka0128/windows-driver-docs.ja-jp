---
title: KSPROPERTY \_ ONESHOT \_ RECONNECT
description: KSK プロパティ \_ ONESHOT \_ RECONNECT プロパティは、Bluetooth オーディオデバイスへの接続を試行するようにオーディオドライバーに指示するために使用されます。
ms.assetid: 54122a02-87e9-4953-aa78-4b9b31447a26
keywords:
- KSPROPERTY_ONESHOT_RECONNECT オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_ONESHOT_RECONNECT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e118d902cd77ae09f89be85dcde5a510eed36a4
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83851287"
---
# <a name="ksproperty_oneshot_reconnect"></a>KSPROPERTY \_ ONESHOT \_ RECONNECT


**Ksk プロパティ \_ ONESHOT \_ RECONNECT**プロパティは、Bluetooth オーディオデバイスへの接続を試行するようにオーディオドライバーに指示するために使用されます。

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

**Ksk プロパティ \_ ONESHOT \_ RECONNECT**プロパティは \_ 、要求が成功した場合に STATUS SUCCESS を返します。

> [!NOTE]
> 要求が成功した場合、ドライバーは Bluetooth オーディオデバイスに接続しようとしましたが、必ずしも試行が成功したことを意味するわけではありません。

 

<a name="remarks"></a>コメント
-------

ドライバーに[**Ksk プロパティジャックの \_ \_ 説明**](ksproperty-jack-description.md)ピンプロパティを実装できます。 この実装では、 **Ksk プロパティ \_ ONESHOT \_ RECONNECT**プロパティ要求を行った後、エンドポイントの接続状態を確認できます。

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

 

 






