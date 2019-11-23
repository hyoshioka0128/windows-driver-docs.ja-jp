---
title: SerCx2 システム-DMA-受信トランザクション
description: 一部のシリアルコントローラードライバーでは、システム DMA コントローラーを使用する receive トランザクションのサポートが実装されています。
ms.assetid: 0374D1BE-96ED-43D6-8661-5E9676B82C0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d0640b8f1ab9a3af7d612d054a0a93ea26eeca4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845399"
---
# <a name="sercx2-system-dma-receive-transactions"></a>SerCx2 システム-DMA-受信トランザクション

一部のシリアルコントローラードライバーでは、システム DMA コントローラーを使用する receive トランザクションのサポートが実装されています。 このようなサポートは省略可能ですが、長時間のデータ転送のためにプログラミング i/o (PIO) を使用する必要がある主なプロセッサを削減することで、パフォーマンスを向上させることができます。 SerCx2 は、システム DMA コントローラーを設定し、シリアルコントローラードライバーの代わりに必要な DMA 転送を開始することによって、システム DMA 受信トランザクションを実行します。

シリアルコントローラードライバーによってシステム dma 受信オブジェクトが作成されると、SerCx2 がシステム DMA アダプターをシステム dma 受信トランザクション用に設定するために使用するパラメーターがドライバーによって提供されます。

システム DMA 受信トランザクションの開始前に、シリアルコントローラードライバーには、トランザクションに必要なシリアルコントローラーハードウェアまたは DMA アダプターの特別なセットを実行するオプションがあります。 トランザクションが完了したら、必要に応じて、ドライバーは必要に応じてシリアルコントローラーのハードウェア状態のクリーンアップを実行できます。

## <a name="creating-the-system-dma-receive-object"></a>システムの DMA-receive オブジェクトの作成

SerCx2 がシリアルコントローラードライバーの*EvtSerCx2SystemDmaReceive*Xxx * * 関数を呼び出すことができるようにするには、ドライバーが[**SerCx2SystemDmaReceiveCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecreate)メソッドを呼び出してこれらの関数を SerCx2 に登録する必要があります。 このメソッドは、入力パラメーターとして、 [**SERCX2\_システムへのポインター\_DMA\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/ns-sercx-_sercx2_system_dma_receive_config) 、ドライバーの*EvtSerCx2SystemDmaReceive*Xxx * * 関数へのポインターを含む\_CONFIG 構造体を受け取ります。

オプションとして、ドライバーは次の機能のいずれかまたはすべてを実装できます。

- [*EvtSerCx2SystemDmaReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_initialize_transaction)
- [*EvtSerCx2SystemDmaReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cleanup_transaction)
- [*EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_configure_dma_channel)

オプションとして、ドライバーは次の2つの関数を実装できます。

- [*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_enable_new_data_notification)
- [*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cancel_new_data_notification)

前の一覧の2つの関数のいずれかを実装するドライバーは、両方を実装する必要があります。

**SerCx2SystemDmaReceiveCreate**メソッドは、システムの DMA 受信オブジェクトを作成し、このオブジェクトへの[**SERCX2SYSTEMDMARECEIVE**](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)ハンドルを呼び出し元のドライバーに提供します。 ドライバーの*EvtSerCx2SystemDmaReceive*Xxx * * 関数はすべて、このハンドルを最初のパラメーターとして受け取ります。 次の SerCx2 メソッドは、このハンドルを最初のパラメーターとして受け取ります。

- [**SerCx2SystemDmaReceiveNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivenewdatanotification)
- [**SerCx2SystemDmaReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceiveinitializetransactioncomplete)
- [**SerCx2SystemDmaReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecleanuptransactioncomplete)
- [**SerCx2SystemDmaReceiveGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivegetdmaenabler)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

一部のシリアルコントローラードライバーでは、システム DMA 受信トランザクションの開始時にシリアルコントローラーハードウェアを初期化するか、トランザクションの終了時にシリアルコントローラーのハードウェア状態をクリーンアップする必要があります。

