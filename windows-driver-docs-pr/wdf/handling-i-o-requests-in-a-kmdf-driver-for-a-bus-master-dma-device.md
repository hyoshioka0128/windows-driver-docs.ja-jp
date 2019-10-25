---
title: バス マスター DMA デバイス用 KMDF ドライバーでの I/O 要求の処理
description: このセクションのこのトピックでは、バスマスタ DMA デバイス用の KMDF ドライバーが i/o 要求を処理する方法について説明します。 システムモードの DMA を実装する KMDF ドライバーを作成する場合は、「システムモードの DMA のサポート」を参照してください。
ms.assetid: c94819c5-212d-404f-a7c7-b736e0832282
keywords:
- DMA 操作 WDK KMDF、i/o 要求
- バスマスタ DMA WDK KMDF、i/o 要求
- I/o 要求 WDK KMDF、DMA デバイス
- 要求処理 WDK KMDF、DMA デバイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f4d69a8c9a01529f6fd4bc1833264d4a5dd38e9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845221"
---
# <a name="handling-io-requests-in-a-kmdf-driver-for-a-bus-master-dma-device"></a>バス マスター DMA デバイス用 KMDF ドライバーでの I/O 要求の処理


\[は KMDF にのみ適用され\]

このセクションのこのトピックでは、バスマスタ DMA デバイス用の KMDF ドライバーが i/o 要求を処理する方法について説明します。 システムモードの DMA を実装する KMDF ドライバーを作成する場合は、「[システムモードの dma のサポート](supporting-system-mode-dma.md)」を参照してください。




バスマスタ DMA デバイス用の KMDF ドライバーで i/o 要求を処理するには、次の図に示すように、ドライバーのイベントコールバック関数のコードが必要です。

![kmdf ドライバーでの dma の実装](images/dma-implementation-in-kmdf.png)

上記のように、DMA 関連の処理は、次の4つのフェーズで行われます。

1.  ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)または[*evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数では、デバイスの[dma トランザクションを有効](enabling-dma-transactions.md)にして、ドライバーがフレームワークの dma 機能を使用できるようにする必要があります。 デバイスとドライバーが共有メモリバッファーへのアクセスを必要とする場合は、同じコールバック関数も[共通のバッファーを作成](using-common-buffers.md)する必要があります。

2.  デバイスが DMA 操作の実行を必要とする i/o 要求を受信すると、ドライバーの[要求ハンドラー](request-handlers.md)の1つが、[新しい dma トランザクションを作成し、初期化](creating-and-initializing-a-dma-transaction.md)する必要があります。 (ドライバーが[DMA トランザクションオブジェクト](reusing-dma-transaction-objects.md)を再利用する場合は、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数でトランザクションオブジェクトを作成できます)。次に、要求ハンドラーは[dma トランザクションを開始](starting-a-dma-transaction.md)する必要があります。これにより、必要に応じて、フレームワークがトランザクションをより小さな DMA 転送に分割し、ドライバーの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を呼び出すことができるようになります。

3.  お使いのドライバーの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数によって[、dma ハードウェアが](programming-dma-hardware.md)1 つの dma 転送用にプログラムされ、デバイスの割り込みが有効になります。

4.  デバイスが割り込みを行うと、フレームワークはドライバーの[*EvtInterruptIsr*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr) callback 関数を呼び出します。これにより、揮発性のデバイス情報が保存され、ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数の実行がスケジュールされます。

    ドライバーの[*EvtInterruptDpc*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)コールバック関数は、ハードウェアが処理を完了した後、[各 DMA 転送を完了](completing-a-dma-transfer.md)します。 DMA トランザクションの最後の転送が完了すると、 *EvtInterruptDpc* callback 関数は[dma トランザクションを完了](completing-a-dma-transaction.md)します。

ドライバーは、 [DMA トランザクションオブジェクトを再利用](reusing-dma-transaction-objects.md)して、メモリリソースが不足しても動作できるようにすることができます。

ドライバーは、 [DMA 固有の電源管理操作](supporting-power-management-for-dma-devices.md)を処理するコールバック関数のセットを提供できます。

一部のドライバーでは、デバイスとドライバーの両方がアクセスできる[共通のバッファーを使用](using-common-buffers.md)します。

 

 





