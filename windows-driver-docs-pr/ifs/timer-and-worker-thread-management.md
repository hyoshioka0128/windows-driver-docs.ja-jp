---
title: タイマーとワーカー スレッド管理
description: タイマーとワーカー スレッド管理
ms.assetid: b1feeb4a-0555-4ed6-a26c-ef2a5fc58280
keywords:
- RDBSS WDK ファイル システム、ワーカー スレッド管理
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、ワーカー スレッド管理
- ファイル システムでは、タイマーの RDBSS WDK
- リダイレクトされたサブシステムの WDK のバッファリングをドライブのファイル システム、タイマー
- タイマー WDK RDBSS
- ワーカー スレッドの WDK RDBSS
- WDK RDBSS 1 回限りの通知
- 定期的なトリガー WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4a8dfe208ca36533faa9cb2f4d614ffac96678e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575124"
---
# <a name="timer-and-worker-thread-management"></a>タイマーとワーカー スレッド管理


## <span id="ddk_timer_and_worker_thread_management_if"></span><span id="DDK_TIMER_AND_WORKER_THREAD_MANAGEMENT_IF"></span>


RDBSS は、ワーカー スレッド管理のためのいくつかのタイマー ルーチンを提供します。 これらのサービスは、すべてのネットワーク ミニ リダイレクター ドライバーに提供されます。 次の種類のタイマーのルーチンを使用できます。

-   定期的なトリガー

-   1 回限りの通知

タイマーは、デバイス オブジェクトとワーカー スレッド ルーチンに関連付けられます。 タイマーの期限が切れると、ワーカー スレッド ルーチンが、最初に、入力パラメーターとして渡される**RxPostOneShotTimerRequest**または**RxPostRecurrentTimerRequest**ルーチンが呼び出されます。

次の RDBSS タイマー ルーチンが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルーチン</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553395" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553395)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、タイマーの要求をキャンセルします。 要求をキャンセルするのへのポインター、ルーチンとコンテキスト パラメーターによって識別されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554612" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554612)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、1 回限りのタイマー要求を初期化するために、ドライバーによって使用されます。 このルーチンに渡されるワーカー スレッド ルーチンは、タイマーが期限切れにすると呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff554615" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff554615)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンでは、定期的なタイマー要求を初期化します。 このルーチンに渡されるワーカー スレッド ルーチンが一定の間隔と呼ばれるこのルーチンへの入力パラメーターに基づいた繰り返しタイマーが起動されるときにします。</p></td>
</tr>
</tbody>
</table>

 

 

 




