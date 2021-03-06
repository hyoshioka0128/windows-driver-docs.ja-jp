---
title: SerCx2 PIO-送信トランザクション
description: SerCx2 すべてシリアル コント ローラーを必要とドライバーのサポートを実装するトランザクションの使用が I/O (PIO) をプログラムを送信します。
ms.assetid: 3BEF9A3D-1FEF-4626-B07F-1670359062AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9127e5c30537d40ab31a955df68a6ce6a9a0112f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356769"
---
# <a name="sercx2-pio-transmit-transactions"></a>SerCx2 PIO-送信トランザクション

SerCx2 すべてシリアル コント ローラーを必要とドライバーのサポートを実装するトランザクションの使用が I/O (PIO) をプログラムを送信します。 SerCx2 PIO 送信トランザクションを開始するには、ドライバーが呼び出す[ *EvtSerCx2PioTransmitWriteBuffer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)イベント コールバック関数と書き込みをバッファーをパラメーターとして提供します。

この呼び出し中に、 *EvtSerCx2PioTransmitWriteBuffer*関数は、FIFO シリアル コント ローラーのハードウェアでの送信に書き込みバッファーからデータを転送します。 このデータ転送は、書き込みバッファーが空か、または送信 FIFO はより多くのデータを受け付けることができませんすぐにまで続けます。 転送の終了時に、関数は、FIFO に書き込みバッファーから正常に転送されたバイト数を返します。

## <a name="creating-the-pio-transmit-object"></a>PIO 送信オブジェクトを作成します。

SerCx2 がコント ローラーのシリアル ドライバーを呼び出す前に*EvtSerCx2PioTransmit*Xxx * * 関数の場合、ドライバーが呼び出す必要があります、 [ **SerCx2PioTransmitCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcreate)メソッドSerCx2 でこれらの関数を登録します。 このメソッドは、入力パラメーターとしてへのポインターを[ **SERCX2\_PIO\_送信\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_pio_transmit_config)ドライバーのへのポインターを含む構造体*EvtSerCx2PioTransmit*Xxx * * 関数。

ドライバーは、次の関数の 3 つすべての実装に必要な。

- [*EvtSerCx2PioTransmitWriteBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)
- [*EvtSerCx2PioTransmitEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)
- [*EvtSerCx2PioTransmitCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)

オプションとして、ドライバーは、次の関数の一方または両方を実装できます。

- [*EvtSerCx2PioTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)
- [*EvtSerCx2PioTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)

オプションとして、ドライバーは、次の 3 つの関数を実装できます。

- [*EvtSerCx2PioTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)
- [*EvtSerCx2PioTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)
- [*EvtSerCx2PioTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_purge_fifo)

ドライバーは、上記の一覧で任意の関数を実装する場合は、3 つすべてを実装する必要があります。

**SerCx2PioTransmitCreate**メソッドが PIO 送信オブジェクトを作成し、呼び出し元のドライバーを提供する[ **SERCX2PIOTRANSMIT** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)このオブジェクトのハンドルします。 ドライバーの*EvtSerCx2PioTransmit*Xxx * * すべての関数は、最初のパラメーターとしてこのハンドルを受け取ります。 次の SerCx2 メソッドは、最初のパラメーターとして、このハンドルを受け取ります。

- [**SerCx2PioTransmitReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitready)
- [**SerCx2PioTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)
- [**SerCx2PioTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)
- [**SerCx2PioTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)
- [**SerCx2PioTransmitPurgeFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitpurgefifocomplete)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアル コント ローラーのドライバーによっては、PIO 送信トランザクションの開始時シリアル コント ローラーのハードウェアを初期化するために、またはトランザクションの最後に、シリアル コント ローラーのハードウェアの状態をクリーンアップする必要があります。

ドライバーが実装されている場合、 [ *EvtSerCx2PioTransmitInitializeTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)イベント コールバック関数、SerCx2 を呼び出す前にシリアル コント ローラーを初期化するためには、この関数、 *EvtSerCx2PioTransmitWriteBuffer*トランザクションを開始した呼び出し。 実装されている場合、 *EvtSerCx2PioTransmitInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2PioTransmitInitializeTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)に通知するメソッドSerCx2 ドライバーでは、シリアル コント ローラーの初期化が完了するとします。

ドライバーが実装されている場合、 [ *EvtSerCx2PioTransmitCleanupTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)イベント コールバック関数では、最後後のハードウェアの状態をクリーンアップするには、この関数を呼び出す SerCx2 *EvtSerCx2PioTransmitWriteBuffer*トランザクションで呼び出します。 実装されている場合、 *EvtSerCx2PioTransmitInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2PioTransmitCleanupTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)に通知するメソッドSerCx2 ドライバーでは、シリアル コント ローラーのクリーンアップが完了するとします。

