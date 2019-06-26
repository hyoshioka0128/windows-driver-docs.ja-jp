---
title: DPC ルーチンの記述に関するガイドライン
description: DPC ルーチンの記述に関するガイドライン
ms.assetid: 570219be-d152-4826-855a-737bbed67ffd
keywords:
- 遅延プロシージャ呼び出しの WDK カーネル
- Dpc WDK カーネル
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a957d8888e3730e39f10264f734f6111491b4e9e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385255"
---
# <a name="guidelines-for-writing-dpc-routines"></a>DPC ルーチンの記述に関するガイドライン





書き込み時に、次の点を留意してください、 [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)または[ *CustomDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-kdeferred_routine)ルーチン。

-   A *DpcForIsr*または*CustomDpc*ルーチンは、物理デバイスへのアクセスを同期する必要があり、共有状態の情報やリソースにドライバーを使用したドライバーでが維持されるのでその他のルーチンを同じデバイスまたはメモリの場所にアクセスします。

    場合、 *DpcForIsr*または*CustomDpc*ルーチン ISR と、デバイスや状態を共有する、呼び出す必要があります[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)、提供ドライバーによって提供されるアドレス[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンをデバイスのプログラムや、共有状態にアクセスします。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

    場合、 *DpcForIsr*または*CustomDpc*共有状態またはを使用したリソースのどちらを保護する必要があります日常的な共有状態や、インター ロックされたキューまたは ISR、以外のルーチンのタイマー オブジェクトなどのリソースをドライバー初期化 executive スピン ロックします。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

-   *DpcForIsr*と*CustomDpc* IRQL でルーチンの実行のディスパッチを =\_レベルで、呼び出すことができますサポート ルーチンのセットを制限します。

    たとえば、 *DpcForIsr*と*CustomDpc*待つことができないルーチンはアクセスも、ページング可能なメモリの割り当てと[カーネルのディスパッチャー オブジェクト](kernel-dispatcher-objects.md)に設定する、状態を通知します。 取得し、executive スピン ロックのドライバーのリリースの一方で、 [ **KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)と[ **KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)これよりも高速実行**KeAcquireSpinLock**と**KeReleaseSpinLock**します。

    実行する作業項目をキューできます DPC ルーチンでは、ブロッキング呼び出しを行うことはできません、[システム ワーカー スレッド](system-worker-threads.md)IRQL で実行される = パッシブ\_レベル。 作業項目には、ディスパッチャー オブジェクトを待機しているブロックの電話をかけることができます。 作業項目をキューに、 *DpcForIsr*ルーチンで、ルーチンをなど、呼び出す通常[ **IoQueueWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioqueueworkitem)、および*CustomDpc*ルーチン通常、 [ **ExQueueWorkItem** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exqueueworkitem)ルーチン。

-   *DpcForIsr*と*CustomDpc*ルーチンは、通常、デバイスで、[次へ] の I/O 操作を開始します。

    使用して、ダイレクト I/O を使用する最下位レベルの物理的なデバイス ドライバーからこの役割に含めることができます、 [ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンを満たすために多くのデータを転送するデバイスのプログラムをドライバーの呼び出しの前に現在の IRP [**います**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-iostartnextpacket)します。

-   *DpcForIsr*と*CustomDpc*ルーチンで、簡単な期間に対してのみ実行する必要があります、ワーカー スレッドにできるだけ多くの処理を委任する必要があります。

    プロセッサの DPC ルーチンの実行中のすべてのスレッドは、同じプロセッサで実行できなくなります。 その他のキューに置かれ、実行する準備ができている DPC ルーチンは、現在 DPC ルーチンが完了するまで実行をブロックできます。 システムの応答性を低下させることを避けるためには、一般的な DPC ルーチンと呼ばれますありませんそれぞれ 100 を超えるマイクロ秒に実行する必要があります。 タスクが 100 マイクロ秒を超える必要があります、IRQL で実行する必要がある場合は、ディスパッチを =\_レベル、DPC ルーチンは 100 マイクロ秒単位と 1 つまたは複数のスケジュールの後に終了する必要があります[ *CustomTimerDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542983)後でタスクを完了するルーチン。 詳細については*CustomTimerDpc*ルーチンを参照してください[タイマー オブジェクトと Dpc](timer-objects-and-dpcs.md)します。

    DPC ルーチンがディスパッチを実行する必要があるタスクのみを実行する必要があります\_レベル、および委任します IRQL で実行しているスレッドに割り込みに関連する残りのすべての作業 = パッシブ\_レベル。 DPC ルーチンがで実行する作業項目をキューなど、[システム ワーカー スレッド](system-worker-threads.md)します。

    DPC ルーチンを呼び出す、 [ **KeStallExecutionProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-kestallexecutionprocessor)実行を遅延させるルーチンが 100 を超えるマイクロ秒の遅延を指定する必要があります。

    WDK のパフォーマンス分析ツールを使用して、DPC ルーチンの実行時間を評価します。 使用する例については、 [Tracelog](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog)を参照してください DPC 実行時間を監視するためのツール[例 15。/ISR DPC 時間の計測](https://docs.microsoft.com/windows-hardware/drivers/devtest/example-15--measuring-dpc-isr-time)します。

-   ドライバーは、DMA を使用している場合、その[ *AdapterControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_control)ルーチンを返します**KeepObject**または**DeallocateObjectKeepRegisters** (それによって。保持 DMA コント ローラーのチャネルをシステムまたはその他の転送操作のバス マスターのアダプター)、 *DpcForIsr*または*CustomDpc*ルーチンは、アダプターを解放します。オブジェクトまたはマップに登録[ **FreeAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_adapter_channel)または[ **FreeMapRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pfree_map_registers)現在完了前にコントロールの IRP を返します。

-   最下位レベルの物理的なデバイス ドライバーが設定したかどうか、[コント ローラー オブジェクト](using-controller-objects.md)に接続されているデバイスは、コント ローラーからの I/O 操作を同期するその*DpcForIsr*または*CustomDpc*ルーチンは、コント ローラーを使用してオブジェクトを解放[ **IoFreeController** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iofreecontroller)前に、現在の IRP が完了すると、コントロールを返します。

-   *DpcForIsr*と*CustomDpc*ルーチンは、一般に必要であり、可能な場合、現在の要求を再試行して、指定した要求の処理中に発生したデバイスのエラーをログに記録状態の I/O ブロックを設定し、呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)現在 IRP の。

-   ドライバーとデバイスは、重複 I/O 操作をサポートしている場合、ドライバーがの規則に従う必要があります[オーバー ラップ I/O 操作の処理](handling-overlapped-i-o-operations.md)します。

-   *DpcForIsr*または*CustomDpc*任意のドライバーのルーチンの通常のみ、ドライバーをサポートする必要があります public I/O 制御のサブセットは、そのコードの I/O の処理が終了します。 具体的には、DPC ルーチンでは、次の特性を持つデバイス制御要求の処理が実行されます。
    -   物理デバイスの状態を変更要求
    -   本質的に揮発性については、物理デバイスの戻り値を必要とする要求

 

 




