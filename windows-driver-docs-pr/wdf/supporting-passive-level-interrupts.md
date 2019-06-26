---
title: パッシブ レベルの割り込みのサポート
description: フレームワーク バージョン 1.11 以降、WDF ドライバーはパッシブ レベルの処理が必要な割り込みオブジェクトを作成できます。
ms.assetid: E464F885-928C-40BC-A09F-7A7921F8FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e08dfa1d9ae8348241e043af442b6407502c20f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368059"
---
# <a name="supporting-passive-level-interrupts"></a>パッシブ レベルの割り込みのサポート


Windows 8 またはそれ以降のバージョンのオペレーティング システムで実行されているドライバーは、framework のバージョン 1.11、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) で始まるパッシブ レベルの処理が必要な割り込みオブジェクトを作成できます。 フレームワークが、ドライバーの割り込みサービス ルーチン (ISR) およびその他の場合は、ドライバーは、パッシブ レベル割り込み処理の割り込みオブジェクトを構成、[オブジェクト イベントのコールバック関数を中断](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/)IRQL = パッシブ\_パッシブ レベル割り込みロックを保持しているときにレベル。

チップ (SoC) プラットフォーム上のシステムを framework ベースのドライバーを開発している場合は、パッシブ モードの割り込みを I²C、SPI、UART などの低速バス経由で、SoC をデバイスとの通信に使用できます。

それ以外の場合、使用する必要があります[デバイスの IRQL で処理が必要な割り込み](creating-an-interrupt-object.md)(DIRQL)。 ドライバーは、メッセージ シグナル割り込み (Msi) をサポートする場合は、DIRQL を使用する必要があります割り込みを処理します。 バージョン 1.9 以降では、フレームワーク、常に処理割り込み IRQL で DIRQL を = です。

