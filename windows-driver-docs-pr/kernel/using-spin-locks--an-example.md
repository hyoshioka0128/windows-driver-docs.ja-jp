---
title: スピンロックの使用例
description: スピンロックの使用例
ms.assetid: 0f3cd7fe-d3e6-4024-9b2f-7140c6ddd1ea
keywords:
- スピンロック WDK カーネル
- 割り込みスピンロックの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfe8f37aed5dc5ee1ba8f4c86805beef34281d75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838335"
---
# <a name="using-spin-locks-an-example"></a>スピンロックの使用: 例





ドライバーがスピンロックを保持する時間を最小限に抑えることで、ドライバーとシステム全体の両方のパフォーマンスを大幅に向上させることができます。 たとえば、次の図について考えてみます。これは、割り込みスピンロックが、ISR と、SMP コンピューターの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)および[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)ルーチン間で共有する必要があるデバイス固有のデータを保護する方法を示しています。

![割り込みスピンロックの使用を示す図](images/16ispnlk.png)

1.  ドライバーの ISR は、1つのプロセッサ上の DIRQL で実行されますが、 *StartIo*ルーチンは、2番目のプロセッサでディスパッチ\_レベルで実行されます。 カーネル割り込みハンドラーは、ドライバーの ISR の InterruptSpinLock を保持します。この ISR は、ドライバーのデバイス拡張機能で、デバイスレジスタ (SynchronizeContext) などの保護されたデバイス固有のデータにアクセスします。 SynchronizeContext にアクセスする準備が整った*StartIo*ルーチンは、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出し、関連付けられている割り込みオブジェクト、共有 SynchronizeContext、およびドライバーの[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンへのポインターを渡します (前の図の AccessDevice)。

    ISR が戻るまで、ドライバーの InterruptSpinLock を解放すると、**KeSynchronizeExecution * ** * は2番目のプロセッサで回転し、Accessdevice が SynchronizeContext にタッチするのを防ぎます。 ただし、 **KeSynchronizeExecution**は、2番目のプロセッサで割り込みオブジェクトの SynchronizeIrql に対して IRQL を発生させます。これにより、そのプロセッサで別のデバイスの割り込みが発生するのを防ぐことができます。これにより、accessdevice は、ISR はを返します。 ただし、その他のデバイスに対する DIRQL 割り込みが高い場合、クロック割り込みが発生し、電源障害が発生しても、どちらのプロセッサでも発生する可能性があります。

2.  ISR がドライバーの*DpcForIsr*をキューに入れ、を返した場合、accessdevice は、関連付けられている割り込みオブジェクトの SynchronizeIrql にある2番目のプロセッサで実行され、SynchronizeContext にアクセスします。 一方、 *DpcForIsr*はディスパッチ\_レベル IRQL で別のプロセッサで実行されます。 また、 *DpcForIsr*は SynchronizeContext にアクセスする準備が整っているため、手順 1. で*StartIo*ルーチンが行ったのと同じパラメーターを使用して**KeSynchronizeExecution**を呼び出します。

    **KeSynchronizeExecution**がスピンロックを取得し、 *StartIo*ルーチンの代わりに accessdevice を実行すると、ドライバーによって指定された同期ルーチン accessdevice に SynchronizeContext への排他アクセスが付与されます。 AccessDevice は SynchronizeIrql で実行されるので、デバイスが AccessDevice の実行中に別のプロセッサで割り込みを行う場合でも、ドライバーの ISR はスピンロックを取得して同じ領域にアクセスすることはできません。

3.  AccessDevice が戻ると、スピンロックが解除されます。 *StartIo*ルーチンは、2番目のプロセッサでディスパッチ\_レベルで実行を再開します。 **KeSynchronizeExecution**は3番目のプロセッサで accessdevice を実行するようになったため、 *DpcForIsr*に代わって SynchronizeContext にアクセスできるようになりました。 ただし、手順 2. で**KeSynchronizeExecution**という*DpcForIsr*が呼び出される前にデバイスの割り込みが発生していた場合は、 **KeSynchronizeExecution**がスピンロックを取得して、accessdevice を3番目のプロセッサ。

前の図に示すように、1つのプロセッサで実行されているルーチンはスピンロックを保持していますが、そのスピンロックを取得しようとしている他のすべてのルーチンは処理を行いません。 既に保持されているスピンロックを取得しようとする各ルーチンは、その所有者がスピンロックを解放するまで、現在のプロセッサを単にスピンさせます。 スピンロックが解放されると、1つのルーチンだけが取得できるようになります。現在同じスピンロックを取得しようとしている他のすべてのルーチンは、引き続きスピンを行います。

任意のスピンロックの所有者は、発生した IRQL で実行されます。たとえば、executive スピンロックの場合はディスパッチ\_レベル、割り込みスピンロックの場合は DIRQL です。 [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)と**KeAcquireInStackQueuedSpinLock**の呼び出し元は、 [**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)または**KeReleaseInStackQueuedSpinLock**を呼び出してロックを解除するまで、ディスパッチ\_レベルで実行されます。 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)の呼び出し元は、呼び出し元が指定した*SynchCritSection*ルーチンが終了し、 **KeSynchronizeExecution**が返されるまで、割り込みオブジェクトの SynchronizeIrql に対して現在のプロセッサの IRQL を自動的に発生させます。制御. 詳細については、「[スピンロックを使用するサポートルーチンの呼び出し](calling-support-routines-that-use-spin-locks.md)」を参照してください。

