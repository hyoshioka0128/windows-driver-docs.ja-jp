---
title: タイマーとワーカー スレッド管理
description: タイマーとワーカー スレッド管理
ms.assetid: b1feeb4a-0555-4ed6-a26c-ef2a5fc58280
keywords:
- RDBSS WDK ファイルシステム、ワーカースレッド管理
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、ワーカースレッド管理
- RDBSS WDK ファイルシステム、タイマー
- リダイレクトされたドライブバッファリングサブシステム WDK ファイルシステム、タイマー
- タイマー WDK RDBSS
- ワーカースレッドの WDK RDBSS
- ワンショット通知 WDK RDBSS
- 定期トリガー WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3891d198a2dcc05650b99d96d57f1cfb2ee15258
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840951"
---
# <a name="timer-and-worker-thread-management"></a>タイマーとワーカー スレッド管理


## <span id="ddk_timer_and_worker_thread_management_if"></span><span id="DDK_TIMER_AND_WORKER_THREAD_MANAGEMENT_IF"></span>


RDBSS には、ワーカースレッド管理用のタイマールーチンがいくつか用意されています。 これらのサービスは、すべてのネットワークミニリダイレクタードライバーに提供されます。 次の種類のタイマールーチンを使用できます。

-   定期的なトリガー

-   ワンショット通知

タイマーは、デバイスオブジェクトとワーカースレッドルーチンに関連付けられています。 タイマーが期限切れになると、最初の**RxPostOneShotTimerRequest**または**RxPostRecurrentTimerRequest**ルーチンに入力パラメーターとして渡されたワーカースレッドルーチンが呼び出されます。

次の RDBSS timer ルーチンが含まれています。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、タイマー要求をキャンセルします。 キャンセルされる要求は、ルーチンへのポインターとコンテキストパラメーターによって識別されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、ドライバーがワンショットタイマー要求を初期化するために使用されます。 タイマーの有効期限が切れると、このルーチンに渡されるワーカースレッドルーチンが1回呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>このルーチンは、定期的なタイマー要求を初期化します。 このルーチンに渡されるワーカースレッドルーチンは、このルーチンへの入力パラメーターに基づいて定期的なタイマーが起動されると、一定の間隔で呼び出されます。</p></td>
</tr>
</tbody>
</table>

 

 

 




