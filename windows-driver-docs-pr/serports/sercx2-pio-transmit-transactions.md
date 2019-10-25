---
title: SerCx2 PIO-送信トランザクション
description: SerCx2 では、プログラムによる i/o (PIO) を使用する送信トランザクションのサポートを実装するために、すべてのシリアルコントローラードライバーが必要です。
ms.assetid: 3BEF9A3D-1FEF-4626-B07F-1670359062AF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 52451ab419507bd7759840fa99e3fc11ce2fcbe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845402"
---
# <a name="sercx2-pio-transmit-transactions"></a>SerCx2 PIO-送信トランザクション

SerCx2 では、プログラムによる i/o (PIO) を使用する送信トランザクションのサポートを実装するために、すべてのシリアルコントローラードライバーが必要です。 PIO 送信トランザクションを開始するために、SerCx2 はドライバーの[*EvtSerCx2PioTransmitWriteBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)イベントコールバック関数を呼び出し、パラメーターとして書き込みバッファーを提供します。

この呼び出しの間に、 *EvtSerCx2PioTransmitWriteBuffer*関数は、書き込みバッファーからシリアルコントローラーハードウェアの伝送 FIFO にデータを転送します。 このデータ転送は、書き込みバッファーが空であるか、送信 FIFO がすぐに多くのデータを受け入れることができなくなるまで続行されます。 転送が終了すると、関数は、書き込みバッファーから FIFO に正常に転送されたバイト数を返します。

## <a name="creating-the-pio-transmit-object"></a>PIO 転送オブジェクトの作成

SerCx2 がシリアルコントローラードライバーの*EvtSerCx2PioTransmit*Xxx * * 関数を呼び出すことができるようにするには、ドライバーが[**SerCx2PioTransmitCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcreate)メソッドを呼び出してこれらの関数を SerCx2 に登録する必要があります。 このメソッドは、入力パラメーターとして、ドライバーの*EvtSerCx2PioTransmit*Xxx * * 関数へのポインターを含む[**SERCX2\_PIO\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_pio_transmit_config)へのポインターの\_送信を受け入れます。

ドライバーは、次の3つの機能すべてを実装する必要があります。

- [*EvtSerCx2PioTransmitWriteBuffer*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_write_buffer)
- [*EvtSerCx2PioTransmitEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)
- [*EvtSerCx2PioTransmitCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)

オプションとして、ドライバーは次の機能のいずれかまたは両方を実装できます。

- [*EvtSerCx2PioTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)
- [*EvtSerCx2PioTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)

オプションとして、ドライバーは次の3つの機能を実装できます。

- [*EvtSerCx2PioTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)
- [*EvtSerCx2PioTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)
- [*EvtSerCx2PioTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_purge_fifo)

ドライバーが上記のリストの関数を実装する場合は、3つすべてを実装する必要があります。

**SerCx2PioTransmitCreate**メソッドは、PIO 転送オブジェクトを作成し、このオブジェクトへの[**SERCX2PIOTRANSMIT**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)ハンドルを呼び出し元のドライバーに提供します。 ドライバーの*EvtSerCx2PioTransmit*Xxx * * 関数はすべて、このハンドルを最初のパラメーターとして受け取ります。 次の SerCx2 メソッドは、このハンドルを最初のパラメーターとして受け取ります。

- [**SerCx2PioTransmitReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitready)
- [**SerCx2PioTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)
- [**SerCx2PioTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)
- [**SerCx2PioTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)
- [**SerCx2PioTransmitPurgeFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitpurgefifocomplete)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

一部のシリアルコントローラードライバーでは、PIO 送信トランザクションの開始時にシリアルコントローラーハードウェアを初期化するか、トランザクションの終了時にシリアルコントローラーのハードウェア状態をクリーンアップすることが必要になる場合があります。

