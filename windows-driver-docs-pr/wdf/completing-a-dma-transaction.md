---
title: DMA トランザクションの完了
description: DMA トランザクションの完了
ms.assetid: 90531b72-e51d-451e-ae84-a9bbf0245665
keywords:
- DMA トランザクションの完了の WDK KMDF
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
- DMA トランザクション WDK KMDF の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6fdfae27e4dcfc6869ffa47ee17718423d69a97
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382884"
---
# <a name="completing-a-dma-transaction"></a>DMA トランザクションの完了


\[KMDF にのみ適用されます。\]




ごとに、ドライバーのハンドヘルド デバイス[DMA 転送が完了すると](completing-a-dma-transfer.md)、ドライバーを呼び出す必要があります[ **WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)、 [ **WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)、または[ **WdfDmaTransactionDmaCompletedFinal** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)し、戻り値を確認します。

戻り値が**TRUE**DMA トランザクション以上ない転送が必要なドライバーは、DMA トランザクションを完了する必要があります。 通常、ドライバーがまだ返ってからその[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数。 そのため、このコールバック関数は、DMA のトランザクションによってを実行します。

1.  呼び出す[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)トランザクション オブジェクトを削除または通話に[ **WdfDmaTransactionRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)場合ドライバー[DMA トランザクション オブジェクトを再利用](reusing-dma-transaction-objects.md)します。

2.  呼び出す[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)または[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)トランザクションは、フレームワークに関連付けられている場合は、要求オブジェクト。

ドライバーを呼び出す場合[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)、それを通常最初に呼び出す[ **WdfDmaTransactionGetBytesTransferred** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetbytestransferred)すべてのトランザクションの転送の合計の長さ (バイト数) を取得します。

これらの手順についてから次のコード例では説明、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)でコールバック関数、 *Isrdpc.c*ファイル。

```cpp
if (readComplete) {
    BOOLEAN              transactionComplete;
    WDFDMATRANSACTION    dmaTransaction;
    size_t               bytesTransferred;

    // Get the current Read DmaTransaction.
    dmaTransaction = devExt->CurrentReadDmaTransaction;

    // Indicate that this DMA operation has completed:
    // This may start the transfer on the next packet if 
    // there is still data to be transferred.
    transactionComplete = 
          WdfDmaTransactionDmaCompleted( dmaTransaction, &status ); 
    if (transactionComplete) {
        // Complete the DmaTransaction and the request.
        devExt->CurrentReadDmaTransaction = NULL;
        bytesTransferred =  
               ((NT_SUCCESS(status)) ? 
               WdfDmaTransactionGetBytesTransferred(dmaTransaction): 0 );
        WdfDmaTransactionRelease(dmaTransaction);
        WdfRequestCompleteWithInformation(request, status, bytesTransferred);
    }
}
```









