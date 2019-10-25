---
title: DMA トランザクションの作成と初期化
description: DMA トランザクションの作成と初期化
ms.assetid: 1982c3fa-9e4a-4b26-8902-321223d9159f
keywords:
- DMA トランザクション WDK KMDF, 初期化
- DMA 操作 WDK KMDF、トランザクション
- バスマスタ DMA WDK KMDF、トランザクション
- DMA トランザクション WDK KMDF, 作成
- DMA トランザクションの初期化 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e34e7c59cdcbc476636cff5cef2d3c7b5ccdaf33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845609"
---
# <a name="creating-and-initializing-a-dma-transaction"></a>DMA トランザクションの作成と初期化


\[は KMDF にのみ適用され\]




ドライバーが DMA デバイスに i/o 要求を送信する前に、ドライバーは次のことを行う必要があります。

1.  [**Wdfdmatransactioncreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)を呼び出して、要求の DMA トランザクションオブジェクトを作成します。

2.  トランザクションオブジェクトを初期化するには、 [**Wdfdmatransactioninitializeenabled request**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)、 [**wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)、または[**wdfdmatransactioninitializeinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)を呼び出します。

通常、ドライバーは[DMA トランザクション](dma-transactions-and-dma-transfers.md)を作成します。これは、[要求ハンドラー](request-handlers.md)が[フレームワーク要求オブジェクト](framework-request-objects.md)を受け取り、要求をハードウェアに渡す必要があるためです。 この場合、ドライバーは[**Wdfdmatransactioninitializeinitializeinitializeinitializerequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)を呼び出す必要があります。この要求は、要求オブジェクトハンドルを入力として受け取り、要求オブジェクトから要求のアドレスパラメーターを抽出します。

ドライバーが、ドライバーによって受信されたフレームワークの要求オブジェクトに基づいて*いない*DMA トランザクションを作成する必要がある場合、ドライバーは[**Wdfdmatransactioninitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)または[**Wdfdmatransactioninitializeinitializeinitializeinitializeoffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)を呼び出すことができます。 どちらのメソッドも、ドライバーが提供するアドレスパラメーターを受け入れます。

3つのすべての初期化メソッドでは、 [*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)イベントコールバック関数のアドレスを入力パラメーターとして指定する必要があります。 このコールバック関数によってデバイスがプログラムされ、 [DMA 転送](dma-transactions-and-dma-transfers.md)が使用可能になるたびにフレームワークによってコールバック関数が呼び出されます。

ドライバーが[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を呼び出して dma イネーブラーオブジェクトを作成すると、ドライバーはデバイスの最大転送長さを含む[**WDF\_dma\_イネーブラー\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)構造を提供します。 フレームワークは、この値をすべての DMA 転送の既定の最大長として使用します。

DMA トランザクションの種類によっては、デバイスの既定の最大長とは異なる最大転送長を指定することが必要になる場合があります。 [**Wdfdmatransactionsetmaximumlength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetmaximumlength)を使用して、個々のトランザクションの最大転送長さを設定できます。 フレームワークは、指定されたトランザクションを処理するときにのみ、指定された最大転送長を使用します。

最大転送長は、オペレーティングシステムが DMA イネーブラーオブジェクトで使用できる[マップレジスタ](https://docs.microsoft.com/windows-hardware/drivers/kernel/map-registers)の数によって制限されていることに注意してください。 使用可能な最大転送長を特定するために、ドライバーは[**WdfDmaEnablerGetFragmentLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablergetfragmentlength)を呼び出すことができます。 **WdfDmaEnablerGetFragmentLength**が返す値が、ドライバーによって[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)に渡された最大転送長より小さい場合、フレームワークでは小さい方の値が使用されます。

ドライバーが DMA トランザクションを作成および初期化した後、ドライバーは[トランザクションを開始](starting-a-dma-transaction.md)する必要があります。

 

 





