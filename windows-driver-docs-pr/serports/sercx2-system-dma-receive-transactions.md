---
title: SerCx2 システム-DMA-受信トランザクション
description: 一部のコント ローラーのシリアル ドライバーのサポートを実装するシステムの DMA コント ローラーを使用するトランザクションを受信します。
ms.assetid: 0374D1BE-96ED-43D6-8661-5E9676B82C0D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6f7d6eafd877b4f2d5bbb425a966a03586c7316
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356767"
---
# <a name="sercx2-system-dma-receive-transactions"></a>SerCx2 システム-DMA-受信トランザクション

一部のコント ローラーのシリアル ドライバーのサポートを実装するシステムの DMA コント ローラーを使用するトランザクションを受信します。 このようなサポートは任意ですが、長い形式のデータ転送に下手順 I/O (PIO) を使用する必要があるメイン プロセッサを削減してパフォーマンスを向上させることができます。 SerCx2 では、システムの DMA コント ローラーを設定し、コント ローラーのシリアル ドライバーの代わりに必要な DMA 転送を開始してシステム DMA 受信トランザクションを実行します。

シリアル コント ローラー ドライバーでは、DMA 受信システム オブジェクトを作成するとき、ドライバーは SerCx2 がシステム DMA 受信トランザクションのシステム DMA アダプターの設定に使用するパラメーターを提供します。

シリアル コント ローラー ドライバーでは、システム DMA 受信トランザクションの開始前に、シリアル コント ローラーのハードウェアまたはトランザクションに必要な可能性のある DMA アダプターのすべての特別な設定を行うオプションがあります。 トランザクションが完了すると、ドライバー、必要に応じて、実行できますクリーンアップの必要になるシリアル コント ローラーのハードウェアの状態。

## <a name="creating-the-system-dma-receive-object"></a>DMA 受信システム オブジェクトを作成します。

SerCx2 がコント ローラーのシリアル ドライバーを呼び出す前に*EvtSerCx2SystemDmaReceive*Xxx * * 関数の場合、ドライバーが呼び出す必要があります、 [ **SerCx2SystemDmaReceiveCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecreate)SerCx2 をこれらの関数を登録するメソッド。 このメソッドは、入力パラメーターとしてへのポインターを[ **SERCX2\_システム\_DMA\_受信\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/ns-sercx-_sercx2_system_dma_receive_config)を含む構造体ドライバーへのポインター *EvtSerCx2SystemDmaReceive*Xxx * * 関数。

オプションとして、ドライバーは、次の関数の一部またはすべてを実装できます。

- [*EvtSerCx2SystemDmaReceiveInitializeTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_initialize_transaction)
- [*EvtSerCx2SystemDmaReceiveCleanupTransaction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_cleanup_transaction)
- [*EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_configure_dma_channel)

オプションとして、ドライバーは、次の 2 つの関数を実装できます。

- [*EvtSerCx2SystemDmaReceiveEnableNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_enable_new_data_notification)
- [*EvtSerCx2SystemDmaReceiveCancelNewDataNotification*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_cancel_new_data_notification)

上記の 2 つの関数のいずれかを実装するドライバーは、両方を実装する必要があります。

**SerCx2SystemDmaReceiveCreate**メソッドは、DMA 受信システム オブジェクトを作成し、呼び出し元のドライバーを提供する[ **SERCX2SYSTEMDMARECEIVE** ](https://docs.microsoft.com/windows-hardware/drivers/serports/sercx2-object-handles)これへのハンドルオブジェクト。 ドライバーの*EvtSerCx2SystemDmaReceive*Xxx * * すべての関数は、最初のパラメーターとしてこのハンドルを受け取ります。 次の SerCx2 メソッドは、最初のパラメーターとして、このハンドルを受け取ります。

- [**SerCx2SystemDmaReceiveNewDataNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivenewdatanotification)
- [**SerCx2SystemDmaReceiveInitializeTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceiveinitializetransactioncomplete)
- [**SerCx2SystemDmaReceiveCleanupTransactionComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecleanuptransactioncomplete)
- [**SerCx2SystemDmaReceiveGetDmaEnabler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivegetdmaenabler)

## <a name="hardware-initialization-and-clean-up"></a>ハードウェアの初期化とクリーンアップ

シリアル コント ローラーのドライバーによっては、システム DMA 受信トランザクションの開始時シリアル コント ローラーのハードウェアを初期化するために、またはトランザクションの最後に、シリアル コント ローラーのハードウェアの状態をクリーンアップする必要があります。

ドライバーが実装されている場合、 [ *EvtSerCx2SystemDmaReceiveInitializeTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_initialize_transaction)イベント コールバック関数、SerCx2 がシリアル コント ローラーを最初の DMA を開始する前に初期化するには、この関数を呼び出すトランザクションで転送します。 実装されている場合、 *EvtSerCx2SystemDmaReceiveInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2SystemDmaReceiveInitializeTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceiveinitializetransactioncomplete)ドライバーでは、シリアル コント ローラーの初期化が完了すると、SerCx2 を通知するメソッドです。

ドライバーが実装されている場合、 [ *EvtSerCx2SystemDmaReceiveCleanupTransaction* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_cleanup_transaction)イベント コールバック関数では、SerCx2 が最終的な DMA 転送の終了後にハードウェアの状態をクリーンアップするには、この関数を呼び出すトランザクション。 実装されている場合、 *EvtSerCx2SystemDmaReceiveInitializeTransaction*関数を呼び出す必要があります、 [ **SerCx2SystemDmaReceiveCleanupTransactionComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivecleanuptransactioncomplete)メソッドドライバーでは、シリアル コント ローラーのクリーンアップが完了すると、SerCx2 を通知します。

