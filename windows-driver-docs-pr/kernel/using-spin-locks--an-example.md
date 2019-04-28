---
title: スピンを使用する例をロックします。
description: スピンを使用する例をロックします。
ms.assetid: 0f3cd7fe-d3e6-4024-9b2f-7140c6ddd1ea
keywords:
- スピン ロック WDK カーネル
- 割り込みスピン ロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d25aa18c1bfe8cc1b2559ca39013d150d0021cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363822"
---
# <a name="using-spin-locks-an-example"></a>スピン ロックの使用: 例





ドライバーは、スピン ロックの全体的なシステムとドライバーの両方のパフォーマンスが大幅に向上を保持する時間を最小限に抑えます。 たとえば、次の図は、割り込みのスピン ロックで ISR 間で共有されるデバイス固有のデータを保護する方法を示していますと[ *StartIo* ](https://msdn.microsoft.com/library/windows/hardware/ff563858)と[ *DpcForIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff544079) SMP マシンでルーチン。

![割り込みスピン ロックを使用する方法を示す図](images/16ispnlk.png)

1.  ドライバーの ISR の DIRQL で 1 つのプロセッサで実行中にその*StartIo*ディスパッチで実行されるルーチン\_2 つ目のプロセッサのレベル。 カーネルの割り込みハンドラーは、ドライバーのデバイスの拡張機能のドライバーの ISR、(SynchronizeContext) を登録すると、状態、デバイスへのポインターなど、アクセス、デバイス固有の保護されたデータを InterruptSpinLock を保持します。 *StartIo* SynchronizeContext にアクセスする準備ができたら、ルーチンを呼び出す[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)割り込みが関連付けられているオブジェクトへのポインターを渡して、共有 SynchronizeContext、およびドライバーの[ *SynchCritSection* ](https://msdn.microsoft.com/library/windows/hardware/ff563928)ルーチン (前の図の AccessDevice)。

    ドライバーの InterruptSpinLock、解放 ISR が返されるまで **KeSynchronizeExecution * * * をスピン*AccessDevice が SynchronizeContext をタッチするを防ぐ、2 つ目のプロセッサ上。 ただし、 **KeSynchronizeExecution**も IRQL AccessDevice できるようにするため、そのプロセッサの発生を防ぐもう 1 つのデバイスの割り込み、中断オブジェクトの SynchronizeIrql に 2 つ目のプロセッサ上で発生します。DIRQL ISR を返し、すぐに実行します。 ただし、他のデバイス、クロック割り込み、および電源障害の割り込みの高い DIRQL 割り込みは、まだいずれかのプロセッサで発生します。

2.  ときに、ドライバーのキュー、ISR *DpcForIsr* SynchronizeContext にアクセスして、割り込みが関連付けられているオブジェクトの SynchronizeIrql に、2 つ目のプロセッサで実行されている AccessDevice を返します。 その一方で、 *DpcForIsr*ディスパッチに別のプロセッサ上で実行\_IRQL のレベル。 *DpcForIsr*も呼び出すように SynchronizeContext にアクセスする準備ができては**KeSynchronizeExecution**同じパラメーターを使用している、 *StartIo*ルーチンは、手順 1. ででした。

    ときに**KeSynchronizeExecution**スピン ロックを取得し、AccessDevice の代理での実行、 *StartIo*ルーチン、AccessDevice がへの排他アクセスを与え、ドライバーによって提供される同期ルーチンSynchronizeContext します。 AccessDevice 実行されるため、SynchronizeIrql で、ドライバーの ISR はスピン ロックの取得し、AccessDevice の実行中にデバイスが別のプロセッサの割り込み場合でも、スピン ロックが解放されるまで、同じ領域にアクセスできません。

3.  AccessDevice を返します、スピン ロックを解放します。 *StartIo*ルーチンの再開をディスパッチで実行されている\_2 つ目のプロセッサのレベル。 **KeSynchronizeExecution** AccessDevice SynchronizeContext の代理でアクセスできるように、3 つ目のプロセッサで実行できるよう、 *DpcForIsr*します。 ただし、前にデバイスの割り込みが発生した場合、 *DpcForIsr*と呼ばれる**KeSynchronizeExecution**する前に別のプロセッサで実行 ISR ステップ 2 で**KeSynchronizeExecution**スピン ロックの取得し、AccessDevice を 3 つ目のプロセッサで実行できます。

前の図に示す 1 つのプロセッサで実行されているルーチンは、スピン ロックを保持している間、そのスピン ロックを取得しようとしています。 その他のすべてのルーチンの作業がないです。 単に、スピンを既に保持されているロックの取得を日常的な各試行しても、所有者は、スピン ロックを解放するまで、現在のプロセッサ上が回転します。 1 つだけのルーチンがそれを取得できます、スピン ロックが解放されると、同じスピン ロックを取得しようとして現在の他のすべてのルーチンは、スピンし続けます。

発生した IRQL でスピン ロックの所有者が実行されます: のいずれかでディスパッチ\_executive スピン ロックでは、または、DIRQL 割り込みスピン ロックのレベル。 呼び出し元[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)と**KeAcquireInStackQueuedSpinLock**ディスパッチ時に実行\_レベルを呼び出すまで[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)または**KeReleaseInStackQueuedSpinLock**ロックを解除します。 呼び出し元[ **KeSynchronizeExecution** ](https://msdn.microsoft.com/library/windows/hardware/ff553302)呼び出し元が指定されるまで、現在のプロセッサに割り込みオブジェクトの SynchronizeIrql の IRQL を自動的に発生*SynchCritSection*ルーチンが終了し、 **KeSynchronizeExecution**コントロールを返します。 詳細については、次を参照してください。[呼び出しサポート ルーチンを使用してスピン ロック](calling-support-routines-that-use-spin-locks.md)します。

**スピン ロックの使用の詳細については、次の点に注意してください。**

低い IRQL で実行されるすべてのコードでは、すべて同じスピン ロックを取得しようとしています。 その他のルーチンとスピン ロック所有者によって占有されているプロセッサのセットでの作業を取得できません。

その結果、ドライバーは、スピンを保持する時間を最小限に抑えることでドライバーのパフォーマンスが著しく向上結果をロックし、システム全体のパフォーマンスが向上に大きく貢献します。

前の図に示すように、カーネルの割り込みハンドラーは、先着順では、マルチプロセッサ コンピューターで同じ IRQL で実行されているルーチンを実行します。 また、カーネルは、次は。

-   ドライバーのルーチンを呼び出すと**KeSynchronizeExecution**、カーネルがドライバーの*SynchCritSection*元となる、同じプロセッサで実行するルーチンの呼び出し**KeSynchronizeExecution** (手順 1. と 3. を参照してください) が発生しました。

-   ときにドライバーの ISR キューその*DpcForIsr*、カーネルによりを IRQL を下回るディスパッチ最初の利用可能なプロセッサ上で実行する DPC\_レベル。 これは必ずしも元となる同じプロセッサ、 [ **IoRequestDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff549657)呼び出しでは、(手順 2 参照) が発生しました。

ドライバーの割り込み駆動の I/O 操作が単一プロセッサのコンピューターでシリアル化する傾向がありますが、同じ操作を SMP マシンで完全に非同期にすることができます。 前に、SMP コンピューターでドライバーの ISR を CPU4 で実行できる前の図に示すようにその*DpcForIsr*を ISR は既に処理 CPU1 でデバイスの割り込み IRP の処理を開始します。

つまり、ことを想定しないでくださいが割り込み、スピン ロックは、ISR を保存する前に別のプロセッサでデバイスの割り込みが発生したときの ISR によって上書きされない 1 つのプロセッサの実行時に操作に固有のデータを保護できる、 *DpcForIsr*または[ *CustomDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542972)ルーチンを実行します。

ドライバーは、ISR によって収集されたデータを保持するために割り込み駆動 I/O 操作すべてをシリアル化しようとする可能性があります、そのドライバーは非常に高速ユニプロセッサ コンピューターよりも、SMP マシンで実行されません。 ユニプロセッサおよびマルチプロセッサ プラットフォームにわたって抑えながら、最適なドライバー パフォーマンス ポータブルを取得するドライバーは、による後続処理の ISR によって取得操作に固有のデータを保存する別の手法を使用する必要があります、 *DpcForIsr*します。

ISR に渡す IRP の操作に固有のデータを保存するなど、 *DpcForIsr*します。 この手法の洗練化を実装するためには、 *DpcForIsr* count ISR が指定したデータを使用して Irp の処理や、カウントを返す前に 0 にリセットする ISR 拡張の数を調べます。 もちろん、カウントする必要があります、ドライバーの割り込みスピン ロックで保護するための ISR、 *SynchCritSection*はその値を動的に保持します。

 

 




