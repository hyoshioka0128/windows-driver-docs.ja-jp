---
title: WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子
description: WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子のプロパティの一覧、有効な特殊な書式設定文字シーケンスを文字列に埋め込むことができます値を WIA\_IP\_プリンター\_裏書き\_文字列プロパティ。
ms.assetid: D7D6BA47-623A-4F8F-9E29-2C9043AD4C2F
keywords:
- WIA_IPS_PRINTER_ENDORSER_VALID_FORMAT_SPECIFIERS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_VALID_FORMAT_SPECIFIERS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ef6b7f9e5404fe827c2b8a893b1ca40223fac8
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464168"
---
# <a name="wiaipsprinterendorservalidformatspecifiers"></a>WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子


**WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子**プロパティが有効な特殊な書式設定文字シーケンスを一覧表示文字の文字列値に埋め込まれている、 [ **WIA\_IP\_プリンター\_裏書き\_文字列**](wia-ips-printer-endorser-string.md)プロパティ。 WIA ミニドライバーは、作成し、このプロパティを保持します。




プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り専用です。

<a name="remarks"></a>コメント
-------

次の表に、有効な定数、 **WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子**プロパティ。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>書式指定文字列</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PRINT_DATE</p></td>
<td><p>L"$DATE$"</p></td>
<td><p>コンピューターのロケールの形式で現在の日付。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_YEAR</p></td>
<td><p>L"$YEAR$"</p></td>
<td><p>現在の年 (4 桁)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_MONTH</p></td>
<td><p>L"$MONTH$"</p></td>
<td><p>現在の月 (1 ~ 12)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_DAY</p></td>
<td><p>L"$DAY$"</p></td>
<td><p>月 (1 ~ 31) の現在の日付。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_WEEK_DAY</p></td>
<td><p>L「$WEEK_DAY$」</p></td>
<td><p>現在の日付 (たとえば、"Wednesday") コンピューターのロケールの言語で曜日の名前。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_TIME_24H</p></td>
<td><p>L"$HOUR_24H$"</p></td>
<td><p>24 時間形式で現在の時間 (0 - 23)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_TIME_12H</p></td>
<td><p>L"$ TIME_12H$"</p></td>
<td><p>コンピューターのロケールの現在の時刻書式設定、12 時間 (標識。)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_HOUR_12H</p></td>
<td><p>L"$HOUR_12H$"</p></td>
<td><p>現在の標識します。 1 時間 (0 ~ 11)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_AM_PM</p></td>
<td><p>L"$AM_PM$"</p></td>
<td><p>"AM"または"PM"です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_MINUTE</p></td>
<td><p>L"$MINUTE$"</p></td>
<td><p>現在の分 (0 - 59)。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PRINT_SECOND</p></td>
<td><p>L"$SECOND$"</p></td>
<td><p>現在の秒 (0 - 59)。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PRINT_PAGE_COUNT</p></td>
<td><p>L「$PAGE_COUNT$」</p></td>
<td><p>(ジョブ別) カウンターの値。</p></td>
</tr>
</tbody>
</table>

 

特別なシーケンス L「$$」は、'$' 文字を意味します。

このプロパティは・ インプリント ・/裏書きデータ ソース アイテムの省略可能です。 シーケンスのプリンター/裏書きデバイスが任意の特殊な形式をサポートしていないサポートされていないことを意味します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





