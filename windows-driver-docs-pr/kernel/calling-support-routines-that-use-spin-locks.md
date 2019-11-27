---
title: スピン ロックを使用するサポート ルーチンの呼び出し
description: スピン ロックを使用するサポート ルーチンの呼び出し
ms.assetid: 89cf1fd4-4f4b-4b82-9e50-e5766918c421
keywords:
- KeAcquireSpinLock
- KeAcquireInStackQueuedSpinLock
- スピンロック WDK カーネル
- スピンロックサポートルーチンの呼び出し (WDK カーネル)
- executive スピンロック WDK カーネル
- 割り込みスピンロックの WDK カーネル
- キューに置かれたスピンロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f490804b9045e7488dcee7255e8348eb24e62c1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837133"
---
# <a name="calling-support-routines-that-use-spin-locks"></a>スピン ロックを使用するサポート ルーチンの呼び出し





[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)または[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))を呼び出すと、 [**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)または[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)への対応する呼び出しまで、現在のプロセッサの IRQL が\_レベルをディスパッチするように設定されます。以前の IRQL を復元します。 そのため、 **KeAcquireSpinLock**または**KeAcquireInStackQueuedSpinLock**を呼び出すと、ドライバーは IRQL &lt;= ディスパッチ\_レベルで実行されている必要があります。

[**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)、 [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))、 [**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)、 [**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)の呼び出し元は、既に存在するため、より高速に実行されます。IRQL = ディスパッチ\_レベルで実行すると、これらのサポートルーチンは現在のプロセッサで IRQL をリセットする必要がありません。 そのため、ほとんどの Windows プラットフォームでは、ディスパッチ\_レベルよりも IRQL が低い状態で実行中に**KeAcquireSpinLockAtDpcLevel**または**KeAcquireInStackQueuedSpinLockAtDpcLevel**を呼び出すことが致命的なエラーになります。 また、呼び出し元の元の IRQL が復元されないため、 **KeReleaseSpinLockFromDpcLevel**を呼び出すことによって**KeAcquireSpinLock**で取得されたスピンロックを解放することもできません。

Exinterlocked ロック Xxx などの executive スピンロックを保持するルーチン<strong> *</strong><em>は、通常、スピンロックを解除して制御を呼び出し元に返すまで、IRQL = ディスパッチ\_レベルで実行されます。ただし、 [ </em><em> ](<https://msdn.microsoft.com/library/windows/hardware/ff547958>) [ </em><em> ](<https://msdn.microsoft.com/library/windows/hardware/ff563928>)ルーチンに渡されたスピンロックが ISR ルーチンと SynchCritSection ルーチンで排他的に使用されている場合に限り、ドライバーの InterruptService ルーチンと SynchCritSection ルーチン (dirql で実行されるルーチン) が、 **</em>***  Exinterlocked ロック xxx の**リスト**ルーチンなどの特定の exinterlocked ロック xxx ルーチンを呼び出すことができます。

割り込みスピンロックを保持する各ルーチンは、割り込みオブジェクトの関連付けられたセットの DIRQL で実行されます。 そのため、ドライバーは**KeAcquireSpinLock**と**KERELEASESPINLOCK** 、および ISR または*SynchCritSection*ルーチンから executive スピンロックを使用するその他のルーチンを呼び出すことはできません。 このような呼び出しは、システムのデッドロックを引き起こす可能性があるエラーであり、ユーザーは自分のコンピューターを再起動する必要があります。 ドライバーの ISR または*SynchCritSection*ルーチンが**Exinterlocked ロック*xxx*リスト**ルーチンを呼び出すと、ドライバーは、 **Ke*xxx*スピンロック**または**ke*Xxx*スピンロック*xxx*DpcLevel**サポートルーチンの呼び出しで、 **exinterlocked ロック*xxx*リスト**ルーチンに渡すスピンロックを再利用できないことに注意してください。

ドライバーに multivector ISR または複数の ISR がある場合、そのルーチンは、接続されているときに、関連付けられている割り込みオブジェクトに対して指定された*SynchronizeIrql*値までの IRQL で実行中に[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出すことができます。

 

 




