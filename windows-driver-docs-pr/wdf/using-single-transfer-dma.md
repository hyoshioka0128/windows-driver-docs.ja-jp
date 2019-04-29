---
title: 単一転送 DMA の使用
description: このトピックでは、KMDF ドライバーが 1 つ転送 DMA を要求する方法について説明します。
ms.assetid: 57bf9988-6eed-42ca-a961-a6d16c5c19c1
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 976eb2ffabef3f732d39c7ca3e1efabadaf8e95e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391836"
---
# <a name="using-single-transfer-dma"></a>単一転送 DMA の使用

既定では、WDF 場合があります複数 DMA の転送に 1 つの DMA トランザクションに分割します。 ただし、一部のデバイスは断片化されたトランザクションを処理できないし、単一の DMA 操作ですべてのデータを受け取る代わりにする必要があります。  たとえば、PCI の一部のネットワーク コント ローラーでをキャッシュし、部分的なデータを再構築するためのハードウェアがあるないための一度に 1 つのネットワーク パケットが必要です。

DMA トランザクションの 1 つの転送が必要である KMDF バージョン 1.19、DMA を使用して、KMDF ドライバー以降 v3 を指定できます。  ドライバーが 1 つ DMA ののみ、トランザクションの 1 つの転送を指定または指定された DMA イネーブラーを使用して作成されたすべての DMA トランザクションの 1 つの転送を指定できます。  

## <a name="setting-single-transfer-for-a-specific-dma-transaction"></a>設定の特定の DMA トランザクションの 1 つの転送

単一のトランザクションの 1 つの転送を設定するには、次のシーケンスを使用します。

1. 呼び出す[ **WdfDmaTransactionCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547027)または[ **WdfDmaTransactionRelease**](https://msdn.microsoft.com/library/windows/hardware/ff547114)します。
2. 呼び出す[ **WdfDmaTransactionSetSingleTransferRequirement**](https://msdn.microsoft.com/library/windows/hardware/988c7e70-3b2a-4a0f-91cf-dfab3ea07f05)します。
3. 呼び出す[ **WdfDmaTransactionInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff547099)します。  
    トランザクションの断片化のための初期化に失敗した場合は、ドライバーには、I/O 要求が失敗する可能性がまたはトランザクションのメモリ バッファーを再配置し、トランザクションを再初期化します。
4. 呼び出す[ **WdfDmaTransactionExecute**](https://msdn.microsoft.com/library/windows/hardware/ff547062)します。

ドライバーをデバッグするときに使用できます、 [ **! wdfkd.wdfdmatransaction** ](https://msdn.microsoft.com/library/windows/hardware/ff565721)拡張機能を特定のトランザクション オブジェクトの 1 つの転送を設定するかどうかを判断します。

## <a name="setting-the-single-transfer-requirement-for-all-dma-transactions-created-with-a-particular-dma-enabler"></a>特定 DMA イネーブラーで作成されたすべての DMA トランザクションの 1 つの移動要求の設定

特定のイネーブラーで作成されたすべてのトランザクションの 1 つの転送を設定するには、指定、 **WDF_DMA_ENABLER_CONFIG_REQUIRE_SINGLE_TRANSFER**フラグ[ **WDF_DMA_ENABLER_CONFIG_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/hh439491)を呼び出すときに[ **WdfDmaEnablerCreate**](https://msdn.microsoft.com/library/windows/hardware/guid)します。  

このフラグを使用するドライバーを呼び出す必要はありません[ **WdfDmaTransactionSetSingleTransferRequirement** ](https://msdn.microsoft.com/library/windows/hardware/988c7e70-3b2a-4a0f-91cf-dfab3ea07f05)を作成するたびにまたはトランザクション オブジェクトを再利用されます。

この設定は、場合にも保持ドライバー[トランザクション オブジェクトを再利用](reusing-dma-transaction-objects.md)します。

使用して、デバッグ時に、 [ **! wdfkd.wdfdmaenabler** ](https://msdn.microsoft.com/library/windows/hardware/ff565717)拡張機能を特定の DMA イネーブラー オブジェクトの 1 つの転送を設定するかどうかを判断します。

WDF 関数を呼び出してドライバーの DMA イベント コールバックの順序の詳細については、次を参照してください。 [KMDF ドライバーでは、バス マスター DMA デバイスの I/O 要求の処理](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)します。
