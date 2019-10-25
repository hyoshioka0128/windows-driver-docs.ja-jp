---
title: DMA トランザクション オブジェクトの再利用
description: DMA トランザクション オブジェクトの再利用
ms.assetid: 4adb8653-48b6-4e22-aba3-b909c95b8d15
keywords:
- DMA トランザクション WDK KMDF、トランザクションオブジェクトの再利用
- DMA 操作 WDK KMDF、トランザクション
- バスマスタ DMA WDK KMDF、トランザクション
- DMA トランザクションオブジェクトの再利用 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8bdff06d4317661c744770551a642ec86299b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842224"
---
# <a name="reusing-dma-transaction-objects"></a>DMA トランザクション オブジェクトの再利用


\[は KMDF にのみ適用され\]




ドライバーは、DMA トランザクションに関連付けられているすべての DMA 転送を処理した後、トランザクションオブジェクトを削除または再利用できます。 通常、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) callback 関数は、( [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すことによって) トランザクションオブジェクトを削除します。 その後、ドライバーは新しい DMA トランザクションを作成するときに、 [**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)を呼び出して新しいトランザクションオブジェクトを作成します。

ただし、ドライバーがトランザクションオブジェクトを再利用するのに便利な場合もあります。 このような場合、ドライバーは、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)ではなく[**Wdfdmatransactionrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)を呼び出します。

たとえば、コンピューターのメモリリソースが不足している場合に、ドライバーとデバイスが動作する必要があるとします。 このメモリの問題に対処するために、ドライバーは次の手順を使用できます。

1.  ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数は、 [**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)を呼び出して1つ以上のトランザクションオブジェクトを作成できます。 ドライバーは、これらのトランザクションオブジェクトへのハンドルを保存します。

2.  ドライバーは、新しいトランザクションを作成し初期化する準備が整うたびに、 [**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)を呼び出します。 このメソッドが\_リソース不足の状態\_返される場合、ドライバーは格納されているトランザクションオブジェクトの1つを使用できます。

3.  ドライバーが格納されているトランザクションオブジェクトの1つを使用している場合は、トランザクションが完了すると、トランザクションオブジェクトを削除するのではなく、トランザクションオブジェクトを再利用する必要があります。 このドライバーは、 [**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)ではなく[**Wdfdmatransactionrelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionrelease)を呼び出して、再利用できるようにトランザクションオブジェクトを設定します。

[PLX9x5x](sample-kmdf-drivers.md)サンプルでは、DMA トランザクションオブジェクトを再利用します。

 

 





