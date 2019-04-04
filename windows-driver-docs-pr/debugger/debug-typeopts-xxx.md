---
title: デバッグ\_TYPEOPTS\_XXX
description: 型のオプションは、数値と文字列の出力のエンジンの書式に影響します。
ms.assetid: 1c39fb80-d51b-43a6-8a68-8479022baf8a
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- DEBUG_TYPEOPTS_UNICODE_DISPLAY
- DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY
- DEBUG_TYPEOPTS_FORCERADIX_OUTPUT
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 09cd01f7195520747426a56f25a75a40b53072b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551275"
---
# <a name="debugtypeoptsxxx"></a>デバッグ\_TYPEOPTS\_XXX


型のオプションは、数値と文字列の出力のエンジンの書式に影響します。

オプションは、次のビット フラグのビット セットで表されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">定数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><span id="DEBUG_TYPEOPTS_UNICODE_DISPLAY"></span><span id="debug_typeopts_unicode_display"></span>
<strong>DEBUG_TYPEOPTS_UNICODE_DISPLAY</strong></td>
<td align="left"><p>このビットが設定されている場合 USHORT ポインターと配列は出力として Unicode 文字です。</p>
<p>これは、デバッガー コマンドに相当<strong>.enable_unicode 1</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY"></span><span id="debug_typeopts_longstatus_display"></span>
<strong>DEBUG_TYPEOPTS_LONGSTATUS_DISPLAY</strong></td>
<td align="left"><p>このビットが設定されている場合は、10 進数ではなく基本の既定の出力が、長整数。</p>
<p>これは、デバッガー コマンドに相当<strong>.enable_long_status 1</strong>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_TYPEOPTS_FORCERADIX_OUTPUT"></span><span id="debug_typeopts_forceradix_output"></span>
<strong>DEBUG_TYPEOPTS_FORCERADIX_OUTPUT</strong></td>
<td align="left"><p>このビットが設定されている場合は、10 進数ではなく基本の既定の出力は (長整数) を除く整数です。</p>
<p>これは、デバッガー コマンドに相当<strong>.force_radix_output 1</strong>します。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>注釈
-------

既定では、すべての型の書式設定オプションはになります。

種類の詳細については、[型](https://msdn.microsoft.com/library/windows/hardware/ff558931)を参照してください。

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
<td align="left">DbgEng.h (DbgEng.h を含む)</td>
</tr>
</tbody>
</table>

 

 





