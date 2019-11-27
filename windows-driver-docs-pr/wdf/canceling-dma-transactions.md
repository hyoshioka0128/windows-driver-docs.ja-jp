---
title: DMA トランザクションのキャンセル
description: DMA トランザクションのキャンセル
ms.assetid: 1E1D659D-80C9-45B1-B96F-78E5A1EE4F6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7bc96743a2c550e498d976a02418765f3ef4238
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845505"
---
# <a name="canceling-dma-transactions"></a>DMA トランザクションのキャンセル


\[は KMDF にのみ適用され\]

ドライバーがバージョン1.11 以降の KMDF でビルドされており、ダイレクトメモリアクセス (DMA) バージョン3を使用して Windows 8 以降で実行されている場合、ドライバーは[**Wdfdmatransactioncancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)メソッドを呼び出して、保留中の DMA トランザクションをキャンセルしようとすることができます.

[**Wdfdmatransactioncancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)を呼び出すと、ドライバーは、指定された DMA トランザクションが呼び出し中に完了していないことを確認する必要があります。 ドライバーは、次の方法を使用して、DMA チャネル割り当ての前またはいくつかの転送操作が既に完了した後に、トランザクションを安全にキャンセルできます。

1.  ドライバーの[要求ハンドラー](request-handlers.md)のいずれかで、ドライバーは[**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出し、i/o 要求に対して[*evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数を提供します。 次に、要求ハンドラーが[**Wdfdmatransactionexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)を呼び出します。
2.  ドライバーの[*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数 ( [**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を呼び出した直後に別のスレッドで実行が開始される場合があります) は、 [**Wdfrequestmarkcancelableex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)を呼び出します。
3.  Wdfdmatransactioncancel を呼び出した後、wdfdmatransactioncancel の呼び出しが行われた[**場合、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)wdfdmatransactioncancel**メソッドが**DMA 割り当てを開始する前に、トランザクションのキャンセルが成功し、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel) **wdfdmatransactioncancel**が TRUE を返します。 この場合、ドライバーの[*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数は[DMA トランザクションを完了](completing-a-dma-transaction.md)する必要があります。 **Wdfdmatransactionexecute**はエラー値を返します。
4.  [**Wdfdmatransactioncancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)メソッドが DMA 割り当てを開始した後に、ドライバーが[**Wdfdmatransactioncancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)を呼び出すと、トランザクションをキャンセルしようとして失敗し、 **WDFDMATRANSACTIONCANCEL**が FALSE を返します。 この場合、 **Wdfdmatransactionexecute**は STATUS\_SUCCESS を返し、ドライバーの要求ハンドラーは[DMA トランザクションを完了](completing-a-dma-transaction.md)する必要があります。

    この時点で、ドライバーがシステムモードの DMA を使用している場合、 [*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数は[**Wdfdmatransactionstopsystemtransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)を呼び出して、進行中のシステムモードの dma 転送を停止しようとすることがあります。 これを実行する方法を示すコード例については、「 [**Wdfdmatransactionstopsystemtransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)」を参照してください。

5.  [**Wdfdmatransactionexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)メソッドが DMA の割り当てを完了した後、フレームワークはドライバーの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を呼び出します。これは、の呼び出し**の直後に別のスレッドで実行を開始する場合があります。WdfDmaTransactionExecute**)。 この時点で、 [**Wdfdmatransactioncancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)メソッドを呼び出すと、FALSE が返されます。

    [*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)では、ドライバーは[**Wdfrequestunmarkmarkを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)呼び出して、要求のキャンセルの可能性を終了できます。 **Wdfrequestunmarkcancelable**可能\_が成功した場合、コールバック関数は、転送を開始するようにハードウェアをプログラミングする必要があります。 **Wdfrequestunmarkcancelable**\_が取り消された場合、要求は取り消されました。 この場合、 *Evtprogramdma*は[**Wdfdmatransactiondmacomtitedtitedtitedtitedtitedtitedtitedtitedfinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)を呼び出し[て、DMA トランザクションを完了](completing-a-dma-transaction.md)する必要があります。

    ドライバーは、何らかの転送操作が既に完了した後に、同じ手法を使用して DMA トランザクションを取り消すことができます。 この場合、ドライバーは[**Wdfdmatransactiondmacomが**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)呼び出された後、 [**Wdfdmatransactioncancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)を呼び出しますが、フレームワークは次の転送操作をプログラムするために[*evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)を呼び出します。 ドライバーが**Wdfdmatransactiondmacomが**呼び出される前に、 **Wdfdmatransactioncancel**を呼び出すと、 **Wdfdmatransactiondmacomが** **TRUE**を返し、DMA トランザクションが完了したことを示します。

 

 





