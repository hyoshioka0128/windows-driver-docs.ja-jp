---
title: KSPROPERTY\_ONESHOT\_切断
description: KSPROPERTY\_ONESHOT\_切断プロパティを使用して、Bluetooth のオーディオ デバイスから切断するオーディオ ドライバーを確認します。
ms.assetid: B79B3B1E-A34A-4FF9-852A-938C0D5202E9
keywords:
- KSPROPERTY_ONESHOT_DISCONNECT オーディオ デバイス
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
ms.openlocfilehash: 3319f86b82fa5d2210d9000a894c45355fc6436d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332690"
---
# <a name="kspropertyoneshotdisconnect"></a>KSPROPERTY\_ONESHOT\_切断


**KSPROPERTY\_ONESHOT\_切断**プロパティを使用して、Bluetooth のオーディオ デバイスから切断するオーディオ ドライバーを確認します。

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

**KSPROPERTY\_ONESHOT\_切断**プロパティは、ステータスを返します\_要求が成功した場合は成功します。

&gt; \[!注\]&gt;要求が成功した場合は、ドライバーがオーディオの Bluetooth デバイスから切断するとしましたが、必ずしも、試行が成功したことを意味します。

 

<a name="remarks"></a>注釈
-------

実装することができます、 [ **KSPROPERTY\_ジャック\_説明**](ksproperty-jack-description.md)ドライバーのプロパティをピン留めします。 この実装を行った後、エンドポイントの接続の状態を確認できます。、 **KSPROPERTY\_ONESHOT\_切断**プロパティ要求。

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

 

 






