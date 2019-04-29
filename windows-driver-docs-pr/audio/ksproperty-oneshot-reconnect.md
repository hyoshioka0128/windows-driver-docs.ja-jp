---
title: KSPROPERTY\_ONESHOT\_再接続
description: KSPROPERTY\_ONESHOT\_再接続プロパティは、Bluetooth のオーディオ デバイスに接続しようとするオーディオ ドライバーを使用します。
ms.assetid: 54122a02-87e9-4953-aa78-4b9b31447a26
keywords:
- KSPROPERTY_ONESHOT_RECONNECT オーディオ デバイス
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
ms.openlocfilehash: 70985def58f7bfcfbfd39c574e910a8dc8b7dcfe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332680"
---
# <a name="kspropertyoneshotreconnect"></a>KSPROPERTY\_ONESHOT\_再接続


**KSPROPERTY\_ONESHOT\_再接続**オーディオの Bluetooth デバイスに接続しようとするオーディオ ドライバーを要求するプロパティを使用します。

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
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>NULL</p></td>
</tr>
</tbody>
</table>

 

このプロパティの要求では、プロパティの値は送信されません。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

**KSPROPERTY\_ONESHOT\_再接続**プロパティは、ステータスを返します\_要求が成功した場合は成功します。

&gt; \[!注\]&gt;要求が成功した場合は、ドライバーがオーディオの Bluetooth デバイスに接続するとしましたが、必ずしも、試行が成功したことを意味します。

 

<a name="remarks"></a>注釈
-------

実装することができます、 [ **KSPROPERTY\_ジャック\_説明**](ksproperty-jack-description.md)ドライバーのプロパティをピン留めします。 この実装を行った後、エンドポイントの接続の状態を確認できます。、 **KSPROPERTY\_ONESHOT\_再接続**プロパティ要求。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 7 および Windows の以降のバージョンで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

[**KSPROPERTY\_ジャック\_の説明**](ksproperty-jack-description.md)

 

 






