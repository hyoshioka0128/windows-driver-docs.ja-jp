---
Description: 関数コントローラークライアントドライバーが USB 関数コントローラー拡張機能 (UFX) と対話するときに実行するさまざまなタスクについて説明します。
title: 関数コントローラークライアントドライバーを記述する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 240cbb5aa16c88545795fac8d1488729af3451b2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845003"
---
# <a name="write-a-function-controller-client-driver"></a>関数コントローラークライアントドライバーを記述する


**要約**

-   関数コントローラークライアントドライバーの予期される動作について説明します。

**適用対象**

-   Windows 10
-   USB デバイス用のコントローラードライバーを記述するドライバー開発者

**重要な API**

-   [USB 関数コントローラークライアントドライバーリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#usb-function-controller-client-driver-reference)


関数コントローラークライアントドライバーが USB 関数コントローラー拡張機能 (UFX) と対話するときに実行するさまざまなタスクについて説明します。 UFX とクライアントドライバーは、export メソッドとイベントコールバック関数を使用して相互に通信します。 エクスポートメソッド ( **Ufxdevicexxx**または**Ufxendpointxxx**) は、ufx によってエクスポートされ、クライアントドライバーによって呼び出されます。 コールバック関数 ( *.evt\_ufx\_Xxx*) は、クライアントドライバーで実装され、ufx によって呼び出されます。

UFX は、すべてのクライアントドライバーのコールバック関数を非同期的に呼び出し、オブジェクトごとに一度に1つのコールバックを呼び出します。 たとえば、USB デバイスオブジェクトと3つのエンドポイントオブジェクトがあるとします。 最大4つのコールバック関数 (1 つはデバイス用、もう1つはエンドポイントごとに1つ) は、一度に呼び出すことができます。 コールバックメソッドごとに、UFX はクライアントドライバーが[**Ufxdeviceeventcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)を呼び出して、ドライバーが要求を完了したことを示すまで待機します。 UFX がこれらのエクスポートを待機しているときにリッスンするその他のエクスポートメソッドは[**UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)です。 多くのクライアントコールバック関数は省略可能です。 必要な関数は次のとおりです。

-   [ *.EVT\_UFX\_デバイス\_既定の\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)
-   [ *.EVT\_UFX\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)
-   [ *.EVT\_UFX\_デバイス\_ホスト\_接続*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)
-   [ *.EVT\_UFX\_デバイス\_ホスト\_切断*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)
-   [ *.EVT\_UFX\_デバイス\_アドレス指定される*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)

## <a name="initialization"></a>初期化


1.  関数コントローラークライアントドライバーは、Windows Driver Foundation (WDF) が[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックのクライアントドライバーの実装を呼び出すときに、初期化プロセスを開始します。 この実装では、クライアントドライバーは[**Ufxfdoinit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxfdoinit)を呼び出し、 [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出すことによってデバイスオブジェクトを作成する必要があります。
2.  クライアントドライバーは[**UfxDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate)を呼び出して、USB デバイスオブジェクトを作成し、ufxdevice ハンドルを取得します。
3.  クライアントドライバーは[**UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready)を呼び出して、クライアントドライバーのコールバック関数を呼び出すことができることを ufx に示します。
4.  UFX は、次のような初期化タスクを実行します。
    -   UFX は、クライアントドライバーの[ *.evt\_ufx\_デバイス\_既定の\_エンド\_ポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)を呼び出し、実装を追加して既定のエンドポイントを作成します。
    -   UFX は、デバイスでサポートされているインターフェイスの子物理デバイスオブジェクト (PDOs) を作成します。
    -   UFX は、デバイスクラスドライバーのアクティブ化を送信するときに\_、デバイスクラスのドライバーのアクティブ化を待機します。このとき、 [ **\_USB\_バス要求をアクティブ化\_、内部\_USBFN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus)ます。 また、デバイスが接続されていることを示す[**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)がクライアントドライバーによって呼び出されるのを待ちます。

## <a name="class-driver-notification"></a>クラスドライバーの通知


セットアップパケットとバスの状態が通知されるようにするには、クラスドライバーが[ **\_USB\_バス要求をアクティブ化\_ための内部\_USBFN\_IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus)を送信する必要があります。 UFX は、これらの要求をクラスドライバー固有の通知キューにキューに入れます。 クライアントドライバーからのバスイベントに関する通知を受信すると、UFX は適切な各キューから pop を受け取り、要求を完了します。 クラスドライバーが通知を使用しないようにするために、UFX はクラスドライバーの通知の固定サイズのキューを保持します。

## <a name="device-attach-and-detach-events"></a>デバイスのアタッチイベントとデタッチイベント


UFX は、関数コントローラークライアントドライバーが[**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)を呼び出すまで、デバイスがデタッチされることを前提としています。

その後、UFX は、USB 仕様で定義されているとおりにデバイスの状態を "**電力**" に設定します。 クライアントドライバーに状態の変更を通知するために、UFX はクライアントドライバーの[ *.evt\_ufx\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)の実装を呼び出します。

デバイスの充電を支援するために、UFX によってチャージャードライバー (Cad) に通知されます。 また、以前にクラスドライバーによって送信された通知要求の[**内部\_USBFN\_BUS\_\_EVENT\_IOCTL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)を完了することで、クラスドライバーに通知します。

バスが切断されると、クライアントドライバーは[**UfxDeviceNotifyDetach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifydetach)を呼び出す必要があります。 クライアントは、 [**UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyattach)を呼び出すたびに、detach を1回だけ呼び出す必要があります。 **UfxDeviceNotifyDetach**の呼び出しの後、Ufx は[ *.evt\_UFX\_デバイス\_ホスト\_切断*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)(これがインターフェイスの変更でない場合) を呼び出します。 次に、すべてのエンドポイントキューの削除や、既定のエンドポイントキューの開始など、すべてのクリーンアップタスクを続行します。 UFX は、 [ *\_ufx\_デバイス\_USB\_状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)を呼び出します。 [**IOCTL\_内部\_USBFN\_BUS\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)を完了して、クラスドライバーに通知します。要求.

**ハードウェア障害**

ハードウェアエラーが発生した場合、クライアントドライバーは[**UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)を呼び出す必要があります。 応答として、UFX はデバイススタックを破棄し、クライアントドライバーの[ *.evt\_ufx\_デバイス\_コントローラー\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_controller_reset)することによって、この状況から回復しようとすることがあります。 クライアントはコントローラーを初期状態にリセットする必要があります。 別のハードウェア障害が発生した場合、クライアントは UfxDeviceNotifyHardwareFailure を再度呼び出す必要があります。 2回目の呼び出しでは、UFX によってその状態とバグチェックが記録されます。

## <a name="port-detection"></a>ポートの検出


ポートの検出は、UFX によって実行されます。 このメソッドは、関数コントローラークライアントドライバーの[ *.evt\_UFX\_デバイス\_ポート*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_detect)を呼び出して、コールバック関数を検出\_、デバイスが接続されているポートの種類を特定します。 クライアントは、 [**Usbfn\_port\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_port_type)に定義されているポートの種類のいずれかを使用して、 [**ufxdeviceportの完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceportdetectcomplete)または[**Ufxdeviceport検出の completeex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceportdetectcompleteex)を呼び出して応答します。

クライアントがポートの種類を特定できない場合、クライアントは**UsbfnUnknownPort**を報告する必要があります。 ポートが不明またはダウンストリームポートの場合、UFX はクライアントドライバーの[ *.evt\_ufx\_デバイス\_ホスト\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)関数を呼び出します。 UFX は、しばらくの間バスをリッスンします。 ポートが不明であるにもかかわらず、セットアップパケットなどのトラフィックがある場合、UFX は**UsbfnStandardDownstreamPort**を想定します。 それ以外の場合は、UFX によってポートが**UsbfnInvalidDedicatedChargingPort**に割り当てられます。 ポートの種類が特定されたら、UFX によって、クライアントドライバーの[ *.evt\_ufx\_デバイス\_ポート\_CHANGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)関数が呼び出されます。 関数では、クライアントドライバーは、UFX ポートの種類に一致するようにハードウェアの状態を変更することを想定しています。

## <a name="endpoint-creation"></a>エンドポイントの作成


UFX は、ホストから送信されたセットアップパケットを処理できるように、クライアントドライバーの[ *.evt\_ufx\_デバイス\_既定の\_エンドポイント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)を呼び出すことによって、既定のエンドポイント (エンドポイント 0) を作成します。 UFX は、 [ *.evt\_ufx\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)を呼び出すことによって、他のエンドポイントを作成します。 UFX は、クライアントドライバーが[**UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready)を呼び出した後にのみ、エンドポイントを作成します。 これらのコールバック関数では、クライアントドライバーは、エンドポイントオブジェクトに対して[**Ufxendpointcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate)を呼び出し、その ufxendpoint ハンドルを取得する必要があります。 UFX は、エンドポイントが属するインターフェイスに関連付けられているクラスドライバー PDO に親を設定します。 既定のエンドポイントの親は、USB デバイスオブジェクトです。 エンドポイントには、転送キューとコマンドキューという2つのフレームワークキューオブジェクトが含まれています。これには、デバイスが構成された状態にある場合にのみアクセスできます (エンドポイント0は除きます。これは、UFX が .Evt\_UFX を呼び出した後にアクセスできます) [ *\_デバイス\_ホスト\_接続*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect))。

-   **コマンドキュー要求**
-   [**IOCTL\_内部\_USBFN\_\_パイプ\_状態の取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_get_pipe_state)
-   [**IOCTL\_内部\_USBFN\_\_パイプ\_状態の設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)
-   [**IOCTL\_内部\_USBFN\_記述子\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)
-   **キュー要求の転送**
-   [**IOCTL\_内部\_USBFN\_転送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)
-   [**IOCTL\_内部\_USBFN\_転送\_\_ゼロ\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)
-   [**IOCTL\_内部\_USBFN\_転送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)
-   [**IOCTL\_内部\_USBFN\_コントロール\_ステータス\_ハンドシェイク\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)
-   [**IOCTL\_内部\_USBFN\_コントロール\_ステータス\_ハンドシェイク\_出力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)

## <a name="device-enumeration"></a>デバイス列挙型


UFX がドライバーの[ *.evt\_ufx\_デバイス\_ホスト\_接続*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)を呼び出す前に、クライアントドライバーがホストへの接続を許可しないようにする必要があります。 クライアントドライバーが[**UfxDeviceNotifyReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyreset)を呼び出すと、デバイスの列挙が開始されます。 **既定**の状態では、ufx は標準のセットアップパケットを処理します。

**リセット**

UFX によってすべてのエンドポイントキューが削除され、 [ **\_内部\_USBFN\_記述子\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)要求がクライアントドライバーに送信され、エンドポイント0の**wMaxPacketSize**が更新されます。 UFX によって既定のエンドポイントのキューが開始され、状態が**既定値**に設定されます。

**標準**

UFX は、クライアントドライバーの[ *.evt\_ufx\_デバイス\_USB\_STATE\_CHANGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)関数を呼び出します。 また、状態のクラスドライバーにも通知します。 UFX は、SET\_ADDRESS standard セットアップパケットを受信した後、状態を**アドレス指定**に設定します。

**実現**

UFX は、クライアントドライバーの[ *.evt\_ufx\_デバイス\_アドレス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)指定関数を呼び出して、クライアントに使用するアドレスを指示します。 -アドレスが0の場合、UFX は状態を**既定値**に設定し、 [ *.evt\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)を呼び出して、クラスドライバーに通知します。 SET\_CONFIGURATION standard セットアップパケットを受信すると、UFX によって状態が "**構成済み**" に設定されます。

**て**

選択した構成が0の場合、UFX によってインターフェイスエンドポイントが削除され、状態が "**アドレス**指定済み" に設定されます。 UFX は[ **\_内部\_USBFN\_記述子\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)要求をクライアントドライバーに送信して、インターフェイスエンドポイントの**wMaxPacketSize**を更新します。 UFX は、すべてのインターフェイスエンドポイントキューが削除され、インターフェイスエンドポイントキューが開始されたことを確認します。 ポートの種類が**UsbfnStandardDownstreamPort**または**UsbfnChargingDownstreamPort**でない場合、ufx はポートの種類を UsbfnStandardDownstreamPort に変更し、に通知します。クライアントドライバーは、 [ *.evt\_ufx\_デバイス\_ポート\_CHANGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)および[ *.evt\_UFX\_デバイス\_USB\_状態を変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)して状態を更新します。構成された状態のクラスドライバー。

## <a name="standard-control-transfers"></a>標準コントロール転送


UFX は、既定のエンドポイントでのコントロールの転送を、既定のエンドポイントを呼び出した後、いつでも処理できます。[*デバイス\_既定の\_エンド\_ポイントを呼び\_\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)出すと、クライアントドライバーはを使用して既定のエンドポイントを作成します。 すべての制御転送は、8バイトのセットアップパケットで開始されます。 セットアップパケットをホストに送信するには、クライアントドライバーで[**Ufxendpointnotifysetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointnotifysetup)を呼び出す必要があります。 標準コントロールの転送は、UFX によって完了します。 コントロール転送に関連付けられているデータがある場合、UFX は、必要に応じて既定のコントロールエンドポイントを読み取り、書き込みます。

## <a name="non-standard-control-transfers"></a>非標準のコントロール転送


UFX が制御転送を処理できない場合、転送は、[**内部\_USBFN\_BUS\_イベント\_通知要求の IOCTL\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)完了することによって、適切なクラスドライバーに転送されます。 エンドポイント記述子にコントロールエンドポイントとして定義されている任意のエンドポイントで、制御転送を行うことができます。 既定のコントロールエンドポイント以外のエンドポイントでの制御転送は、常に非標準のコントロール転送です。 コントロールエンドポイントが既定のコントロールエンドポイントである場合、UFX は、そのクラスドライバーのクラス要求としてマークされているセットアップパケットのクラスドライバーに通知します。 コントロールエンドポイントがインターフェイスに属している場合、UFX はそのインターフェイスに関連付けられているクラスドライバーに通知します。 必要に応じて、クラスドライバーはコントロールエンドポイントからの読み取りと書き込みを行う必要があります。

## <a name="data-transfers"></a>データ転送


データ転送はクラス\_ドライバーによって開始されます。そのためには、[**内部\_usbfn\_転送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)、 [**ioctl\_内部\_USBFN\_転送\_\_追加\_ゼロ @no__ t14_ PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)または[**IOCTL\_内部\_usbfn\_転送要求\_転送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)します。 これらの要求を検証した後、UFX はそれを適切なエンドポイントキューに転送して、クライアントドライバーによって処理されるようにします。 クライアントドライバーは、追加の検証を実行することが想定されています。 クライアントドライバーは、エンドポイントキューで転送要求を受信します。 クライアントドライバーは、バス使用率を最大化するために必要な数の要求をこのキューから取得できます。 クライアントドライバーは、正常に完了した要求を正常に完了する必要があります\_成功します。 ドライバーは、要求をキャンセルし、キャンセルされた場合に状態\_キャンセルされた要求を完了するために、ベストエフォートの試行を行う必要があります。 無効なパラメーターが渡された場合、クライアントドライバーは、状態\_無効な\_パラメーターを使用して要求を完了します。

**転送の制御**

制御転送は、8バイトのセットアップパケットで開始されます。 セットアップパケットをホストに送信するには、クライアントドライバーで[**Ufxendpointnotifysetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointnotifysetup)を呼び出す必要があります。 UFX は、通知要求を完了することによって、非標準のコントロール転送のクラスドライバーに通知します。 クライアントと UFX は両方とも IOCTL を使用して[ **\_内部\_usbfn\_転送\_で**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)は、 [**ioctl\_内部\_USBFN\_転送\_\_\_を追加\_0 PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)、または[**IOCTL\_内部\_USBFN\_転送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out) 、既定のコントロールエンドポイントへの読み取りと書き込みを行います。 ただし、インターフェイスでは、対応するクラスドライバーだけが使用できる他のコントロールエンドポイントを定義できます。 コントロールエンドポイントは、セットアップパケットに応答して停止することができます。 クラスドライバーは、 [**IOCTL\_内部\_USBFN\_設定\_パイプ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)要求を送信してエンドポイントを停止します。 ハードウェアまたはクライアントドライバーは、停止が送信された後、エンドポイントのトラフィックを直ちに再開することが予想されます。 コントロールエンドポイントは、以前のデータを使用せずに、長さが0のパケット (ZLP) を送受信することもできます。 クライアントドライバーと UFX は、Ioctl を使用してこれを行うことができます。そのためには、 [ **\_内部\_usbfn\_コントロール\_状態\_ハンドシェイク**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)\_[**内部\_usbfn\_コントロール\_状態\_t_14_ ハンドシェイク\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)ます。

**一括転送と割り込み転送**

一括転送はデータ配信を保証し、大量のデータを送信するために使用されます。 転送は、Ioctl を使用して一括エンドポイントで送信することができます。 [ **\_内部\_usbfn\_transfer\_で**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)は、 [**ioctl\_内部\_USBFN\_転送\_の\_\_を追加\_0、PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)、または[**IOCTL\_内部\_usbfn\_転送\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)します。 バルクエンドポイントは、IOCTL を使用したエンドポイントの制御と同様に停止できます。 [ **\_内部\_USBFN\_\_パイプの\_状態を設定**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)します。 クライアントドライバーは、すべてのホスト要求に応答し、IOCTL 要求を保持するために、ストールパケットを送信することが想定されています。 コントロールエンドポイントとは異なり、失速状態が明示的にクリアされるまで、停止した一括エンドポイントが停止したままになります。

割り込み転送の割り込み転送は一括転送に似ていますが、待機時間は保証されています。 割り込み転送には一括転送と同じインターフェイスがありますが、ストリーミング機能はありません。

**アイソクロナス転送**

クライアントドライバーは、このバージョンではアイソクロナス転送をサポートしていません。

## <a name="power-management"></a>電源管理


クライアントドライバーは、電源管理のすべての側面を所有します。 コールバック関数は非同期であるため、クライアントドライバーは適切な電源状態に戻り、要求を完了してから、 [**Ufxdeviceeventcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)などの適切なイベント完了エクスポート関数を呼び出す必要があります。

デバイスの状態 ( [**Usbfn\_device\_state**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_device_state)で定義) が**UsbfnDeviceStateSuspended**および**UsbfnDeviceStateAttached**で、ポートの種類がレポートされていない場合、ufx は動作中の状態になります。 または、UFX がポートの種類 ( [**Usbfn\_port\_type**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnbase/ne-usbfnbase-_usbfn_port_type)) **UsbfnStandardDownstreamPort**または**UsbfnChargingDownstreamPort**で定義されていることを報告しています。

UFX は、 [ *.evt\_ufx\_デバイス\_USB\_状態\_change*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)または[ *.evt\_UFX\_デバイス\_ポート\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)の実装を呼び出すことによって、動作状態を入力して終了します。 クライアントドライバーが[**Ufxdeviceeventcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)を呼び出すと、動作状態との間の切り替えが完了します。

動作中の状態では、UFX は任意のコールバックを呼び出すことができます。 動作状態ではありませんが、UFX は、[*デバイス\_USB\_\_状態を\_\_UFX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)を呼び出して、動作状態に移行します。[ *.Evt\_UFX\_デバイス\_リモート\_ウェイクアップ\_シグナル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal)で、中断中にリモートウェイクを発行します (サポートされている場合)。

**デバイスの中断**

デバイスの中断は、バス上に3ミリ秒間トラフィックがない場合に発生します。 この場合、クライアントドライバーは、 [**UfxDeviceNotifySuspend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifysuspend)および[**UfxDeviceNotifyResume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicenotifyresume)を呼び出して、中断と再開を検出したときに ufx に通知する必要があります。 これらの呼び出しを受信すると、UFX は[ *.evt\_ufx\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)を呼び出し、 [**IOCTL\_内部\_USBFN\_BUS\_イベントを完了してクラスドライバーに通知\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)要求。 リモートウェイクがデバイスでサポートされていて、ホストによって有効になっている場合、UFX は、リモートウェイクシグナルの発行を中断されている間に、*デバイス\_USB\_状態\_変更*を呼び出すことができ\_ufx\_呼び出します。

## <a name="related-topics"></a>関連トピック
[Windows の USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)  
[USB ファンクション コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)  
[USB 関数クライアントドライバーで使用される UFX オブジェクトとハンドル](ufx-objects-and-handles-used-by-a-usb-function-controller.md)  