システムの DMA コント ローラー システム DMA 受信トランザクションの開始時の特別な構成を行う必要があるシリアル コント ローラー ドライバーが実装する必要があります、 [ *EvtSerCx2SystemDmaReceiveConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_configure_dma_channel)イベント コールバック関数。 この関数を呼び出すことができます、 [ **SerCx2SystemDmaReceiveGetDmaEnabler** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivegetdmaenabler)トランザクションに使用されるシステム DMA アダプターの DMA イネーブラーを取得します。 SerCx2 は、トランザクションの最初の DMA 転送を開始する前に、この関数を呼び出します。 DMA イネーブラーに関する詳細については、次を参照してください。 [DMA のトランザクションを有効にする](https://docs.microsoft.com/windows-hardware/drivers/wdf/enabling-dma-transactions)します。

## <a name="new-data-notifications"></a>新しいデータの通知

オプションとして、シリアル コント ローラー ドライバーを実装できる、 [ *EvtSerCx2SystemDmaReceiveEnableNewDataNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_enable_new_data_notification)イベント コールバック関数。 実装されている場合、SerCx2 はシステム DMA 受信トランザクションとして処理されます。 読み取り要求の処理中にタイムアウトの間隔を効率的に管理するこの関数を使用します。

間隔、タイムアウトは、シリアル コント ローラーで受信した 2 つの連続するバイトまでの間隔は、クライアントが指定した最大時間を超えた場合に発生します。 SerCx2 に周辺機器のドライバーが読み取り要求を送信すると後に、少なくとも 1 バイトのデータを逐次的に接続されている周辺機器のデバイスから受信した後までの間隔、タイムアウトは発生しません。 到着までの時間は、読み取り要求と周辺機器のデバイスからのデータの最初のバイトの受信、最初のバイトを受信した後、残りの読み取り要求のデータを受信するために必要な時間よりも大幅に長くする場合可能性があります。 詳細については、次を参照してください。 [**シリアル\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts)します。

SerCx2 呼び出し、 *EvtSerCx2SystemDmaReceiveEnableNewDataNotification*関数を実装すると、有効にする場合、*新しいデータ通知*します。 この通知が有効になりシリアル コント ローラーは、周辺機器のデバイスから新しいデータの 1 つまたは複数のバイトを受信したり、既にデータがある場合、FIFO の受信、シリアル コント ローラーのドライバーを呼び出す必要があります、 [ **SerCx2SystemDmaReceiveNewDataNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nf-sercx-sercx2systemdmareceivenewdatanotification) SerCx2 に通知するメソッド。

SerCx2 可能な間隔のタイムアウトを検出するために呼び出す定期的に、 [ **ReadDmaCounter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pread_dma_counter)前の間隔中に、任意のデータを受信したかどうかを確認するシステム DMA アダプターのルーチンです。 シリアル コント ローラー ドライバーが実装するかどうかによって異なります SerCx2 によるデータの最初のバイトの受信の検出、 *EvtSerCx2SystemDmaReceiveEnableNewDataNotification*関数。 この関数が実装されている場合、SerCx2 は、新しいデータ通知を有効にする関数を呼び出すし、データの最初のバイトが受信したときに、ドライバーによって通知されます。 SerCx2 が定期的に呼び出す場合は、 **ReadDmaCounter**最初のバイト、および可能性がありますの受信を検出するためには、これらの呼び出しを実行するプロセッサを定期的にスリープ解除する必要があります。 したがって、実装するドライバー、 *EvtSerCx2SystemDmaReceiveEnableNewDataNotification*関数は、プロセッサを何度でもスリープ解除する必要がない電力消費量を減らすことができます。

**注**  SerCx2 依存、 **ReadDmaCounter**システム DMA 受信トランザクションとシステム DMA 送信トランザクションの中にタイムアウトを監視するシステム DMA アダプターの日常的な。 ハードウェア アブストラクション レイヤー (HAL) を完全に機能する必要があります実装**ReadDmaCounter**ルーチン DMA コント ローラーのシステムとシリアル コント ローラーの間のデータを転送するために使用します。

システム DMA 受信トランザクションの新しいデータの通知をサポートしているシリアル コント ローラー ドライバーが実装する必要があります、 [ *EvtSerCx2SystemDmaReceiveCancelNewDataNotification* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sercx/nc-sercx-evt_sercx2_system_dma_receive_cancel_new_data_notification)イベント コールバック関数を SerCx2 が起きる前に有効になっている新しいデータ通知を取り消すことができます。 保留中の読み取り要求が取り消されたときに、新しいデータの通知が有効になっている場合、または合計のタイムアウトが発生する SerCx2 呼び出し、 *EvtSerCx2SystemDmaReceiveCancelNewDataNotification*通知をキャンセルする関数。 返すかどうかはこの関数は、保留中の通知を正常にキャンセル、 **TRUE**します。 戻り値**TRUE**シリアル コント ローラー ドライバーが呼び出すことが保証されます**SerCx2SystemDmaReceiveNewDataNotification**します。 戻り値**FALSE**ドライバーと呼ばれるかがすぐに呼び出すことを示します**SerCx2SystemDmaReceiveNewDataNotification**します。 合計タイムアウトの詳細については、次を参照してください。 [**シリアル\_タイムアウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddser/ns-ntddser-_serial_timeouts)します。
