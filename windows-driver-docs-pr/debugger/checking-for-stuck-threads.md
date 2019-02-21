---
title: スレッドのスタックのチェック
description: スレッドのスタックのチェック
ms.assetid: ffb1ff13-fc4c-4aaf-a8fe-b473b51b9db0
keywords:
- RPC がスタックしているスレッドのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39db2ef7eb8143fd4d44a7ea384403bea7302eb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552211"
---
# <a name="checking-for-stuck-threads"></a>スレッドのスタックのチェック


## <span id="ddk_checking_for_stuck_threads_dbg"></span><span id="DDK_CHECKING_FOR_STUCK_THREADS_DBG"></span>


RPC では、そのワーカー スレッドが正常に実行するために使用できる必要があります。 一般的な問題は、同じプロセス内でいくつかのコンポーネント (たとえば、ローダー ロックまたはロック ヒープ) は、グローバルのクリティカル セクションのいずれかを保持しているときにデッドロックが発生します。 これにより多くのスレッドがハング - 非常に高い可能性など、一部の RPC ワーカー スレッド。

この場合、RPC サーバーは外部に応答しません。 RPC の呼び出しは RPC を返します\_S\_SERVER\_使用不可] または [RPC\_S\_SERVER\_すぎます\_ビジーです。

同様の問題は、障害のあるドライバーが Irp の完了と、RPC サーバーに到達できないようにする場合に発生します。

これらの問題のいずれかが発生する可能性があると思われる場合を使用させるために、 **-t**スイッチ (を使用して、または、 [ **! rpcexts.getthreadinfo** ](-rpcexts-getthreadinfo.md)拡張機能)。 プロセス ID は、パラメーターとして使用する必要があります。 次の例では、プロセス ID が 0xC4 と想定しています。

```dbgcmd
D:\wmsg>dbgrpc -t -P c4
Searching for thread info ...
## PID  CELL ID   ST TID      LASTTIME
-----------------------------------
00c4 0000.0004 03 0000011c 000f164f
00c4 0000.0007 03 00000120 008a6290
00c4 0000.0015 03 0000018c 008a6236
00c4 0000.0026 03 00000264 0005c443
00c4 0000.002d 03 00000268 000265bb
00c4 0000.0030 03 0000026c 000f1d32
00c4 0000.0034 03 00000388 007251e9
```

TID 列は、各スレッドのスレッド ID を示します。 LASTTIME 列には、各スレッドの状態の最終変更タイムスタンプが含まれています。

サーバーが要求を受信するたびに、状態を変更するには少なくとも 1 つのスレッドと、そのタイムスタンプが更新されます。 そのため、サーバーに対する RPC 要求は、要求が失敗したタイムスタンプのいずれを変更する場合を示します、要求によって RPC ランタイムに実際に到達しないように。 この問題の原因を調査する必要があります。

 

 





