---
title: DMA リソースの予約
description: DMA リソースの予約
ms.assetid: 8C5FF779-8D54-47D9-8EC6-7D4921F8F697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7230536989f58fb4f86a8be3fc8a542ab76ed5fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842218"
---
# <a name="reserving-dma-resources"></a>DMA リソースの予約


\[は KMDF にのみ適用され\]

通常、フレームワークベースのドライバーでは、マップレジスタが事前に予約されていません。 ただし、特定の状況では、ドライバーがこれらのリソースを事前に予約する必要がある場合があります。

Windows 8 以降で実行されているフレームワークベースのドライバーは、パケットまたはシステムプロファイルを指定する DMA イネーブラーに対して、指定された数のマップレジスタを予約できます。 これを行うために、ドライバーは[**WdfDmaTransactionAllocateResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)を呼び出し、 [*evtreの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)コールバック関数を登録します。

フレームワークは、マップレジスタおよび WDM DMA アダプターのロックが予約されている場合に、ドライバーの[*Evtreを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)呼び出します。 次に、ドライバーはトランザクションオブジェクトを最後に解放する前に、同じトランザクションオブジェクトを使用してトランザクションを複数回初期化して開始できます。 DMA リソースを解放してシステムに戻すには、ドライバーは[**WdfDmaTransactionFreeResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)を呼び出します。

トランザクションに必要なマップレジスタの数を確認するには、 [**WdfDmaTransactionAllocateResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)を呼び出す前に、ドライバーが[**Wdfdmatransactiongettransferinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongettransferinfo)を呼び出すことができます。 ドライバーは、 **Wdfdmatransactiongettransferinfo**を呼び出す前にトランザクションを初期化する必要があります。

次の手順では、指定されたトランザクションで排他的に使用するために、ドライバーが DMA イネーブラーを予約および解放する方法を示します。

1.  ドライバーは i/o 要求を受信します。

2.  ドライバーの[要求ハンドラー](request-handlers.md)は、 [**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)を呼び出して、要求の DMA トランザクションオブジェクトを作成します。

3.  ドライバーの[要求ハンドラー](request-handlers.md)は、リソースを予約するために[**WdfDmaTransactionAllocateResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)を呼び出します。

4.  フレームワークは、要求されたリソースを予約している場合に、 [*Evtreの Edma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)を呼び出します。

5.  [*Evtreservedma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)では、ドライバーは[**Wdfdmatransactioninitializeenabled 要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)または[**wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)を呼び出して、トランザクションオブジェクトを初期化します。

6.  [*Evtreservedma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)では、ドライバーは[**Wdfdmatransactionexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)メソッドを呼び出してトランザクションを開始します。 トランザクションに予約されたリソースがあるため、フレームワークはすぐにドライバーの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を呼び出します。

7.  [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDmaTransactionDmaTransferComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)では、ドライバーは、 [**wdfdmatransactiondmacomを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)呼び出します。 [**wdfdmatransactiondmacomtedtedwithlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)または[**wdfdmatransactiondmacomを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)呼び出します。その後に、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)または[**Wdfdmatransactionrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)が続きます。 ドライバーは、トランザクションが完了または取り消されるまで、トランザクションを削除したり解放したりしないでください。 この手順が完了すると、マップレジスタは予約されたままになります。

8.  ドライバーは、必要な回数だけ手順 5 ~ 7 を繰り返します。

    ドライバーが予約を必要としなくなった場合、ドライバーは[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[*EvtDmaTransactionDmaTransferComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)から[**WdfDmaTransactionFreeResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)を呼び出します。 または、ドライバーは、 [*EvtreWdfDmaTransactionFreeResources Edma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)イベントコールバック関数からを呼び出すことができます。

 

 





