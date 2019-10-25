---
title: WDI IHV ドライバー インターフェイス
description: WDI IHV ミニポートは、他の NDIS ミニポートドライバーと同じように、NDIS ミニポートの開発方法とドキュメントに従っています。
ms.assetid: B4528C70-9FE4-4E00-9D0B-8832CCEC982E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec567a375806ae73477c015caf86c078f38db260
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842925"
---
# <a name="wdi-ihv-driver-interfaces"></a>WDI IHV ドライバー インターフェイス


WDI IHV ミニポートは、他の NDIS ミニポートドライバーと同じように、NDIS ミニポートの開発方法とドキュメントに従っています。 NDIS ハンドラーに対するネイティブ WLAN ミニポートドライバーの役割は、MS コンポーネントと WDI IHV ドライバーの間で分割されます。 Microsoft WLAN コンポーネントは、すべての Wi-fi ミニポートに適用される NDIS 要件を処理します。これにより、すべての IHV がすべての動作を再実行する必要がなくなります。 WDI IHV ミニポートに適用される場合、ネイティブ WLAN IHV ミニポートの NDIS ハンドラーに対するとの動作の変更について以下に説明します。

-   [ドライバーのインストール](#driver-installation)
-   [DriverEntry](#driverentry)
-   [MiniportSetOptions](#miniportsetoptions)
-   [MiniportInitializeEx](#miniportinitializeex)
-   [ミニ Porthaltex](#miniporthaltex)
-   [MiniportDriverUnload](#miniportdriverunload)
-   [MiniportPause](#miniportpause)
-   [MiniportRestart](#miniportrestart)
-   [MiniportResetEx](#miniportresetex)
-   [MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)
-   [MiniportShutdownEx](#miniportshutdownex)
-   [MiniportOidRequest](#miniportoidrequest)
-   [MiniportCancelOidRequest](#miniportcanceloidrequest)
-   [NdisMIndicateStatusEx](#ndismindicatestatusex)
-   [MiniportDirectOidRequest](#miniportdirectoidrequest)
-   [Miniportcancelt Toidrequest](#miniportcanceldirectoidrequest)
-   [MiniportSendNetBufferLists](#miniportsendnetbufferlists)
-   [MiniportCancelSend](#miniportcancelsend)
-   [MiniportReturnNetBufferLists](#miniportreturnnetbufferlists)
-   [WDI handler: MiniportWdiOpenAdapter](#wdi-handler-miniportwdiopenadapter)
-   [WDI handler: MiniportWdiCloseAdapter](#wdi-handler-miniportwdicloseadapter)

## <a name="driver-installation"></a>ドライバーのインストール


WDI IHV ミニポートドライバーをシステムに読み込んでインストールする方法に変更はありません。 INF とインストールのプロセスは、IHV ネイティブ WLAN ミニポートドライバーの処理と似ています。 既存の NDIS ドライバーと同様に、ihv の WLAN アダプターを使用するために IHV ドライバーを読み込む必要がある場合、オペレーティングシステムは IHV ミニポートドライバーの DriverEntry ルーチンを呼び出します。

## <a name="driverentry"></a>DriverEntry


オペレーティングシステムは、WDI IHV ミニポートドライバーの DriverEntry ルーチンを直接呼び出します。 IHV ミニポートは、通常の NDIS ミニポートの DriverEntry ルーチンのガイドラインの大部分に従います。 1つの例外として、 [**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出す代わりに、IHV ミニポートは[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)を呼び出して、Microsoft WLAN コンポーネントを有効にするようにオペレーティングシステムに指示します。

[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)の主なパラメーターを次に示します。

-   [**Ndis\_ミニポート\_ドライバー\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics): これは、ネイティブの wi-fi ミニポートが ndis に登録するために使用する元の ndis 構造です。 WDI モデルでは、ほとんどのハンドラーパラメーターは省略可能です。 必須のハンドラーは、**ミニポート\_OID\_要求\_ハンドラー** 、および**ミニポート\_ドライバー\_アンロード**です。 WDI メッセージを IHV ドライバーに渡すために、**ミニポート\_OID\_要求\_ハンドラー**が使用されます。 他のハンドラーが指定されている場合、通常、Microsoft WLAN コンポーネントはハンドラーに対して独自の処理を実行した後にハンドラーを呼び出します。
-   [**NDIS\_ミニポート\_ドライバー\_WDI\_の特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics): これは、WDI ミニポートドライバーが実装する必要がある新しいハンドラーのセットです。 これは、IHV ドライバーによって使用され、コントロールパス用の追加のハンドラーと、データパスのすべてのハンドラーのセットを登録します。

IHV ミニポートが NdisMRegisterWdiMiniportDriver を呼び出すと、Microsoft WLAN コンポーネントによって、 [**ndis\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)のハンドラーが更新され、Ndis の[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)が呼び出されます。 更新プログラムが実行されるので、Microsoft WLAN コンポーネントは、WDI IHV ミニポートドライバーに対する支援/単純化を提供できるハンドラーをインターセプトできます。

WDI IHV ミニポートドライバーの DriverEntry プロセスの一般的なフローを次に示します。

![wdi driverentry フロー](images/wdi-driverentry-flow.png)

DriverEntry の詳細については、「 [**driverentry OF NDIS ミニポートドライバー**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)」を参照してください。

## <a name="miniportsetoptions"></a>MiniportSetOptions


上記の DriverEntry ダイアグラムに示されているように、WDI IHV ミニポートで[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)ハンドラーが登録されている場合、オペレーティングシステムは[**NdisMRegisterWdiMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nf-dot11wdi-ndismregisterwdiminiportdriver)を呼び出すミニポートドライバーのコンテキストでその機能を呼び出します。

IHV ミニポートドライバーが[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)を使用してオプションハンドラーを登録した場合、Microsoft コンポーネントによって、これらのハンドラーが WDI レイヤーを介してシリアル化されない可能性があります。 そのため、IHV コンポーネントは、これらのハンドラーの同期要件を処理する役割を担います。

## <a name="miniportinitializeex"></a>MiniportInitializeEx


WDI モデルは、 [*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)の動作を複数の WDI インターフェイス呼び出しに分割します。

1.  [*Miniportwdiallocateadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)を呼び出します。

    オペレーティングシステムが IHV ハードウェアのインスタンスを検出すると、WDI IHV ミニポートドライバーへの最初の呼び出しになります。 この呼び出しで、WDI ミニポートは、デバイスのソフトウェア表現 (**Miniportadaptercontext**) を作成するために必要なアクションを実行します。 また、デバイスに関する情報を確認して、 [**NDIS\_ミニポート\_アダプター\_登録\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)構造に入力します。 デバイスと Wi-fi スタックの実際の初期化は、Microsoft コンポーネントが特定の初期化を実行するために WDI コマンドを送信するときに、後で実行されます。

    Microsoft コンポーネントは、WDI IHV ミニポートドライバーから取得したデータを使用して[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、NDIS [ **\_ミニポート\_アダプター\_登録\_の属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_registration_attributes)を ndis に設定します。 **NDIS\_ミニポート\_アダプター\_登録\_属性**のほとんどのフィールドには、Microsoft コンポーネントによって既定値が設定されます。 IHV ドライバーは、 **Miniportadaptercontext**フィールドと**InterfaceType**フィールドに入力する必要があります。

    この呼び出しが IHV ミニポートドライバーから戻ると、[*ミニ Portoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)ハンドラー経由で WDI コマンドの受信が開始されます。 この呼び出しの間に、Microsoft コンポーネントがリセット/回復操作を実行できない可能性があるため、ここで実行されるすべてのアクティビティを迅速かつ信頼性の高いものにする必要があります。

2.  [*Miniportwdiopenadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)を呼び出します。

    [*ミニ Portwdiallocateadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)の後、Microsoft コンポーネントは[*Miniportwdiopenadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)を呼び出して、ファームウェアを読み込み、ハードウェアを初期化します。

3.  [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)を使用する複数の WDI コマンド。

    [*Miniportwdiopenadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)の後、Microsoft コンポーネントは、次のタスク/プロパティ/呼び出しを IHV ミニポートに送信します。

    1.  [*MiniportWdiTalTxRxInitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_initialize)を呼び出して、データパスと交換ハンドラーを初期化します。
    2.  OID\_WDI を呼び出して、アダプターの機能を取得する[\_アダプターの\_機能を取得\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)ます。
    3.  [OID\_WDI を呼び出して\_アダプター\_構成を設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration)し、アダプターを構成\_ます。
    4.  [OID\_WDI\_タスク\_\_設定](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-set-radio-state)して、必要な状態にない場合は、ラジオ\_の初期状態を設定します。
    5.  [*MiniportWdiTalTxRxStart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_start)を呼び出して、データパスを設定します。
    6.  [OID\_WDI\_タスク\_作成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)し、初期ポートを作成するための\_ポートを作成します。

    その他のコマンドは、Microsoft コンポーネントの MiniportInitializeEx 処理の一部として、IHV コンポーネントに送信されることもあります。 ただし、 [*MiniportWdiStartOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_start_adapter_operation)が呼び出されるまで、Microsoft コンポーネントは無線通信を必要とするタスクを送信しません。 [OID\_WDI\_タスク\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-open)最初に常に送信されている場合を除き、他のコマンド/呼び出しの順序が変わる可能性があります。

    Microsoft コンポーネントは、WDI IHV ミニポートドライバーから取得したデータを使用して[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出し、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)および[**ndis\_ミニポートを設定します。\_アダプター\_ネイティブ\_802\_11\_** ](https://docs.microsoft.com/previous-versions/windows/hardware/wireless/ff565926(v=vs.85)) NDIS の属性です。

4.  [*MiniportWdiStartOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_start_adapter_operation)を呼び出します。

    これは、 [**NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)に含まれるオプションの WDI ミニポートハンドラーであり、IHV ドライバーは追加の MiniportInitializeEx タスクを実行するために使用できます。 また、IHV ミニポートは、Microsoft コンポーネントがミニポートの初期化を完了したことを示すヒントとして使用することもできます。また、ミニポートは必要なバックグラウンドアクティビティを開始できます。

    次の図は、MiniportInitializeEx のフローを示しています。

    ![wdi ミニポート初期化フロー](images/wdi-miniport-initialization-flow.png)

    中間操作が失敗した場合は、Microsoft コンポーネントによって前の操作が元に戻され、ミニポートの表示が失敗します。 たとえば、 [oid\_WDI\_タスク\_作成\_ポート](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-create-port)に障害が発生した場合、データパスはクリーンアップされ、 [OID\_WDI\_タスク\_CLOSE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-close)が送信され、ミニポートは失敗します。

## <a name="miniporthaltex"></a>ミニ Porthaltex


ネイティブ Wi-fi ミニポートでは、ミニアドオンを使用し[*て、操作*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)を停止し、アダプターインスタンスをクリーンアップするようにミニポートに指示します。 WDI モデルでは、Microsoft コンポーネントが元の*Miniporthaltex*呼び出しを処理し、複数の WDI インターフェイス呼び出しに分割します。

1.  [*MiniportWdiStopOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_stop_adapter_operation)を呼び出します。

    これは、 [*MiniportWdiStartOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_start_adapter_operation)で実行された操作を IHV ドライバーが元に戻すために使用できる、 [**NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)内のオプションの WDI ミニポートハンドラーです。

2.  [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)を使用する複数の WDI コマンド。

    [*MiniportWdiStopOperation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_stop_adapter_operation)の後、Microsoft コンポーネントは、ihv ドライバーの現在の状態をクリーンアップするために、タスク/プロパティを ihv ミニポートに送信します。 このクリーンアップには、次のものが含まれる場合があります。

    1.  [Oid\_WDI\_タスク\_切断](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-disconnect)/[oid\_WDI\_タスクを停止\_AP を停止](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-stop-ap)して既存の接続を破棄します。
    2.  [OID\_WDI\_タスク\_削除\_ポートを削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-delete-port)して、作成されたすべてのポートを削除します。
    3.  [*MiniportWdiTalTxRxStop*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_stop)を呼び出して、データパスを停止します。
    4.  [*MiniportWdiTalTxRxDeinitialize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tal_txrx_deinitialize)を呼び出して、データパスを deinitialize します。
    5.  を呼び出して、ハードウェアの状態をクリーンアップします。 これは、IHV ドライバーによって登録された[*Miniportwdicloseadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_close_adapter)を使用して ihv に送信されます。

3.  上記のすべてのコマンドが呼び出されると、Microsoft コンポーネントは[*Miniportwdifreeadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_free_adapter)を呼び出して、必要なソフトウェアの状態を IHV ドライバーが削除できるようにします。

次の図は、MiniportHaltEx のフローを示しています。

![wdi ミニポート停止フロー](images/wdi-miniport-halt-flow.png)

デバイスが突然削除された場合、またはシステムの電源がオフになっている場合、ミニ Porthaltex 処理は実行されません。 突然の削除については、 [MiniportDevicePnPEventNotify](#miniportdevicepnpeventnotify)ハンドラーの動作を参照してください。 システムのシャットダウンについては、「 [Miniportshutdownex](#miniportshutdownex)ハンドラーの動作」を参照してください。

## <a name="miniportdriverunload"></a>MiniportDriverUnload


[*Miniportdriverunload*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_unload)は、WDI IHV ミニポートがアンロードされる前に呼び出されるハンドラーです。 WDI IHV ミニポートドライバーは、Microsoft コンポーネントを呼び出して、自身の登録を解除します。 Microsoft コンポーネントは[**NdisMDeregisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismderegisterminiportdriver)を呼び出します。

次の図は、MiniportDriverUnload のフローを示しています。

![wdi ミニポートドライバーのアンロードフロー](images/wdi-miniport-driver-unload-flow.png)

## <a name="miniportpause"></a>MiniportPause


NDIS [*Miniportpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_pause)の要件は、Microsoft コンポーネントによって処理されます。 MiniportPause の一部として、Microsoft コンポーネントはデータパスを停止し、クリーンアップを待機します。 WDI IHV ミニポートは、必要に応じて、データパスのクリーンアップが完了した後に Microsoft コンポーネントによって呼び出される[*Miniportwdipostadapterpause*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_post_adapter_pause)コールバックに登録できます。

次の図は、MiniportPause のフローを示しています。

![wdi ミニポートの一時停止フロー](images/wdi-miniport-pause-flow.png)

## <a name="miniportrestart"></a>MiniportRestart


NDIS [*Miniportrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart)の要件は、Microsoft コンポーネントによって処理されます。 MiniportRestart の一部として、Microsoft コンポーネントは Miniportrestart の一部として実行されたデータパスの一時停止作業を元に戻します。 WDI IHV ミニポートは、必要に応じて、データパスの再起動が完了した後に Microsoft コンポーネントによって呼び出される[*Miniportwdipostadapterrestart*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_post_adapter_restart)コールバックに登録できます。

次の図は、MiniportRestart のフローを示しています。

![wdi ミニポートの再起動フロー](images/wdi-miniport-restart-flow.png)

## <a name="miniportresetex"></a>MiniportResetEx


[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)は、Microsoft コンポーネントによって処理されません。 WDI IHV ミニポートは、必要に応じて、Microsoft コンポーネントによって呼び出される*Miniportresetex*コールバックに登録できます。

## <a name="miniportdevicepnpeventnotify"></a>MiniportDevicePnPEventNotify


[*MiniportDevicePnPEventNotify*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_device_pnp_event_notify)は、デバイスの突然の削除などの PNP イベントを NDIS ドライバーに通知するために使用されます。 NDIS がこの通知を送信すると、まず、処理のために WDI IHV ミニポートに転送されます。 IHV コンポーネントの処理が完了すると、Microsoft コンポーネントはこのイベントに対して適切な処理を実行します。 IHV コンポーネントに転送される呼び出しは、他のタスクやコールバックと共にシリアル化されません。

次の図は、MiniportDevicePnPEventNotify のフローを示しています。

![wdi ミニポートドライブの pnp 通知フロー](images/wdi-miniport-device-pnp-notification-flow.png)

## <a name="miniportshutdownex"></a>MiniportShutdownEx


[*Miniportshutdownex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_shutdown)は、システムシャットダウンイベントについて NDIS ドライバーに通知するために使用されます。 NDIS がこの通知を送信すると、まず Microsoft コンポーネントによって処理されます。 Microsoft コンポーネントの処理が完了すると、イベントが処理のために WDI IHV ミニポートに渡されます。

次の図は、MiniportShutdownEx のフローを示しています。

![wdi ミニポートのシャットダウンフロー](images/wdi-miniport-shutdown-flow.png)

## <a name="miniportoidrequest"></a>MiniportOidRequest


[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)ハンドラーは、WDI IHV ミニポートで実装する必要がある必須のハンドラーです。 これは、WDI コマンドを IHV ミニポートに送信するために Microsoft コンポーネントによって使用されます。 また、Microsoft コンポーネントが IHV ミニポートに対して処理しない Oid を転送するためにも使用されます。

WDI IHV ミニポートへの[*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)呼び出しは、WDI コマンドの M1 メッセージとして考慮する必要があります。 OID の完了 ( [**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)を介して、または*Miniportoidrequest*からの非保留を返す) は、WDI Task/command の M3 メッセージと見なす必要があります。

WDI のすべてのコマンドには、次の2つのフィールドがあります。このフィールドには、NDIS\_状態コードを操作のために返すことができます。これには、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)呼び出し (または[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)) からのステータスコード、および WDI の状態コードを指定し[ **\_MESSAGE\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)フィールド (OID 入力候補または[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)経由)。 Microsoft コンポーネントは、 **WDI\_MESSAGE\_HEADERStatus**フィールドを確認する前に、常に、OID の\_状態を OID の完了から調べます。 WDI OID 処理のための IHV コンポーネントの期待は次のとおりです。

1.  WDI Oid は、 [**NDIS\_oid\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)**RequestType**を使用して IHV コンポーネントに送信さ**れ、それ**に対応するメッセージとメッセージ長がデータに含まれ**ます。メソッド\_情報。 InformationBuffer**と**DATA。メソッド\_情報。InputBufferLength**フィールドそれぞれ。
2.  コマンドの処理中にエラーが発生した場合、IHV コンポーネントは OID の完了時にエラーを報告します。 Wi-fi レベルの障害が発生している場合は、 [**WDI\_MESSAGE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)の Status フィールドを no success に設定します。
3.  タスクとプロパティの場合、要求のポート番号は、 [**WDI\_MESSAGE\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)**ポート id**フィールドにあります。 [**NDIS\_OID\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)の**ポート**番号は、常に0に設定されます。
4.  OID を完成させるには、 [*Miniportoidrequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)が NDIS\_STATUS\_を返し、後で[**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)を使用して (同期または非同期に) oid を完了することが許容されます。
5.  IHV コンポーネントが NDIS\_STATUS\_SUCCESS の OID を完了した場合、 [**WDI\_MESSAGE\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)の領域を含む、oid 要求の**byteswritten**れたフィールドに適切なバイト数を設定する必要があります.
6.  IHV コンポーネントのデータに十分な領域がない場合 **。メソッド\_情報。OutputBufferLength**フィールドは、応答を埋めるために、NDIS\_STATUS の OID を完了し\_バッファー\_短\_すぎてデータを設定し**ます。メソッド\_情報。BytesNeeded**フィールドです。 Microsoft コンポーネントが、要求されたサイズのバッファーを割り当てて、新しい要求を IHV に送信しようとする場合があります。
7.  タスクの場合、タスクの M4 ([**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)) は、タスクが正常に開始したと報告された場合にのみ指定する必要があります--oid の完了が成功し、 [**WDI\_MESSAGE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_message_header)の**状態**が oid で表示されます。完了は成功しました。

次の図は、単一の WDI コマンドにマップされる NDIS OID 要求の例を示しています。 OID 要求がオペレーティングシステムによって送信されると、Microsoft コンポーネントはそれを WDI OID 要求に変換し、WDI OID 要求を IHV ミニポートに送信します。 IHV ミニポートが OID を完了すると、Microsoft コンポーネントが元の OID 要求を適切に完了します。

![single wdi コマンドの wdi ミニポート oid 要求シーケンス](images/wdi-miniport-oid-request-single.png)

WDI が複数の OidRequests にマップされ、いずれかの WDI 要求が失敗した場合、Aloidrequest も失敗します。 中間操作のサブセットが既に完了している場合、Microsoft コンポーネントはクリーンアップをサポートする操作を元に戻しようとします。

次の図は、Microsoft コンポーネントによって処理された NDIS OID 要求の例を示しています。 OID 要求がオペレーティングシステムによって送信されると、Microsoft コンポーネントは OID を処理して完了します。 この OID は、WDI IHV ミニポートに渡されません。

![microsoft コンポーネントによって処理される oid の wdi ミニポート oid 要求シーケンス](images/wdi-miniport-oid-request-wdi-handled.png)

Microsoft コンポーネントによって認識されない Oid は、処理のために IHV コンポーネントに直接転送されます。

![wdi microsoft コンポーネントによって処理されない oid のミニポート oid の要求シーケンス](images/wdi-miniport-oid-request-unknown.png)

WDI IHV ミニポートドライバーでは、MiniportOidRequest の動作は変更されていません (ネイティブ Wi-fi ミニポートと比較)。 呼び出しはシリアル化され、IHV ミニポートは、 [**NdisMOidRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismoidrequestcomplete)の呼び出しを使用して同期的または非同期的に完了できます。

## <a name="miniportcanceloidrequest"></a>MiniportCancelOidRequest


これは、WDI メッセージにマップされていない Oid を処理する必要がある WDI IHV ミニポートによって使用される省略可能なハンドラーです。 このハンドラーは、どの WDI Oid にも使用されません。 WDI Oid は迅速に完了する必要があります。また、IHV ミニポートドライバーが保留中の OID をキャンセルしようとする必要はありません。 WDI タスクの取り消しは、適切な cancel task OID 要求を使用して処理されます。 マップされていない Oid の場合、想定される動作は NDIS によって定義されます。

## <a name="ndismindicatestatusex"></a>NdisMIndicateStatusEx


[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)は、WDI IHV ミニポートが Microsoft コンポーネントに通知を送信するために使用されます。 この表示には、TKIP MIC の故障などの非要請の兆候や、タスクの完了 (M4) に関する要請された表示などがあります。

次の図は、対応する NDIS/ネイティブ Wi-fi を示す WDI の例を示しています。 指示が IHV ミニポートによって Microsoft コンポーネントに送信されると、Microsoft コンポーネントはそれを既存の指示に変換し、オペレーティングシステムに転送します。

![wdi ミニポートの状態を示すフロー](images/wdi-miniport-status-indication-flow.png)

次の図は、対応する NDIS/ネイティブ Wi-fi を示していない WDI を示す例を示しています。 これは、Microsoft コンポーネントによって処理されます。

![wdi ndis に直接マッピングされることがない状態を示す](images/wdi-miniport-status-indication-not-ndis.png)

次の図は、Microsoft コンポーネントによって認識されないことを示しています。 この通知は、オペレーティングシステムにそのように転送されます。

![wdi microsoft コンポーネントによって認識されない状態を示す](images/wdi-miniport-status-indication-unknown.png)

NdisMIndicateStatusEx の動作は、WDI IHV ミニポートドライバーでは変更されません (ネイティブ Wi-fi ミニポートと比較)。

## <a name="miniportdirectoidrequest"></a>MiniportDirectOidRequest


これは、WDI メッセージにマップされていない直接の Oid を処理する必要がある場合に、WDI IHV ミニポートドライバーによって登録される省略可能なハンドラーです。 Wi-fi Direct 用の既存の直接 Oid はすべて WDI メッセージにマップされるため、このハンドラーはその機能をサポートするためには必要ありません。 サポートされていない直接 Oid は、Microsoft コンポーネントによってシリアル化されません。

## <a name="miniportcanceldirectoidrequest"></a>Miniportcancelt Toidrequest


これは、WDI メッセージにマップされていない直接の Oid を処理する必要がある WDI IHV ミニポートによって使用される省略可能なハンドラーです。 マップされていない Oid の場合、想定される動作は NDIS によって定義されます。

## <a name="miniportsendnetbufferlists"></a>MiniportSendNetBufferLists


このハンドラーは、WDI IHV ミニポートドライバーでは使用されないため、指定しないでください。 Microsoft コンポーネントでは、 [**NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)によって登録されたデータパスハンドラーを使用して、送信パケットを IHV ミニポートに送信します。

## <a name="miniportcancelsend"></a>MiniportCancelSend


このハンドラーは、WDI IHV ミニポートドライバーでは使用されないため、指定しないでください。

## <a name="miniportreturnnetbufferlists"></a>MiniportReturnNetBufferLists


このハンドラーは、WDI IHV ミニポートドライバーでは使用されないため、指定しないでください。 Microsoft コンポーネントは、 [**NDIS\_ミニポート\_ドライバー\_WDI\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_miniport_driver_wdi_characteristics)によって登録されたデータパスハンドラーを使用して、受信したパケットを IHV ミニポートに返します。

## <a name="wdi-handler-miniportwdiopenadapter"></a>WDI handler: MiniportWdiOpenAdapter


[*Miniportwdiopenadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_open_adapter)ハンドラーは、IHV ドライバーで Open Task 操作を開始するために Microsoft コンポーネントによって使用されます。 この呼び出しは迅速に完了する必要があります。また、オープン操作が正常に開始された場合、IHV は、この呼び出しで NDIS\_STATUS\_SUCCESS を返し、Ndis\_WDI に渡される[**Openadaptercomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_open_adapter_complete)ハンドラーを呼び出す必要があり[ **\_INIT\_PARAMETERS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters)パラメーターを[*Miniportwdiallocateadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)に指定します。

## <a name="wdi-handler-miniportwdicloseadapter"></a>WDI handler: MiniportWdiCloseAdapter


[*Miniportwdicloseadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_close_adapter)ハンドラーは、IHV ドライバーでタスクの終了操作を開始するために Microsoft コンポーネントによって使用されます。 この呼び出しは迅速に完了する必要があります。また、オープン操作が正常に開始された場合、IHV は、この呼び出しで NDIS\_STATUS\_SUCCESS を返し、Ndis\_WDI に渡される[**Closeadaptercomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_close_adapter_complete)ハンドラーを呼び出す必要があり[ **@no_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_ndis_wdi_init_parameters) [*Miniportwdiallocateadapter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_allocate_adapter)の _T_7_ INIT\_PARAMETERS パラメーター

 

 