**スピンロックの使用については、次の点に注意してください。**

低い IRQL で実行されるすべてのコードは、スピンロックの所有者と、同じスピンロックを取得しようとする他のルーチンによって実行されるプロセッサセットに対して実行される処理を取得できません。

その結果、ドライバーがスピンロックを保持する時間を最小限に抑えると、ドライバーのパフォーマンスが大幅に向上し、システム全体のパフォーマンスが大幅に向上します。

前の図に示すように、カーネル割り込みハンドラーは、最初に提供された、マルチプロセッサコンピューターで同じ IRQL で実行されるルーチンを実行します。 カーネルは次のことも行います。

-   ドライバールーチンが**KeSynchronizeExecution**を呼び出すと、カーネルによって、ドライバーの*SynchCritSection*ルーチンが**KeSynchronizeExecution**の呼び出しが発生したのと同じプロセッサ上で実行されます (手順1と3を参照)。

-   ドライバーの ISR がその*DpcForIsr*をキューに入れた場合、カーネルは、IRQL がディスパッチ\_レベルを下回る最初の使用可能なプロセッサ上で DPC を実行します。 これは、必ずしも[**IoRequestDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdpc)呼び出しが発生したプロセッサと同じではありません (手順2を参照)。

ドライバーの割り込みドリブン i/o 操作は、ユニプロセッサコンピューターではシリアル化される傾向がありますが、SMP コンピューターでは、同じ操作を実際に非同期に行うことができます。 前の図に示されているように、ドライバーの ISR は、SMP コンピューターの CPU4 で実行され、ISR が CPU1 のデバイス割り込みを既に処理している IRP の処理を開始する前に、その*DpcForIsr*が SMP マシンで実行される可能性があります。

つまり、 *DpcForIsr*の前に別のプロセッサでデバイスの割り込みが発生したときに、isr が1つのプロセッサで実行したときに、isr によって上書きされない操作固有のデータを、割り込みスピンロックで保護できると想定しないでください。または[*Customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンが実行されています。

ドライバーは、すべての割り込みドリブン i/o 操作をシリアル化して、ISR によって収集されたデータを保持することもできますが、SMP コンピューターでは、そのドライバーはユニプロセッサコンピューターよりもはるかに高速に実行されません。 ユニプロセッサおよびマルチプロセッサプラットフォーム間で移植性を維持したまま、最適なドライバーパフォーマンスを得るには、ドライバーは他の手法を使用して、 *DpcForIsr*による後続の処理のために ISR によって取得された操作固有のデータを保存する必要があります。

たとえば、ISR は、 *DpcForIsr*に渡す IRP に操作固有のデータを保存できます。 この手法を改良することは、ISR によって強化された数を調べ、ISR が提供するデータを使用して Irp の数を処理し、カウントをゼロにリセットしてから戻る前に、 *DpcForIsr*を実装することです。 もちろん、このカウントは、ISR と*SynchCritSection*が動的に値を維持するため、ドライバーの割り込みスピンロックによって保護されている必要があります。

 

 




