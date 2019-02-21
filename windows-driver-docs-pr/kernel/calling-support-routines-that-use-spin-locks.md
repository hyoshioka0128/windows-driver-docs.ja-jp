---
title: スピン ロックを使用するサポート ルーチンを呼び出す
description: スピン ロックを使用するサポート ルーチンを呼び出す
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
ms.openlocfilehash: 64aef56ef4001526e43badff3e88767a3aa16c84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549990"
---
# <a name="calling-support-routines-that-use-spin-locks"></a>スピン ロックを使用するサポート ルーチンを呼び出す





呼び出す[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)または[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)ディスパッチに現在のプロセッサ上のIRQLを設定\_レベルに対応する呼び出しまで[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)または[ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130)復元前の IRQL します。 その結果、ドライバーは IRQL で実行する必要があります&lt;= ディスパッチ\_レベルの呼び出し時に**KeAcquireSpinLock**または**KeAcquireInStackQueuedSpinLock**します。

呼び出し元[ **KeAcquireSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551921)、 [ **KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff551908)、 [ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)、および[ **KeReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553150) IRQL で既に実行されているため、高速実行 =ディスパッチ\_のため、これらのルーチンをサポートのレベルが、現在のプロセッサで IRQL にリセットしない必要があります。 したがって、これが致命的なエラーを呼び出すのほとんどの Windows プラットフォームで**KeAcquireSpinLockAtDpcLevel**または**KeAcquireInStackQueuedSpinLockAtDpcLevel** IRQL ディスパッチ未満で実行中に\_レベル。 取得されたスピン ロックを解除するエラーも**KeAcquireSpinLock**呼び出して**KeReleaseSpinLockFromDpcLevel**呼び出し元が元の IRQL が復元されません。

ルーチン、役員を保持するなど、ロックを回転、 <strong>ExInterlocked*Xxx</strong><em>、IRQL で通常実行 = ディスパッチ\_スピン ロックを解放する呼び出し元に制御を返すまでのレベルします。ただし、ドライバーの可能性は[ </em>InterruptService<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff547958>)ルーチンと[ </em>SynchCritSection<em> ](<https://msdn.microsoft.com/library/windows/hardware/ff563928>)するルーチン (DIRQL で実行) されます。呼び出す特定**ExInterlocked</em>Xxx*** ルーチンなど、 **ExInterlocked*Xxx*一覧**ルーチン、スピン限りルーチンに渡されるロックは、ISR によって排他的に使用し、 *SynchCritSection*ルーチン。

関連付けられている割り込みオブジェクトのセットの DIRQL 割り込みスピン ロックを保持する各ルーチンを実行します。 したがって、ドライバーを呼び出す必要がありますいない**KeAcquireSpinLock**と**KeReleaseSpinLock**もその ISR から、executive スピン ロックを使用するその他の任意のルーチンまたは*SynchCritSection*ルーチン。 このような呼び出しは、ユーザーに自分のマシンの再起動を必要とする、システムのデッドロックを引き起こす可能性のあるエラーです。 ドライバーの ISR ことに注意してくださいまたは*SynchCritSection*ルーチンの呼び出し、 **ExInterlocked*Xxx*一覧**、日常的なドライバーを再利用できません、に渡す、スピンロック**ExInterlocked*Xxx*一覧**ルーチンの呼び出しで、 **Ke*Xxx*スピンロック**または**Ke*Xxx*SpinLock*Xxx*DpcLevel**ルーチンをサポートします。

そのルーチンを呼び出すことができる場合、ドライバーは multivector ISR または 1 つ以上の ISR、 [ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302) IRQL で最大の実行中に、 *SynchronizeIrql*値接続されているときに割り込みが関連付けられているオブジェクトに指定します。

 

 




