---
title: DMA リソースの予約
description: DMA リソースの予約
ms.assetid: 8C5FF779-8D54-47D9-8EC6-7D4921F8F697
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d76698c0c8b89b907354e1f06bb30730d277d8fb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325170"
---
# <a name="reserving-dma-resources"></a>DMA リソースの予約


\[KMDF にのみ適用されます。\]

通常、フレームワーク ベースのドライバーは、前もってマップ レジスタを予約できません。 ただし、特定の状況では、ドライバーはこれらのリソースを事前に予約する必要があります。

Windows 8 以降を実行している framework ベースのドライバーでは、パケットまたはシステムのプロファイルを指定する DMA イネーブラーのマップ レジスタの指定した数を予約できます。 これは、ドライバーの呼び出しを行うに[ **WdfDmaTransactionAllocateResources** ](https://msdn.microsoft.com/library/windows/hardware/hh451123)し、登録、 [ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)コールバック関数。

フレームワークは、ドライバーの[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)は予約マップ レジスタおよび WDM DMA アダプターのロック時に機能します。 ドライバーは、初期化し、最後にトランザクション オブジェクトを解放する前に、同じトランザクション オブジェクトを使用して複数回のトランザクションを開始します。 DMA を解放するリソースのバックアップ システム、ドライバーの呼び出しに[ **WdfDmaTransactionFreeResources**](https://msdn.microsoft.com/library/windows/hardware/hh451177)します。

トランザクションに必要なマップのレジスタの数を確認するには、ドライバーを呼び出すことができます[ **WdfDmaTransactionGetTransferInfo** ](https://msdn.microsoft.com/library/windows/hardware/hh451179)呼び出す前に[ **WdfDmaTransactionAllocateResources**](https://msdn.microsoft.com/library/windows/hardware/hh451123)します。 ドライバーは、呼び出す前にトランザクションを初期化する必要があります**WdfDmaTransactionGetTransferInfo**します。

次の手順では、ドライバーの予約および指定されたトランザクションを排他的に使用 DMA イネーブラーをリリースする方法を示します。

1.  ドライバーは、I/O 要求を受信します。

2.  ドライバーの[要求ハンドラー](request-handlers.md)呼び出し[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)要求に対して DMA トランザクション オブジェクトを作成します。

3.  ドライバーの[要求ハンドラー](request-handlers.md)呼び出し[ **WdfDmaTransactionAllocateResources** ](https://msdn.microsoft.com/library/windows/hardware/hh451123)リソースを予約します。

4.  Framework 呼び出し[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)ときに、要求されたリソースが予約されます。

5.  [ *EvtReserveDma*](https://msdn.microsoft.com/library/windows/hardware/hh406425)、ドライバー呼び出し[ **WdfDmaTransactionInitializeUsingRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff547107)または[ **WdfDmaTransactionInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff547099)トランザクション オブジェクトを初期化します。

6.  [ *EvtReserveDma*](https://msdn.microsoft.com/library/windows/hardware/hh406425)、ドライバーの呼び出し、 [ **WdfDmaTransactionExecute** ](https://msdn.microsoft.com/library/windows/hardware/ff547062)トランザクションを開始する方法。 フレームワークは、ドライバーのすぐに呼び出しますので、トランザクションには、リソースが予約されていますが、 [ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)コールバック関数。

7.  [ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDmaTransactionDmaTransferComplete*](https://msdn.microsoft.com/library/windows/hardware/hh406418)、ドライバー呼び出し[ **WdfDmaTransactionDmaCompleted**](https://msdn.microsoft.com/library/windows/hardware/ff547039)、 [ **WdfDmaTransactionDmaCompletedWithLength**](https://msdn.microsoft.com/library/windows/hardware/ff547052)、または[ **WdfDmaTransactionDmaCompletedFinal**](https://msdn.microsoft.com/library/windows/hardware/ff547049)、その後に[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)または[ **WdfDmaTransactionRelease**](https://msdn.microsoft.com/library/windows/hardware/ff547114). ドライバーの削除またはトランザクションが完了またはキャンセルされるまで、トランザクションを解放する必要がありますされません。 この手順が完了した後、マップのレジスタまま予約済みです。

8.  ドライバーは、必要な回数だけ手順 5 ~ 7 を繰り返すことができます。

    ドライバーには、予約が不要、ドライバーが呼び出し[ **WdfDmaTransactionFreeResources** ](https://msdn.microsoft.com/library/windows/hardware/hh451177)から[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)または[ *EvtDmaTransactionDmaTransferComplete*](https://msdn.microsoft.com/library/windows/hardware/hh406418)します。 または、ドライバーが呼び出せる**WdfDmaTransactionFreeResources**からその[ *EvtReserveDma* ](https://msdn.microsoft.com/library/windows/hardware/hh406425)イベント コールバック関数。

 

 





