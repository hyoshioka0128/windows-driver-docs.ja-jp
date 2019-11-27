---
title: DMA トランザクションの完了
description: DMA トランザクションの完了
ms.assetid: 90531b72-e51d-451e-ae84-a9bbf0245665
keywords:
- DMA トランザクション WDK KMDF、完了
- DMA 操作 WDK KMDF、トランザクション
- バスマスタ DMA WDK KMDF、トランザクション
- DMA トランザクションの完了 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 457a5c5236c22a725e28bd901083c2bea13a6cd7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843555"
---
# <a name="completing-a-dma-transaction"></a>DMA トランザクションの完了


\[は KMDF にのみ適用され\]




ドライバーのデバイスが[DMA 転送を完了](completing-a-dma-transfer.md)するたびに、ドライバーは[**wdfdmatransactiondmacomを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)呼び出す必要があります。 wdfdmatransactiondmacomtedtedwithlength または[**wdfdmatransactiondmacomが**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)、戻り値を確認します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)

戻り値が**TRUE**の場合、dma トランザクションに対してこれ以上転送は必要なく、ドライバーは dma トランザクションを完了する必要があります。 通常、ドライバーは[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数から返されていません。 したがって、このコールバック関数は、次の方法で DMA トランザクションを完了します。

1.  [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出してトランザクションオブジェクトを削除するか、ドライバーが[DMA トランザクションオブジェクト](reusing-dma-transaction-objects.md)を再利用する場合は[**Wdfdmatransactionrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)を呼び出します。

2.  トランザクションがフレームワークの要求オブジェクトに関連付けられている場合は、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)または[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)を呼び出します。

ドライバーが[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)を呼び出す場合、通常はまず[**WdfDmaTransactionGetBytesTransferred**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetbytestransferred)を呼び出して、すべてのトランザクション転送の合計長 (バイト数) を取得します。

次の手順は、 *Isrdpc. c*ファイルの[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数から抜粋した次のコード例に示されています。

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









