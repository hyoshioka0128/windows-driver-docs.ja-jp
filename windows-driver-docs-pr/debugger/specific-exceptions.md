---
title: 特定の例外
description: 特定の例外
ms.assetid: e9fec81f-7e93-47cd-b496-a5e2a58f3b19
keywords:
- 特定の例外の Windows デバッグ
topic_type:
- apiref
api_name:
- Specific Exceptions
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68c797365bdc3e99e10e587d294c72d5207cd843
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368084"
---
# <a name="specific-exceptions"></a>特定の例外


次の表では、特定の例外フィルターの例外コードを示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例外コード</th>
<th align="left">例外</th>
<th align="left">ヘッダー ファイルまたは値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_ACCESS_VIOLATION</p></td>
<td align="left"><p>アクセス違反</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_ASSERTION_FAILURE</p></td>
<td align="left"><p>アサーション エラー</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_APPLICATION_HANG</p></td>
<td align="left"><p>アプリケーションのハング</p></td>
<td align="left"><p>0xCFFFFFFF</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_BREAKPOINT</p></td>
<td align="left"><p>中断命令例外</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_CPP_EH_EXCEPTION</p></td>
<td align="left"><p>C++ 例外処理の例外</p></td>
<td align="left"><p>0xE06D7363</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_CLR_EXCEPTION</p></td>
<td align="left"><p>共通言語ランタイム (CLR) 例外</p></td>
<td align="left"><p>0xE0434f4D</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DBG_CONTROL_BREAK</p></td>
<td align="left"><p>CTRL + Break 例外</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_CONTROL_C</p></td>
<td align="left"><p>CTRL + C 例外</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DATATYPE_MISALIGNMENT</p></td>
<td align="left"><p>データの不整合</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>DBG_COMMAND_EXCEPTION</p></td>
<td align="left"><p>デバッガー コマンド例外</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_GUARD_PAGE_VIOLATION</p></td>
<td align="left"><p>ガード ページ違反</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_ILLEGAL_INSTRUCTION</p></td>
<td align="left"><p>無効な命令</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_IN_PAGE_ERROR</p></td>
<td align="left"><p>ページ I/O エラー</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INTEGER_DIVIDE_BY_ZERO</p></td>
<td align="left"><p>整数 0 による除算</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INTEGER_OVERFLOW</p></td>
<td align="left"><p>整数のオーバーフロー</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INVALID_HANDLE</p></td>
<td align="left"><p>ハンドルが無効です。</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_LOCK_SEQUENCE</p></td>
<td align="left"><p>無効なロックのシーケンス</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INVALID_SYSTEM_SERVICE</p></td>
<td align="left"><p>無効なシステムの呼び出し</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_PORT_DISCONNECTED</p></td>
<td align="left"><p>ポートの切断</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_SINGLE_STEP</p></td>
<td align="left"><p>シングル ステップの例外</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_STACK_BUFFER_OVERRUN</p></td>
<td align="left"><p>スタック バッファー オーバーフロー</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_STACK_OVERFLOW</p></td>
<td align="left"><p>スタック オーバーフロー</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_VERIFIER_STOP</p></td>
<td align="left"><p>アプリケーションの検証の停止</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_WAKE_SYSTEM_DEBUGGER</p></td>
<td align="left"><p>デバッガーを起動します。</p></td>
<td align="left"><p>NtStatus.h</p></td>
</tr>
</tbody>
</table>

 

 

 





