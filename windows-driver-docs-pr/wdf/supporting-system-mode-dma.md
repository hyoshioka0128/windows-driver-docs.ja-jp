---
title: システム モード DMA のサポート
description: KMDF ドライバーがそのイベントに提供するコードを記述システム モード DMA のデバイスの I/O 要求を処理するコールバック関数。
ms.assetid: CCC77C15-69CA-44CB-8DEB-29F3EAEA44F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2c57c58d44919417f01eeb9218ee5a9653014b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368039"
---
# <a name="supporting-system-mode-dma"></a>システム モード DMA のサポート


\[KMDF にのみ適用されます。\]

対照的に、システム モード DMA*バス マスター* DMA では、複数のデバイスが、通常、マルチ チャネルの 1 つの DMA コント ローラーを共有する構成を説明します。

カーネル モード ドライバー フレームワーク (KMDF) バージョン 1.11 以降は、フレームワークがサポートするシステム モードの DMA チップ (SoC) のシステムに – ベースの Windows 8 または Windows オペレーティング システムの以降のバージョンで実行されているシステム。

このトピックでは、KMDF ドライバーは、そのイベントのコールバック関数や、登録する省略可能なイベント コールバック関数で提供する必要があるコードを説明しますシステム モード DMA のデバイスの I/O 要求を処理します。

KMDF とバス マスター DMA については、次を参照してください。 [KMDF ドライバーでは、バス マスター DMA デバイスの I/O 要求の処理](handling-i-o-requests-in-a-kmdf-driver-for-a-bus-master-dma-device.md)します。

次の図は、イベントには、ドライバーはサポート システム モードの DMA を使用してコールバック関数を示します。

![kmdf ドライバーでのシステム モード dma の実装](images/sys-mode-dma-in-kmdf.png)

## <a name="creating-a-system-mode-dma-enabler"></a>システム モードの DMA イネーブラーを作成します。


2 段階のプロセスは、システム モード DMA プロファイルを作成します。 次の手順では、一般的なシナリオを表します。

1.  では通常、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数では、ドライバー呼び出し[ **WDF\_DMA\_イネーブラー\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdf_dma_enabler_config_init)で、設定、**プロファイル**パラメーターを**SystemMode**または**SystemModeDuplex**します。 ドライバーを呼び出して[ **WdfDmaEnablerCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablercreate)を渡して、 [ **WDF\_DMA\_イネーブラー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/ns-wdfdmaenabler-_wdf_dma_enabler_config)受信したことを構造体します。

    ドライバー イネーブラー中に作成または[ *EvtDevicePrepareHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)します。

2.  ドライバーの[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数は、呼び出すことによって、DMA リソースを DMA イネーブラーを関連付けます、 [ **WdfDmaEnablerConfigureSystemProfile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)メソッド。 ドライバーの呼び出しを双方向のイネーブラー [ **WdfDmaEnablerConfigureSystemProfile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile) 2 回、各転送の方向を構成する 1 回です。

    ドライバーが呼び出せる[ **WdfDmaEnablerConfigureSystemProfile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerconfiguresystemprofile)後[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)が完了したらが、ドライバーは、DMA のトランザクションを初期化する前に、このメソッドを呼び出す必要があります。

## <a name="providing-optional-callback-functions"></a>省略可能なコールバック関数を提供します。


### <a href="" id="configuring-a-system-mode-dma-enabler"></a>DMA チャネルを構成します。

通常、KMDF ドライバーでは、DMA チャネルは構成しないでください。 ただし、特定の状況では、ドライバーはチャネル固有の構成を実行する必要があります。 たとえば、ドライバーでは、DMA コント ローラーで、次の手順を使用して実装されているカスタム関数を呼び出すことができます。

1.  ドライバーのいずれかで[要求ハンドラー](request-handlers.md)、ドライバー呼び出し[ **WdfDmaTransactionSetChannelConfigurationCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsetchannelconfigurationcallback)を登録する、 [ *EvtDmaTransactionConfigureDmaChannel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel)コールバック関数。
2.  ドライバーの[ *EvtDmaTransactionConfigureDmaChannel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel)コールバック関数の呼び出し[ **WdfDmaEnablerWdmGetDmaAdapter** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmaenabler/nf-wdfdmaenabler-wdfdmaenablerwdmgetdmaadapter)にWDM へのポインターを取得[ **DMA\_アダプター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_adapter)します。 この構造体は、ドライバーのシステム モード DMA チャネルを表すアダプター オブジェクトです。
3.  ドライバーを呼び出して[ **ConfigureAdapterChannel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-pconfigure_adapter_channel) DMA コント ローラーによって実装されるカスタム関数を有効にします。 このルーチンはで返されるアドレスからポインターによってのみ呼び出し可能な[ **DMA\_操作**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_dma_operations)構造体。
4.  ドライバーの[ *EvtDmaTransactionConfigureDmaChannel* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_configure_dma_channel)コールバック関数は、DMA チャネルを正常に構成した場合に TRUE を返します。
5.  フレームワークは、ドライバーの[ *EvtProgramDma* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_program_dma)コールバック関数。

### <a name="receiving-notification-of-transfer-completion"></a>転送完了の通知を受信

をバス マスターのコント ローラーを使用するデバイスとは異なりシステム モード DMA デバイスのハードウェアは、割り込みを発行して DMA 転送の完了を通知可能性があります。

デバイスは DMA 転送の完了を通知する割り込みが発生しない場合、ドライバーを提供できます、 [ *EvtDmaTransactionDmaTransferComplete* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nc-wdfdmatransaction-evt_wdf_dma_transaction_dma_transfer_complete)ときにフレームワークから呼び出されるイベント コールバック関数システム モード DMA の転送が完了しました。

このコールバック関数を登録するドライバーを呼び出す[ **WdfDmaTransactionSetTransferCompleteCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdmatransaction/nf-wdfdmatransaction-wdfdmatransactionsettransfercompletecallback)のいずれかからその[要求ハンドラー](request-handlers.md)。

 

 





