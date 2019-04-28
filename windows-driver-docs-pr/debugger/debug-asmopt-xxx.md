---
title: デバッグ\_ASMOPT\_XXX
description: デバッグ\_ASMOPT\_XXX 定数は、デバッガー エンジンがアセンブルおよびターゲットのプロセッサの命令を逆アセンブルする方法に影響します。
ms.date: 08/10/2018
topic_type:
- apiref
api_name:
- DEBUG_ASMOPT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: f3f7b50a8401cd5f49e8cf80f9a99a6d43f5e4d8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368678"
---
# <a name="debugasmoptxxx"></a>デバッグ\_ASMOPT\_XXX

アセンブリとの逆アセンブル オプションは、デバッガー エンジンがアセンブルおよびターゲットのプロセッサの命令を逆アセンブルする方法に影響します。


オプションは、次のビット フラグのビットセットで表されます。

<table>
<tr>
<th>定数</th>
<th>説明</th>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_VERBOSE"></a><a id="debug_asmopt_verbose"></a><dl>
<dt><b>DEBUG_ASMOPT_VERBOSE</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>このビットが設定されている場合は、逆アセンブルで追加情報が含まれています。</p>
<p>これは、<b>詳細</b>オプション、 <b>.asm</b>コマンド。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_NO_CODE_BYTES"></a><a id="debug_asmopt_no_code_bytes"></a><dl>
<dt><b>DEBUG_ASMOPT_NO_CODE_BYTES</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>このビットが設定されている場合、命令の生のバイトは、逆アセンブリに含まれません。</p>
<p>これは、 <b>no_code_bytes</b>オプション、 <b>.asm</b>コマンド。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_IGNORE_OUTPUT_WIDTH"></a><a id="debug_asmopt_ignore_output_width"></a><dl>
<dt><b>DEBUG_ASMOPT_IGNORE_OUTPUT_WIDTH</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>このビットが設定されている場合、デバッガーは、逆アセンブリ中に指示をフォーマットするときに、出力の表示の幅を無視します。</p>
<p>これは、 <b>ignore_output_width</b>オプション、 <b>.asm</b>コマンド。</p>
</td>
</tr>
<tr VALIGN="top">
<td align="left" width="40%"><a id="DEBUG_ASMOPT_SOURCE_LINE_NUMBER"></a><a id="debug_asmopt_source_line_number"></a><dl>
<dt><b>DEBUG_ASMOPT_SOURCE_LINE_NUMBER</b></dt>
</dl>
</td>
<td align="left" width="60%">
<p>このビットが設定されている場合、逆アセンブリの出力の各行はシンボル情報が提供するソース コードの行番号のプレフィックスします。</p>
<p>これは、 <b>source_line</b>オプション、 <b>.asm</b>コマンド。</p>
</td>
</tr>
</table>


**注釈**

さらに、DEBUG_ASMOPT_DEFAULT 値は、アセンブリとの逆アセンブル オプションの既定のセットを表します。 これは、上の表でのすべてのオプションをオフにされていることを意味します。 



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

 

 





