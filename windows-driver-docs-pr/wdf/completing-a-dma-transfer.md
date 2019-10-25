---
title: DMA 転送の完了
description: DMA 転送の完了
ms.assetid: 86383b9f-9b82-4afa-81ac-2ab09bd8778b
keywords:
- DMA 操作 WDK KMDF、転送
- バスマスタ DMA WDK KMDF、転送
- DMA 転送 WDK KMDF、完了
- DMA 転送の完了 (WDK KMDF)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1646d0ab87170f3222adebb45a062ccadff51f58
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844610"
---
# <a name="completing-a-dma-transfer"></a>DMA 転送の完了


\[は KMDF にのみ適用され\]




通常、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、各 DMA 転送の処理を完了します。

1つ目は、複数の DMA トランザクションが同時に実行される可能性があるためです。そのため、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、完了した転送が関連付けられている dma トランザクションを特定する必要があります。 このコールバック関数は、 [DMA トランザクションの開始](starting-a-dma-transaction.md)時にドライバーが格納したトランザクションハンドルを取得することによって、この処理を実行できます。 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルでは、デバイス拡張機能を取得するために、 **PLxGetDeviceContext**という名前の関数を独自のヘッダーファイルで定義しています。

```cpp
WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(DEVICE_EXTENSION, PLxGetDeviceContext)
```

次に、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバックで、次のことを行います。

```cpp
WDFDMATRANSACTION   dmaTransaction;
PDEVICE_EXTENSION   devExt;
...
devExt  = PLxGetDeviceContext(WdfInterruptGetDevice(Interrupt));
...
dmaTransaction = devExt->WriteDmaTransaction;
```

次に、 [*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、次のいずれかの転送完了メソッドを呼び出すことによって、転送が完了したことをフレームワークに通知する必要があります。

-   [**Wdfdmatransactiondmacom*** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompleted)転送が正常に完了し、ハードウェアが転送されたバイト数を報告しない場合。

-   [**Wdfdmatransactiondmacompletedwithlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)。転送が正常に完了し、ハードウェアが転送されたバイト数 (または転送されていないバイト数) を報告した場合、またはドライバーがエラーを検出し、転送カウントを0に指定した場合は、転送を再試行してください。 ドライバーで転送カウントが0に指定されている場合、フレームワークは、保持されているバイト数から0を減算します。これにより、同じ転送が[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数に送信されます。

-   [**Wdfdmatransactiondmacomて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedfinal)、ハードウェアがアンダーランまたはエラー状態を報告する場合は、最終です。

ドライバーは、 [**Wdfdmatransactiongetcurrentdmatransの長さ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiongetcurrentdmatransferlength)を呼び出して、完了した転送の元の長さを取得できます。 この呼び出しは、転送されなかったバイト数をデバイスが報告する場合に便利です。これは、ドライバーが元の転送の長さから転送できないバイト数を減算して、 **Wdfdmatransactiongetcurrentdmatransferlength**をに呼び出すことができるためです。実際の転送サイズを報告します。

上記の各転送完了メソッドは、( [dma トランザクション](dma-transactions-and-dma-transfers.md)全体ではなく) シングル[dma 転送](dma-transactions-and-dma-transfers.md)が完了したことをフレームワークに通知します。 ドライバーは、これらのメソッドのいずれかを呼び出すと、メソッドの戻り値をチェックして、トランザクションにより多くの転送が必要かどうかを確認します。

-   完了メソッドの戻り値が**FALSE**の場合、このフレームワークは dma トランザクションの処理を完了するために追加の dma 転送が必要であると判断しました。

    通常、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数はを返します。 フレームワークは、ドライバーの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を再度呼び出します。コールバック関数は、次の転送用にハードウェアをプログラミングできます。

    転送の完了方法では、状態の値が提供されます。この値は常に STATUS\_\_処理\_必要があります。

-   戻り値が**TRUE**の場合、DMA トランザクションに対してこれ以上の転送は行われません。

    転送の完了メソッドは、状態の値を提供します。 状態の値\_が [成功] の場合、DMA トランザクションのすべての転送が完了し、ドライバーが[dma トランザクションを完了](completing-a-dma-transaction.md)する必要があります。 状態の値が他の値の場合は、エラーが発生し、DMA トランザクションが完了していない可能性があります。

[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数がエラーを検出した場合、通常はタイマーの有効期限が切れたか、転送エラーを通知するハードウェア割り込みが原因で、ドライバーはトランザクションの現在の転送を再開できます。

トランザクションの現在の転送を再開するには、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、 *transferredlength*パラメーターを0に設定して[**Wdfdmatransactiondmacompletedwithlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactiondmacompletedwithlength)を呼び出すことができます。

 

 





