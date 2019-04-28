---
title: デバッグ\_OUTCTL\_XXX
description: デバッグ\_OUTCTL\_XXX 定数は、出力の制御を使用します。 定数は、出力を送信する場所の現在のポリシーを指定するビット フィールドを形成します。 ビット フィールドは、2 つのセクションに分かれています。
ms.assetid: 94d3416a-082e-488b-adc2-8b837bb1c1cb
ms.date: 12/07/2017
keywords:
- デバッグ DEBUG_OUTCTL_XXX Windows
topic_type:
- apiref
api_name:
- DEBUG_OUTCTL_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 071d675430ac36829a6f7121d24ac02dcff836e9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366222"
---
# <a name="debugoutctlxxx"></a>デバッグ\_OUTCTL\_XXX


デバッグ\_OUTCTL\_*XXX*定数は、出力の制御を使用します。 定数は、出力を送信する場所の現在のポリシーを指定するビット フィールドを形成します。 ビット フィールドは、2 つのセクションに分かれています。

## <span id="ddk_debug_outctl_xxx_dbx"></span><span id="DDK_DEBUG_OUTCTL_XXX_DBX"></span>


下位ビットあります正確に、次の値のいずれか。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_THIS_CLIENT</p></td>
<td align="left"><p>このクライアントによって呼び出されるメソッドによって生成される出力は、このクライアントにのみ送信されます<a href="https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks" data-raw-source="[output callbacks](https://msdn.microsoft.com/library/windows/hardware/ff560116#output-callbacks)">コールバックを出力</a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_ALL_CLIENTS</p></td>
<td align="left"><p>出力は、すべてのクライアントに送信されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_ALL_OTHER_CLIENTS</p></td>
<td align="left"><p>出力は、すべてのクライアントに送信されます (出力を生成したクライアントを除く)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_IGNORE</p></td>
<td align="left"><p>出力はすぐに破棄してログに記録またはされませんコールバックに送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_LOG_ONLY</p></td>
<td align="left"><p>出力をログに記録が、コールバックに送信されません。</p></td>
</tr>
</tbody>
</table>

 

ビット フィールドの上位ビットは、次の値を含めることができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_NOT_LOGGED</p></td>
<td align="left"><p>グローバルのログ ファイルには、このクライアントからの出力を配置しないでください。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_OVERRIDE_MASK</p></td>
<td align="left"><p>出力をクライアントの出力のマスクことを許可するかどうかに関係なくクライアントに送信します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_DML</p></td>
<td align="left"><p>デバッガーのマークアップ言語 (DML) をサポートする出力の場合は、DML の形式で出力を送信します。</p></td>
</tr>
</tbody>
</table>

 

有効な出力制御ビット フィールドを作成するには、2 番目のテーブルでは、0 個以上の値と共に、最初のテーブルから 1 つの値を取得し、ビットごとの OR 演算子を使用してそれらを結合します。

出力制御ビット フィールドの既定値はデバッグ\_OUTCTL\_すべて\_クライアント。

独自の出力制御ビット フィールドを作成する代わりに、次の値のいずれかを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_DML</p></td>
<td align="left"><p>新しい出力コントロールを現在の出力のコントロールと同じ値に設定し、出力が DML 形式になるように指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_TEXT</p></td>
<td align="left"><p>新しい出力コントロールを現在の出力のコントロールと同じ値に設定し、出力がテキスト形式であることを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_OUTCTL_AMBIENT</p></td>
<td align="left"><p>DEBUG_OUTCTL_AMBIENT_TEXT と同じです。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>必要条件
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

 

 





