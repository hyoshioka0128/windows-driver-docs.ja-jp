---
title: タイマーのシステムによって割り当てられたオブジェクトの削除
description: Windows 8.1 以降、ExDeleteTimer ルーチンは ExAllocateTimer ルーチンによって作成されたタイマー オブジェクトを削除します。
ms.assetid: 7D119448-3890-4E8F-BC79-7FEB3213B693
keywords:
- ExXxxTimer ルーチン
- ExAllocateTimer
- ExDeleteTimer
- ExSetTimer
- ExCancelTimer
- ExTimerCallback
- ExTimerDeleteCallback
- EX_TIMER
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e5af582c1926f1222f53050f749438548dea06
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557555"
---
# <a name="deleting-a-system-allocated-timer-object"></a>タイマーのシステムによって割り当てられたオブジェクトの削除


Windows 8.1 では、以降、 [ **ExDeleteTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265181)ルーチンによって作成されたタイマー オブジェクトの削除、 [ **ExAllocateTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265179)ルーチンです。 このタイマー オブジェクトは、システムによって割り当てられた[ **EX\_タイマー** ](https://msdn.microsoft.com/library/windows/hardware/dn265199)のメンバーは、ドライバーを非透過構造体。 タイマー オブジェクトを削除すると、前に**ExDeleteTimer**さらに、オブジェクトに対する操作をタイマーを無効にし、キャンセルまたは保留中の進行中の可能性のあるオブジェクトの操作が完了するとします。

ドライバーを呼び出してから**ExDeleteTimer**、このルーチンは、いくつかの手順をタイマー オブジェクトを安全に削除できることを確認します。 まず、 **ExDeleteTimer**ドライバーが、オブジェクトを使用して、新しいタイマー操作を開始するを防ぐために無効になっている、タイマー オブジェクトをマークします。 タイマー オブジェクトを無効にするへの呼び出し、 [ **ExSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265188)または[ **ExCancelTimer** ](https://msdn.microsoft.com/library/windows/hardware/dn265180)ルーチンがを直ちに返します**FALSE**演算を実行しないとします。 2 番目の呼び出しにも、 **ExDeleteTimer**返します**FALSE**演算を実行しないとします。

次に、 **ExDeleteTimer**タイマーがかどうかを確認します。 以前の呼び出しから保留中のままで**ExDeleteTimer**します。 タイマー オブジェクトを無効にする場合は、オブジェクトが無効になる前に設定されたタイマーは取り消されません。 次の 2 つのケースのいずれか、タイマー オブジェクトを無効にした後、設定されているタイマーが期限切れ。

-   タイマーは、定期的なです。
-   タイマーが 1 回限り (または非連続) と、まだ切れていません。

定期的なタイマーはことができます、タイマー オブジェクトを無効にした後で 2 回以上有効期限はありません。

ドライバーが実装されている場合、 [ *ExTimerCallback* ](https://msdn.microsoft.com/library/windows/hardware/dn265190)コールバック ルーチン、*タイマー*タイマーを有効なポインター オブジェクト (が常にこのルーチンへのパラメーターのことが保証されます**EX\_タイマー**構造) タイマーが切れたタイマー オブジェクトを無効にした後場合でも、します。

タイマーが保留中でない場合**ExDeleteTimer**タイマー オブジェクトを削除し、待機せずに戻ります。

場合は、タイマーは保留中のときに、 **ExDeleteTimer**を呼び出すと、*キャンセル*と*待機*このルーチンには、ドライバーが提供されるパラメーターの値は、ルーチンの動作を制御します。 *キャンセル*パラメーターは指示**ExDeleteTimer**保留中のタイマーをキャンセルしようとするかどうか。 *待機*パラメーターは指示**ExDeleteTimer**を返す、タイマー オブジェクトが削除されるまで待機するかどうか。

場合*キャンセル*は**FALSE** (この場合は、*待機*必要があります**FALSE**)、タイマーが保留中、および**ExDeleteTimer**、タイマー、タイマー オブジェクトを削除する前に有効期限が切れることができます。 この場合、 **ExDeleteTimer**保留中のタイマーの期限が切れた後に削除することを示す、タイマー オブジェクトをマーク (および、最後のコールバックを*ExTimerCallback*ルーチンが完了すると)。 **ExDeleteTimer**タイマーが期限切れにする [完了]、または削除するオブジェクトを待機せずに戻ります。

場合*キャンセル*は**TRUE**、 **ExDeleteTimer**有効期限が切れる前に、保留中のタイマーをキャンセルしようとしています。 **ExDeleteTimer**返します**TRUE**タイマーを正常にキャンセルした場合。 **ExDeleteTimer**返します**FALSE**ワンショット タイマーを既に切れているかが期限切れにならない処理中の場合、タイマーを取り消すことはできないかどうか。 **ExDeleteTimer**も返します**FALSE** (1 回限りまたは定期的な) タイマーをする前にキャンセルされたかどうか、 **ExDeleteTimer**呼び出しまたはタイマーが設定されていないかどうか。

場合*キャンセル*は**TRUE**と*待機*は**FALSE**、 **ExDeleteTimer**呼び出し元のスレッドをブロックしません。 タイマー オブジェクトを直ちに削除できない場合**ExDeleteTimer**保留中のタイマーは、期限切れにならないが完了した後に削除することを示す、タイマー オブジェクトをマークし、タイマーがいずれかを待機することがなくすぐに返します有効期限が切れる、または削除するオブジェクト。

場合*キャンセル*と*待機*はどちらも**TRUE**、 **ExDeleteTimer**タイマー オブジェクトを直ちに削除できない場合は、呼び出し元のスレッドをブロック. **ExDeleteTimer** 、タイマーが期限切れにならないを完了し、ドライバーに実装する任意のコールバックの必要な場合、待機*ExTimerCallback*ルーチンを完了します。 次に、 **ExDeleteTimer**タイマー オブジェクトと呼び出しを削除、 [ *ExTimerDeleteCallback* ](https://msdn.microsoft.com/library/windows/hardware/dn265192)ルーチン、ドライバーは、このルーチンを実装している場合。 最後に、 **ExDeleteTimer**を返します。

ドライバーを呼び出すことができます**ExDeleteTimer**からドライバーの*ExTimerCallback* IRQL で実行されるルーチンは、ディスパッチ =\_レベルでは、ドライバーを設定する必要があります、*待機*この呼び出しでパラメーター **FALSE**します。

オプションとして、ドライバーを実装できる、 *ExTimerDeleteCallback*タイマー オブジェクトを削除した後に実行するコールバック ルーチン。 通常、 *ExTimerDeleteCallback*ルーチンは、タイマー オブジェクトを使用するドライバーが割り当てられているシステム リソースを解放します。

**ExDeleteTimer**ドライバー実装をスケジュール*ExTimerDeleteCallback*タイマー オブジェクトが削除された後に実行する日常的などの時点でこのオブジェクトへのポインターが無効になっています。 場合、*待機*パラメーターが**TRUE**で、 **ExDeleteTimer**へのコールバックを呼び出す、 *ExTimerDeleteCallback*ルーチンが完了します。前に**ExDeleteTimer**を返します。 場合*待機*は**FALSE**、 *ExTimerDeleteCallback*ルーチンが前に、または後に実行が**ExDeleteTimer**を返します。

詳細については、次を参照してください。 [Ex*Xxx*タイマー ルーチンと EX\_タイマー オブジェクト](exxxxtimer-routines-and-ex-timer-objects.md)します。

 

 




