---
title: バグ チェック 0x1C5 IO_THREADPOOL_DEADLOCK_LIVEDUMP
description: IO_THREADPOOL_DEADLOCK_LIVEDUMP のバグ チェックでは、0x000001C5 の値を持ちます。 これは、カーネル モードの threadpool にデッドロックが発生したことを示します。
ms.assetid: CBAB931F-E2A9-4843-9565-DC1CA3B557E6
keywords:
- バグ チェック 0x1C5 IO_THREADPOOL_DEADLOCK_LIVEDUMP
- IO_THREADPOOL_DEADLOCK_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IO_THREADPOOL_DEADLOCK_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e31823fd67d2794ba72c8c8d7706d0606cf8f620
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552237"
---
# <a name="bug-check-0x1c5-iothreadpooldeadlocklivedump"></a>バグ チェック 0x1C5 の。IO\_THREADPOOL\_デッドロック\_LIVEDUMP


IO\_THREADPOOL\_デッドロック\_LIVEDUMP バグ チェックが 0x000001C5 の値を持ちます。 これは、カーネル モードの threadpool にデッドロックが発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="iothreadpooldeadlocklivedump-parameters"></a>IO\_THREADPOOL\_デッドロック\_LIVEDUMP パラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>プールの数。</p>
<p>0x0 :ExPoolUntrusted</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">PEX_WORK_QUEUE へのポインター</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">予約済み</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">予約済み</td>
</tr>
</tbody>
</table>

 

 

 




