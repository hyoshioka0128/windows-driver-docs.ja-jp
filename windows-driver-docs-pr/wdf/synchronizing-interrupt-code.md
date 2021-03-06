---
title: 割り込みコードの同期
description: 割り込みコードの同期
ms.assetid: a24477dc-f75d-4ab6-8695-d8a85247e276
keywords:
- ハードウェアの割り込み WDK KMDF、同期
- WDK KMDF、同期を中断します。
- 同期の WDK の割り込み
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb2030c82e0daca43f7741d2f7d7f56c82a2a092
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363860"
---
# <a name="synchronizing-interrupt-code"></a>割り込みコードの同期


次の要因には、マルチプロセッサ システムでハードウェアの割り込みを処理するドライバーのコードが複雑になります。

-   デバイスが中断するたびに、次回デバイスを中断したときに上書きできるため、揮発性が割り込みに固有の情報が提供します。

-   比較的高い Irql と、割り込みサービス ルーチン (Isr) デバイスの割り込みは、その他のドライバー コードの実行を中断できます。

-   DIRQL の割り込みの ISR する必要があります実行 DIRQL で、ドライバーによって提供されるスピン ロックを保持しているときに ISR は揮発性の情報を保存中に追加の割り込みを防ぐことができます。 DIRQL が、現在のプロセッサで中断することを防止し、スピン ロックは、別のプロセッサによって中断を防止します。

-   デバイスが ISR の実行中に中断できないために、ISR はすぐに実行する必要があります。 ISR 実行時間が長いでは、システムを遅くしたり、データの損失が発生することができます。

-   ISR と遅延プロシージャ呼び出し (DPC) のルーチンの両方では、ISR デバイスの揮発性データを格納するストレージ領域通常アクセスする必要があります。 これらのルーチンは、同時に、記憶域にアクセスしないように互いと同期する必要があります。

割り込みを処理するドライバーのコードを記述する場合、すべてこれらの要因のため、次の規則を使用する必要があります。

-   のみ、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数が割り込み情報を含むデバイス レジスタなどの揮発性の割り込みのデータにアクセスします。

    [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数は、揮発性データを割り込みのドライバーの定義済みのデータ バッファーを移動する必要があります、ドライバーの[ *EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数、 [ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数、または複数[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数にアクセスできます。

    お使いのドライバーする場合[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)の割り込みオブジェクト、最適なコールバック関数割り込みのデータを格納する場所は、割り込みオブジェクトの[コンテキスト領域](framework-object-context-space.md)します。 割り込みオブジェクトのコールバック関数は、受け取ったオブジェクトのハンドルを使用して、オブジェクトのコンテキストの領域にアクセスできます。

    場合は、ドライバーは、複数[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)ごとのコールバック関数[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数があります各 DPC オブジェクトのコンテキストの領域では、割り込みのデータを格納します。

-   ルーチンを 1 つだけでデータにアクセスできるように、割り込みのデータ バッファーにアクセスするすべてのドライバー コードを同期する必要があります。

    DIRQL 割り込みオブジェクトの場合、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数は、IRQL でこのデータ バッファー割り込みオブジェクトのドライバーによって提供されるスピン ロックを保持しながら DIRQL を = です。 そのため、バッファーにアクセスするすべてのルーチンは、スピン ロックを保持しながら DIRQL で実行もする必要があります。 (通常、割り込みの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数は、のみ他のルーチンにアクセスする必要がありますバッファーです。)

    を除き、割り込みデータ バッファーにアクセスするすべてのルーチン、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数は、次のいずれかで行う必要があります。

    -   呼び出す[ **WdfInterruptSynchronize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)をスケジュールする、 [ *EvtInterruptSynchronize* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_synchronize)割り込みにアクセスするコールバック関数データ バッファー。
    -   割り込みのデータ バッファーへの呼び出しの間にアクセスするコードを配置[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)と[ **WdfInterruptReleaseLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547376).

    これらの手法の両方を許可する、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)押しながら割り込み DIRQL でデータにアクセスする関数割り込みのスピン ロックします。 DIRQL が、現在のプロセッサで中断することを防止し、スピン ロックは、別のプロセッサによって中断を防止します。

    デバイスは、複数のベクトルの割り込みまたはメッセージをサポートしている場合、およびこれらの割り込みのドライバーの処理を同期する場合は、複数 DIRQL 割り込みオブジェクトを単一のスピン ロックを割り当てることができます。 同期されたコードは、任意のベクトルの割り込みまたは、セット内のメッセージを中断できないように常にその DIRQL でスピン ロックを取得、およびフレームワークが割り込み、一連の最も高い DIRQL を決定します。

    [パッシブ レベル割り込みオブジェクト](supporting-passive-level-interrupts.md)、フレームワークは、ドライバーを呼び出す前にパッシブ レベル割り込みロックを獲得[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数IRQL = パッシブ\_レベル。 結果として、バッファーにアクセスするすべてのルーチンする必要があります割り込みロックを取得または内部バッファーへのアクセスを同期します。 通常、割り込みの[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数は、のみ他のルーチン、バッファーにアクセスします。 割り込みのロックを取得する方法については、 *EvtInterruptWorkItem*コールバック関数をそのページの「解説」を参照してください。

    パッシブ レベルの割り込みの複数のオブジェクトを 1 つの待機のロックを割り当てることで複数のベクトルの割り込みのドライバーの処理を同期することもできます。

-   IRQL で DIRQL 割り込みを処理するコードの一部を実行する必要があります = パッシブ\_レベル、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDpcFunc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)コールバック関数が 1 つまたは複数作成できます[作業項目](using-framework-work-items.md)としてコードが実行されるよう[ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数。

    または、KMDF バージョン 1.11 以降では、ドライバーを要求できます割り込みの作業項目を呼び出すことによって[ **WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)します。 (リコールを運転免許[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数を呼び出すことができます**WdfInterruptQueueWorkItemForIsr**または[ **WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)、両方ではなく)。

-   ドライバーを同期する必要がある場合[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)と[ *EvtDpcFunc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nc-wdfdpc-evt_wdf_dpc)互いとコールバック関数その他のデバイスに関連付けられているコールバック関数には、ドライバーを設定できます、 **AutomaticSerialization**メンバー **TRUE**の割り込みの[ **WDF\_INTERRUPT\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造と DPC オブジェクトの[ **WDF\_DPC\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/ns-wdfdpc-_wdf_dpc_config)構造体。 また、ドライバーを使用できる[framework スピン ロック](using-framework-locks.md#framework-spin-locks)します。 (設定、 **AutomaticSerialization**メンバー **TRUE**同期しません、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)でコールバック関数その他のコールバック関数。 使用[ **WdfInterruptSynchronize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)または[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)を同期する、 *EvtInterruptIsr*コールバック関数は、このトピックで前述のようです)。

ドライバーのルーチンの同期の詳細については、次を参照してください。 [Framework ベースのドライバーの同期手法](synchronization-techniques-for-wdf-drivers.md)します。

 

 





