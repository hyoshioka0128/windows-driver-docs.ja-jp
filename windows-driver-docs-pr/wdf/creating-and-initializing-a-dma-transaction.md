---
title: DMA トランザクションの作成と初期化
description: DMA トランザクションの作成と初期化
ms.assetid: 1982c3fa-9e4a-4b26-8902-321223d9159f
keywords:
- DMA トランザクション WDK KMDF、初期化しています
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
- DMA トランザクション WDK KMDF、作成します。
- DMA トランザクション WDK KMDF の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34f7aecbdd4b1a66e916180e769dcbceac69f74b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383107"
---
# <a name="creating-and-initializing-a-dma-transaction"></a>DMA トランザクションの作成と初期化


\[KMDF にのみ適用されます。\]




ドライバーは、DMA デバイスに、I/O 要求を送信できるように、ドライバーが必要です。

1.  呼び出す[ **WdfDmaTransactionCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioncreate)要求に対して DMA トランザクション オブジェクトを作成します。

2.  呼び出す[ **WdfDmaTransactionInitializeUsingRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)、 [ **WdfDmaTransactionInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)、または[ **WdfDmaTransactionInitializeUsingOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)トランザクション オブジェクトを初期化します。

ドライバーは通常、作成、 [DMA トランザクション](dma-transactions-and-dma-transfers.md)ため、[要求ハンドラー](request-handlers.md)が受信した、 [framework 要求オブジェクト](framework-request-objects.md)とハードウェアに要求を渡す必要があります。 この場合、ドライバーを呼び出す必要があります[ **WdfDmaTransactionInitializeUsingRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingrequest)、入力として要求オブジェクトのハンドルを受け入れるし、要求オブジェクトからアドレスの要求のパラメーターを抽出します.

DMA トランザクションである、ドライバーを作成する必要があります*いない*をドライバーが受け取った framework 要求オブジェクトに基づき、ドライバー、呼び出すことができます[ **WdfDmaTransactionInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitialize)または[ **WdfDmaTransactionInitializeUsingOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactioninitializeusingoffset)します。 両方のメソッドは、ドライバーが用意されているアドレス パラメーターを受け取ります。

次の 3 つすべての初期化メソッドのアドレスが必要、 [ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)入力パラメーターとしてイベント コールバック関数。 このコールバック関数、デバイスでは、プログラムし、フレームワークにより、コールバック関数が毎回呼び出さ、 [DMA 転送](dma-transactions-and-dma-transfers.md)は使用できます。

ドライバーを呼び出すと[ **WdfDmaEnablerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)ドライバー提供の DMA イネーブラー オブジェクトを作成する、 [ **WDF\_DMA\_の有効化\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)デバイスの最大転送の長さを含む構造体。 フレームワークは、DMA のすべての転送に既定の最大長としてこの値を使用します。

DMA のトランザクションの種類によっては、デバイスの既定の最大長とは異なる転送の最大長を指定する必要があります。 使用することができます[ **WdfDmaTransactionSetMaximumLength** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetmaximumlength)個々 のトランザクションの転送の最大長を設定します。 フレームワークは、指定されたトランザクションを処理するときにのみ指定された最大転送の長さを使用します。

転送の最大長がの数によって制限されることに注意してください。[レジスタにマップ](https://docs.microsoft.com/windows-hardware/drivers/kernel/map-registers)オペレーティング システムは、DMA のイネーブラー オブジェクトで使用できることです。 使用できる最大転送の長さを確認するには、ドライバーを呼び出すことができます[ **WdfDmaEnablerGetFragmentLength**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablergetfragmentlength)します。 場合、値を**WdfDmaEnablerGetFragmentLength**返しますが、ドライバーに指定された最大転送の長さより小さい[ **WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)、フレームワークは、小さい方の値を使用します。

ドライバーである必要があります、ドライバーが作成されし、DMA のトランザクションを初期化します、[トランザクションを開始](starting-a-dma-transaction.md)します。

 

 





