---
title: DMA ハードウェアのプログラミング
description: このトピックでは、バス マスター DMA デバイス用の KMDF ドライバーは、その EvtProgramDma イベントのコールバック関数では、通常は、機能について説明します。
ms.assetid: 5e74fe74-d38f-4cca-b0cf-8a6f170c4dc5
keywords:
- DMA 操作 WDK KMDF、転送
- バス マスター DMA WDK KMDF の転送
- DMA は、WDK KMDF、ハードウェアを転送します。
- DMA は、WDK KMDF、以降の転送します。
- WDK KMDF を転送 DMA の開始
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c2e6461297a8e59b158ca10b7591bbb63d8de99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376307"
---
# <a name="programming-dma-hardware"></a>DMA ハードウェアのプログラミング


\[KMDF にのみ適用されます。\]

このトピックで通常のバス マスター DMA デバイス KMDF ドライバーを提供する機能を説明するその[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)イベント コールバック関数。 ドライバーは、DMA のフレームワークのサポートを使用している場合、ドライバーは、このコールバックを提供する必要があります。 この情報は、KMDF ドライバーにも適用されます、[システム モード DMA デバイス](supporting-system-mode-dma.md)ハードウェア割り込みを持ちます。




[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) IRQL で呼び出されるコールバック関数のディスパッチを =\_レベルで開始するデバイスをプログラムを[DMA 転送](dma-transactions-and-dma-transfers.md)します。 このコールバック関数の入力パラメーターは、転送の方向 (入力または出力) とスキャッター/ギャザーの一覧を指定します。 で 1 つのパケットの転送が構成される場合、スキャッター/ギャザー一覧には、1 つの要素が含まれています。

[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数は、ハードウェア リソースを使用して、デバイスをプログラムするドライバーの[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)受信したコールバック関数。 場合、 *EvtProgramDma*返しますコールバック関数では、ハードウェアが正常にプログラム、 **TRUE**します。

ハードウェアには、DMA 転送が完了した後、通常、ハードウェアの問題、割り込み、システムは、ドライバーの[ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数。 ドライバーの*EvtInterruptIsr*コールバック関数の場合、通常は。

-   ハードウェアの割り込みをクリアします。

-   必要な場合は、割り込みのコンテキスト情報を保存します。 コールバック関数が返すし、(、IRQL の削減により、追加の割り込みが発生する) ために、システムは、IRQL を削減した後、この情報は失われます。

-   呼び出し[ **WdfInterruptQueueDpcForIsr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nf-wdfinterrupt-wdfinterruptqueuedpcforisr)をスケジュールする、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数。

[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数[DMA 転送が完了すると](completing-a-dma-transfer.md)コンテキスト情報を使用している、 [ *EvtInterruptIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)コールバック関数を保存します。

場合、 [ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数には、エラーが検出される、ドライバーは、トランザクションを停止できます。

ドライバーは、エラーを検出したときに、トランザクションを停止する、 [ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数にする必要があります。

1.  呼び出す[ **WdfDmaTransactionDmaCompletedFinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)します。

2.  呼び出す[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) DMA トランザクション オブジェクトを削除または呼び出し[ **WdfDmaTransactionRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)を解放し、DMA の再利用トランザクション オブジェクトです。

3.  [I/O 要求をキューに再登録](requeuing-i-o-requests.md)または[I/O 要求を完了](completing-i-o-requests.md)トランザクションがフレームワークの要求オブジェクトに関連付けられている場合は、します。 ドライバーを呼び出すことができます、要求を識別するハンドルを取得する[ **WdfDmaTransactionGetRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetrequest)します。

4.  返す**FALSE**します。

手順 1 と 4 がから取得した次のコード例で示すよう、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma) で読み取り要求のコールバック関数*Read.c*ファイル。

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

例では、 **PLxReadRequestComplete**手順 2. および 3. を実行する関数。

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









