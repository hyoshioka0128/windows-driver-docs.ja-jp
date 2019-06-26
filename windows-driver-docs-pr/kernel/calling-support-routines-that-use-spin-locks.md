---
title: スピン ロックを使用するサポート ルーチンの呼び出し
description: スピン ロックを使用するサポート ルーチンの呼び出し
ms.assetid: 89cf1fd4-4f4b-4b82-9e50-e5766918c421
keywords:
- KeAcquireSpinLock
- KeAcquireInStackQueuedSpinLock
- スピン ロック WDK カーネル
- スピン ロック サポート ルーチン WDK カーネルの呼び出し
- executive スピン ロック WDK カーネル
- 割り込みスピン ロック WDK カーネル
- スピン ロック WDK カーネルをキューに登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be17e4e695f64b6cc7e10730f6fcc390d9bea3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385259"
---
# <a name="calling-support-routines-that-use-spin-locks"></a>スピン ロックを使用するサポート ルーチンの呼び出し





呼び出す[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)または[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))ディスパッチに現在のプロセッサ上のIRQLを設定\_レベルに対応する呼び出しまで[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)または[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)復元前の IRQL します。 その結果、ドライバーは IRQL で実行する必要があります&lt;= ディスパッチ\_レベルの呼び出し時に**KeAcquireSpinLock**または**KeAcquireInStackQueuedSpinLock**します。

呼び出し元[ **KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)、 [ **KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))、 [ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)、および[ **KeReleaseSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel) IRQL で既に実行されているため、高速実行 =ディスパッチ\_のため、これらのルーチンをサポートのレベルが、現在のプロセッサで IRQL にリセットしない必要があります。 したがって、これが致命的なエラーを呼び出すのほとんどの Windows プラットフォームで**KeAcquireSpinLockAtDpcLevel**または**KeAcquireInStackQueuedSpinLockAtDpcLevel** IRQL ディスパッチ未満で実行中に\_レベル。 取得されたスピン ロックを解除するエラーも**KeAcquireSpinLock**呼び出して**KeReleaseSpinLockFromDpcLevel**呼び出し元が元の IRQL が復元されません。

ルーチン、役員を保持するなど、ロックを回転、 <strong>ExInterlocked*Xxx</strong><em>、IRQL で通常実行 = ディスパッチ\_スピン ロックを解放する呼び出し元に制御を返すまでのレベルします。ただし、ドライバーの可能性は[ </em>InterruptService<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff547958>)ルーチンと[ </em>SynchCritSection<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff563928>)するルーチン (DIRQL で実行) されます。呼び出す特定**ExInterlocked</em>Xxx*** ルーチンなど、 **ExInterlocked*Xxx*一覧**ルーチン、スピン限りルーチンに渡されるロックは、ISR によって排他的に使用し、 *SynchCritSection*ルーチン。

関連付けられている割り込みオブジェクトのセットの DIRQL 割り込みスピン ロックを保持する各ルーチンを実行します。 したがって、ドライバーを呼び出す必要がありますいない**KeAcquireSpinLock**と**KeReleaseSpinLock**もその ISR から、executive スピン ロックを使用するその他の任意のルーチンまたは*SynchCritSection*ルーチン。 このような呼び出しは、ユーザーに自分のマシンの再起動を必要とする、システムのデッドロックを引き起こす可能性のあるエラーです。 ドライバーの ISR ことに注意してくださいまたは*SynchCritSection*ルーチンの呼び出し、 **ExInterlocked*Xxx*一覧**、日常的なドライバーを再利用できません、に渡す、スピンロック**ExInterlocked*Xxx*一覧**ルーチンの呼び出しで、 **Ke*Xxx*スピンロック**または**Ke*Xxx*SpinLock*Xxx*DpcLevel**ルーチンをサポートします。

そのルーチンを呼び出すことができる場合、ドライバーは multivector ISR または 1 つ以上の ISR、 [ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution) IRQL で最大の実行中に、 *SynchronizeIrql*値接続されているときに割り込みが関連付けられているオブジェクトに指定します。

 

 




