---
title: DMA リソースの予約
description: DMA リソースの予約
ms.assetid: 8C5FF779-8D54-47D9-8EC6-7D4921F8F697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d006a61aa214b717d0eca588d841c189e29460c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376266"
---
# <a name="reserving-dma-resources"></a>DMA リソースの予約


\[KMDF にのみ適用されます。\]

通常、フレームワーク ベースのドライバーは、前もってマップ レジスタを予約できません。 ただし、特定の状況では、ドライバーはこれらのリソースを事前に予約する必要があります。

Windows 8 以降を実行している framework ベースのドライバーでは、パケットまたはシステムのプロファイルを指定する DMA イネーブラーのマップ レジスタの指定した数を予約できます。 これは、ドライバーの呼び出しを行うに[ **WdfDmaTransactionAllocateResources** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)し、登録、 [ *EvtReserveDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)コールバック関数。

フレームワークは、ドライバーの[ *EvtReserveDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)は予約マップ レジスタおよび WDM DMA アダプターのロック時に機能します。 ドライバーは、初期化し、最後にトランザクション オブジェクトを解放する前に、同じトランザクション オブジェクトを使用して複数回のトランザクションを開始します。 DMA を解放するリソースのバックアップ システム、ドライバーの呼び出しに[ **WdfDmaTransactionFreeResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)します。

トランザクションに必要なマップのレジスタの数を確認するには、ドライバーを呼び出すことができます[ **WdfDmaTransactionGetTransferInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongettransferinfo)呼び出す前に[ **WdfDmaTransactionAllocateResources**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)します。 ドライバーは、呼び出す前にトランザクションを初期化する必要があります**WdfDmaTransactionGetTransferInfo**します。

次の手順では、ドライバーの予約および指定されたトランザクションを排他的に使用 DMA イネーブラーをリリースする方法を示します。

1.  ドライバーは、I/O 要求を受信します。

2.  ドライバーの[要求ハンドラー](request-handlers.md)呼び出し[ **WdfDmaTransactionCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)要求に対して DMA トランザクション オブジェクトを作成します。

3.  ドライバーの[要求ハンドラー](request-handlers.md)呼び出し[ **WdfDmaTransactionAllocateResources** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionallocateresources)リソースを予約します。

4.  Framework 呼び出し[ *EvtReserveDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)ときに、要求されたリソースが予約されます。

5.  [ *EvtReserveDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)、ドライバー呼び出し[ **WdfDmaTransactionInitializeUsingRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)または[ **WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)トランザクション オブジェクトを初期化します。

6.  [ *EvtReserveDma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)、ドライバーの呼び出し、 [ **WdfDmaTransactionExecute** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)トランザクションを開始する方法。 フレームワークは、ドライバーのすぐに呼び出しますので、トランザクションには、リソースが予約されていますが、 [ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数。

7.  [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDmaTransactionDmaTransferComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)、ドライバー呼び出し[ **WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)、 [ **WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)、または[ **WdfDmaTransactionDmaCompletedFinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)、その後に[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)または[ **WdfDmaTransactionRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease). ドライバーの削除またはトランザクションが完了またはキャンセルされるまで、トランザクションを解放する必要がありますされません。 この手順が完了した後、マップのレジスタまま予約済みです。

8.  ドライバーは、必要な回数だけ手順 5 ~ 7 を繰り返すことができます。

    ドライバーには、予約が不要、ドライバーが呼び出し[ **WdfDmaTransactionFreeResources** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionfreeresources)から[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)または[ *EvtDmaTransactionDmaTransferComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)します。 または、ドライバーが呼び出せる**WdfDmaTransactionFreeResources**からその[ *EvtReserveDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_reserve_dma)イベント コールバック関数。

 

 





