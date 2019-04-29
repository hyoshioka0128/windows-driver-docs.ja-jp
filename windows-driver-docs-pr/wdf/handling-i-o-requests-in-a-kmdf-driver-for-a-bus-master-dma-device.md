---
title: バス マスター DMA デバイス用 KMDF ドライバーでの I/O 要求の処理
description: このセクションでは、このトピックでは、KMDF ドライバー、バス マスター DMA デバイスが I/O 要求を処理する方法について説明します。 システム モードの DMA を実装する KMDF ドライバーを作成する場合は、システム モード DMA のサポートを参照してください。
ms.assetid: c94819c5-212d-404f-a7c7-b736e0832282
keywords:
- DMA 操作 WDK KMDF、I/O 要求します。
- バス マスター DMA WDK KMDF、I/O 要求します。
- I/O 要求の WDK KMDF、DMA デバイス
- 要求の WDK KMDF、DMA デバイスの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c5cdc8b599b3d6bcb97779509040043f4603f03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391901"
---
# <a name="handling-io-requests-in-a-kmdf-driver-for-a-bus-master-dma-device"></a>バス マスター DMA デバイス用 KMDF ドライバーでの I/O 要求の処理


\[KMDF にのみ適用されます。\]

このセクションでは、このトピックでは、KMDF ドライバー、バス マスター DMA デバイスが I/O 要求を処理する方法について説明します。 システム モードの DMA を実装する KMDF ドライバーを作成する場合は、次を参照してください。[をサポートしているシステム モード DMA](supporting-system-mode-dma.md)します。




KMDF ドライバーでは、バス マスター DMA デバイスの I/O 要求の処理と、次の図に示すように、ドライバーのイベントのコールバック関数のいくつかのコードが必要です。

![kmdf ドライバーで dma の実装](images/dma-implementation-in-kmdf.png)

上記のように、DMA に関連する処理を 4 つのフェーズで行います。

1.  ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)または[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数にする必要があります[DMA を有効にします。トランザクション](enabling-dma-transactions.md)デバイスの場合、ドライバーは、framework の DMA の機能を使用できるようにします。 同じコールバック関数にもする必要があります[一般的なバッファーを作成](using-common-buffers.md)場合は、デバイスとドライバーは、共有メモリ バッファーへのアクセスを必要とします。

2.  ドライバーがドライバーのいずれかの DMA 操作を実行するデバイスを必要とする I/O 要求を受信すると[要求ハンドラー](request-handlers.md)する必要があります[を作成し、新しいトランザクションを DMA を初期化](creating-and-initializing-a-dma-transaction.md)します。 (その場合、ドライバーに注意してください[DMA トランザクション オブジェクトを再利用](reusing-dma-transaction-objects.md)、ドライバーの[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック関数は、トランザクション オブジェクトを作成できます)。要求ハンドラーにする必要がありますし、 [DMA トランザクション開始](starting-a-dma-transaction.md)フレームワークが小さい DMA 転送では、必要に応じて、トランザクションに分割を開始し、ドライバーを呼び出すように[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)コールバック関数。

3.  ドライバーの[ *EvtProgramDma* ](https://msdn.microsoft.com/library/windows/hardware/ff541816)コールバック関数[プログラム DMA ハードウェア](programming-dma-hardware.md)単一 DMA 転送し、デバイスの割り込みを有効にします。

4.  デバイスが割り込み、ときにフレームワークのドライバーの[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)コールバック関数は、揮発性のデバイス情報を保存し、ドライバーの実行をスケジュール[*EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数。

    ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数[DMA の各転送が完了すると](completing-a-dma-transfer.md)ハードウェアでは、処理が完了したら。 転送が完了すると、DMA トランザクションが最終的にした後、 *EvtInterruptDpc*コールバック関数[DMA トランザクションを完了](completing-a-dma-transaction.md)します。

ドライバーが[DMA トランザクション オブジェクトを再利用](reusing-dma-transaction-objects.md)メモリ リソースが少ないときに操作できることを確認します。

ドライバーを処理するコールバック関数のセットを提供できます[DMA 固有の電源管理操作](supporting-power-management-for-dma-devices.md)します。

一部のドライバー[一般的なバッファーを使用して、](using-common-buffers.md)デバイスとドライバーの両方にアクセスできます。

 

 