このトピックで説明する方法[作成](#creating-a-passive-level-interrupt)、[サービス](#servicing)、および[同期](#synchronizing)パッシブ レベルの割り込みです。

## <a name="creating-a-passive-level-interrupt"></a>パッシブ レベル割り込みを作成します。


パッシブ レベル割り込みオブジェクトを作成するドライバーを初期化する必要があります、 [ **WDF\_割り込み\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体に渡すと、 [ **WdfInterruptCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッド。 構成構造体で、ドライバーを行ってください。

-   設定、 **PassiveHandling**メンバーを TRUE にします。
-   提供、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)パッシブ レベルで呼び出されるコールバック関数。
-   必要に応じて設定、 **AutomaticSerialization**を TRUE にします。 ドライバーが設定されている場合**AutomaticSerialization**を TRUE に、フレームワークは、割り込みオブジェクトの実行を同期し、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)割り込みの親オブジェクトの下にあるその他のオブジェクトからのコールバック関数のコールバック関数。
-   どちらも、ドライバーが必要に応じて、提供、 [ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) IRQL で呼び出されるコールバック関数、パッシブ =\_レベル、または[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) IRQL で呼び出されるコールバック関数のディスパッチを =\_レベル。

上記構成構造体のメンバーの設定の詳細については、次を参照してください。 [ **WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)します。
有効にして、パッシブ レベルの割り込みを無効化については、次を参照してください。[の有効化と無効にする割り込み](enabling-and-disabling-interrupts.md)します。

## <a href="" id="servicing"></a>パッシブ レベル割り込みを処理します。


[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) IRQL で実行されるコールバック関数は、パッシブ =\_割り込みが作業項目または割り込みを DPC レベル パッシブ レベル割り込みロックを保持し、通常のスケジュール後で割り込み関連の情報を処理します。 フレームワーク ベースのドライバーは、作業項目またはとして DPC ルーチンを実装[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)または[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数。

実行をスケジュールする、 [ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数では、ドライバーを呼び出す[ **WdfInterruptQueueWorkItemForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)内から、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数。

実行をスケジュールする、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数では、ドライバーを呼び出す[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)から内で、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数。 (リコールを運転免許*EvtInterruptIsr*コールバック関数を呼び出すことができます[ **WdfInterruptQueueWorkItemForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)または**WdfInterruptQueueDpcForIsr**、両方ではなく)。

ほとんどのドライバーを使用して、1 つ[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)または[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)割り込みの種類ごとのコールバック関数。 ドライバーは、割り込みオブジェクト デバイスごとに複数のフレームワークを作成する場合は、別の使用を検討*EvtInterruptWorkItem*または*EvtInterruptDpc*各割り込みのコールバック。

ドライバーは、通常の I/O 要求を完了、 [ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)または[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数。

次のコード例では、パッシブ レベルの割り込みを使用して、ドライバー可能性がありますスケジュールを設定する方法を示します、 [ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック内からその[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)関数。

```cpp
BOOLEAN

EvtInterruptIsr(
    _In_  WDFINTERRUPT Interrupt,
    _In_  ULONG        MessageID
    )
/*++

  Routine Description:

    This routine responds to interrupts generated by the hardware.
    It stops the interrupt and schedules a work item for 
    additional processing.

    This ISR is called at PASSIVE_LEVEL (passive-level interrupt handling).

  Arguments:
  
    Interrupt - a handle to a framework interrupt object
    MessageID - message number identifying the device's
        hardware interrupt message (if using MSI)

  Return Value:

    TRUE if interrupt recognized.

--*/
{
    
    UNREFERENCED_PARAMETER(MessageID);

    NTSTATUS                status;
    PDEV_CONTEXT            devCtx;
    WDFREQUEST              request;
    WDF_MEMORY_DESCRIPTOR   memoryDescriptor;
    INT_REPORT              intReport = {0};
    BOOLEAN                 intRecognized;
    WDFIOTARGET             ioTarget;
    ULONG_PTR               bytes;
    WDFMEMORY               reqMemory;

    intRecognized = FALSE;

    //         
    // Typically the pattern in most ISRs (DIRQL or otherwise) is to:
    // a) Check if the interrupt belongs to this device (shared interrupts).
    // b) Stop the interrupt if the interrupt belongs to this device.
    // c) Acknowledge the interrupt if the interrupt belongs to this device.
    //
   
   
    //
    // Retrieve device context so that we can access our queues later.
    //    
    devCtx = GetDevContext(WdfInterruptGetDevice(Interrupt));

     
    //
    // Init memory descriptor.
    //    
    WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(
                         &memoryDescriptor,
                         &intReport,
                         sizeof(intReport);

    //
    // Send read registers/data IOCTL. 
    // This call stops the interrupt and reads the data at the same time.
    // The device will reinterrupt when a new read is sent.
    //
    bytes = 0;
    status = WdfIoTargetSendIoctlSynchronously(
                             ioTarget,
                             NULL,
                             IOCTL_READ_REPORT,
                             &memoryDescriptor,
                             NULL,
                             NULL,
                             &bytes);
     
    //
    // Return from ISR if this is not our interrupt.
    // 
    if (intReport->Interrupt == FALSE) {
        goto exit;
    }

    intRecognized = TRUE;

    //
    // Validate the data received.
    //
    ...

    //
    // Retrieve the next read request from the ReportQueue which
    // stores all the incoming IOCTL_READ_REPORT requests
    // 
    request = NULL;
    status = WdfIoQueueRetrieveNextRequest(
                            devCtx->ReportQueue,
                            &request);

    if (!NT_SUCCESS(status) || (request == NULL)) {
        //
        // No requests to process. 
        //
        goto exit;
    }
    
    //
    // Retrieve the request buffer.
    //
    status = WdfRequestRetrieveOutputMemory(request, &reqMemory);

    //
    // Copy the data read into the request buffer.
    // The request will be completed in the work item.
    //
    bytes = intReport->Data->Length;
    status = WdfMemoryCopyFromBuffer(
                            reqMemory,
                            0,
                            intReport->Data,
                            bytes);

    //
    // Report how many bytes were copied.
    //
    WdfRequestSetInformation(request, bytes);

    //
    // Forward the request to the completion queue.
    //
    status = WdfRequestForwardToIoQueue(request, devCtx->CompletionQueue);
    
    //
    // Queue a work-item to complete the request.
    //
    WdfInterruptQueueWorkItemForIsr(FxInterrupt);

exit:
    return intRecognized;
}

VOID
EvtInterruptWorkItem(
    _In_ WDFINTERRUPT   Interrupt,
    _In_ WDFOBJECT      Device
    )
/*++

Routine Description:

    This work item handler is triggered by the interrupt ISR.

Arguments:

    WorkItem - framework work item object

Return Value:

    None

--*/
{
    UNREFERENCED_PARAMETER(Device);

    WDFREQUEST              request;
    NTSTATUS                status;
    PDEV_CONTEXT            devCtx;
    BOOLEAN                 run, rerun;
    
    devCtx = GetDevContext(WdfInterruptGetDevice(Interrupt));

    WdfSpinLockAcquire(devCtx->WorkItemSpinLock);
    if (devCtx->WorkItemInProgress) {
        devCtx->WorkItemRerun = TRUE;
        run = FALSE;
    }
    else {
        devCtx->WorkItemInProgress = TRUE;
        devCtx->WorkItemRerun = FALSE;
        run = TRUE;
    }
    WdfSpinLockRelease(devCtx->WorkItemSpinLock);

    if (run == FALSE) {
        return;
    }

    do {  
        for (;;) {
            //
            // Complete all report requests in the completion queue.
            //
            request = NULL;
            status = WdfIoQueueRetrieveNextRequest(devCtx->CompletionQueue, 
                                                   &request);
            if (!NT_SUCCESS(status) || (request == NULL)) {
                break;
            }
            
            WdfRequestComplete(request, STATUS_SUCCESS);
        }
        
        WdfSpinLockAcquire(devCtx->WorkItemSpinLock);
        if (devCtx->WorkItemRerun) {
            rerun = TRUE;
            devCtx->WorkItemRerun = FALSE;
        }
        else {
            devCtx->WorkItemInProgress = FALSE;
            rerun = FALSE;
        }
        WdfSpinLockRelease(devCtx->WorkItemSpinLock);
    }
    while (rerun);
}

VOID
EvtIoInternalDeviceControl(
    _In_  WDFQUEUE      Queue,
    _In_  WDFREQUEST    Request,
    _In_  size_t        OutputBufferLength,
    _In_  size_t        InputBufferLength,
    _In_  ULONG         IoControlCode
    )
{
    NTSTATUS            status;
    DEVICE_CONTEXT      devCtx;
    devCtx = GetDeviceContext(WdfIoQueueGetDevice(Queue));
    
    switch (IoControlCode) 
    {
    ...
    case IOCTL_READ_REPORT:

        //
        // Forward the request to the manual ReportQueue to be completed
        // later by the interrupt work item.
        //
        status = WdfRequestForwardToIoQueue(Request, devCtx->ReportQueue);
        break;
   
    ...
    }

    if (!NT_SUCCESS(status)) {
        WdfRequestComplete(Request, status);
    }
}
```

## <a href="" id="synchronizing"></a>パッシブ レベル割り込みを同期します。


デッドロックを防ぐためには、パッシブ レベル割り込み処理を実装するドライバーを記述する場合、次のガイドラインに従います。

-   場合**AutomaticSerialization** TRUE に設定されていない[同期要求を送信する](sending-i-o-requests-synchronously.md)内から、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数。
-   前にパッシブ レベル割り込みロックの解放[I/O 要求の完了](completing-i-o-requests.md)します。
-   提供[ *EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)、 [ *EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)、および[ *EvtInterruptWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)に応じて。
-   場合は、ドライバーになど、任意のスレッド コンテキストでは、割り込みに関連する作業を実行する必要があります、[要求ハンドラー](request-handlers.md)を使用して、 [ **WdfInterruptTryToAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/hh439284)と[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)します。 呼び出さない[ **WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)、 [ **WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)、 [ **WdfInterruptEnable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)、または[ **WdfInterruptDisable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable)任意のスレッド コンテキストから。 呼び出すことによって生じるおそれのあるデッドロックのシナリオの例については**WdfInterruptAcquireLock**任意のスレッド コンテキストからの「解説」を参照してください。 [ **WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340).

    場合への呼び出し[ **WdfInterruptTryToAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/hh439284)作業項目に割り込みに関連する作業を延期できるは、ドライバーは失敗します。 その作業項目で、ドライバーに安全にロックを取得できる割り込みを呼び出して[ **WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)します。 詳細については、次を参照してください。 [ **WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)します。

    ドライバーを呼び出すことができます、作業項目などの非任意のスレッド コンテキストで[ **WdfInterruptAcquireLock** ](https://msdn.microsoft.com/library/windows/hardware/ff547340)または[ **WdfInterruptSynchronize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize).

詳細については、割り込みのロックを使用して、次を参照してください。[同期割り込みコード](synchronizing-interrupt-code.md)します。

 

 





