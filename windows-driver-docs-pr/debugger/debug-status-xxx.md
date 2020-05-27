---
title: デバッグ \_ ステータス \_ XXX
description: デバッグ \_ ステータス \_ XXX
ms.assetid: 3f5fcdb6-b4fc-4155-bf39-929d00fb210c
ms.date: 12/07/2017
keywords:
- Windows デバッグの DEBUG_STATUS_XXX
topic_type:
- apiref
api_name:
- DEBUG_STATUS_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 0eecbf3795f7820372ffd6f803c4b366fc035f7a
ms.sourcegitcommit: 2f37e8de9759164804a3b1c7f5c9e497a607539b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/26/2020
ms.locfileid: "83852215"
---
# <a name="debug_status_xxx"></a>デバッグ \_ ステータス \_ XXX


## <span id="ddk_debug_status_xxx_dbx"></span><span id="DDK_DEBUG_STATUS_XXX_DBX"></span>


デバッグ \_ ステータス \_ *XXX*の状態コードには2つの目的があります。 これらは、ターゲットの実行を続行する方法をエンジンに指示し、エンジンがターゲットの実行状態を報告するために使用します。

イベントが発生すると、エンジンは、ターゲットでの実行の進行状況を通知するいくつかの命令を受け取ることができます。 この場合、優先順位が最も高い命令に対して動作します。 通常、優先順位の高いステータスコードは、ターゲットの実行が少ないことを表します。

次の表に示す値は、優先順位に従って逆順に並べられています。テーブルの前に表示されている値の方が優先順位が高くなります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">状態コード</th>
<th align="left">レポート時</th>
<th align="left">指示するタイミング</th>
<th align="left">優先順位</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_NO_DEBUGGEE</p></td>
<td align="left"><p>アクティブなデバッグセッションがありません。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_OUT_OF_SYNC</p></td>
<td align="left"><p>デバッガーの通信チャネルが同期されていません。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_WAIT_INPUT</p></td>
<td align="left"><p>ターゲットは、ユーザーからの入力を待機しています。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_TIMEOUT</p></td>
<td align="left"><p>デバッガー通信チャネルがタイムアウトしました。</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_BREAK</p></td>
<td align="left"><p>ターゲットが中断されています。</p></td>
<td align="left"><p>ターゲットを中断します。</p></td>
<td align="left"><p>最高の優先順位</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_INTO</p></td>
<td align="left"><p>ターゲットが1つの命令を実行しています。</p></td>
<td align="left"><p>1つの命令について、ターゲットの実行を継続します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_STEP_BRANCH</p></td>
<td align="left"><p>ターゲットは次の分岐命令まで実行されています。</p></td>
<td align="left"><p>次の分岐命令までターゲットの実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_OVER</p></td>
<td align="left"><p>ターゲットが1つの命令を実行しているか、その命令がサブルーチン呼び出し--サブルーチンの場合。</p></td>
<td align="left"><p>1つの命令について、ターゲットの実行を継続します。 命令がサブルーチン呼び出しの場合は、呼び出しが入力され、サブルーチンが戻るまでターゲットの実行が許可されます。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO_NOT_HANDLED</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>ターゲットの実行を継続し、イベントを処理しないとしてフラグを付けます。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_GO_HANDLED</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>ターゲットの実行を継続し、イベントを処理済みとしてフラグを付けます。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO</p></td>
<td align="left"><p>ターゲットは正常に実行されています。</p></td>
<td align="left"><p>ターゲットの通常の実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_IGNORE_EVENT</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>イベントを無視して、ターゲットの前の実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_RESTART_REQUESTED</p></td>
<td align="left"><p>ターゲットを再起動しています。</p></td>
<td align="left"><p>ターゲットを再起動します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_NO_CHANGE</p></td>
<td align="left"><p>該当なし</p></td>
<td align="left"><p>命令がありません。 この値は、ターゲットでの実行の続行方法をエンジンに指示しない場合に、イベントコールバックメソッドによって返されます。</p></td>
<td align="left"><p>最も低い優先順位</p></td>
</tr>
</tbody>
</table>

> [!NOTE]
> 状態コードの優先順位は、定数の数値に従っていません。



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
<td align="left">DbgEng .h (DbgEng .h を含む)</td>
</tr>
</tbody>
</table>

 

 





