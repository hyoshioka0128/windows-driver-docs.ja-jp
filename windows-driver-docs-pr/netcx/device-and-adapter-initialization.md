---
title: デバイスとアダプターの初期化
description: デバイスとアダプターの初期化
ms.assetid: EBBEF0FB-6CDB-4899-AAE9-71812EE20AFB
keywords:
- NetAdapterCx デバイスの初期化, NetCx デバイスの初期化, NetAdapterCx アダプターの初期化, NetCx アダプターの初期化
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.custom: Vib
ms.openlocfilehash: fa223b69e656015ff82bcdaebc79283eb52df292
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210888"
---
# <a name="device-and-adapter-initialization"></a>デバイスとアダプターの初期化

このトピックでは、NetAdapterCx クライアントドライバーが WDFDEVICE オブジェクトと NETADAPTER オブジェクトを初期化して起動する手順について説明します。 これらのオブジェクトとそれらの関係の詳細については、「 [NetAdapterCx オブジェクトの概要](summary-of-netadaptercx-objects.md)」を参照してください。

## <a name="evt_wdf_driver_device_add"></a>EVT_WDF_DRIVER_DEVICE_ADD

NetAdapterCx クライアントドライバーは、その[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)ルーチンから[**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出すときに、 [*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を登録します。

[*EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)では、NetAdapterCx クライアントドライバーは次の処理を順番に実行する必要があります。

1. [**Netdeviceinitconfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netdevice/nf-netdevice-netdeviceinitconfig)を呼び出します。

    ```C++
    status = NetDeviceInitConfig(DeviceInit);
    if (!NT_SUCCESS(status)) 
    {
        return status;
    }
    ```

2. [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出します。 

    > [!TIP]
    > デバイスで複数の NETADAPTER がサポートされている場合は、各アダプターへのポインターをデバイスコンテキストに保存することをお勧めします。

3. NETADAPTER オブジェクトを作成します。 これを行うために、クライアントは[**NetAdapterInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterinitallocate)を呼び出した後、オプションの**NetAdapterInitSetXxx**メソッドを呼び出して、アダプターの属性を初期にします。 最後に、クライアントは[**NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)を呼び出します。 

    次の例は、クライアントドライバーが NETADAPTER オブジェクトを初期化する方法を示しています。 この例では、エラー処理が簡略化されていることに注意してください。

    ```C++
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attribs, MY_ADAPTER_CONTEXT);

    //
    // Allocate the initialization structure
    //
    PNETADAPTER_INIT adapterInit = NetAdapterInitAllocate(device);
    if(adapterInit == NULL)
    {
        return status;
    }        

    //
    // Optional: set additional attributes
    //

    // Datapath callbacks for creating packet queues
    NET_ADAPTER_DATAPATH_CALLBACKS datapathCallbacks;
    NET_ADAPTER_DATAPATH_CALLBACKS_INIT(&datapathCallbacks,
                                        MyEvtAdapterCreateTxQueue,
                                        MyEvtAdapterCreateRxQueue);
    NetAdapterInitSetDatapathCallbacks(adapterInit,
                                       datapathCallbacks);
    // 
    // Required: create the adapter
    //
    NETADAPTER* netAdapter;
    status = NetAdapterCreate(adapterInit, &attribs, netAdapter);
    if(!NT_SUCCESS(status))
    {
        NetAdapterInitFree(adapterInit);
        adapterInit = NULL;
        return status;
    }

    //
    // Required: free the adapter initialization object even 
    // if adapter creation succeeds
    //
    NetAdapterInitFree(adapterInit);
    adapterInit = NULL;

    //
    // Optional: initialize the adapter's context
    //
    PMY_ADAPTER_CONTEXT adapterContext = GetMyAdapterContext(&netAdapter);
    ...
    ```

必要に応じて、NETADAPTER オブジェクトにコンテキスト空間を追加できます。 任意の WDF オブジェクトにコンテキストを設定できるため、WDFDEVICE オブジェクトと NETADAPTER オブジェクト用に個別のコンテキスト領域を追加することができます。 手順3の例では、クライアントが NETADAPTER オブジェクトに `MY_ADAPTER_CONTEXT` を追加します。 詳細については、「[フレームワークオブジェクトコンテキスト空間](../wdf/framework-object-context-space.md)」を参照してください。

WDFDEVICE のコンテキストにデバイス関連のデータを配置し、ネットワーク関連のデータ (リンク層のアドレスなど) を NETADAPTER コンテキストに格納することをお勧めします。 既存の NDIS 6.x ドライバーを移植する場合は、ネットワーク関連のデータとデバイス関連のデータを1つのデータ構造に結合する MiniportAdapterContext が1つ存在する可能性があります。 移植プロセスを単純化するには、その構造全体を WDFDEVICE コンテキストに変換し、NETADAPTER のコンテキストを WDFDEVICE のコンテキストを指す小さな構造体にします。

必要に応じて、 [**NET_ADAPTER_DATAPATH_CALLBACKS_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)メソッドに2つのコールバックを提供できます。

* [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)
* [*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)

これらのコールバックの実装で提供する内容の詳細については、個々のリファレンスページを参照してください。

## <a name="evt_wdf_device_prepare_hardware"></a>EVT_WDF_DEVICE_PREPARE_HARDWARE

多くの NetAdapterCx クライアントドライバーは、 [*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数内からアダプターを起動しますが、[モバイルブロードバンドクラス拡張クライアントドライバー](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)の注目すべき例外があります。 *EVT_WDF_DEVICE_PREPARE_HARDWARE*コールバック関数を登録するには、NetAdapterCx client ドライバーが[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)を呼び出す必要があります。 

[*EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)では、クライアントドライバーは[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出す必要がありますが、その他のハードウェア準備タスクにもなります。 これを行う前に、ドライバーは必要に応じてアダプターの機能を設定できます。

次の例は、クライアントドライバーが NETADAPTER オブジェクトを開始する方法を示しています。 各アダプターの機能を設定するために必要なコードは、簡潔でわかりやすくするために残されており、エラー処理が簡略化されています。

```C++
PMY_DEVICE_CONTEXT deviceContext = GetMyDeviceContext(device);

NETADAPTER netAdapter = deviceContext->NetAdapter;

PMY_ADAPTER_CONTEXT adapterContext = GetMyAdapterContext(netAdapter);

//
// Optional: set adapter capabilities
//

// Link layer capabilities
...
NetAdapterSetDatapathCapabilities(netAdapter, 
                                  &txCapabilities, 
                                  &rxCapabilities);
...
NetAdapterSetLinkLayerCapabilities(netAdapter,
                                   &linkLayerCapabilities);

NetAdapterSetLinkLayerMtuSize(netAdapter,
                              MY_MAX_PACKET_SIZE - ETHERNET_HEADER_LENGTH);

NetAdapterSetPermanentLinkLayerAddress(netAdapter,
                                       &adapterContext->PermanentAddress);

NetAdapterSetCurrentLinkLayerAddress(netAdapter,
                                     &adapterContext->CurrentAddress);

// Datapath capabilities
...
NetAdapterSetDatapathCapabilities(netAdapter,
                                  &txCapabilities,
                                  &rxCapabilities);

// Receive scaling capabilities
...
NetAdapterSetReceiveScalingCapabilities(netAdapter,
                                        &receiveScalingCapabilities);

// Hardware offload capabilities
...
NetAdapterOffloadSetChecksumCapabilities(netAdapter,
                                         &checksumCapabilities);
...
NetAdapterOffloadSetLsoCapabilities(netAdapter,
                                    &lsoCapabilities);
                                    ...
NetAdapterOffloadSetRscCapabilities(netAdapter,
                                    &rscCapabilities);

//
// Required: start the adapter
//
status = NetAdapterStart(netAdapter);
if(!NT_SUCCESS(status))
{
    return status;
}
```
