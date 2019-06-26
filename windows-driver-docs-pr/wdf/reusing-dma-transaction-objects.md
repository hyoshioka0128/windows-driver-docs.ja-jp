---
title: DMA トランザクション オブジェクトの再利用
description: DMA トランザクション オブジェクトの再利用
ms.assetid: 4adb8653-48b6-4e22-aba3-b909c95b8d15
keywords:
- DMA トランザクション WDK KMDF、トランザクション オブジェクトを再利用
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
- オブジェクトの WDK KMDF DMA のトランザクションを再利用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 160575cb287318a1eaa735f4540b2a0909cb68ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376258"
---
# <a name="reusing-dma-transaction-objects"></a>DMA トランザクション オブジェクトの再利用


\[KMDF にのみ適用されます。\]




ドライバーでは、すべて DMA トランザクションに関連付けられている DMA 転送の処理、後に、ドライバーが削除またはトランザクション オブジェクトを再利用できます。 通常、ドライバーの[ *EvtInterruptDpc* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数は、トランザクション オブジェクトを削除します (呼び出して[ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)). その後、ドライバーは、DMA の新しいトランザクションを作成、呼び出し[ **WdfDmaTransactionCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)新しいトランザクション オブジェクトを作成します。

場合もありますが、トランザクション オブジェクトを再利用するドライバーな役に立ちます。 このような場合、ドライバーが呼び出す[ **WdfDmaTransactionRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)の代わりに[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

など、ドライバーとデバイスが動作する必要があるとするときコンピューター メモリ リソースが不足します。 このメモリの問題を処理するには、ドライバーは、次の手順を使用できます。

1.  ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出すことができます[ **WdfDmaTransactionCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate) 1 つまたは複数のトランザクションを作成するにはオブジェクト。 ドライバーは、これらのトランザクション オブジェクトへのハンドルを保存します。

2.  呼び出すたびに、ドライバーは作成し、新しいトランザクションを初期化する準備ができて[ **WdfDmaTransactionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)します。 このメソッドは、状態を返す場合\_不十分\_リソースを使用できます、保存されているトランザクション オブジェクトの 1 つ。

3.  ドライバーは、その保存されているトランザクション オブジェクトのいずれかを使用している場合は、トランザクションが完了したときに、削除する代わりに、トランザクション オブジェクトを再利用する必要があります。 ドライバーを再利用できるトランザクション オブジェクトを呼び出すことによって設定[ **WdfDmaTransactionRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)の代わりに[ **WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)します。

[PLX9x5x](sample-kmdf-drivers.md)サンプルは、DMA トランザクション オブジェクトを再利用されます。

 

 





