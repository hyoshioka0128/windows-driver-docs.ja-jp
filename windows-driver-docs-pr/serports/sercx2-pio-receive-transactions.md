---
title: SerCx2 PIO-受信トランザクション
description: SerCx2 では、プログラム i/o (PIO) を使用する受信トランザクションのサポートを実装するために、すべてのシリアルコントローラードライバーが必要です。
ms.assetid: 00C43A55-ACAF-4AB6-BDFB-F3D9350C4536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74b09b724e4b4a08ac7fea592f0de353649a6e47
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845403"
---
# <a name="sercx2-pio-receive-transactions"></a>SerCx2 PIO-受信トランザクション

SerCx2 では、プログラム i/o (PIO) を使用する受信トランザクションのサポートを実装するために、すべてのシリアルコントローラードライバーが必要です。 PIO 受信トランザクションを開始するために、SerCx2 はドライバーの[*EvtSerCx2PioReceiveReadBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)イベントコールバック関数を呼び出し、パラメーターとして読み取りバッファーを提供します。

この呼び出し中、 *EvtSerCx2PioReceiveReadBuffer*関数は、シリアルコントローラーハードウェアの受信 FIFO から読み取りバッファーにデータを転送します。 このデータ転送は、読み取りバッファーがいっぱいになるか、receive FIFO からすぐに使用できるデータがない状態になるまで続行されます。 転送が終了すると、この関数は、FIFO から読み取りバッファーに正常に転送されたバイト数を返します。 この関数は、さらに多くのデータを受信するのを待機することはありません。

## <a name="creating-the-pio-receive-object"></a>PIO 受信オブジェクトの作成

SerCx2 がシリアルコントローラードライバーの*EvtSerCx2PioReceive*Xxx * * 関数を呼び出すことができるようにするには、ドライバーが[**SerCx2PioReceiveCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecreate)メソッドを呼び出してこれらの関数を SerCx2 に登録する必要があります。 このメソッドは、入力パラメーターとして、 [**SERCX2\_PIO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_pio_receive_config)へのポインターとして、ドライバーの*EvtSerCx2PioReceive*Xxx * * 関数へのポインターを含む CONFIG 構造体を\_受け取ります。

ドライバーは、次の3つの機能すべてを実装する必要があります。

- [*EvtSerCx2PioReceiveReadBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)
- [*EvtSerCx2PioReceiveEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)
- [*EvtSerCx2PioReceiveCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)

オプションとして、ドライバーは次の機能のいずれかまたは両方を実装できます。

- [*EvtSerCx2PioReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)
- [*EvtSerCx2PioReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)

**SerCx2PioReceiveCreate**メソッドは、PIO 受信オブジェクトを作成し、このオブジェクトへの[**SERCX2PIORECEIVE**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)ハンドルを呼び出し元のドライバーに提供します。 ドライバーの*EvtSerCx2PioReceive*Xxx * * 関数はすべて、このハンドルを最初のパラメーターとして受け取ります。 次の SerCx2 メソッドは、このハンドルを最初のパラメーターとして受け取ります。

- [**SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveready)
- [**SerCx2PioReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)
- [**SerCx2PioReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアルコントローラードライバーによっては、PIO 受信トランザクションの開始時にシリアルコントローラーハードウェアを初期化したり、トランザクションの終了時にシリアルコントローラーのハードウェア状態をクリーンアップしたりすることが必要になる場合があります。

ドライバーが[*EvtSerCx2PioReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションを開始する*EvtSerCx2PioReceiveReadBuffer*呼び出しの前にシリアルコントローラーを初期化します。 実装されている場合、 *EvtSerCx2PioReceiveInitializeTransaction*関数は[**SerCx2PioReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーの初期化を完了したときに SerCx2 に通知する必要があります。

ドライバーが[*EvtSerCx2PioReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションの最終*EvtSerCx2PioReceiveReadBuffer*呼び出しの後にハードウェアの状態をクリーンアップします。 実装されている場合、 *EvtSerCx2PioReceiveInitializeTransaction*関数は[**SerCx2PioReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーのクリーンアップを完了したことを SerCx2 に通知する必要があります。

## <a name="ready-notifications"></a>準備完了の通知

Receive FIFO から読み取ることができるデータがなくなったために*EvtSerCx2PioReceiveReadBuffer*呼び出しが終了した場合、SerCx2 は、後でシリアルコントローラーがより多くのデータを受信するまで、PIO 受信トランザクションを完了できません。 この場合、SerCx2 は[*EvtSerCx2PioReceiveEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)イベントコールバック関数を呼び出して、準備完了の通知を有効にします。 通常、この関数は、1バイト以上のデータを受信 FIFO から読み取ることができる場合に、割り込みがトリガーされるようにします。 この通知が有効になっている場合にのみ、シリアルコントローラードライバーは[**SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveready)メソッドを呼び出して、受信 FIFO が空になっていないことをドライバーが検出したときに SerCx2 に通知します。 この通知に応答して、SerCx2 は*EvtSerCx2PioReceiveReadBuffer*関数を呼び出して、新しく受信したデータを読み取ります。

また、SerCx2 は準備完了の通知を使用して、PIO-受信トランザクションとして処理される読み取り要求の処理中にタイムアウトを効率的に管理します。 これらのタイムアウトの詳細については、「 [**SERIAL\_のタイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)」を参照してください。

読み取り要求がタイムアウトまたはキャンセルされたときに準備完了の通知が有効になっている場合、SerCx2 は[*EvtSerCx2PioReceiveCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)イベントコールバック関数を呼び出して、保留中の通知をキャンセルします。 この関数が保留中の通知を正常にキャンセルした場合は、 **TRUE**を返します。 戻り値が**TRUE の場合**、シリアルコントローラードライバーは[**SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2pioreceiveready)を呼び出さないことを保証します。 戻り値が**FALSE**の場合は、コントローラードライバーが既に呼び出されているか、すぐに**SerCx2PioReceiveReady**を呼び出したことを示します。
