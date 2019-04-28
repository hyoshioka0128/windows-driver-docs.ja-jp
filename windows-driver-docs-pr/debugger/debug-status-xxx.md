---
title: デバッグ\_状態\_XXX
description: デバッグ\_状態\_XXX
ms.assetid: 3f5fcdb6-b4fc-4155-bf39-929d00fb210c
ms.date: 12/07/2017
keywords:
- DEBUG_STATUS_XXX Windows Debugging
topic_type:
- apiref
api_name:
- DEBUG_STATUS_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 0d519107896a617b3d66091ff2f16a4e447b5434
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374836"
---
# <a name="debugstatusxxx"></a>デバッグ\_状態\_XXX


## <span id="ddk_debug_status_xxx_dbx"></span><span id="DDK_DEBUG_STATUS_XXX_DBX"></span>


デバッグ\_状態\_*XXX*状態コードの 2 つの目的があります。 ターゲットで実行する必要があります続行方法をエンジンに指示して、ターゲットの実行状態をレポートに、エンジンによって使用されます。

イベントの発生後に、エンジンは、ターゲットの実行を続ける方法を指定するいくつかの手順を受信できます。 この場合は、機能、命令で優先順位が最も高いします。 通常より高い優先順位の状態コードは、ターゲットの少ない実行を表します。

次の表に、値はリバース; の優先順位によって順序付け前の表に表示される値では、高い優先順位があります。

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
<th align="left">レポートするときに</th>
<th align="left">指示するときに</th>
<th align="left">優先度</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_NO_DEBUGGEE</p></td>
<td align="left"><p>デバッグ セッションがアクティブではありません。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_OUT_OF_SYNC</p></td>
<td align="left"><p>デバッガーの通信チャネルは同期されていません。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_WAIT_INPUT</p></td>
<td align="left"><p>ターゲットは、ユーザーからの入力を待機しています。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_TIMEOUT</p></td>
<td align="left"><p>デバッガーの通信チャネルがタイムアウトしました。</p></td>
<td align="left"><p>なし</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_BREAK</p></td>
<td align="left"><p>ターゲットは中断されます。</p></td>
<td align="left"><p>ターゲットを中断します。</p></td>
<td align="left"><p>最高の優先順位</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_INTO</p></td>
<td align="left"><p>ターゲットは、1 つの命令を実行しています。</p></td>
<td align="left"><p>1 つの命令のターゲットの実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_STEP_BRANCH</p></td>
<td align="left"><p>ターゲットは、次の分岐命令まで実行しています。</p></td>
<td align="left"><p>[次へ] の分岐命令まで、ターゲットの実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_STEP_OVER</p></td>
<td align="left"><p>ターゲットが 1 つの命令を実行する命令がサブルーチンの呼び出し - または--サブルーチンです。</p></td>
<td align="left"><p>1 つの命令のターゲットの実行を続行します。 命令がサブルーチンの呼び出しの場合は、呼び出しを入力し、ターゲットのサブルーチンを返すまでの実行が許可されます。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO_NOT_HANDLED</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>未処理の例外として、イベントにフラグを設定、ターゲットの実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_GO_HANDLED</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>イベントを処理済みとしてフラグ設定、ターゲットの実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_STATUS_GO</p></td>
<td align="left"><p>通常は、ターゲットを実行します。</p></td>
<td align="left"><p>ターゲットの通常の実行を続行します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_STATUS_IGNORE_EVENT</p></td>
<td align="left"><p>なし</p></td>
<td align="left"><p>イベントを無視して、ターゲットの前回の実行を続行します。</p></td>
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
<td align="left"><p>なし</p></td>
<td align="left"><p>いない命令です。 ターゲットの実行を続行する方法をエンジンに指示する望んでいない場合、イベントのコールバック メソッドでこの値が返されます。</p></td>
<td align="left"><p>最低の優先順位</p></td>
</tr>
</tbody>
</table>

 

&gt; \[!注\]&gt;状態コードの優先順位が定数の数値の値に従っていません。

 

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

 

 





