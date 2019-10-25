---
title: DMA ハードウェアのプログラミング
description: このトピックでは、通常、バスマスタ DMA デバイス用の KMDF ドライバーが EvtProgramDma イベントコールバック関数で提供する機能について説明します。
ms.assetid: 5e74fe74-d38f-4cca-b0cf-8a6f170c4dc5
keywords:
- DMA 操作 WDK KMDF、転送
- バスマスタ DMA WDK KMDF、転送
- DMA 転送 WDK KMDF、ハードウェア
- DMA 転送 WDK KMDF、開始
- DMA 転送の開始 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 143a0aa6a72296dbfd1ae4f1b6587f343c8982b6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842230"
---
# <a name="programming-dma-hardware"></a>DMA ハードウェアのプログラミング


\[は KMDF にのみ適用され\]

このトピックでは、通常、バスマスタ DMA デバイス用の KMDF ドライバーが[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)イベントコールバック関数で提供する機能について説明します。 ドライバーがフレームワークの DMA サポートを使用している場合、ドライバーはこのコールバックを提供する必要があります。 この情報は、ハードウェアの割り込みがある[システムモードの DMA デバイス](supporting-system-mode-dma.md)用の kmdf ドライバーにも適用されます。




IRQL = ディスパッチ\_レベルで呼び出される[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数は、 [DMA 転送](dma-transactions-and-dma-transfers.md)を開始するようにデバイスをプログラムします。 このコールバック関数の入力パラメーターは、転送の方向 (入力または出力) とスキャッター/ギャザーリストを指定します。 転送が1つのパケットで構成されている場合、スキャッター/ギャザーリストには1つの要素が含まれます。

[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数は、ドライバーの[*evtprogramdma ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数が受信したハードウェアリソースを使用して、デバイスをプログラムします。 *Evtprogramdma*コールバック関数によってハードウェアが正常にプログラムされた場合、 **TRUE**が返されます。

ハードウェアが DMA 転送を完了すると、通常、ハードウェアは割り込みを発行し、システムはドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数を呼び出します。 通常、ドライバーの*EvtInterruptIsr*コールバック関数は次のようになります。

-   ハードウェアの割り込みを解除します。

-   必要に応じて、割り込みのコンテキスト情報を保存します。 この情報は、コールバック関数が戻り、システムによって IRQL が低下した場合に失われる可能性があります (IRQL を下げることで、追加の割り込みが発生することがあります)。

-   [**WdfInterruptQueueDpcForIsr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)を呼び出して、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数をスケジュールします。

[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、 [*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数によって保存されたコンテキスト情報を使用して、 [DMA 転送を完了](completing-a-dma-transfer.md)します。

[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数によってエラーが検出された場合、ドライバーはトランザクションを停止できます。

ドライバーがエラーを検出したときにトランザクションを停止するには、 [*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数で次のことを行う必要があります。

1.  [**Wdfdmatransactiondmacomを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)呼び出します。

2.  [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出して、dma トランザクションオブジェクトを削除するか、 [**Wdfdmatransactionrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)を呼び出して、dma トランザクションオブジェクトを解放して再利用します。

3.  トランザクションがフレームワークの要求オブジェクトに関連付けられている場合は、i/o[要求をキューへ](requeuing-i-o-requests.md)するか、i/o[要求を完了](completing-i-o-requests.md)します。 要求へのハンドルを取得するために、ドライバーは[**Wdfdmatransactiongetrequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetrequest)を呼び出すことができます。

4.  **FALSE**を返します。

手順 1. と 4. を次のコード例に示します。このコード例では、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数から、 *read .c*ファイル内の読み取り要求を取得しています。

```cpp
    // If errors occur in the EvtProgramDma callback,
    // release the DMA transaction object and complete the request.

    if (errors) {
        NTSTATUS status;

        //
        // Must abort the transaction before deleting.
        //
        (VOID) WdfDmaTransactionDmaCompletedFinal(Transaction, 0, &status);
        ASSERT(NT_SUCCESS(status));

        PLxReadRequestComplete( Transaction, STATUS_INVALID_DEVICE_STATE );
        TraceEvents(TRACE_LEVEL_ERROR, DBG_READ,
                    "<-- PLxEvtProgramReadDma: errors ****");
        return FALSE;
    }
```

この例では、 **Plxreadrequestcomplete**関数を呼び出して、手順 2. と 3. を実行します。

```cpp
VOID
PLxReadRequestComplete(
    IN WDFDMATRANSACTION  DmaTransaction,
    IN NTSTATUS           Status
    )
/*++

Routine Description:

Arguments:

Return Value:

--*/
{
    WDFREQUEST         request;
    size_t             bytesTransferred;

    //
    // Get the associated request from the transaction.
    //
    request = WdfDmaTransactionGetRequest(DmaTransaction);

    ASSERT(request);

    //
    // Get the final bytes transferred count.
    //
    bytesTransferred =  WdfDmaTransactionGetBytesTransferred( DmaTransaction );

    TraceEvents(TRACE_LEVEL_INFORMATION, DBG_DPC,
                "PLxReadRequestComplete:  Request %p, Status %!STATUS!, "
                "bytes transferred %d\n",
                 request, Status, (int) bytesTransferred );

    WdfDmaTransactionRelease(DmaTransaction);

    //
    // Complete this Request.
    //
    WdfRequestCompleteWithInformation( request, Status, bytesTransferred);

}
```









