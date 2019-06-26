---
title: DMA 転送の完了
description: DMA 転送の完了
ms.assetid: 86383b9f-9b82-4afa-81ac-2ab09bd8778b
keywords:
- DMA 操作 WDK KMDF、転送
- バス マスター DMA WDK KMDF の転送
- DMA は、WDK KMDF、完了の転送します。
- WDK KMDF 転送が DMA の完了
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a81150c78514ea0ad46487480120fce46d6add9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382889"
---
# <a name="completing-a-dma-transfer"></a>DMA 転送の完了


\[KMDF にのみ適用されます。\]




通常、ドライバーの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数には、DMA の各転送の処理が完了します。

最初、DMA の複数のトランザクションが同時に、進行中であることができますので、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) DMA トランザクション完了の転送に関連付けられているコールバック関数が決定する必要があります。 コールバック関数はときに、ドライバーが格納されるトランザクション ハンドルを取得することによってこれを行うことができます、 [DMA トランザクションを開始](starting-a-dma-transaction.md)します。 デバイス拡張機能を取得する、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルが呼び出される関数を定義します**PLxGetDeviceContext** Private.h ヘッダー ファイルで。

```cpp
WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(DEVICE_EXTENSION, PLxGetDeviceContext)
```

その後、ドライバーの  [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバックは次のこと。

```cpp
WDFDMATRANSACTION   dmaTransaction;
PDEVICE_EXTENSION   devExt;
...
devExt  = PLxGetDeviceContext(WdfInterruptGetDevice(Interrupt));
...
dmaTransaction = devExt->WriteDmaTransaction;
```

次に、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数は、フレームワークを通知する必要があります、転送は、次の転送の完了方法のいずれかを呼び出して完了すると。

-   [**WdfDmaTransactionDmaCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)転送が正常に完了し、ハードウェアが転送されるバイト数を報告しない場合、します。

-   [**WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)転送が正常に完了し、ハードウェアは、転送済みバイト数 (または転送されないバイト数) の数を報告する場合、またはドライバーがエラーを検出し、指定した場合、転送する、転送を再試行するゼロの数。 フレームワークが 0 のままにし、そのために同じ転送を送信するバイト数から減算します、ドライバーは、0 の転送数を指定する場合、 [ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数。

-   [**WdfDmaTransactionDmaCompletedFinal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)ハードウェア、アンダーランまたは失敗の状態を報告する場合。

ドライバーを呼び出すことができます[ **WdfDmaTransactionGetCurrentDmaTransferLength** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetcurrentdmatransferlength)の完成した転送元の長さを取得します。 この呼び出しは、デバイスがない転送されたバイト数を報告する場合に役立ちますドライバーが非転送の数を減算するため、元のバイトの長さを転送しを呼び出す **。WdfDmaTransactionGetCurrentDmaTransferLength**を実際の転送サイズを報告します。

フレームワークに通知の前の転送の完了メソッドを 1 つ[DMA 転送](dma-transactions-and-dma-transfers.md)(全体ではない[DMA トランザクション](dma-transactions-and-dma-transfers.md)) が完了します。 ドライバーは、これらのメソッドのいずれかを呼び出してから、ドライバーはかどうか、トランザクションが複数の転送が必要ですかを確認するメソッドの戻り値を確認します。

-   完了メソッドの戻り値の値が**FALSE**フレームワークに追加の DMA 転送は DMA のトランザクションの処理を完了に必要なことが決定されます。

    通常、ドライバーの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数だけを返します。 フレームワークは、ドライバーの[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数をもう一度とコールバック関数は、次の転送では、ハードウェアをプログラミングできます。

    転送の完了方法の状態では常にステータス値を指定\_詳細\_処理\_ここで必要です。

-   戻り値が場合**TRUE**、DMA トランザクションの複数の転送が発生します。

    転送の完了メソッドでは、状態値を提供します。 状態値が状態の場合\_成功した場合、DMA トランザクションのすべての転送が完了して、ドライバーである必要があります[DMA のトランザクションを完了](completing-a-dma-transaction.md)します。 状態値が何である場合は、エラーが発生し、DMA トランザクションが完了していません。

場合、 [ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数には、エラーが検出される、通常、タイマーの期限切れや、転送エラーのシグナル通知ハードウェア割り込みによってドライバーを再起動現在のトランザクションの転送します。

トランザクションの現在の転送をドライバーの再起動を[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数を呼び出すことができます[ **WdfDmaTransactionDmaCompletedWithLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)で、 *TransferredLength*パラメーター 0 に設定します。

 

 





