---
title: パッシブ レベルの割り込みのサポート
description: Framework バージョン1.11 以降では、WDF ドライバーは、パッシブレベルの処理を必要とする割り込みオブジェクトを作成できます。
ms.assetid: E464F885-928C-40BC-A09F-7A7921F8FF37
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24d99eadcc8999e3dd2daec4e7639f3a67f221c9
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242941"
---
# <a name="supporting-passive-level-interrupts"></a>パッシブ レベルの割り込みのサポート


Framework バージョン1.11 以降では、Windows 8 以降のバージョンのオペレーティングシステムで実行されているカーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) ドライバーは、パッシブレベルの処理を必要とする割り込みオブジェクトを作成できます。 ドライバーがパッシブレベルの割り込み処理用に割り込みオブジェクトを構成した場合、フレームワークは、パッシブレベルの割り込みロックを保持しながら、ドライバーの interrupt service ルーチン (ISR) およびその他の[割り込みオブジェクトイベントコールバック関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/)を IRQL = パッシブ\_レベルで呼び出します。

チップ (SoC) プラットフォーム上のシステム用のフレームワークベースのドライバーを開発している場合は、パッシブモードの割り込みを使用して、(I ² C、SPI、UART などの) 高速バス経由で SoC 以外のデバイスと通信することができます。

それ以外の場合は、[デバイスの IRQL](creating-an-interrupt-object.md) (dirql) での処理を必要とする割り込みを使用する必要があります。 ドライバーがメッセージシグナル割り込み (Msi) をサポートしている場合は、DIRQL 割り込み処理を使用する必要があります。 バージョン1.9 以前では、フレームワークは常に IRQL = DIRQL で割り込みを処理します。

このトピックでは、パッシブレベルの割り込みを[作成](#creating-a-passive-level-interrupt)、[サービス](#servicing)、および[同期](#synchronizing)する方法について説明します。

## <a name="creating-a-passive-level-interrupt"></a>パッシブレベルの割り込みの作成


パッシブレベルの割り込みオブジェクトを作成するには、ドライバーが[**WDF\_interrupt\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)構造体を初期化し、それを[**WdfInterruptCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)メソッドに渡す必要があります。 構成構造では、ドライバーは次のことを行う必要があります。

-   "設定のない**ve"** メンバーを TRUE に設定します。
-   [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数を指定します。このコールバック関数は、パッシブレベルで呼び出されます。
-   必要に応じて、自動**シリアル化**を TRUE に設定します。 ドライバーが自動**シリアル化**を TRUE に設定した場合、フレームワークは、割り込みオブジェクトの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数と、その割り込みの親オブジェクトの下にある他のオブジェクトからのコールバック関数の実行を同期します。
-   必要に応じて、ドライバーは、IRQL = パッシブ\_レベルで呼び出される[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバック関数を提供したり、IRQL = DISPATCH\_レベルで呼び出される[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数を提供したりすることができます。

構成構造の上のメンバーを設定する方法の詳細については、「 [**WDF\_INTERRUPT\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)」を参照してください。
パッシブレベルの割り込みの有効化と無効化の詳細については、「[割り込みの有効化と無効化](enabling-and-disabling-interrupts.md)」を参照してください。

## <a href="" id="servicing"></a>パッシブレベルの割り込みの提供


[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数は、パッシブレベルの割り込みロックが保持されている IRQL = パッシブ\_レベルで実行されます。通常、割り込みに関連する情報を後で処理するために、割り込み作業項目または割り込み DPC をスケジュールします。 フレームワークベースのドライバーは、作業項目または DPC ルーチンを[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)または[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数として実装します。

[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) callback 関数の実行をスケジュールするために、ドライバーは[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) Callback 関数内から[**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)を呼び出します。

[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数の実行をスケジュールするために、ドライバーは[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) Callback 関数内から[**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)を呼び出します。 (ドライバーの*EvtInterruptIsr* callback 関数は[**WdfInterruptQueueWorkItemForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueueworkitemforisr)または**WdfInterruptQueueDpcForIsr**を呼び出すことができますが、両方は呼び出せないことに注意してください)。

ほとんどのドライバーでは、割り込みの種類ごとに1つの[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)または[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数を使用します。 ドライバーが各デバイスに対して複数のフレームワーク割り込みオブジェクトを作成する場合は、割り込みごとに個別の*EvtInterruptWorkItem*または*EvtInterruptDpc*コールバックを使用することを検討してください。

ドライバーは通常、 [*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)または[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数で i/o 要求を完了します。

次のコード例は、パッシブレベルの割り込みを使用するドライバーが、 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)関数内から[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)コールバックをスケジュールする方法を示しています。

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

## <a href="" id="synchronizing"></a>パッシブレベルの割り込みの同期


デッドロックを回避するには、次のガイドラインに従って、パッシブレベルの割り込み処理を実装するドライバーを記述します。

-   自動**シリアル化**が TRUE に設定されている場合、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) callback 関数内から[同期要求を送信](sending-i-o-requests-synchronously.md)しません。
-   [I/o 要求を完了](completing-i-o-requests.md)する前に、パッシブレベルの割り込みロックを解放します。
-   必要に応じて、 [*EvtInterruptDisable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)、 [*EvtInterruptEnable*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)、および[*EvtInterruptWorkItem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)を指定します。
-   ドライバーが、[要求ハンドラー](request-handlers.md)など、任意のスレッドコンテキストで割り込み関連の作業を実行する必要がある場合は、 [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)と[**WdfInterruptReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff547376)を使用します。 任意のスレッドコンテキストから[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)、 [**WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)、 [**WdfInterruptEnable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptenable)、または[**WdfInterruptDisable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptdisable)を呼び出さないでください。 任意のスレッドコンテキストから**WdfInterruptAcquireLock**を呼び出すことによって発生する可能性のあるデッドロックシナリオの例については、 [**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)の「解説」を参照してください。

    [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)の呼び出しが失敗した場合、ドライバーは、その割り込みに関連する作業を作業項目に延期できます。 この作業項目では、ドライバーは[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)を呼び出すことによって、割り込みロックを安全に取得できます。 詳細については、「 [**WdfInterruptTryToAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/hh439284)」を参照してください。

    任意のスレッドコンテキスト (作業項目など) では、ドライバーは[**WdfInterruptAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff547340)または[**WdfInterruptSynchronize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsynchronize)を呼び出すことができます。

割り込みロックの使用の詳細については、「[割り込みコードの同期](synchronizing-interrupt-code.md)」を参照してください。

 

 





