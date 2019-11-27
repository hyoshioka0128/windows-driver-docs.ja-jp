---
title: システム モード DMA のサポート
description: システムモードの DMA デバイスの i/o 要求を処理するために、KMDF ドライバーによってイベントコールバック関数に提供されるコードについて説明します。
ms.assetid: CCC77C15-69CA-44CB-8DEB-29F3EAEA44F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7818ade3cb98794e0f42194a07014b55019769f0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831695"
---
# <a name="supporting-system-mode-dma"></a>システム モード DMA のサポート


\[は KMDF にのみ適用され\]

*バスマスタ*dma とは対照的に、システムモードの dma では、複数のデバイスが1つの通常のマルチチャネル dma コントローラーを共有する構成を記述します。

カーネルモードドライバーフレームワーク (KMDF) バージョン1.11 以降では、フレームワークは、Windows 8 以降のバージョンの Windows オペレーティングシステムで実行されているチップ (SoC) ベースのシステム上のシステムモードの DMA をサポートしています。

このトピックでは、KMDF ドライバーがイベントコールバック関数で提供する必要があるコードについて説明します。また、システムモードの DMA デバイスの i/o 要求を処理するために登録できるオプションのイベントコールバック関数についても説明します。

KMDF とバスマスタ DMA の詳細については、「 [Bus マスタ Dma デバイス用の Kmdf ドライバーでの I/o 要求の処理](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)」を参照してください。

次の図は、ドライバーがシステムモードの DMA をサポートするために使用するイベントコールバック関数を示しています。

![kmdf ドライバーでのシステムモードの dma の実装](images/sys-mode-dma-in-kmdf.png)

## <a name="creating-a-system-mode-dma-enabler"></a>システムモードの DMA イネーブラーの作成


システムモードの DMA プロファイルの作成は、2段階のプロセスです。 次の手順は、一般的なシナリオを表します。

1.  通常、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数では、ドライバーは[**WDF\_DMA\_イネーブラ\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdf_dma_enabler_config_init)を呼び出し、**プロファイル**パラメーターを**systemmode**または**systemmodeduplex に設定します。** . 次に、ドライバーは[**WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を呼び出し、 [**WDF\_DMA\_イネーブラ\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)構造体を渡します。

    また、ドライバーは、 [*Evtdeviceのハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)でも、このイネーブラーを作成することがあります。

2.  ドライバーの[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数は、 [**WdfDmaEnablerConfigureSystemProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)メソッドを呼び出して、DMA のイネーブラーを dma リソースに関連付けます。 双方向イネーブラーの場合、ドライバーは[**WdfDmaEnablerConfigureSystemProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)を2回呼び出し、各転送方向を構成します。

    このドライバーは、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile) [*EvtdeviceWdfDmaEnablerConfigureSystemProfile ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)の完了後に、このメソッドを呼び出すことができます。ただし、ドライバーは DMA トランザクションを初期化する前にこのメソッドを呼び出す必要があります。

## <a name="providing-optional-callback-functions"></a>オプションのコールバック関数の提供


### <a href="" id="configuring-a-system-mode-dma-enabler"></a>DMA チャネルの構成

通常、KMDF ドライバーは DMA チャネルを構成しません。 ただし、特定の状況では、ドライバーがチャネル固有の構成を実行することが必要になる場合があります。 たとえば、次の手順を実行して、DMA コントローラーによって実装されたカスタム関数をドライバーが呼び出す場合があります。

1.  ドライバーの[要求ハンドラー](request-handlers.md)のいずれかで、ドライバーは[**Wdfdmatransactionsetchannelconfigurationcallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetchannelconfigurationcallback)を呼び出して、 [*EvtDmaTransactionConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel) callback 関数を登録します。
2.  ドライバーの[*EvtDmaTransactionConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel) callback 関数は、 [**WdfDmaEnablerWdmGetDmaAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)を呼び出して、WDM [**DMA\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_adapter)へのポインターを取得します。 この構造体は、ドライバーのシステムモードの DMA チャネルを表すアダプターオブジェクトです。
3.  その後、ドライバーは[**ConfigureAdapterChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-pconfigure_adapter_channel)を呼び出して、DMA コントローラーによって実装されたカスタム関数を有効にすることができます。 このルーチンは、 [**DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_dma_operations)構造体で返されたアドレスからのポインターによってのみ呼び出すことができます。
4.  ドライバーの[*EvtDmaTransactionConfigureDmaChannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel) callback 関数は、DMA チャネルが正常に構成された場合に TRUE を返します。
5.  フレームワークは、ドライバーの[*Evtprogramdma*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数を呼び出します。

### <a name="receiving-notification-of-transfer-completion"></a>転送の完了通知を受信しています

バスマスタリングコントローラーを使用するデバイスとは異なり、システムモードの DMA デバイスのハードウェアでは、割り込みを発行することによって、DMA 転送の完了をシグナルにすることはできません。

デバイスで DMA 転送の完了を通知する割り込みが発生しない場合、ドライバーは、システムモードの DMA 転送が完了したときにフレームワークが呼び出す[*EvtDmaTransactionDmaTransferComplete*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)イベントコールバック関数を提供できます。

このコールバック関数を登録するために、ドライバーは、[要求ハンドラー](request-handlers.md)の1つから[**WdfDmaTransactionSetTransferCompleteCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsettransfercompletecallback)を呼び出します。

 

 





