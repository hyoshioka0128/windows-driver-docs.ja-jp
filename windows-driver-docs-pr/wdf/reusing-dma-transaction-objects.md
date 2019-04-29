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
ms.openlocfilehash: 9d1192296f31c275ac4552498e99f3120a77579d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325183"
---
# <a name="reusing-dma-transaction-objects"></a>DMA トランザクション オブジェクトの再利用


\[KMDF にのみ適用されます。\]




ドライバーでは、すべて DMA トランザクションに関連付けられている DMA 転送の処理、後に、ドライバーが削除またはトランザクション オブジェクトを再利用できます。 通常、ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数は、トランザクション オブジェクトを削除します (呼び出して[ **WdfObjectDelete** ](https://msdn.microsoft.com/library/windows/hardware/ff548734)). その後、ドライバーは、DMA の新しいトランザクションを作成、呼び出し[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)新しいトランザクション オブジェクトを作成します。

場合もありますが、トランザクション オブジェクトを再利用するドライバーな役に立ちます。 このような場合、ドライバーが呼び出す[ **WdfDmaTransactionRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff547114)の代わりに[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)します。

など、ドライバーとデバイスが動作する必要があるとするときコンピューター メモリ リソースが不足します。 このメモリの問題を処理するには、ドライバーは、次の手順を使用できます。

1.  ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数を呼び出すことができます[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027) 1 つまたは複数のトランザクションを作成するにはオブジェクト。 ドライバーは、これらのトランザクション オブジェクトへのハンドルを保存します。

2.  呼び出すたびに、ドライバーは作成し、新しいトランザクションを初期化する準備ができて[ **WdfDmaTransactionCreate**](https://msdn.microsoft.com/library/windows/hardware/ff547027)します。 このメソッドは、状態を返す場合\_不十分\_リソースを使用できます、保存されているトランザクション オブジェクトの 1 つ。

3.  ドライバーは、その保存されているトランザクション オブジェクトのいずれかを使用している場合は、トランザクションが完了したときに、削除する代わりに、トランザクション オブジェクトを再利用する必要があります。 ドライバーを再利用できるトランザクション オブジェクトを呼び出すことによって設定[ **WdfDmaTransactionRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff547114)の代わりに[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)します。

[PLX9x5x](sample-kmdf-drivers.md)サンプルは、DMA トランザクション オブジェクトを再利用されます。

 

 





