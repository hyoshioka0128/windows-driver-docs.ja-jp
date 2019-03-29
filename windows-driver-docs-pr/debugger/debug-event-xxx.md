---
title: デバッグ\_イベント\_XXX
description: デバッグ\_イベント\_XXX 定数は、ターゲットによって生成されるイベント フラグ。
ms.date: 08/13/2018
topic_type:
- apiref
api_name:
- DEBUG_EVENT_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 40d0fbc01267f596d8630eb771d13566b5b41b26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574552"
---
# <a name="debugeventxxx"></a>デバッグ\_イベント\_XXX

次のイベントは、ターゲットによって生成されます。

<table>
<tr>
<th>Flag</th>
<th>IDebugEventCallbacksMethod </th>
<th>イベントの説明</th>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_BREAKPOINT</p>
</td>
<td>
<p><b>IDebugEventCallbacks::Breakpoint</b></p>
</td>
<td>
<p>ターゲットでブレークポイント例外が発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_EXCEPTION</p>
</td>
<td>
<p><b>IDebugEventCallbacks::Exception</b></p>
</td>
<td>
<p>ターゲットで例外デバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CREATE_THREAD</p>
</td>
<td>
<p><b>IDebugEventCallbacks::CreateThread</b></p>
</td>
<td>
<p>ターゲットで、作成スレッドのデバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_EXIT_THREAD</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ExitThread</b></p>
</td>
<td>
<p>ターゲットの終了スレッドのデバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CREATE_PROCESS</p>
</td>
<td>
<p><b>IDebugEventCallbacks::CreateProcess</b></p>
</td>
<td>
<p>ターゲットの作成プロセスのデバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_EXIT_PROCESS</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ExitProcess</b></p>
</td>
<td>
<p>ターゲットの終了プロセスのデバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_LOAD_MODULE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::LoadModule</b></a></p>
</td>
<td>
<p>ターゲットでモジュールの読み込みのデバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_UNLOAD_MODULE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::UnloadModule</b></a></p>
</td>
<td>
<p>ターゲットでモジュールのアンロードのデバッグ イベントが発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_SYSTEM_ERROR</p>
</td>
<td>
<p><b>IDebugEventCallbacks::SystemError</b></a></p>
</td>
<td>
<p>ターゲットでシステム エラーが発生しました。</p>
</td>
</tr>
</table>
<p> </p>
<p>次のイベントは、デバッガー エンジンによって生成されます。</p>
<table>
<tr>
<th>Flag</th>
<th>IDebugEventCallbacksMethod </th>
<th>説明</th>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_SESSION_STATUS</p>
</td>
<td>
<p><b>IDebugEventCallbacks::SessionStatus</b></p>
</td>
<td>
<p>セッションの状態では、変更が発生しました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CHANGE_DEBUGGEE_STATE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ChangeDebuggeeState</b></p>
</td>
<td>
<p>エンジンが行われたまたはターゲットの状態の変更が検出します。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CHANGE_ENGINE_STATE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ChangeEngineState</b></a></p>
</td>
<td>
<p>エンジンの状態が変更されました。</p>
</td>
</tr>
<tr>
<td>
<p>DEBUG_EVENT_CHANGE_SYMBOL_STATE</p>
</td>
<td>
<p><b>IDebugEventCallbacks::ChangeSymbolState</b></a></p>
</td>
<td>
<p>シンボルの状態が変更されました。</p>
</td>
</tr>
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

 

 





