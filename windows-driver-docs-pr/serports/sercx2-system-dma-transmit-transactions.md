---
title: SerCx2 システム-DMA-送信トランザクション
description: 一部のシリアルコントローラードライバーでは、システム DMA コントローラーを使用する転送トランザクションのサポートが実装されています。
ms.assetid: 8569E76F-CAFF-4A2C-8052-62B340C5ADED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9921c8c310f19bdbb047d9e6b4554c769c75b5c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845397"
---
# <a name="sercx2-system-dma-transmit-transactions"></a>SerCx2 システム-DMA-送信トランザクション

一部のシリアルコントローラードライバーでは、システム DMA コントローラーを使用する転送トランザクションのサポートが実装されています。 このようなサポートは省略可能ですが、長時間のデータ転送のためにプログラミング i/o (PIO) を使用する必要がある主なプロセッサを削減することで、パフォーマンスを向上させることができます。 SerCx2 は、システム DMA コントローラーを設定し、シリアルコントローラードライバーの代わりに必要な DMA 転送を開始することによって、システム DMA 送信トランザクションを実行します。

シリアルコントローラードライバーがシステム dma 送信オブジェクトを作成すると、SerCx2 がシステム DMA アダプターをシステム dma 送信トランザクション用に設定するために使用するパラメーターがドライバーによって提供されます。

トランザクションが開始される前に、シリアルコントローラードライバーには、トランザクションに必要なシリアルコントローラーハードウェアまたは DMA アダプターの特別なセットを実行するオプションがあります。 トランザクションが終了した後、ドライバーは、転送 FIFO をドレインし、必要に応じてシリアルコントローラーのハードウェア状態をクリーンアップするオプションを備えています。

## <a name="creating-the-system-dma-transmit-object"></a>システムの DMA 転送オブジェクトの作成

SerCx2 がシリアルコントローラードライバーの*EvtSerCx2SystemDmaTransmit*Xxx * * 関数を呼び出すことができるようにするには、ドライバーが[**SerCx2SystemDmaTransmitCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcreate)メソッドを呼び出してこれらの関数を SerCx2 に登録する必要があります。 このメソッドは、入力パラメーターとして、ドライバーの*EvtSerCx2SystemDmaTransmit*Xxx * * 関数へのポインターを含む[**SERCX2\_システムへのポインター\_DMA\_\_送信**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_system_dma_transmit_config)します。

オプションとして、ドライバーは次の機能のいずれかまたはすべてを実装できます。

- [*EvtSerCx2SystemDmaTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_initialize_transaction)
- [*EvtSerCx2SystemDmaTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cleanup_transaction)
- [*EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_configure_dma_channel)

オプションとして、ドライバーは次の機能を実装できます。

- [*EvtSerCx2SystemDmaTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_drain_fifo)
- [*EvtSerCx2SystemDmaTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cancel_drain_fifo)
- [*EvtSerCx2SystemDmaTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_purge_fifo)

上記の一覧のいずれかの関数を実装するドライバーは、3つすべてを実装する必要があります。

