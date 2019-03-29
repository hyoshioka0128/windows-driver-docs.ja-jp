---
title: MBB NetAdapterCx クライアント ドライバーを作成します。
description: MBB NetAdapter クラスの拡張機能と、クライアント ドライバーが MBB moderm に対して実行する必要がありますタスクの動作について説明します。
ms.assetid: FE69E832-848F-475A-9BF1-BBB198D08A86
keywords:
- (MBB モバイル ブロード バンド) WDF クラスの拡張機能、MBBCx、モバイル ブロード バンド NetAdapterCx
ms.date: 03/19/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18fdbe9f8861a0db9217fdbf4c6276003547a815
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136125"
---
# <a name="writing-an-mbbcx-client-driver"></a>MBBCx クライアント ドライバーの作成

[!include[MBBCx Beta Prerelease](../mbbcx-beta-prerelease.md)]

>[!WARNING]
>このトピックの「シーケンス図では、あくまで説明のため。 パブリック コントラクトが、今後変更される可能性が。

## <a name="inf-files-for-mbbcx-client-drivers"></a>MBBCx クライアント ドライバーの INF ファイル

MBBCx クライアント ドライバーの INF ファイルでは、その他の NetAdapterCx クライアント ドライバーと同じです。 詳細については、次を参照してください。 [NetAdapterCx クライアント ドライバーの INF ファイル](inf-files-for-netadaptercx-client-drivers.md)します。

## <a name="initialize-the-device"></a>デバイスを初期化します。

これらのタスクの NetAdapterCx で必要なだけでなく[NetAdapter デバイスの初期化](device-and-adapter-initialization.md)、MBB のクライアント ドライバーで次のタスクを実行する必要があります、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

1. 呼び出す[ **MbbDeviceInitConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdeviceinitconfig)呼び出した後[ *NetAdapterDeviceInitConfig* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterdeviceinitconfig)呼び出す前に[ *WdfDeviceCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate)、同じ参照[ **WDFDEVICE\_INIT** ](../wdf/wdfdevice_init.md)フレームワークによってオブジェクトが渡されます。

2. 呼び出す[ **MbbDeviceInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdeviceinitialize) MBB デバイスに固有のコールバックを登録する機能が初期化されたを使用して[ **MBB_DEVICE_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/ns-mbbcx-_mbb_device_config)構造体と WDFDEVICE オブジェクトから取得*WdfDeviceCreate*します。

次の例では、MBB デバイスを初期化する方法を示します。 エラー処理はわかりやすくするため省略してをいます。

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

NetAdapterCx ドライバーの他の種類とは異なり MBB クライアント ドライバーする必要がありますいないオブジェクトを作成、NETADAPTER 内から、 *EvtDriverDeviceAdd*コールバック関数。 代わりに、後でを MBBCx によって指示されるは。