## <a name="draining-and-purging-the-transmit-fifo"></a>ドレインと送信の FIFO の削除

シリアル コント ローラーのドライバーを実装する必要があります、 [ *EvtSerCx2PioTransmitDrainFifo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)送信 FIFO を空にすると、ドライバーが検出された場合に、イベント コールバック関数。 実装されている場合、SerCx2 は、FIFO の送信に PIO 送信トランザクション内のデータの最後のバイトが書き込まれた後、この関数を呼び出します。 この呼び出し中に、 *EvtSerCx2PioTransmitDrainFifo*関数は、通常、割り込み送信 FIFO が空にするときにトリガーされるように、待機せず返しますにできます。 FIFO を空に、ドライバーが呼び出し、 [ **SerCx2PioTransmitDrainFifoComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete) SerCx2 に通知するメソッド。 この通知を受信した後にのみが SerCx2 完了保留中の書き込み ([**IRP\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) PIO 送信トランザクションに関連付けられている要求。

シリアル コント ローラー ドライバーが実装していない場合、 *EvtSerCx2PioTransmitDrainFifo*関数、SerCx2 する必要があります保留中の書き込みの要求を完了せず、送信 FIFO を空にすることを確認しています。 大幅な遅延なし、FIFO に書き込まれたデータが送信されることの保証はできません。 送信できる前に、書き込み要求が完了した後、FIFO に残っているすべてのデータは失われます。 この予期しないデータの損失を正常に完了した書き込み要求では、要求を送信した周辺のドライバーの信頼性の問題を作成できます。

実装するドライバー、 *EvtSerCx2PioTransmitDrainFifo*関数を実装する必要がありますも[ *EvtSerCx2PioTransmitCancelDrainFifo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)と[ *EvtSerCx2PioTransmitPurgeFifo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)イベント コールバック関数。

*EvtSerCx2PioTransmitCancelDrainFifo*関数が完了する前に、実行中の FIFO ドレイン操作をキャンセルする SerCx2 を有効にします。 SerCx2 は、書き込み要求がタイムアウトになるかが取り消された場合、この操作を取り消すことがあります。 場合、 *EvtSerCx2PioTransmitCancelDrainFifo* FIFO ドレイン操作が正常にキャンセルする関数と、この関数を返します**TRUE**します。 戻り値**TRUE**シリアル コント ローラー ドライバーが呼び出さし、呼び出すことが保証されます**SerCx2PioTransmitDrainFifoComplete**します。 戻り値**FALSE**ことを示します、 *EvtSerCx2PioTransmitDrainFifo*関数が呼び出されてまたは呼び出しはすぐに**SerCx2PioTransmitDrainFifoComplete**します。

PIO 送信トランザクションに関連付けられた書き込み要求をキャンセルまたは時刻を完了前に SerCx2 を呼び出す場合、 *EvtSerCx2PioTransmitPurgeFifo*関数は、これを実装している可能性があります、未送信のデータを破棄する場合FIFO の送信を維持します。 SerCx2 には、正確にデータのバイト数が正常にによって送信された周辺機器への書き込み要求を周辺のドライバーに通知するこの関数から取得する情報が使用されます。

## <a name="ready-notifications"></a>準備完了の通知

ときに、 *EvtSerCx2PioTransmitWriteBuffer*呼び出し終了送信 FIFO より多くのデータを受け入れるすぐにできないため、SerCx2 が後では、FIFO の詳細を受け入れるように準備できるまでは、PIO 受信トランザクションを完了するまで待機する必要がありますデータ。 この場合、SerCx2 を呼び出す、 [ *EvtSerCx2PioTransmitEnableReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)準備完了の通知を送信するシリアル コント ローラーのドライバーを有効にするイベントのコールバック関数。 シリアル コント ローラー ドライバーが呼び出すこの通知が有効になっている場合、 [ **SerCx2PioTransmitReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2piotransmitready) SerCx2 送信 FIFO 準備ができているドライバーを検出したときに通知するメソッドより多くのデータをそのまま使用します。 この通知に応答して、SerCx2 呼び出し、 *EvtSerCx2PioTransmitWriteBuffer* FIFO により多くのデータを書き込む関数。

SerCx2 を呼び出す書き込み要求がタイムアウトになるかが取り消されたときに、準備完了の通知が有効である場合、 [ *EvtSerCx2PioTransmitCancelReadyNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)をキャンセルするイベントのコールバック関数、保留中通知します。 返すかどうかはこの関数は、保留中の通知を正常にキャンセル、 **TRUE**します。 戻り値**TRUE**シリアル コント ローラー ドライバーが呼び出すことが保証されます**SerCx2PioTransmitReady**します。 戻り値**FALSE**ことを示します、 *EvtSerCx2PioTransmitDrainFifo*関数が呼び出されてまたは呼び出す**SerCx2PioTransmitReady**します。
