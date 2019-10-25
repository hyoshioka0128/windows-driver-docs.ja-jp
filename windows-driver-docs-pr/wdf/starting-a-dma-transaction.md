---
title: DMA トランザクションの開始
description: DMA トランザクションの開始
ms.assetid: fa26ef08-01c0-4502-9cb3-865000242e4a
keywords:
- DMA トランザクション WDK KMDF、開始
- DMA 操作 WDK KMDF、トランザクション
- バスマスタ DMA WDK KMDF、トランザクション
- DMA トランザクションの開始 (WDK KMDF)
- スキャッター/ギャザー DMA WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 762ebbb9f70989fa73d673e9f0397309c5d1562e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845193"
---
# <a name="starting-a-dma-transaction"></a>DMA トランザクションの開始


\[は KMDF にのみ適用され\]




ドライバーによって[DMA トランザクションが作成および初期化されると](creating-and-initializing-a-dma-transaction.md)、ドライバーは[**Wdfdmatransactionexecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionexecute)メソッドを呼び出してトランザクションを開始できます。 このメソッドは、トランザクションに関連付けられている最初の[DMA 転送](dma-transactions-and-dma-transfers.md)のスキャッター/ギャザーリストを構築します。 次に、メソッドは、ドライバーによってトランザクション用に登録された[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を呼び出します。 コールバック関数は、 [DMA ハードウェアをプログラム](programming-dma-hardware.md)して転送を開始します。

ドライバーが**Wdfdmatransactionexecute**を呼び出す前に、ドライバーは、後でトランザクションに関連付けられている各 dma 転送を完了したときに取得できるように、dma トランザクションハンドルを格納する必要があります。 トランザクションハンドルを格納するための適切な場所は、フレームワークオブジェクト (通常はデバイスのフレームワークデバイスオブジェクト) のコンテキストメモリ内にあります。 オブジェクトコンテキストメモリの使用の詳細については、「[フレームワークオブジェクトコンテキスト空間](framework-object-context-space.md)」を参照してください。

[PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルの次のコード例は、DMA トランザクションを初期化して実行する方法を示しています。 このコードは、 *Read .c*ファイルに記述されています。

```cpp
VOID PLxEvtIoRead(
    IN WDFQUEUE         Queue,
    IN WDFREQUEST       Request,
    IN size_t           Length
    )
{
    NTSTATUS            status = STATUS_UNSUCCESSFUL;
    PDEVICE_EXTENSION   devExt;
    // Get the DevExt from the queue handle
    devExt = PLxGetDeviceContext(WdfIoQueueGetDevice(Queue));
    do {
        // Validate the Length parameter.
        if (Length > PCI9656_SRAM_SIZE)  {
            status = STATUS_INVALID_BUFFER_SIZE;
            break;
        }
        // Initialize the DmaTransaction.
        status = 
           WdfDmaTransactionInitializeUsingRequest(
                 devExt->ReadDmaTransaction,
                 Request, 
                 PLxEvtProgramReadDma, 
                 WdfDmaDirectionReadFromDevice 
           );
        if(!NT_SUCCESS(status)) {
            . . . //Error-handling code omitted
            break; 
        }
        // Execute this DmaTransaction.
        status = WdfDmaTransactionExecute( devExt->ReadDmaTransaction, 
                                           WDF_NO_CONTEXT);
        if(!NT_SUCCESS(status)) {
            . . . //Error-handling code omitted
            break; 
        }
        // Indicate that the DMA transaction started successfully.
        // The DPC routine will complete the request when the DMA
        // transaction is complete.
        status = STATUS_SUCCESS;
    } while (0);
    // If there are errors, clean up and complete the request.
    if (!NT_SUCCESS(status )) {
        WdfDmaTransactionRelease(devExt->ReadDmaTransaction); 
        WdfRequestComplete(Request, status);
    }
    return;
}
```









