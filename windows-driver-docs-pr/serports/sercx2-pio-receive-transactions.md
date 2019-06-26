---
title: SerCx2 PIO-受信トランザクション
description: SerCx2 すべてシリアル コント ローラーを必要とドライバーのサポートを実装するトランザクションの使用が I/O (PIO) をプログラムを受信します。
ms.assetid: 00C43A55-ACAF-4AB6-BDFB-F3D9350C4536
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a29de3836a96c4e0a5b9cbd2985bd00548664f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356774"
---
# <a name="sercx2-pio-receive-transactions"></a>SerCx2 PIO-受信トランザクション

SerCx2 すべてシリアル コント ローラーを必要とドライバーのサポートを実装するトランザクションの使用が I/O (PIO) をプログラムを受信します。 SerCx2 PIO 受信トランザクションを開始するには、ドライバーが呼び出す[ *EvtSerCx2PioReceiveReadBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)イベント コールバック関数と、読み取りバッファーのパラメーターとして提供します。

この呼び出し中に、 *EvtSerCx2PioReceiveReadBuffer*関数は、FIFO シリアル コント ローラーのハードウェアでの受信から読み取りバッファーにデータを転送します。 このデータ転送では、読み取りバッファーがいっぱいか、または、データの受信 FIFO からすぐに利用できるまで続けられます。 転送の終了時に、関数は、FIFO から読み取りバッファーに正常に転送されたバイト数を返します。 この関数より多くのデータを受信することのない待機します。

## <a name="creating-the-pio-receive-object"></a>PIO 受信オブジェクトを作成します。

SerCx2 がコント ローラーのシリアル ドライバーを呼び出す前に*EvtSerCx2PioReceive*Xxx * * 関数の場合、ドライバーが呼び出す必要があります、 [ **SerCx2PioReceiveCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecreate)メソッドSerCx2 でこれらの関数を登録します。 このメソッドは、入力パラメーターとしてへのポインターを[ **SERCX2\_PIO\_受信\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_pio_receive_config)ドライバーのへのポインターを含む構造体*EvtSerCx2PioReceive*Xxx * * 関数。

ドライバーは、次の関数の 3 つすべての実装に必要な。

- [*EvtSerCx2PioReceiveReadBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_read_buffer)
- [*EvtSerCx2PioReceiveEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)
- [*EvtSerCx2PioReceiveCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)

オプションとして、ドライバーは、次の関数の一方または両方を実装できます。

- [*EvtSerCx2PioReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)
- [*EvtSerCx2PioReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)

**SerCx2PioReceiveCreate**メソッドが PIO 受信オブジェクトを作成し、呼び出し元のドライバーを提供する[ **SERCX2PIORECEIVE** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)このオブジェクトのハンドルします。 ドライバーの*EvtSerCx2PioReceive*Xxx * * すべての関数は、最初のパラメーターとしてこのハンドルを受け取ります。 次の SerCx2 メソッドは、最初のパラメーターとして、このハンドルを受け取ります。

- [**SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveready)
- [**SerCx2PioReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)
- [**SerCx2PioReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアル コント ローラーのドライバーによっては、PIO 受信トランザクションの開始時シリアル コント ローラーのハードウェアを初期化するために、またはトランザクションの最後に、シリアル コント ローラーのハードウェアの状態をクリーンアップする必要があります。

ドライバーが実装されている場合、 [ *EvtSerCx2PioReceiveInitializeTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_initialize_transaction)イベント コールバック関数、SerCx2 を呼び出す前にシリアル コント ローラーを初期化するためには、この関数、 *EvtSerCx2PioReceiveReadBuffer*トランザクションを開始した呼び出し。 実装されている場合、 *EvtSerCx2PioReceiveInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2PioReceiveInitializeTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveinitializetransactioncomplete)に通知するメソッドSerCx2 ドライバーでは、シリアル コント ローラーの初期化が完了するとします。

ドライバーが実装されている場合、 [ *EvtSerCx2PioReceiveCleanupTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cleanup_transaction)イベント コールバック関数では、最後後のハードウェアの状態をクリーンアップするには、この関数を呼び出す SerCx2 *EvtSerCx2PioReceiveReadBuffer*トランザクションで呼び出します。 実装されている場合、 *EvtSerCx2PioReceiveInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2PioReceiveCleanupTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceivecleanuptransactioncomplete) SerCx2 を通知するためにメソッドときに、ドライバーでは、シリアル コント ローラーのクリーンアップが完了するとします。

## <a name="ready-notifications"></a>準備完了の通知

ときに、 *EvtSerCx2PioReceiveReadBuffer*以上データはすぐに読み取りが可能な受信 FIFO から SerCx2 後、シリアル コント ローラーで、まで PIO 受信トランザクションを完了できませんので終了を呼び出す多くのデータを受信します。 この場合、SerCx2 を呼び出す、 [ *EvtSerCx2PioReceiveEnableReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_enable_ready_notification)準備完了の通知を有効にするイベントのコールバック関数。 通常、この関数には、1 つまたは複数のバイトのデータは FIFO の受信から読み取り可能なときにトリガーされるように、割り込みが有効にします。 この通知が有効になっている場合にのみシリアル コント ローラー ドライバーが呼び出す、 [ **SerCx2PioReceiveReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveready)受信 FIFO は空でないことに、ドライバーが検出されたときに、SerCx2 を通知するメソッド。 SerCx2 の呼び出しでこの通知に応答して、 *EvtSerCx2PioReceiveReadBuffer*新しく受信したデータを読み取る関数。

さらに SerCx2 では、準備完了の通知を使用して、PIO 受信トランザクションとして処理されます。 読み取り要求の処理中にタイムアウトを効率的に管理します。 これらのタイムアウトの詳細については、次を参照してください。 [**シリアル\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts)します。

SerCx2 を呼び出して、読み取り要求がタイムアウトになるかが取り消されたときに、準備完了の通知が有効である場合、 [ *EvtSerCx2PioReceiveCancelReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_receive_cancel_ready_notification)をキャンセルするイベントのコールバック関数、保留中通知します。 返すかどうかはこの関数は、保留中の通知を正常にキャンセル、 **TRUE**します。 戻り値**TRUE**シリアル コント ローラー ドライバーが呼び出すことが保証されます[ **SerCx2PioReceiveReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2pioreceiveready)します。 戻り値**FALSE**コント ローラー ドライバーが既に呼び出されてかがすぐに呼び出すことを示します**SerCx2PioReceiveReady**します。
