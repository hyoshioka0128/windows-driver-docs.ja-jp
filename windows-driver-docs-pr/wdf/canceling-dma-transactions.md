---
title: DMA トランザクションのキャンセル
description: DMA トランザクションのキャンセル
ms.assetid: 1E1D659D-80C9-45B1-B96F-78E5A1EE4F6B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8893f534b05f289bf994ae2091c14464542c693d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374621"
---
# <a name="canceling-dma-transactions"></a>DMA トランザクションのキャンセル


\[KMDF にのみ適用されます。\]

ドライバーはダイレクト メモリ アクセス (DMA) バージョン 3 を使用して後で呼び出すことによって、保留中の DMA トランザクションをキャンセルする試みることができますか、ドライバーのバージョン 1.11 または KMDF の以降のバージョンが組み込まれています、Windows 8 で実行されている場合、 [ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)メソッド。

呼び出すときに[ **WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)ドライバーでは、呼び出し中に指定された DMA トランザクションが完了していないことを確認する必要があります。 ドライバーは、DMA チャネル割り当てする前に、または既にいくつか転送操作の完了後、トランザクションをキャンセルしても安全に、次の手法を使用できます。

1.  ドライバーのいずれかで[要求ハンドラー](request-handlers.md)、ドライバー呼び出し[ **WdfRequestMarkCancelableEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)を示し、 [ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel) I/O 要求のコールバック関数。 要求ハンドラーを呼び出して[ **WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)します。
2.  ドライバーの[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数 (への呼び出し後すぐに別のスレッドで実行を開始することがあります[ **WdfRequestMarkCancelableEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestmarkcancelableex)) 呼び出し[ **WdfDmaTransactionCancel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)します。
3.  場合に呼び出し[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)への呼び出し後に発生します[ **WdfDmaTransactionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)、前に**WdfDmaTransactionExecute**メソッドには、DMA 割り当てが開始された、トランザクションの取り消しに成功して**WdfDmaTransactionCancel** TRUE を返します。 ここでは、ドライバーの[ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数にする必要があります[DMA のトランザクションを完了](completing-a-dma-transaction.md)します。 **WdfDmaTransactionExecute**エラー値を返します。
4.  ドライバーを呼び出す場合[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)後、 [ **WdfDmaTransactionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)メソッドが DMA の割り当てを開始しますトランザクションが失敗する、取り消しを試行して**WdfDmaTransactionCancel** FALSE を返します。 この場合、 **WdfDmaTransactionExecute**ステータスを返します\_成功とドライバーの要求のハンドラーにする必要があります[DMA のトランザクションを完了](completing-a-dma-transaction.md)します。

    ドライバーはシステム モードの DMA を使用している場合、この時点で、 [ *EvtRequestCancel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)コールバック関数を呼び出すことがあります[ **WdfDmaTransactionStopSystemTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)しようとすると、進行中のシステム モード DMA の転送を中止します。 これを行う方法を示すコード例を参照してください。 [ **WdfDmaTransactionStopSystemTransfer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionstopsystemtransfer)します。

5.  後に、 [ **WdfDmaTransactionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)メソッド DMA の割り当てが完了すると、フレームワークは、ドライバーの[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数 (への呼び出し後すぐに別のスレッドで実行を開始することがあります**WdfDmaTransactionExecute**)。 この時点での呼び出しを[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)メソッドは FALSE を返します。

    [ *EvtProgramDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)、ドライバーを呼び出すことができます[ **WdfRequestUnmarkCancelable** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestunmarkcancelable)要求のキャンセルの可能性を終了します。 場合**WdfRequestUnmarkCancelable**ステータスを返します\_成功した場合、コールバック関数は、転送を開始するためのハードウェアをプログラムする必要があります。 場合**WdfRequestUnmarkCancelable**ステータスを返します\_取り消された場合、要求はキャンセルされました。 この場合、 *EvtProgramDma*呼び出す必要があります[ **WdfDmaTransactionDmaCompletedFinal** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)に[DMA のトランザクションを完了](completing-a-dma-transaction.md)します。

    ドライバーは、既にいくつか転送操作の完了後に、DMA トランザクションをキャンセルするのに同じ手法を使用できます。 この場合、ドライバーを呼び出す[ **WdfDmaTransactionCancel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncancel)呼び出した後[ **WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)、する前に、フレームワーク[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)転送の次の操作をプログラミングします。 呼び出す場合は、ドライバー **WdfDmaTransactionCancel**を呼び出す前に**WdfDmaTransactionDmaCompleted**、 **WdfDmaTransactionDmaCompleted**返します**TRUE**、DMA トランザクションが完了したことを示します。

 

 