ドライバーが[*EvtSerCx2SystemDmaReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_initialize_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションで最初の DMA 転送を開始する前にシリアルコントローラーを初期化します。 実装されている場合、 *EvtSerCx2SystemDmaReceiveInitializeTransaction*関数は[**SerCx2SystemDmaReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceiveinitializetransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーの初期化を完了したときに SerCx2 に通知する必要があります。

ドライバーが[*EvtSerCx2SystemDmaReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cleanup_transaction)イベントコールバック関数を実装している場合、SerCx2 はこの関数を呼び出して、トランザクションでの最終的な DMA 転送が終了した後にハードウェアの状態をクリーンアップします。 実装されている場合、 *EvtSerCx2SystemDmaReceiveInitializeTransaction*関数は[**SerCx2SystemDmaReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivecleanuptransactioncomplete)メソッドを呼び出して、ドライバーがシリアルコントローラーのクリーンアップを完了したことを SerCx2 に通知する必要があります。

システムの dma 受信トランザクションの開始時にシステム DMA コントローラーの特別な構成を行う必要があるシリアルコントローラードライバーは、 [*EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_configure_dma_channel)イベントコールバック関数を実装する必要があります。 この関数は、 [**SerCx2SystemDmaReceiveGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivegetdmaenabler)メソッドを呼び出して、トランザクションに使用されるシステム dma アダプターの dma イネーブラーを取得できます。 SerCx2 は、トランザクションで最初の DMA 転送を開始する前に、この関数を呼び出します。 DMA イネーブラーの詳細については、「 [Dma トランザクションの有効化](https://docs.microsoft.com/windows-hardware/drivers/wdf/enabling-dma-transactions)」を参照してください。

## <a name="new-data-notifications"></a>新規-データ通知

オプションとして、シリアルコントローラードライバーは[*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_enable_new_data_notification)イベントコールバック関数を実装できます。 実装されている場合、SerCx2 はこの関数を使用して、システム-DMA-receive トランザクションとして処理される読み取り要求の処理中の間隔タイムアウトを効率的に管理します。

シリアルコントローラーによって受信された2つの連続するバイトの間隔がクライアントが指定した最大時間を超えた場合、間隔のタイムアウトが発生します。 周辺機器のドライバーから SerCx2 に読み取り要求が送信された後、シリアル接続された周辺機器から少なくとも1バイトのデータを受信するまで、間隔のタイムアウトは発生しません。 最初のバイトを受信した後、読み取り要求が到着してから、周辺機器からデータの最初のバイトが受信されるまでにかかる時間は、読み取り要求の残りのデータを受信するために必要な時間よりもかなり長くなる可能性があります。 詳細については、「 [**SERIAL\_のタイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)」を参照してください。

SerCx2 は、 *EvtSerCx2SystemDmaReceiveEnableNewDataNotification*関数が実装されている場合、その関数を呼び出して、*新しいデータ通知*を有効にします。 この通知が有効になっていて、シリアルコントローラーが周辺機器から1バイト以上の新しいデータを受信した場合、または既にデータを受信 FIFO に保持している場合、シリアルコントローラードライバーは[**SerCx2SystemDmaReceiveNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nf-sercx-sercx2systemdmareceivenewdatanotification)メソッドを呼び出して SerCx2 に通知する必要があります。

有効期間タイムアウトを検出するために、SerCx2 はシステムの DMA アダプターの[**ReadDmaCounter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pread_dma_counter)ルーチンを定期的に呼び出して、前の間隔でデータが受信されたかどうかを確認します。 SerCx2 がデータの最初のバイトの受信を検出する方法は、シリアルコントローラードライバーが*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*関数を実装しているかどうかによって異なります。 この関数が実装されている場合、SerCx2 は関数を呼び出して新しいデータ通知を有効にし、データの最初のバイトが受信されたときにドライバーによって通知されます。 それ以外の場合、SerCx2 は、最初のバイトの受信を検出するために**ReadDmaCounter**を定期的に呼び出します。また、これらの呼び出しを行うには、プロセッサを定期的にスリープ解除する必要があります。 したがって、 *EvtSerCx2SystemDmaReceiveEnableNewDataNotification*関数を実装するドライバーは、プロセッサが頻繁にスリープ解除されることを必要としないため、電力消費を減らすことができます。

**注**  SerCx2 はシステム dma アダプターの**ReadDmaCounter**ルーチンを利用して、システム dma 受信トランザクションとシステム dma 送信トランザクションの間のタイムアウトを監視します。 ハードウェアアブストラクションレイヤー (HAL) は、シリアルコントローラーとの間でデータを転送するために使用されるシステム DMA コントローラーに対して、完全に機能する**ReadDmaCounter**ルーチンを実装する必要があります。

システム DMA 受信トランザクションの新規データ通知をサポートするシリアルコントローラードライバーは、 [*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/sercx/nc-sercx-evt_sercx2_system_dma_receive_cancel_new_data_notification)イベントコールバック関数を実装する必要があります。これにより、SerCx2 は、有効な新しいデータ通知が発生する前にキャンセルできます。 保留中の読み取り要求が取り消されたとき、または合計タイムアウトが発生したときに、新しいデータ通知が有効になっている場合、SerCx2 は*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*関数を呼び出して通知をキャンセルします。 この関数が保留中の通知を正常にキャンセルした場合は、 **TRUE**を返します。 戻り値が**TRUE の場合**、シリアルコントローラードライバーは**SerCx2SystemDmaReceiveNewDataNotification**を呼び出さないことを保証します。 戻り値が**FALSE**の場合は、ドライバーがを呼び出したか、すぐに**SerCx2SystemDmaReceiveNewDataNotification**を呼び出したことを示します。 タイムアウトの合計の詳細については、「 [**SERIAL\_のタイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_timeouts)」を参照してください。
