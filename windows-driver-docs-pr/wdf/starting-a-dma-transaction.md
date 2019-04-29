---
title: DMA トランザクションの開始
description: DMA トランザクションの開始
ms.assetid: fa26ef08-01c0-4502-9cb3-865000242e4a
keywords:
- DMA トランザクション WDK KMDF、開始
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
- DMA トランザクション WDK KMDF の開始
- スキャッター/ギャザー DMA WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68c7a60344d3a9f86d034b679d9b10fb04f87cea
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325128"
---
# <a name="starting-a-dma-transaction"></a>DMA トランザクションの開始


\[KMDF にのみ適用されます。\]




ドライバーが[作成され、DMA トランザクションを初期化](creating-and-initializing-a-dma-transaction.md)、ドライバーを呼び出すことができます、 [ **WdfDmaTransactionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff547062)トランザクションを開始する方法。 このメソッドは、最初のスキャッター/ギャザー リストを構築[DMA 転送](dma-transactions-and-dma-transfers.md)トランザクションに関連付けられています。 次に、メソッドを呼び出して、 [ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)トランザクションのドライバーが登録されているコールバック関数。 コールバック関数[プログラム DMA ハードウェア](programming-dma-hardware.md)転送を開始します。

ドライバーの呼び出しの前に**WdfDmaTransactionExecute**ドライバーはドライバーには、トランザクションに関連付けられている各 DMA 転送が完了すると後で取得することができるように、DMA のトランザクション ハンドルを格納する必要があります。 Framework のオブジェクトでは、通常、デバイスの framework デバイス オブジェクトのコンテキストのメモリはトランザクション ハンドルを格納する適切な場所。 オブジェクト コンテキストのメモリの使用に関する詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](framework-object-context-space.md)します。

次のコード例から、 [PLX9x5x](https://go.microsoft.com/fwlink/p/?linkid=256157)サンプルを初期化し、DMA トランザクションを実行する方法を示しています。 このコードは、 *Read.c*ファイル。

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









