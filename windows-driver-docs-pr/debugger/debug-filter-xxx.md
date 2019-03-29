---
title: デバッグ\_フィルター\_XXX
description: デバッグ\_フィルター\_XXX
ms.assetid: 1f8f738b-7b2b-419a-949e-b71f937de02d
ms.date: 12/07/2017
keywords:
- デバッグ DEBUG_FILTER_XXX Windows
topic_type:
- apiref
api_name:
- DEBUG_FILTER_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: b7b14a63a64fde54a1139652850f70dceb861b67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578118"
---
# <a name="debugfilterxxx"></a>デバッグ\_フィルター\_XXX


デバッグ\_フィルター\_*XXX*定数は、次の 3 つの異なる目的で使用: の処理状態を指定して、イベント フィルターの中断状態を指定する、個々 の特定のイベント フィルターを指定するには例外フィルター。

### <a name="span-idspecificeventfilterspanspan-idspecificeventfilterspanspecific-event-filter"></a><span id="specific_event_filter"></span><span id="SPECIFIC_EVENT_FILTER"></span>特定のイベント フィルター

次の定数を使用して、特定のイベント フィルターを指定します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">event</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_CREATE_THREAD</p></td>
<td align="left"><p>スレッドを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_EXIT_THREAD</p></td>
<td align="left"><p>スレッドを終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_CREATE_PROCESS</p></td>
<td align="left"><p>プロセスを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_EXIT_PROCESS</p></td>
<td align="left"><p>プロセスを終了します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_LOAD_MODULE</p></td>
<td align="left"><p>モジュールの読み込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_UNLOAD_MODULE</p></td>
<td align="left"><p>モジュールのアンロード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_SYSTEM_ERROR</p></td>
<td align="left"><p>システム エラー</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_INITIAL_BREAKPOINT</p></td>
<td align="left"><p>最初のブレークポイント</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_INITIAL_MODULE_LOAD</p></td>
<td align="left"><p>初期のモジュールの読み込み</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_DEBUGGEE_OUTPUT</p></td>
<td align="left"><p>ターゲットの出力</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idbreakstatusspanspan-idbreakstatusspanbreak-status"></a><span id="break_status"></span><span id="BREAK_STATUS"></span>中断状態

次の定数を使用して、イベント フィルターの中断状態を指定します。

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
<td align="left"><p>DEBUG_FILTER_BREAK</p></td>
<td align="left"><p>イベントがデバッガーに中断されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_SECOND_CHANCE_BREAK</p></td>
<td align="left"><p>イベントは、2 つ目の例外である場合、デバッガーに中断されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_OUTPUT</p></td>
<td align="left"><p>イベントの通知は、デバッガーのコンソールに印刷されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_IGNORE</p></td>
<td align="left"><p>イベントは無視されます。</p></td>
</tr>
</tbody>
</table>

 

さらに、任意の例外フィルターでは、デバッグを中断状態に設定\_フィルター\_削除、イベントのフィルターを削除します。

### <a name="span-idhandlingstatusspanspan-idhandlingstatusspanhandling-status"></a><span id="handling_status"></span><span id="HANDLING_STATUS"></span>処理状態

次の定数を使用すると、例外フィルターの処理状態を指定します。

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
<td align="left"><p>DEBUG_FILTER_GO_HANDLED</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556279#wdkgloss-exception" data-raw-source="&lt;em&gt;exception&lt;/em&gt;"><em>例外</em></a>が処理されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_GO_NOT_HANDLED</p></td>
<td align="left"><p>例外が処理されていません。</p></td>
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

 

 





