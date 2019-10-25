---
title: 割り込みコードの同期
description: 割り込みコードの同期
ms.assetid: a24477dc-f75d-4ab6-8695-d8a85247e276
keywords:
- ハードウェア割り込み WDK KMDF、同期
- WDK KMDF の割り込み、同期
- WDK 割り込みの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf9dbb9b423745ed8e17611476428a7fd45f300a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831622"
---
# <a name="synchronizing-interrupt-code"></a>割り込みコードの同期


次の要因により、マルチプロセッサシステムでハードウェア割り込みを処理するドライバーコードが複雑になります。

-   デバイスが割り込みを行うたびに、デバイスが次に割り込みを行ったときに上書きされる可能性があるため、揮発性の割り込み固有の情報が提供されます。

-   比較的高 IRQLs のデバイスが中断され、割り込みサービスルーチン (Isr) によって、他のドライバーコードの実行が中断されることがあります。

-   DIRQL 割り込みの場合、ISR はドライバーが提供するスピンロックを保持した状態で DIRQL で実行する必要があります。これにより、ISR は、揮発性の情報を保存している間に追加の割り込みを防ぐことができます。 DIRQL は、現在のプロセッサによる中断を防ぎ、スピンロックは別のプロセッサによる中断を防ぎます。

-   Isr の実行中にデバイスが中断できないため、ISR を迅速に実行する必要があります。 ISR の実行時間が長いと、システムの速度が低下するか、データが失われる可能性があります。

-   ISR と遅延プロシージャ呼び出し (DPC) ルーチンは、通常、ISR がデバイスの揮発性データを格納するストレージ領域にアクセスする必要があります。 これらのルーチンは、ストレージ領域に同時にアクセスしないように、互いに同期させる必要があります。

これらの要因のすべてにより、割り込みを処理するドライバーコードを記述するときに、次の規則を使用する必要があります。

-   [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数だけが、割り込み情報を含むデバイスレジスタなど、揮発性の割り込みデータにアクセスします。

    [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は、ドライバーによって定義された割り込みデータバッファーに、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数、 [*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) callback 関数、または multiple[*で揮発性データを移動する必要があります。EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数はにアクセスできます。

    ドライバーが割り込みオブジェクトに対して[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数を提供している場合、割り込みデータを格納する最適な場所は、割り込みオブジェクトの[コンテキスト空間](framework-object-context-space.md)です。 割り込みオブジェクトのコールバック関数は、受け取ったオブジェクトハンドルを使用して、オブジェクトのコンテキスト空間にアクセスできます。

    ドライバーが各[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数に対して複数の[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数を提供している場合は、各 DPC オブジェクトのコンテキスト空間に割り込みデータを格納できます。

-   割り込みデータバッファーにアクセスするすべてのドライバーコードは、一度に1つのルーチンのみがデータにアクセスするように同期する必要があります。

    DIRQL interrupt オブジェクトの場合、 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は、割り込みオブジェクトのドライバーによって提供されるスピンロックを保持した状態で、IRQL = dirql でこのデータバッファーにアクセスします。 そのため、バッファーにアクセスするすべてのルーチンは、スピンロックを保持しながら、DIRQL でも実行する必要があります。 (通常、割り込みの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) callback 関数は、バッファーにアクセスする必要がある唯一のルーチンです)。

    [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数を除く、割り込みデータバッファーにアクセスするすべてのルーチンは、次のいずれかを実行する必要があります。

    -   [**WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)を呼び出して、割り込みデータバッファーにアクセスする[*EvtInterruptSynchronize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_synchronize)コールバック関数をスケジュールします。
    -   [**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)と[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)の呼び出しの間の割り込みデータバッファーにアクセスするコードを配置します。

    どちらの方法でも、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)関数は、割り込みのスピンロックを保持しながら、dirql の割り込みデータにアクセスできます。 DIRQL は、現在のプロセッサによる中断を防ぎ、スピンロックは別のプロセッサによる中断を防ぎます。

    デバイスが複数の割り込みベクターまたはメッセージをサポートしていて、ドライバーの割り込み処理を同期する場合は、1つのスピンロックを複数の DIRQL 割り込みオブジェクトに割り当てることができます。 このフレームワークは、割り込みセットの最大の DIRQL を特定し、その DIRQL のスピンロックを常に取得します。これにより、セット内の割り込みベクターやメッセージによって同期されたコードを中断できなくなります。

    [パッシブレベルの割り込みオブジェクト](supporting-passive-level-interrupts.md)の場合、このフレームワークは、IRQL = パッシブ\_レベルでドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数を呼び出す前に、パッシブレベルの割り込みロックを取得します。 その結果、バッファーにアクセスするすべてのルーチンは、割り込みロックを取得するか、または内部的にバッファーアクセスを同期する必要があります。 通常、割り込みの[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) callback 関数は、バッファーにアクセスする唯一のルーチンです。 *EvtInterruptWorkItem* callback 関数から割り込みロックを取得する方法の詳細については、そのページの「解説」を参照してください。

    また、1つの待機ロックを複数のパッシブレベルの割り込みオブジェクトに割り当てることによって、ドライバーの複数の割り込みベクターの処理を同期させることもできます。

-   DIRQL 割り込みを処理するコードの一部を IRQL = パッシブ\_レベルで実行する必要がある場合は、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc) callback 関数で1つ以上の[作業項目](using-framework-work-items.md)を作成して、コードが[*evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)として実行されるようにすることができます。コールバック関数。

    また、KMDF バージョン1.11 以降では、ドライバーは[**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)を呼び出すことによって、割り込み作業項目を要求できます。 (ドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は**WdfInterruptQueueWorkItemForIsr**または[**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)を呼び出すことができますが、両方は呼び出せないことに注意してください)。

-   ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)と[*EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nc-wdfdpc-evt_wdf_dpc)のコールバック関数を相互に同期し、デバイスに関連付けられている他のコールバック関数と同期することが重要な場合は、ドライバーで自動**シリアル化**を設定できます。割り込みの[**WDF\_割り込み\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体および dpc オブジェクトの[**WDF\_dpc\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/ns-wdfdpc-_wdf_dpc_config)構造**体のメンバー** 。 また、ドライバーでフレームワークの[スピンロック](using-framework-locks.md#framework-spin-locks)を使用することもできます。 (自動**シリアル化**メンバーを**TRUE**に設定しても、 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数と他のコールバック関数は同期されません。 [**WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)または[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)を使用して、このトピックで既に説明したように、 *EvtInterruptIsr*コールバック関数を同期します。)

ドライバールーチンの同期の詳細については、「[フレームワークベースのドライバーの同期方法](synchronization-techniques-for-wdf-drivers.md)」を参照してください。

 

 





