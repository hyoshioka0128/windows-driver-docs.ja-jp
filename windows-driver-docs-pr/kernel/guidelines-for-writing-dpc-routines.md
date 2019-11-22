---
title: DPC ルーチンの記述に関するガイドライン
description: DPC ルーチンの記述に関するガイドライン
ms.assetid: 570219be-d152-4826-855a-737bbed67ffd
keywords:
- 遅延プロシージャ呼び出し WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b13fe14e4e891198ece076914c961f0f1754dd98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838682"
---
# <a name="guidelines-for-writing-dpc-routines"></a>DPC ルーチンの記述に関するガイドライン





[*DpcForIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine)または[*customdpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine)ルーチンを記述するときは、次の点に注意してください。

-   *DpcForIsr*または*customdpc*ルーチンは、物理デバイスへのアクセス、およびドライバーによって保持されている共有の状態情報またはリソースへのアクセスを同期する必要があります。また、ドライバーのその他のルーチンは、同じデバイスまたはメモリの場所にアクセスします。

    *DpcForIsr*または*customdpc*ルーチンがデバイスまたは状態を ISR と共有している場合は、 [**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出して、デバイスをプログラムしたり、共有状態にアクセスしたりするドライバーによって提供される[*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンのアドレスを指定する必要があります。 詳細については、「[クリティカルセクションの使用](using-critical-sections.md)」を参照してください。

    *DpcForIsr*または*customdpc*ルーチンが、非インタロックキューやタイマーオブジェクトなどの状態またはリソースを、ISR 以外のルーチンを使用して共有している場合、ドライバーで初期化された executive スピンロックで共有状態またはリソースを保護する必要があります。 詳細については、「[スピンロック](spin-locks.md)」を参照してください。

-   *DpcForIsr*および*customdpc*ルーチンは、IRQL = ディスパッチ\_レベルで実行されます。これにより、呼び出し可能な一連のサポートルーチンが制限されます。

    たとえば、 *DpcForIsr*および*customdpc*ルーチンは、ページング可能なメモリにアクセスしたり割り当てたりすることはできません。また、[カーネルディスパッチャーオブジェクト](kernel-dispatcher-objects.md)がシグナル状態に設定されるのを待機することもできません。 その一方で、 [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)と[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)を使用してドライバーの executive スピンロックを取得して解放することができます。この場合、 **KeAcquireSpinLock**と**KeReleaseSpinLock**よりも高速に実行されます。

    DPC ルーチンはブロック呼び出しを行うことができませんが、IRQL = パッシブ\_レベルで実行される[システムワーカースレッド](system-worker-threads.md)で実行されるように、作業項目をキューにすることができます。 作業項目は、ディスパッチャーオブジェクトを待機するブロック呼び出しを行うことができます。 *DpcForIsr*ルーチンは、通常、作業項目をキューに置いて、 [**ioqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)などのルーチンを呼び出します。また、 *customdpc*ルーチンは、通常、 [**exqueueworkitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exqueueworkitem)ルーチンを呼び出します。

-   *DpcForIsr*と*customdpc*ルーチンは、通常、デバイスで次の i/o 操作を開始します。

    ダイレクト i/o を使用する最下位レベルの物理デバイスドライバーでは、 [*SynchCritSection*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine)ルーチンを使用して、ドライバーが[**Iostartnextpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)を呼び出す前に、現在の IRP を満たすために、より多くのデータを転送するようにデバイスをプログラミングすることができます。

-   *DpcForIsr*と*customdpc*ルーチンは短時間だけ実行する必要があり、ワーカースレッドにできるだけ多くの処理を委任する必要があります。

    DPC ルーチンはプロセッサ上で実行されますが、すべてのスレッドが同じプロセッサで実行されることはありません。 キューに登録され、実行準備ができているその他の DPC ルーチンは、現在の DPC ルーチンが終了するまで実行をブロックできます。 システムの応答性が低下しないように、一般的な DPC ルーチンは、呼び出されるたびに100マイクロ秒以内に実行する必要があります。 タスクに100マイクロ秒より長い時間が必要であり、IRQL = ディスパッチ\_レベルで実行する必要がある場合、DPC ルーチンは100マイクロ秒後に終了し、1つ以上の[*Customtimerdpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983)ルーチンが後でタスクを完了するようにスケジュールを設定します。 *Customtimerdpc*ルーチンの詳細については、「 [Timer オブジェクトと dpc](timer-objects-and-dpcs.md)」を参照してください。

    DPC ルーチンは、ディスパッチ\_レベルで実行する必要があるタスクだけを実行し、残りの割り込み関連の作業を IRQL = パッシブ\_レベルで実行されるスレッドに委任する必要があります。 たとえば、DPC ルーチンは、作業項目をキューに置いて、[システムワーカースレッド](system-worker-threads.md)で実行できます。

    [**Kestallexecutionprocessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor)ルーチンを呼び出して実行を遅延させる DPC ルーチンでは、100マイクロ秒を超える遅延を指定することはできません。

    WDK のパフォーマンス分析ツールを使用して、DPC ルーチンの実行時間を評価します。 [トレースログ](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)ツールを使用して dpc の実行時間を監視する例については、「[例 15: Dpc/ISR 時間の測定](https://docs.microsoft.com/windows-hardware/drivers/devtest/example-15--measuring-dpc-isr-time)」を参照してください。

-   ドライバーが DMA を使用し、その[*Adaptercontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control)ルーチンが**KeepObject**または**DeallocateObjectKeepRegisters**を返した場合 (これにより、追加の転送操作のためにシステム DMA コントローラーチャネルまたはバスマスターアダプターが保持されます)、 *DpcForIsr*または*customdpc*ルーチンは、現在の IRP を完了して制御を返す前に、アダプターオブジェクトを解放するか、レジスタを[**Freeadapterchannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel)または[**FreeMapRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers)にマップします。

-   最低レベルの物理デバイスドライバーでコントローラー[オブジェクト](using-controller-objects.md)を設定して、コントローラーを介して接続されているデバイスに i/o 操作を同期させる場合は、その*DpcForIsr*または*customdpc*ルーチンがコントローラーオブジェクトを解放する必要があります。現在の IRP を完了する前に[**IoFreeController**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller)を使用して、制御を返します。

-   *DpcForIsr*および*customdpc*ルーチンは、通常、特定の要求の処理中に発生したデバイスエラーをログに記録し、必要に応じて現在の要求を再試行し、i/o 状態ブロックを設定します。現在の IRP に対して[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出しています。

-   ドライバーとデバイスが重複 i/o 操作をサポートしている場合、ドライバーは、重複 i/o[操作を処理](handling-overlapped-i-o-operations.md)するための規則に従う必要があります。

-   通常、任意のドライバーの*DpcForIsr*または*customdpc*ルーチンは、ドライバーがサポートする必要がある公開 i/o 制御コードのサブセットについてのみ、i/o 処理を完了します。 特に、DPC ルーチンは、次の特性を持つデバイスコントロール要求の操作を完了します。
    -   物理デバイスの状態を変更する要求
    -   物理デバイスに関する本質的に不安定な情報を返す必要がある要求

 

 




