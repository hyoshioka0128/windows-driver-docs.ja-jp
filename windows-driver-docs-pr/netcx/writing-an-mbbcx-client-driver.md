---
title: MBB-NetAdapterCx クライアントドライバーを作成する
description: MBB クラス拡張と、クライアントドライバーが MBB moderm に対して実行する必要があるタスクの動作について説明します。
ms.assetid: FE69E832-848F-475A-9BF1-BBB198D08A86
keywords:
- モバイルブロードバンド (MBB) WDF クラス拡張、MBBCx、モバイルブロードバンド NetAdapterCx
ms.date: 03/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc98feda0b608ca5dff32664e392454912bcdefb
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208942"
---
# <a name="writing-an-mbbcx-client-driver"></a>MBBCx クライアント ドライバーの作成

>[!WARNING]
>このトピックのシーケンス図は、例示のみを目的としています。 パブリックコントラクトではなく、将来変更される可能性があります。

## <a name="inf-files-for-mbbcx-client-drivers"></a>MBBCx クライアントドライバー用の INF ファイル

MBBCx クライアントドライバーの INF ファイルは、他の NetAdapterCx クライアントドライバーと同じです。 詳細については、「 [INF files For NetAdapterCx client drivers](inf-files-for-netadaptercx-client-drivers.md)」を参照してください。

## <a name="initialize-the-device"></a>デバイスを初期化する

NetAdapterCx が[Netadapter デバイスの初期化](device-and-adapter-initialization.md)に必要なタスクに加えて、MBB クライアントドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数で次のタスクも実行する必要があります。