**SerCx2SystemDmaTransmitCreate**メソッドは、システムの DMA 送信オブジェクトを作成し、このオブジェクトへの[**SERCX2SYSTEMDMATRANSMIT**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles#sercx2systemdmatransmit-object-handle)ハンドルを呼び出し元のドライバーに提供します。 ドライバーの*EvtSerCx2SystemDmaTransmit*Xxx * * 関数はすべて、このハンドルを最初のパラメーターとして受け取ります。 次の SerCx2 メソッドは、このハンドルを最初のパラメーターとして受け取ります。

- [**SerCx2SystemDmaTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitdrainfifocomplete)
- [**SerCx2SystemDmaTransmitPurgeFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitpurgefifocomplete)
- [**SerCx2SystemDmaTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitinitializetransactioncomplete)
- [**SerCx2SystemDmaTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcleanuptransactioncomplete)
- [**SerCx2SystemDmaTransmitGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitgetdmaenabler)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

一部のシリアルコントローラードライバーでは、システム DMA 送信トランザクションの開始時にシリアルコントローラーハードウェアを初期化するか、トランザクションの終了時にシリアルコントローラーのハードウェア状態をクリーンアップすることが必要になる場合があります。

ドライバーが[*EvtSerCx2SystemDmaTransmitInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_initialize_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションで最初の DMA 転送を開始する前にシリアルコントローラーを初期化します。 実装されている場合、 *EvtSerCx2SystemDmaTransmitInitializeTransaction*関数は[**SerCx2SystemDmaTransmitInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitinitializetransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーの初期化を完了したときに SerCx2 に通知する必要があります.

ドライバーが[*EvtSerCx2SystemDmaTransmitCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cleanup_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションでの最終的な DMA 転送が終了した後にハードウェアの状態をクリーンアップします。 実装されている場合、 *EvtSerCx2SystemDmaTransmitInitializeTransaction*関数は[**SerCx2SystemDmaTransmitCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitcleanuptransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーのクリーンアップを完了したことを SerCx2 に通知する必要があります。

システムの dma 送信トランザクションの開始時にシステム DMA コントローラーの特別な構成を行う必要があるシリアルコントローラードライバーは、 [*EvtSerCx2SystemDmaTransmitConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_configure_dma_channel)イベントコールバック関数を実装する必要があります。 この関数は、 [**SerCx2SystemDmaTransmitGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitgetdmaenabler)メソッドを呼び出して、トランザクションに使用されるシステム dma アダプターの dma イネーブラーを取得できます。 SerCx2 は、トランザクションで最初の DMA 転送を開始する前に、この関数を呼び出します。 DMA イネーブラーの詳細については、「 [Dma トランザクションの有効化](https://docs.microsoft.com/windows-hardware/drivers/wdf/enabling-dma-transactions)」を参照してください。

## <a name="draining-and-purging-the-transmit-fifo"></a>送信 FIFO のドレインと削除

システム DMA 送信トランザクションをサポートするシリアルコントローラードライバーは、送信 FIFO が空になったときにドライバーが検出できる場合、 [*EvtSerCx2SystemDmaTransmitDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_drain_fifo)イベントコールバック関数を実装する必要があります。 実装されている場合、SerCx2 は、システムの DMA 送信トランザクションのデータの最後のバイトが送信 FIFO に書き込まれた後に、この関数を呼び出します。 この呼び出しの間、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数は通常、送信 FIFO が空になったときにトリガーされる割り込みを有効にし、その後、割り込みを待機せずに制御を戻します。 FIFO が空になると、ドライバーは[**SerCx2SystemDmaTransmitDrainFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitdrainfifocomplete)メソッドを呼び出して SerCx2 に通知します。 この通知を受信した後にのみ、SerCx2 トランザクションに関連付けられている保留中の書き込み ([**IRP\_MJ\_write**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))) 要求が完了します。

シリアルコントローラードライバーが*EvtSerCx2SystemDmaTransmitDrainFifo*関数を実装していない場合、SerCx2 は、転送 FIFO が空であることを最初に確認せずに、保留中の書き込み要求を完了する必要があります。 FIFO に書き込まれたデータが、大幅な遅延なしに転送されるという保証はありません。 書き込み要求の完了後に FIFO に残ったデータは、転送される前に失われる可能性があります。 正常に完了した書き込み要求でこの予期しないデータ損失が発生すると、要求を送信した周辺機器ドライバーの信頼性の問題が発生する可能性があります。

*EvtSerCx2SystemDmaTransmitDrainFifo*関数を実装するドライバーは、 [*EvtSerCx2SystemDmaTransmitCancelDrainFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_cancel_drain_fifo)および[*EvtSerCx2SystemDmaTransmitPurgeFifo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_transmit_purge_fifo)イベントコールバック関数も実装する必要があります。

*EvtSerCx2SystemDmaTransmitCancelDrainFifo*関数を使用すると、SerCx2 は完了前に実行中の FIFO ドレイン操作を取り消すことができます。 書き込み要求が取り消された場合、またはシリアルコントローラーが D0 デバイスの電源状態を終了しようとして低電力状態になる場合、SerCx2 はこの操作をキャンセルすることがあります。 *EvtSerCx2SystemDmaTransmitCancelDrainFifo*関数が FIFO ドレイン操作を正常にキャンセルした場合、この関数は**TRUE**を返します。 戻り値が**TRUE の場合**は、最初に**SerCx2SystemDmaTransmitDrainFifoComplete**を呼び出さなくても、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数はを返すことを保証します。 戻り値が**FALSE**の場合は、 *EvtSerCx2SystemDmaTransmitDrainFifo*関数がを呼び出したか、または**SerCx2SystemDmaTransmitDrainFifoComplete**を呼び出したことを示します。

システム DMA 送信トランザクションに関連付けられた書き込み要求が取り消された場合、または完了前にタイムアウトになった場合、SerCx2 は、 *EvtSerCx2SystemDmaTransmitPurgeFifo*関数が実装されている場合は、その関数を呼び出します。転送 FIFO。 FIFO が削除されると、 *EvtSerCx2SystemDmaTransmitPurgeFifo*関数は[**SerCx2SystemDmaTransmitPurgeFifoComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmatransmitpurgefifocomplete)メソッドを呼び出して SerCx2 に通知します。 この通知を受信した後にのみ、SerCx2 によって新しい i/o トランザクションが開始されます。
