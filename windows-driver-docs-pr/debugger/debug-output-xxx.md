---
title: デバッグ\_出力\_XXX
description: デバッグ\_出力\_XXX 定数は、出力のフラグ。 出力のフラグは、それに伴う出力の種類を示すビット フィールドを形成します。
ms.assetid: 0c500a2e-0817-45de-8607-4cd4a29d5813
ms.date: 11/13/2018
topic_type:
- apiref
api_name:
- DEBUG_OUTPUT_NORMAL
- DEBUG_OUTPUT_ERROR
- DEBUG_OUTPUT_WARNING
- DEBUG_OUTPUT_VERBOSE
- DEBUG_OUTPUT_PROMPT
- DEBUG_OUTPUT_PROMPT_REGISTERS
- DEBUG_OUTPUT_EXTENSION_WARNING
- DEBUG_OUTPUT_DEBUGGEE
- DEBUG_OUTPUT_DEBUGGEE_PROMPT
- DEBUG_OUTPUT_SYMBOLS
- DEBUG_OUTPUT_STATUS
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: fd52f1179291e48b61466c1c1d653e6838e68cd1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558126"
---
# <a name="debugoutputxxx"></a>デバッグ\_出力\_XXX


デバッグ\_出力\_*XXX*定数は、出力のフラグ。 出力のフラグは、それに伴う出力の種類を示すビット フィールドを形成します。

使用可能な値は、次に示します。

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
<td align="left"><span id="DEBUG_OUTPUT_NORMAL"></span><span id="debug_output_normal"></span>
<strong>DEBUG_OUTPUT_NORMAL</strong></td>
<td align="left"><p>通常の出力。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_ERROR"></span><span id="debug_output_error"></span>
<strong>DEBUG_OUTPUT_ERROR</strong></td>
<td align="left"><p>エラー出力。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_WARNING"></span><span id="debug_output_warning"></span>
<strong>DEBUG_OUTPUT_WARNING</strong></td>
<td align="left"><p>警告です。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_VERBOSE"></span><span id="debug_output_verbose"></span>
<strong>DEBUG_OUTPUT_VERBOSE</strong></td>
<td align="left"><p>追加の出力。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_PROMPT"></span><span id="debug_output_prompt"></span>
<strong>DEBUG_OUTPUT_PROMPT</strong></td>
<td align="left"><p>プロンプトの出力。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_PROMPT_REGISTERS"></span><span id="debug_output_prompt_registers"></span>
<strong>DEBUG_OUTPUT_PROMPT_REGISTERS</strong></td>
<td align="left"><p>プロンプトの前にダンプを登録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_EXTENSION_WARNING"></span><span id="debug_output_extension_warning"></span>
<strong>DEBUG_OUTPUT_EXTENSION_WARNING</strong></td>
<td align="left"><p>警告が拡張機能の操作に固有です。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_DEBUGGEE"></span><span id="debug_output_debuggee"></span>
<strong>DEBUG_OUTPUT_DEBUGGEE</strong></td>
<td align="left"><p>デバッグ ターゲットの出力を (たとえば、 <strong>OutputDebugString</strong>または<strong>による DbgPrint</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_DEBUGGEE_PROMPT"></span><span id="debug_output_debuggee_prompt"></span>
<strong>DEBUG_OUTPUT_DEBUGGEE_PROMPT</strong></td>
<td align="left"><p>デバッグ対象が予期する入力 (たとえば、 <strong>DbgPrompt</strong>)。</p></td>
</tr>
<tr class="even">
<td align="left"><span id="DEBUG_OUTPUT_SYMBOLS"></span><span id="debug_output_symbols"></span>
<strong>DEBUG_OUTPUT_SYMBOLS</strong></td>
<td align="left"><p>メッセージのシンボル (たとえば、 <strong>! sym ノイズの多い</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><span id="DEBUG_OUTPUT_STATUS "></span><span id="debug_output_status"></span>
<strong>DEBUG_OUTPUT_STATUS </strong></td>
<td align="left"><p>ステータス バーを変更する出力。</p></td>
</tr>
</tbody>
</table>

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

 

 