ドライバーが[*EvtSerCx2PioTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_initialize_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションを開始する*EvtSerCx2PioTransmitWriteBuffer*呼び出しの前にシリアルコントローラーを初期化します。 実装されている場合、 *EvtSerCx2PioTransmitInitializeTransaction*関数は[**SerCx2PioTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitinitializetransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーの初期化を完了したときに SerCx2 に通知する必要があります。

ドライバーが[*EvtSerCx2PioTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cleanup_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションの最終*EvtSerCx2PioTransmitWriteBuffer*呼び出しの後にハードウェアの状態をクリーンアップします。 実装されている場合、 *EvtSerCx2PioTransmitInitializeTransaction*関数は[**SerCx2PioTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitcleanuptransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーのクリーンアップを完了したことを SerCx2 に通知する必要があります。

## <a name="draining-and-purging-the-transmit-fifo"></a>送信 FIFO のドレインと削除

シリアルコントローラードライバーは、送信 FIFO が空になったときにドライバーが検出できる場合、 [*EvtSerCx2PioTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)イベントコールバック関数を実装する必要があります。 実装されている場合、SerCx2 は、PIO 送信トランザクション内のデータの最後のバイトが送信 FIFO に書き込まれた後に、この関数を呼び出します。 この呼び出し中に、 *EvtSerCx2PioTransmitDrainFifo*関数は通常、送信 FIFO が空になったときに割り込みがトリガーされるようにし、待機せずに制御を戻します。 FIFO が空になると、ドライバーは[**SerCx2PioTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitdrainfifocomplete)メソッドを呼び出して SerCx2 に通知します。 この通知を受信した後にのみ、PIO 送信トランザクションに関連付けられている保留中の書き込み ([**IRP\_MJ\_write**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 要求が完了します。

シリアルコントローラードライバーが*EvtSerCx2PioTransmitDrainFifo*関数を実装していない場合、SerCx2 は、転送 FIFO が空であることを最初に確認せずに、保留中の書き込み要求を完了する必要があります。 FIFO に書き込まれたデータが、大幅な遅延なしに転送されるという保証はありません。 書き込み要求の完了後に FIFO に残ったデータは、転送される前に失われる可能性があります。 正常に完了した書き込み要求でこの予期しないデータ損失が発生すると、要求を送信した周辺機器ドライバーの信頼性の問題が発生する可能性があります。

*EvtSerCx2PioTransmitDrainFifo*関数を実装するドライバーは、 [*EvtSerCx2PioTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_drain_fifo)および[*EvtSerCx2PioTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_drain_fifo)イベントコールバック関数も実装する必要があります。

*EvtSerCx2PioTransmitCancelDrainFifo*関数を使用すると、SerCx2 は完了前に実行中の FIFO ドレイン操作を取り消すことができます。 SerCx2 は、書き込み要求がタイムアウトまたは取り消された場合に、この操作をキャンセルすることがあります。 *EvtSerCx2PioTransmitCancelDrainFifo*関数が FIFO ドレイン操作を正常にキャンセルした場合、この関数は**TRUE**を返します。 戻り値が**TRUE の場合**は、シリアルコントローラードライバーが呼び出されておらず、 **SerCx2PioTransmitDrainFifoComplete**を呼び出さないことを保証します。 戻り値が**FALSE**の場合は、 *EvtSerCx2PioTransmitDrainFifo*関数がを呼び出したか、すぐに**SerCx2PioTransmitDrainFifoComplete**を呼び出したことを示します。

PIO 転送トランザクションに関連付けられた書き込み要求が取り消された場合、または完了する前にタイムアウトになった場合、SerCx2 は、 *EvtSerCx2PioTransmitPurgeFifo*関数が実装されている場合は、その関数を呼び出して、送信 FIFO が残っている可能性のある未送信データを破棄します。 SerCx2 は、この関数から取得した情報を使用して、書き込み要求によって周辺機器に正常に送信されたデータのバイト数を、周辺ドライバーに正確に伝えます。

## <a name="ready-notifications"></a>準備完了の通知

*EvtSerCx2PioTransmitWriteBuffer*の呼び出しが終了するのは、転送 fifo がすぐにデータを受け入れることができないため、SerCx2 は、後で fifo がより多くのデータを受け入れることができるようになるまで、PIO 受信トランザクションの完了を待機する必要があるためです。 この場合、SerCx2 は[*EvtSerCx2PioTransmitEnableReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_enable_ready_notification)イベントコールバック関数を呼び出して、シリアルコントローラードライバーが準備完了の通知を送信できるようにします。 この通知が有効になっている場合、シリアルコントローラードライバーは[**SerCx2PioTransmitReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2piotransmitready)メソッドを呼び出して、送信 FIFO の受信準備が完了したことをドライバーが検出したときに SerCx2 に通知します。 この通知に応答して、SerCx2 は*EvtSerCx2PioTransmitWriteBuffer*関数を呼び出して、より多くのデータを FIFO に書き込みます。

書き込み要求がタイムアウトまたはキャンセルされたときに準備完了の通知が有効になっている場合、SerCx2 は[*EvtSerCx2PioTransmitCancelReadyNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_pio_transmit_cancel_ready_notification)イベントコールバック関数を呼び出して、保留中の通知をキャンセルします。 この関数が保留中の通知を正常にキャンセルした場合は、 **TRUE**を返します。 戻り値が**TRUE の場合**、シリアルコントローラードライバーは**SerCx2PioTransmitReady**を呼び出さないことを保証します。 戻り値が**FALSE**の場合は、 *EvtSerCx2PioTransmitDrainFifo*関数がを呼び出したか、または**SerCx2PioTransmitReady**を呼び出したことを示します。
