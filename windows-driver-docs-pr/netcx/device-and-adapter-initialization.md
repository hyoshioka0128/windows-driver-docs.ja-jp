---
title: デバイスとアダプターの初期化
description: デバイスとアダプターの初期化
ms.assetid: EBBEF0FB-6CDB-4899-AAE9-71812EE20AFB
keywords:
- NetAdapterCx デバイスの初期化、NetCx デバイスの初期化、NetAdapterCx アダプターの初期化、NetCx アダプターの初期化
ms.date: 08/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e3e14e6c80f6ef27fdea607b9ce70ebd988ddc59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582446"
---
# <a name="device-and-adapter-initialization"></a>デバイスとアダプターの初期化

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

このトピックでは、NetAdapterCx クライアント ドライバーを初期化して WDFDEVICE および NETADAPTER オブジェクトを開始する手順について説明します。 これらのオブジェクトとの関係に関する詳細については、次を参照してください。[概要の NetAdapterCx オブジェクト](summary-of-netadaptercx-objects.md)します。

## <a name="evtwdfdriverdeviceadd"></a>EVT_WDF_DRIVER_DEVICE_ADD

NetAdapterCx のクライアント ドライバーは、登録、 [ *EVT_WDF_DRIVER_DEVICE_ADD* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数を呼び出すときに[ **WdfDriverCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547175)その[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff540807)ルーチン。

[ *EVT_WDF_DRIVER_DEVICE_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)、NetAdapterCx クライアント ドライバーは、次の順序で行う必要があります。

1. 呼び出す[ **NetAdapterDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)します。

    ```C++
    status = NetAdapterDeviceInitConfig(DeviceInit);
    if (!NT_SUCCESS(status)) 
    {
        return status;
    }
    ```

2. 呼び出す[ **WdfDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545926)します。 

    > [!TIP]
    > デバイスは、1 つ以上の NETADAPTER をサポートする、デバイス コンテキストで各アダプターへのポインターを格納することをお勧めします。

3. NETADAPTER オブジェクトを作成します。 これを行うには、クライアントを呼び出すか[ **NetDefaultAdapterInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netdefaultadapterinitallocate)または[ **NetAdapterInitAllocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterinitallocate)、その後に省略可能な**NetAdapterInitSetXxx**を初期化するメソッド、アダプターの属性。 最後に、クライアントが呼び出す[ **NetAdapterCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)します。 

    次の例では、クライアント ドライバーが既定 NETADAPTER オブジェクトを初期化する方法を示します。 この例では、エラー処理が簡略化されたことに注意してください。

    ```C++
    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attribs, MY_ADAPTER_CONTEXT);

    //
    // Allocate the initialization structure
    //
    PNETADAPTER_INIT adapterInit = NetDefaultAdapterInitAllocate(device);
    if(adapterInit == NULL)
    {
        return status;
    }        

    //
    // Optional: set additional attributes
    //

    // Datapath callbacks for creating packet queues
    PNET_ADAPTER_DATAPATH_CALLBACKS datapathCallbacks;
    NET_ADAPTER_DATAPATH_CALLBACKS_INIT(datapathCallbacks,
                                        MyEvtAdapterCreateTxQueue,
                                        MyEvtAdapterCreateRxQueue);
    NetAdapterInitSetDatapathCallbacks(adapterInit,
                                        datapathCallbacks);

    // Power settings attributes
    NetAdapterInitSetNetPowerSettingsAttributes(adapterInit,
                                                attribs);

    // Net request attributes
    NetAdapterInitSetNetRequestAttributes(adapterInit,
                                            attribs);

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

必要に応じて、NETADAPTER オブジェクトにコンテキストの領域を追加できます。 WDF のオブジェクトに対するコンテキストを設定することができますので、WDFDEVICE と NETADAPTER オブジェクトに対して別のコンテキストの領域を追加できます。 手順 3 での例で、クライアントの追加`MY_ADAPTER_CONTEXT`NETADAPTER オブジェクトにします。 詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](../wdf/framework-object-context-space.md)します。

WDFDEVICE のコンテキストでのデバイス関連データを配置し、リンク層などのネットワーク関連のデータは、NETADAPTER コンテキストに対処することをお勧めします。 既存の NDIS 6.x ドライバーを移植する場合はネットワーク関連およびデバイス関連データを 1 つのデータ構造に結合する 1 つ MiniportAdapterContext 可能性があります。 移植プロセスを簡素化するには、WDFDEVICE コンテキストにその全体の構造を変換し、NETADAPTER のコンテキストに WDFDEVICE のコンテキストを指している小規模な構造を作成します。

2 つのコールバックを行うことができます必要に応じて、 [ **NET_ADAPTER_DATAPATH_CALLBACKS_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-net_adapter_datapath_callbacks_init)メソッド。

* [*EVT_NET_ADAPTER_CREATE_TXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_txqueue)
* [*EVT_NET_ADAPTER_CREATE_RXQUEUE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nc-netadapter-evt_net_adapter_create_rxqueue)

詳細については、これらのコールバックの実装に提供するものは、個々 のリファレンス ページを参照してください。

## <a name="evtwdfdevicepreparehardware"></a>EVT_WDF_DEVICE_PREPARE_HARDWARE

多くの NetAdapterCx クライアント ドライバー内から、アダプターを開始する、 [ *EVT_WDF_DEVICE_PREPARE_HARDWARE* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)の注目すべき例外でのコールバック関数[モバイル ブロード バンド クラス拡張機能のクライアント ドライバー](mobile-broadband-mbb-wdf-class-extension-mbbcx.md)します。 登録する、 *EVT_WDF_DEVICE_PREPARE_HARDWARE* NetAdapterCx クライアント ドライバーで呼び出す必要がありますコールバック関数、 [ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)します。 

[ *EVT_WDF_DEVICE_PREPARE_HARDWARE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)、他のハードウェアの準備タスクに加えて、クライアント ドライバーを呼び出す必要があります[ **NetAdapterStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart). これを行うには、前に、ドライバーはアダプターの機能を必要に応じて設定できます。

次の例では、クライアント ドライバーが NETADAPTER オブジェクトを開始する方法を示します。 各アダプターの機能のメソッドを設定するために必要なコードを省略して簡潔さとわかりやすくするために、エラー処理が簡略化されたことに注意してください。

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

// Power capabilities
...
NetAdapterSetPowerCapabilities(netAdapter,
                               &powerCapabilities);

// Receive scaling capabilities
...
NetAdapterSetReceiveScalingCapabilities(netAdapter,
                                        receiveScalingCapabilities);

// Hardware offload capabilities
...
NetAdapterOffloadSetChecksumCapabilities(netAdapter,
                                         &checksumCapabilities,
                                         EvtAdapterOffloadSetChecksum);
...
NetAdapterOffloadSetLsoCapabilities(netAdapter,
                                    &lsoCapabilities,
                                    EvtAdapterOffloadSetLso);

//
// Required: start the adapter
//
status = NetAdapterStart(netAdapter);
if(!NT_SUCCESS(status))
{
    return status;
}
```