次に、クライアント ドライバーを呼び出す必要があります[ **MbbDeviceSetMbimParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdevicesetmbimparameters)、通常、 [ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック次の関数。

このメッセージのフロー図は、初期化プロセスを示しています。

![MBBCx クライアント ドライバーの初期化プロセス](images/mbbcx_initializing.png)

このメッセージのフロー図は、初期化プロセスを示しています。

![MBBCx クライアント ドライバーの初期化プロセス](images/mbbcx_initializing.png)

## <a name="handling-mbim-control-messages"></a>MBIM コントロール メッセージの処理

MBBCx は、MBIM 仕様バージョン 1.0 では、8、9、および 10 のセクションでは、コントロール プレーンので定義されている標準 MBIM 制御コマンドを使用します。 コマンドと応答は、一連のクライアント ドライバーによって提供されるコールバック関数と MBBCx で提供される Api を介して交換されます。 MBBCx は、MBIM 仕様バージョン 1.0、5.3、セクションでこれらの関数呼び出しを使用して定義されている、MBIM デバイスの運用モデルを模倣します。

- MBBCx クライアント ドライバーに呼び出すことによって MBIM コマンド メッセージを送信するその[ *EvtMbbDeviceSendMbimFragment* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/nc-mbbcx-evt_mbb_device_send_mbim_fragment)コールバック関数。 クライアント ドライバーは非同期的に呼び出すことによってこの送信要求を完了[ **MbbRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbrequestcomplete)します。
- クライアント ドライバーは、呼び出すことによって、結果の可用性を通知[ **MbbDeviceResponseAvailable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdeviceresponseavailable)します。
- MBBCx クライアント ドライバーから呼び出すことによって、MBIM 応答メッセージをフェッチするその[ *EvtMbbDeviceReceiveMbimFragment* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_receive_mbim_fragment)コールバック関数。 クライアント ドライバーは非同期的に呼び出すことでこの取得応答の要求を完了[ **MbbRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbrequestcompletewithinformation)します。
- MBB クライアント ドライバーは呼び出すことによって要請されていないデバイス イベントの MBBCx を通知する可能性があります**MbbDeviceResponseAvailable**します。 MBBCx し、情報を取得しますクライアント ドライバーから同様にする MBIM 応答メッセージがフェッチされます。

次の図は、MBBCx クライアント ドライバーのメッセージ交換フローを示しています。

![Mbim メッセージ交換](images/mbim.png)

### <a name="synchronization-of-mbim-control-messages"></a>MBIM コントロール メッセージの同期

MBBCx フレームワークは、クライアント ドライバーへの呼び出しを常にシリアル化*EvtMbbDeviceSendMbimFragment*と*EvtMbbDeviceReceiveMbimFragment*コールバック関数。 新しい呼び出しは行われません、フレームワークによって、クライアント ドライバーでは、いずれかを呼び出すまで**MbbRequestComplete**または**MbbRequestCompleteWithInformation**します。

クライアント ドライバーがオーバー ラップを受け取らないように保証中*EvtMbbDeviceSendMbimFragment*または*EvtMbbDeviceReceiveMbimFragment*コールバックを受け取るを連続してそれらを複数回呼び出す場合があります前に、前のコマンドに対する応答を指定する場合は、デバイスで実行できます。

デバイスがない場合、 *D0* MBBCx フレームワークが D0 にデバイスを最初には、状態 (つまり、呼び出す[ *EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry))を呼び出す前に*EvtMbbDeviceSendMbimFragment*または*EvtMbbDeviceReceiveMbimFragment*します。 MBBCx フレームワークも保証されることが維持されますデバイス D0 状態では呼び出しませんつまり[ *EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)クライアントを呼び出すまで、 **MbbRequestComplete**または**MbbRequestCompleteWithInformation**します。

## <a name="creating-the-netadapter-interface-for-the-pdp-contexteps-bearer"></a>PDP コンテキスト/EPS ベアラーの NetAdapter インターフェイスの作成

データのセッションを確立する前に MBBCx が NETADAPTER オブジェクトを作成するクライアント ドライバーを指示してデータ セッションがアクティブ化のネットワーク インターフェイスを表す MBBCx で使用されます。 これは、MBBCx クライアント ドライバーへの呼び出しによって実現されます[ *EvtMbbDeviceCreateAdapter* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_create_adapter)コールバック関数。

実装では、 *EvtMbbDeviceCreateAdapter*コールバック関数、MBBCx クライアント ドライバーはすべて NetAdapterCx クライアント ドライバー NETADAPTER オブジェクトを作成するために必要な同じタスクを実行する必要がありますまずします。 さらに、次の追加タスクを実行にする必要があります。

1. 呼び出す[ **MbbAdapterInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbadapterinitialize)によって作成された NETADAPTER オブジェクトで[ *NetAdapterCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptercreate)します。

2. 呼び出した後*MbbAdapterinitialize*、呼び出す[ **MbbAdapterGetSessionId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbadaptergetsessionid)を取得する MBBCx のデータのセッション ID がこの NETADAPTER オブジェクトを使用します。 たとえば、返される値が 0 の場合に MBBCx では、この NETADAPTER インターフェイスを使用してデータ セッションがプライマリの PDP コンテキストと既定の EPS ベアラーを確立するにはなります。

3. MBBCx クライアント ドライバーが作成された NETADAPTER オブジェクトおよび返された間の内部マッピングを維持することをお勧めします。 *SessionId*します。 これにより、複数の PDP コンテキスト/EPS 担ぎがアクティブになったときに特に便利ですが、データ セッション-NETADAPTER にオブジェクト リレーションシップを追跡できます。

4. 返す前に*EvtMbbDeviceCreateAdapter*、クライアント ドライバーはアダプターを呼び出すことによって開始する必要があります[ **NetAdapterStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadapterstart)します。 1 つ以上のこれらの関数を呼び出すことによって、アダプターの機能も設定、必要に応じて、*する前に*呼び出し**NetAdapterStart**:
    - [**NetAdapterSetDatapathCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetdatapathcapabilities)
    - [**NetAdapterSetLinkLayerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetlinklayercapabilities)
    - [**NetAdapterSetLinkLayerMtuSize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetlinklayermtusize)
    - [**NetAdapterSetPowerCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/netadapter/nf-netadapter-netadaptersetpowercapabilities)

MBBCx は、常にプライマリの PDP コンテキストと既定の EPS ベアラーの 1 つの NETADPATER オブジェクトがあるため、少なくとも 1 回このコールバック関数を呼び出します。 複数の PDP コンテキスト/EPS 担ぎがアクティブになる場合 MBBCx がこのコールバック関数を呼び出します他にも 1 回が確立されているすべてのデータ セッション。 次の図に示すように、NETADAPTER オブジェクトおよびデータのセッションで表される、ネットワーク インターフェイスの間で一対一のリレーションシップが必要があります。

![複数の NetAdapters](images/multi-netadapter.png)

次の例では、データ セッション NETADAPTER オブジェクトを作成する方法を示します。 エラー処理とアダプターの機能を設定するために必要なコードを簡潔にするためにわかりやすくするため左はことに注意してください。

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

データパス機能の設定のコード例では、次を参照してください。[ネットワーク データ バッファー管理](network-data-buffer-management.md)します。

呼び出していることを保証 MBBCx *EvtMbbDeviceCreateAdapter*要求する前に**MBIM_CID_CONNECT**同じのセッション ID に置き換えます。 次のフロー図は、NETADAPTER オブジェクトを作成するクライアント ドライバーと、クラス拡張の間の相互作用を示しています。  

![NETADAPTER 作成と、MBB クライアント ドライバーの有効化](images/activation.png)

プライマリの PDP コンテキストと既定の EPS ベアラーは MBBCx によって開始されるは、NETADAPTER オブジェクトを作成するためのフローと[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)が正常に完了します。

によってセカンダリ PDP コンテキスト/専用の EPS ベアラーがトリガーされるは、NETADAPTER オブジェクトを作成するためのフロー *WwanSvc*アプリケーションがオンデマンドでの接続を要求するたびにします。

### <a name="lifetime-of-the-netadapter-object"></a>NETADAPTER オブジェクトの有効期間

クライアント ドライバーによって作成された NETADAPTER オブジェクトが自動的にで破壊する MBBCx 使用がの場合。 たとえば、追加の PDP コンテキスト/EPS 担ぎが非アクティブ化した後にこれが発生します。 **MBBCx クライアント ドライバーを呼び出してはならない[WdfObjectDelete](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete) NETADAPTER オブジェクトを作成します。**

クライアント ドライバーを NETADAPTER オブジェクトに関連付けられているコンテキスト データをクリーンアップする必要がある場合は指定する必要があります、 [ *EvtDestroyCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)関数、オブジェクトの属性の構造を呼び出すときに**NetAdapterCreate**します。  

## <a name="power-management-of-the-mbb-device"></a>MBB デバイスの電源管理

電源管理のためのクライアント ドライバーが NETPOWERSETTINGS オブジェクトを使用します。[などの他の種類のクライアント ドライバーの NetAdapterCx](configuring-power-management.md)します。

## <a name="handling-device-service-sessions"></a>デバイス サービス セッションの処理

アプリケーションでは、モデム デバイス DSS データを送信する MBBCx 呼び出しますクライアント ドライバーの[ *EvtMbbDeviceSendServiceSessionData* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nc-mbbcx-evt_mbb_device_send_device_service_session_data)コールバック関数。 クライアント ドライバーし、データの送信は非同期的に呼び出しとデバイスに[ **MbbDeviceSendDeviceServiceSessionDataComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdevicesenddeviceservicesessiondatacomplete)送信が完了すると、そのため MBBCx し、メモリを解放できますデータに割り当てられます。

逆に、クライアント ドライバーを呼び出す[ **MbbDeviceReceiveDeviceServiceSessionData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mbbcx/nf-mbbcx-mbbdevicereceivedeviceservicesessiondata) MBBCx 経由でアプリケーションまで、データの受け渡しします。
