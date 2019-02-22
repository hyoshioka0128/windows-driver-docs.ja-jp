---
title: 作成と初期化 DMA トランザクション
description: 作成と初期化 DMA トランザクション
ms.assetid: 1982c3fa-9e4a-4b26-8902-321223d9159f
keywords:
- DMA トランザクション WDK KMDF、初期化しています
- DMA 操作 WDK KMDF、トランザクション
- バス マスター DMA WDK KMDF、トランザクション
- DMA トランザクション WDK KMDF、作成します。
- DMA トランザクション WDK KMDF の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef4e5b19acb4c005e2280d2eb234969df171b0a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531588"
---
# <a name="creating-and-initializing-a-dma-transaction"></a>作成と初期化 DMA トランザクション


\[KMDF にのみ適用されます。\]




ドライバーは、DMA デバイスに、I/O 要求を送信できるように、ドライバーが必要です。

1.  呼び出す[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)要求に対して DMA トランザクション オブジェクトを作成します。

2.  呼び出す[ **WdfDmaTransactionInitializeUsingRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547107)、 [ **WdfDmaTransactionInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff547099)、または[ **WdfDmaTransactionInitializeUsingOffset** ](https://msdn.microsoft.com/library/windows/hardware/hh451182)トランザクション オブジェクトを初期化します。

ドライバーは通常、作成、 [DMA トランザクション](dma-transactions-and-dma-transfers.md)ため、[要求ハンドラー](request-handlers.md)が受信した、 [framework 要求オブジェクト](framework-request-objects.md)とハードウェアに要求を渡す必要があります。 この場合、ドライバーを呼び出す必要があります[ **WdfDmaTransactionInitializeUsingRequest**](https://msdn.microsoft.com/library/windows/hardware/ff547107)、入力として要求オブジェクトのハンドルを受け入れるし、要求オブジェクトからアドレスの要求のパラメーターを抽出します.

DMA トランザクションである、ドライバーを作成する必要があります*いない*をドライバーが受け取った framework 要求オブジェクトに基づき、ドライバー、呼び出すことができます[ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)または[ **WdfDmaTransactionInitializeUsingOffset**](https://msdn.microsoft.com/library/windows/hardware/hh451182)します。 両方のメソッドは、ドライバーが用意されているアドレス パラメーターを受け取ります。

次の 3 つすべての初期化メソッドのアドレスが必要、 [ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)入力パラメーターとしてイベント コールバック関数。 このコールバック関数、デバイスでは、プログラムし、フレームワークにより、コールバック関数が毎回呼び出さ、 [DMA 転送](dma-transactions-and-dma-transfers.md)は使用できます。

ドライバーを呼び出すと[ **WdfDmaEnablerCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff546983)ドライバー提供の DMA イネーブラー オブジェクトを作成する、 [ **WDF\_DMA\_の有効化\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff551290)デバイスの最大転送の長さを含む構造体。 フレームワークは、DMA のすべての転送に既定の最大長としてこの値を使用します。

DMA のトランザクションの種類によっては、デバイスの既定の最大長とは異なる転送の最大長を指定する必要があります。 使用することができます[ **WdfDmaTransactionSetMaximumLength** ](https://msdn.microsoft.com/library/windows/hardware/ff547127)個々 のトランザクションの転送の最大長を設定します。 フレームワークは、指定されたトランザクションを処理するときにのみ指定された最大転送の長さを使用します。

転送の最大長がの数によって制限されることに注意してください。[レジスタにマップ](https://msdn.microsoft.com/library/windows/hardware/ff554406)オペレーティング システムは、DMA のイネーブラー オブジェクトで使用できることです。 使用できる最大転送の長さを確認するには、ドライバーを呼び出すことができます[ **WdfDmaEnablerGetFragmentLength**](https://msdn.microsoft.com/library/windows/hardware/ff546986)します。 場合、値を**WdfDmaEnablerGetFragmentLength**返しますが、ドライバーに指定された最大転送の長さより小さい[ **WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/ff546983)、フレームワークは、小さい方の値を使用します。

ドライバーである必要があります、ドライバーが作成されし、DMA のトランザクションを初期化します、[トランザクションを開始](starting-a-dma-transaction.md)します。

 

 