1. [*NetAdapterDeviceInitConfig*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterdeviceinitconfig)を呼び出した後、 [*WdfDeviceCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出す前に[**MbbDeviceInitConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdeviceinitconfig)を呼び出します。このとき、フレームワークによって渡された同じ[**wdfdevice\_INIT**](../wdf/wdfdevice_init.md)オブジェクトを参照します。

2. [**MbbDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdeviceinitialize)を呼び出して、初期化された[**MBB_DEVICE_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/ns-mbbcx-_mbb_device_config)構造体と*WdfDeviceCreate*から取得した wdfdevice オブジェクトを使用して、MBB デバイス固有のコールバック関数を登録します。

次の例は、MBB デバイスを初期化する方法を示しています。 わかりやすくするために、エラー処理は省略されています。

```C++
    status = NetAdapterDeviceInitConfig(deviceInit);
    status = MbbDeviceInitConfig(deviceInit);

    // Set up other callbacks such as Pnp and Power policy

    status = WdfDeviceCreate(&deviceInit, &deviceAttributes, &wdfDevice);

    MBB_DEVICE_CONFIG mbbDeviceConfig;
    MBB_DEVICE_CONFIG_INIT(&mbbDeviceConfig,
                           EvtMbbDeviceSendMbimFragment,
                           EvtMbbDeviceReceiveMbimFragment,
                           EvtMbbDeviceSendServiceSessionData,
                           EvtMbbDeviceCreateAdapter);

    status = MbbDeviceInitialize(wdfDevice, &mbbDeviceConfig);
```

他の種類の NetAdapterCx ドライバーとは異なり、MBB クライアントドライバーでは、 *Evtdriverdeviceadd*コールバック関数内から netadapter オブジェクトを作成することはできません。 代わりに、後で MBBCx によって指示されます。

次に、クライアントドライバーは[**MbbDeviceSetMbimParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdevicesetmbimparameters)を呼び出す必要があります。通常は、次のような[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で呼び出します。

このメッセージフローダイアグラムは、初期化プロセスを示しています。

![MBBCx クライアントドライバーの初期化プロセス](images/mbbcx_initializing.png)

このメッセージフローダイアグラムは、初期化プロセスを示しています。

![MBBCx クライアントドライバーの初期化プロセス](images/mbbcx_initializing.png)

## <a name="handling-mbim-control-messages"></a>MBIM 制御メッセージの処理

MBBCx では、コントロールプレーンの MBIM 仕様リビジョン1.0、セクション8、9、および10で定義されている標準の MBIM 制御コマンドを使用します。 コマンドと応答は、MBBCx によって提供されるクライアントドライバーおよび Api によって提供される一連のコールバック関数によって交換されます。 MBBCx は、次の関数呼び出しを使用して、MBIM 仕様リビジョン1.0、セクション5.3 で定義されている MBIM デバイスの運用モデルを模倣しています。

- MBBCx は、 [*Evtmbbデバイス Endmbimfragment*](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/nc-mbbcx-evt_mbb_device_send_mbim_fragment)コールバック関数を呼び出すことによって、mbim コマンドメッセージをクライアントドライバーに送信します。 クライアントドライバーは、 [**MbbRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbrequestcomplete)を呼び出すことによって、この送信要求を非同期に完了します。
- クライアントドライバーは、 [**MbbDeviceResponseAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdeviceresponseavailable)を呼び出すことによって、結果の可用性を通知します。
- MBBCx は、 [*EvtMbbDeviceReceiveMbimFragment*](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_receive_mbim_fragment) callback 関数を呼び出して、クライアントドライバーから mbim 応答メッセージをフェッチします。 クライアントドライバーは、 [**MbbRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbrequestcompletewithinformation)を呼び出すことによって、この get 応答要求を非同期に完了します。
- MBB client ドライバーは、 **MbbDeviceResponseAvailable**を呼び出して、要請されていないデバイスイベントを MBBCx に通知する場合があります。 次に、MBBCx は、MBIM 応答メッセージをフェッチするのと同様に、クライアントドライバーから情報を取得します。

次の図は、MBBCx のドライバーメッセージ交換フローを示しています。

![Mbim メッセージ交換](images/mbim.png)

### <a name="synchronization-of-mbim-control-messages"></a>MBIM 制御メッセージの同期

MBBCx フレームワークは、常に、クライアントドライバーの*Evtmbb Endmbimfragment*および*EvtMbbDeviceReceiveMbimFragment*コールバック関数への呼び出しをシリアル化します。 クライアントドライバーが**MbbRequestComplete**または**MbbRequestCompleteWithInformation**のいずれかを呼び出すまで、フレームワークによって新しい呼び出しは行われません。

クライアントドライバーは、重複する*EvtmbbEvtMbbDeviceReceiveMbimFragment Endmbimfragment*または** コールバックを受信しないことが保証されていますが、前のコマンドの応答がデバイスから利用できるようになるまで、連続して複数の呼び出しを受け取る場合があります。

デバイスが*d0*状態でない場合、MBBCx フレームワークは最初にデバイスを d0 に (つまり、 [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)を呼び出して)、 *Evtmbb Endmbimfragment*または*EvtMbbDeviceReceiveMbimFragment*を呼び出します。 また、MBBCx フレームワークでは、デバイスを D0 状態のままにすることも保証されます。つまり、クライアントが**MbbRequestComplete**または**MbbRequestCompleteWithInformation**を呼び出すまで、 [*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)は呼び出されません。

## <a name="creating-the-netadapter-interface-for-the-pdp-contexteps-bearer"></a>PDP コンテキスト/EPS ベアラー用の NetAdapter インターフェイスを作成する

データセッションを確立する前に、MBBCx は NETADAPTER オブジェクトを作成するようにクライアントドライバーに指示します。このオブジェクトは、アクティブ化されたデータセッションのネットワークインターフェイスを表すために MBBCx によって使用されます。 これは、クライアントドライバーの[*EvtMbbDeviceCreateAdapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter) callback 関数を呼び出すことによって MBBCx によって実現されます。

*EvtMbbDeviceCreateAdapter* callback 関数の実装では、MBBCx client ドライバーは、netadapter オブジェクトを任意の NetAdapterCx クライアントドライバーとして作成するために必要なタスクと同じタスクを最初に実行する必要があります。 さらに、次の追加のタスクも実行する必要があります。

1. [*NetAdapterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptercreate)によって作成された netadapter オブジェクトで[**MbbAdapterInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbadapterinitialize)を呼び出します。

2. *MbbAdapterinitialize*を呼び出した後、 [**MbbAdapterGetSessionId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbadaptergetsessionid)を呼び出して、MBBCX がこの netadapter オブジェクトを使用するデータセッション ID を取得します。 たとえば、戻り値が0の場合、MBBCx は、プライマリ PDP コンテキスト/既定の EPS ベアラーによって確立されたデータセッションに対して、この NETADAPTER インターフェイスを使用することを意味します。

3. MBBCx クライアントドライバーは、作成された NETADAPTER オブジェクトと返された*SessionId*の間の内部マッピングを保持することをお勧めします。 これは、データセッションから NETADAPTER へのオブジェクトの関係を追跡するのに役立ちます。これは、複数の PDP コンテキスト/EPS bearers がアクティブ化されている場合に特に便利です。

4. *EvtMbbDeviceCreateAdapter*から戻る前に、クライアントドライバーは[**NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadapterstart)を呼び出してアダプターを開始する必要があります。 必要に応じて、 **NetAdapterStart**の呼び出しの*前に*、次の関数の1つ以上を呼び出して、アダプターの機能を設定することもできます。
    - [**NetAdapterSetDatapathCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)
    - [**NetAdapterSetLinkLayerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetlinklayercapabilities)
    - [**NetAdapterSetLinkLayerMtuSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetlinklayermtusize)
    - [**NetAdapterSetPowerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/netadapter/nf-netadapter-netadaptersetpowercapabilities)

MBBCx は、このコールバック関数を少なくとも1回呼び出します。そのため、プライマリ PDP コンテキスト/既定の EPS ベアラーには、常に1つの NETADPATER オブジェクトが存在します。 複数の PDP コンテキスト/EPS bearers がアクティブ化されている場合、MBBCx は、すべてのデータセッションが確立されるたびに、このコールバック関数をより多く呼び出します。 次の図に示すように、NETADAPTER オブジェクトとデータセッションによって表されるネットワークインターフェイスの間に、一対一のリレーションシップが存在している必要があります。

![複数の NetAdapters](images/multi-netadapter.png)

次の例は、データセッションの NETADAPTER オブジェクトを作成する方法を示しています。 アダプターの機能を設定するために必要なエラー処理とコードは、簡潔でわかりやすくするために残されています。

```C++
    NTSTATUS
    EvtMbbDeviceCreateAdapter(
        WDFDEVICE  Device,
        PNETADAPTER_INIT AdapterInit
    )
    {
        // Get the client driver defined per-device context
        PMY_DEVICE_CONTEXT deviceContext = MyGetDeviceContext(Device);

        // Set up the client driver defined per-adapter context
        WDF_OBJECT_ATTRIBUTES adapterAttributes;
        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&adapterAttributes,
                                                MY_NETADAPTER_CONTEXT);


        // Create the NETADAPTER object
        NETADAPTER netAdapter;
        NTSTATUS status = NetAdapterCreate(AdapterInit,
                                           &adapterAttributes,
                                           &netAdapter);

        // Initialize the adapter for MBB
        status = MbbAdapterInitialize(netAdapter);

        // Retrieve the Session ID and use an array to store
        // the session <-> NETADAPTER object mapping
        ULONG sessionId;
        PMY_NETADAPTER_CONTEXT netAdapterContext = MyGetNetAdapterContext(netAdapter);

        netAdapterContext->NetAdapter = netAdapter;

        sessionId = MbbAdapterGetSessionId(netAdapter);

        netAdapterContext->SessionId = sessionId;

        deviceContext->Sessions[sessionId].NetAdapterContext = netAdapterContext;

        //
        // Optional: set adapter capabilities
        //
        ...
        NetAdapterSetDatapathCapabilities(netAdapter,
                                          &txCapabilities,
                                          &rxCapabilities);

        ...
        NetAdapterSetLinkLayerCapabilities(netAdapter,
                                           &linkLayerCapabilities);

        ...
        NetAdapterSetLinkLayerMtuSize(netAdapter,
                                      MY_MAX_PACKET_SIZE - ETHERNET_HEADER_LENGTH);

        //
        // Required: start the adapter
        //
        status = NetAdapterStart(netAdapter);

        return status;
    }
```

データパス機能の設定のコード例については、「[ネットワークデータバッファー管理](network-data-buffer-management.md)」を参照してください。

MBBCx は、同じセッション ID を持つ**MBIM_CID_CONNECT**を要求する前に、 *EvtMbbDeviceCreateAdapter*を呼び出すことを保証します。 次のフロー図は、NETADAPTER オブジェクトを作成するときのクライアントドライバーとクラス拡張との相互作用を示しています。  

![MBB クライアントドライバーの NETADAPTER の作成とアクティブ化](images/activation.png)

プライマリ PDP コンテキスト/既定の EPS ベアラーの NETADAPTER オブジェクトを作成するためのフローは、 [*EvtdeviceMBBCx ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)が正常に終了したときに、によって開始されます。

セカンダリ PDP コンテキスト/専用 EPS ベアラーの NETADAPTER オブジェクトを作成するフローは、オンデマンド接続がアプリケーションによって要求されるたびに、 *Wwansvc*によってトリガーされます。

### <a name="lifetime-of-the-netadapter-object"></a>NETADAPTER オブジェクトの有効期間

クライアントドライバーによって作成された NETADAPTER オブジェクトは、使用されなくなったときに MBBCx によって自動的に破棄されます。 たとえば、追加の PDP コンテキスト/EPS bearers が非アクティブ化された後に発生します。 **MBBCx クライアントドライバーは、作成する NETADAPTER オブジェクトで[Wdfobjectdelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)を呼び出すことはできません。**

クライアントドライバーが NETADAPTER オブジェクトに関連付けられたコンテキストデータをクリーンアップする必要がある場合、 **NetAdapterCreate**を呼び出すときに、オブジェクト属性構造に[*Evtdestroycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)関数を提供する必要があります。  

## <a name="power-management-of-the-mbb-device"></a>MBB デバイスの電源管理

電源管理では、クライアントドライバーは、[他の種類の NetAdapterCx クライアントドライバーと同様](configuring-power-management.md)に NETPOWERSETTINGS オブジェクトを使用する必要があります。

## <a name="handling-device-service-sessions"></a>デバイスサービスセッションの処理

アプリケーションが DSS データをモデムデバイスに送信すると、MBBCx はクライアントドライバーの[*Evtmbbデバイス Endservicesessiondata*](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nc-mbbcx-evt_mbb_device_send_device_service_session_data) callback 関数を呼び出します。 その後、クライアントドライバーはデータを非同期にデバイスに送信し、送信が完了した後に[**MbbDeviceSendDeviceServiceSessionDataComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdevicesenddeviceservicesessiondatacomplete)を呼び出す必要があります。 MBBCx を使用すると、データに割り当てられたメモリを解放できます。

逆に、クライアントドライバーは[**MbbDeviceReceiveDeviceServiceSessionData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mbbcx/nf-mbbcx-mbbdevicereceivedeviceservicesessiondata)を呼び出して、MBBCx を介してアプリケーションにデータを渡します。
