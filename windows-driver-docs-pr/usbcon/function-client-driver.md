---
Description: 関数のコント ローラーのクライアント ドライバーを USB 関数コント ローラーの拡張機能 (UFX) と対話中に実行するさまざまなタスクについて説明します。
title: 関数のコント ローラーのクライアント ドライバーを記述します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082da7b62437589c8cc7c8ef907828197f3df3d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378364"
---
# <a name="write-a-function-controller-client-driver"></a>関数のコント ローラーのクライアント ドライバーを記述します。


**概要**

-   関数のコント ローラーのクライアント ドライバーの想定される動作をについて説明します。

**適用対象**

-   Windows 10
-   USB デバイスのコント ローラーのドライバーを記述するドライバー開発者

**重要な API**

-   [USB 関数コント ローラーのクライアント ドライバー リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#usb-function-controller-client-driver-reference)


関数のコント ローラーのクライアント ドライバーを USB 関数コント ローラーの拡張機能 (UFX) と対話中に実行するさまざまなタスクについて説明します。 UFX と、クライアント ドライバーは、エクスポート メソッドとイベントのコールバック関数を使用して相互に通信します。 メソッドをエクスポート (名前付き**UfxDeviceXxx**または**UfxEndpointXxx**) は UFX によってエクスポートされ、クライアント ドライバーによって呼び出されます。 コールバック関数 (という*EVT\_UFX\_Xxx*) クライアント ドライバーで実装され、UFX によって呼び出されます。

UFX が非同期に、すべてのクライアント ドライバーのコールバック関数を呼び出すと、オブジェクトごとに一度に 1 つのコールバック。 たとえばが USB デバイス オブジェクトと次の 3 つのエンドポイント オブジェクトです。 一度に最大で 4 つコールバック関数 (デバイスとエンドポイントごとに 1 つ) を呼び出すことができます。 クライアント ドライバー呼び出されるまで待機する UFX 各コールバック メソッドの[ **UfxDeviceEventComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)をドライバーが要求を完了したことを示します。 のみの他のエクスポート メソッド UFX をこれらのエクスポートを待機中に待機する[ **UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)します。 クライアントのコールバック関数の多くは省略可能です。 必要な関数は次のとおりです。

-   [*EVT\_UFX\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)
-   [*EVT\_UFX\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)
-   [*EVT\_UFX\_デバイス\_ホスト\_接続*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)
-   [*EVT\_UFX\_デバイス\_ホスト\_切断*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)
-   [*EVT\_UFX\_デバイス\_アドレス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_addressed)

## <a name="initialization"></a>初期化


1.  Windows Driver Foundation (WDF) のクライアント ドライバーの実装を呼び出すときに、関数のコント ローラーのクライアント ドライバーが初期化プロセスを開始、 [ **EVT_WDF_DRIVER_DEVICE_ADD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック。 呼び出す、その実装では、クライアント ドライバーが期待どおり[ **UfxFdoInit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxfdoinit)呼び出すことによって、デバイス オブジェクトを作成および[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate).
2.  クライアント ドライバーの呼び出し[ **UfxDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicecreate) USB デバイス オブジェクトを作成および UFXDEVICE ハンドルを取得します。
3.  クライアント ドライバーの呼び出し[ **UfxDeviceNotifyHardwareReady** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready)に示す UFX クライアント ドライバーのコールバック関数を呼び出すこともできますようになりました。
4.  UFX など初期化タスクを実行します。
    -   UFX 呼び出し、クライアント ドライバーの[ *EVT\_UFX\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)実装は、既定値を作成するにはエンドポイント。
    -   UFX は、物理デバイス オブジェクト (Pdo) デバイスでサポートされるインターフェイスの子を作成します。
    -   UFX は送信時にデバイス クラス ドライバーのアクティブ化の待機、 [ **IOCTL\_内部\_USBFN\_ACTIVATE\_USB\_BUS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus)要求。 呼び出すクライアント ドライバー待機[ **UfxDeviceNotifyAttach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyattach)がアタッチされると、デバイスを示します。

## <a name="class-driver-notification"></a>クラスのドライバーの通知


クラスのドライバーを送信する必要があります、パケットのセットアップとバスの状態の通知を受け取るため、 [ **IOCTL\_内部\_USBFN\_ACTIVATE\_USB\_BUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_activate_usb_bus)要求。 UFX クラス ドライバー固有の通知キューにこれらの要求をキューします。 バス イベントに関する通知を受信するには、クライアント ドライバーからは、UFX は適切な各キューからをポップし、要求を完了します。 不足している通知のクラス ドライバーを防ぐためには、UFX クラス ドライバーの通知の固定サイズのキューを保持します。

## <a name="device-attach-and-detach-events"></a>デバイスは、アタッチし、デタッチのイベント


UFX まで、デバイスがデタッチされたことを想定しています、関数コント ローラーのクライアント ドライバーは[ **UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyattach)します。

UFX デバイスの状態を設定する呼び出しの後**Powered** USB 仕様で定義されています。 状態の変更について、クライアント ドライバーを通知する UFX に呼び出すクライアント ドライバーの[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)実装します。

UFX では、(Cad.sys) にデバイスを充電を支援する充電器ドライバーに通知します。 UFX もを実行して、クラス ドライバーに通知[ **IOCTL\_内部\_USBFN\_BUS\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)クラスのドライバーが既に送信された要求。

クライアント ドライバーを呼び出す必要があります[ **UfxDeviceNotifyDetach** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifydetach)バスがデタッチされます。 各呼び出しの後に 1 回、クライアントの必要がありますのみ呼び出しがデタッチ[ **UfxDeviceNotifyAttach**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyattach)します。 後に、 **UfxDeviceNotifyDetach**を呼び出すと、UFX 呼び出し[ *EVT\_UFX\_デバイス\_ホスト\_切断*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect) (これがない場合、インターフェイスの変更) です。 UFX し、すべての処理の進行状況は、エンドポイントのすべてのキューを削除して、既定のエンドポイント キューの開始などのタスクをクリーンアップします。 UFX 呼び出し[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)クラス ドライバーに通知を実行して、 [**IOCTL\_内部\_USBFN\_BUS\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)要求。

**ハードウェア障害**

呼び出すクライアント ドライバーが必要ですが、ハードウェア エラーが発生した場合[ **UfxDeviceNotifyHardwareFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyhardwarefailure)します。 応答として、UFX デバイス スタックを破棄し、ドライバーのクライアントを呼び出すことによってこの状況から回復しよう[ *EVT\_UFX\_デバイス\_コント ローラー\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_controller_reset). クライアントは、コント ローラーを初期状態にリセットする必要があります。 別のハードウェア障害が発生した場合、クライアントは UfxDeviceNotifyHardwareFailure をもう一度呼び出す必要があります。 2 つ目の呼び出しでその状態とバグ チェック UFX が記録されます。

## <a name="port-detection"></a>ポートの検出


ポートの検出は、UFX によって実行されます。 呼び出す関数のコント ローラー クライアント ドライバーの[ *EVT\_UFX\_デバイス\_ポート\_検出*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_port_detect)ポートの種類を決定するコールバック関数デバイスをアタッチします。 クライアントが呼び出すことによって応答[ **UfxDevicePortDetectComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdeviceportdetectcomplete)または[ **UfxDevicePortDetectCompleteEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdeviceportdetectcompleteex)ポートのいずれかで定義された型[ **USBFN\_ポート\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnbase/ne-usbfnbase-_usbfn_port_type)します。

クライアントを報告するかどうか、ポートの種類を判断できないのは、クライアント、 **UsbfnUnknownPort**します。 不明またはダウン ストリームのポートにポートがあるかどうかは、UFX 呼び出し、クライアント ドライバーの[ *EVT\_UFX\_デバイス\_ホスト\_CONNECT* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)関数。 UFX は、しばらくの間、バスをリッスンします。 ポートが不明な場合は、セットアップのパケットをなど、トラフィックがある場合、UFX が前提としています**UsbfnStandardDownstreamPort**します。 それ以外の場合、UFX があるポートを割り当てます**UsbfnInvalidDedicatedChargingPort**します。 UFX が Cad.sys を通知し、呼び出し、クライアント ドライバーのポートの種類が決定されると、 [ *EVT\_UFX\_デバイス\_ポート\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_port_change)関数。 関数で、クライアント ドライバーに ed UFX ポートの種類に一致するハードウェアの状態を変更するのには、期待しています。

## <a name="endpoint-creation"></a>エンドポイントの作成


UFX を呼び出して、クライアント ドライバーの既定のエンドポイント (エンドポイント 0) を作成します[ *EVT\_UFX\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)ホストによって送信されたセットアップ パケットを処理できるようにします。 UFX を呼び出してその他のエンドポイントを作成します[ *EVT\_UFX\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)します。 UFX のみエンドポイントを作成しますクライアント後ドライバー呼び出し[ **UfxDeviceNotifyHardwareReady**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyhardwareready)します。 これらのコールバック関数を呼び出すクライアント ドライバーを必要[ **UfxEndpointCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxendpointcreate)エンドポイントにオブジェクトし、その UFXENDPOINT ハンドルを取得します。 UFX は、クラス ドライバーの PDO は、エンドポイントが所属するインターフェイスに関連付けられている親を設定します。 既定のエンドポイントの親は、USB デバイス オブジェクトです。 エンドポイントに 2 つのフレームワークのキュー オブジェクトが含まれています転送キューでは、およびコマンドのどちらものみアクセスできる、デバイスが構成済みの状態の場合、キュー (が、0、エンドポイントを除く UFX 呼び出しの後にアクセスできる[ *。EVT\_UFX\_デバイス\_ホスト\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_connect))。

-   **コマンド キューの要求**
-   [**IOCTL\_内部\_USBFN\_取得\_パイプ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_get_pipe_state)
-   [**IOCTL\_内部\_USBFN\_設定\_パイプ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)
-   [**IOCTL\_内部\_USBFN\_記述子\_UPDATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)
-   **転送キューの要求**
-   [**IOCTL\_内部\_USBFN\_転送\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)
-   [**IOCTL\_内部\_USBFN\_転送\_IN\_APPEND\_0\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)
-   [**IOCTL\_内部\_USBFN\_転送\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)
-   [**IOCTL\_内部\_USBFN\_コントロール\_状態\_ハンドシェイク\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)
-   [**IOCTL\_内部\_USBFN\_コントロール\_状態\_ハンドシェイク\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out)

## <a name="device-enumeration"></a>デバイスの列挙


UFX 呼び出してドライバーの前に、クライアント ドライバーがホストへの接続を許可しないでください[ *EVT\_UFX\_デバイス\_ホスト\_CONNECT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)します。 クライアント ドライバーを呼び出すときに、デバイスの列挙が開始されます[ **UfxDeviceNotifyReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyreset)します。 **既定**状態では、UFX は標準のセットアップのパケットを処理します。

**リセット**

UFX エンドポイントのすべてのキューを削除し、送信、 [ **IOCTL\_内部\_USBFN\_記述子\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)要求クライアント ドライバーを更新するには**wMaxPacketSize**エンドポイント 0 の。 既定のエンドポイントのキューを開始し、状態を設定します UFX**既定**します。

**Default**

UFX 呼び出し、クライアント ドライバーの[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)関数。 また、状態のクラス ドライバーを通知します。 UFX セットの受信後\_UFX、アドレスの標準セットアップ パケットでは、状態を設定**アドレス**します。

**アドレス指定**

UFX 呼び出し、クライアント ドライバーの[ *EVT\_UFX\_デバイス\_アドレス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_addressed)それに対応するクライアントに示すために関数を使用する必要があります。 場合、アドレスは 0、UFX セットの状態をバックアップする**既定**と呼び出し[ *EVT\_UFX\_デバイス\_USB\_状態\_の変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)しクラス ドライバーに通知します。 セットを受信する\_構成標準セットアップ パケット、UFX 状態を設定する**構成済み**します。

**構成されています。**

UFX がインターフェイスのエンドポイントを削除し、状態を設定します、選択した構成が 0 の場合は、**アドレス**します。 UFX 送信、 [ **IOCTL\_内部\_USBFN\_記述子\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxbase/ni-ufxbase-ioctl_internal_usbfn_descriptor_update)クライアント ドライバーを更新する要求、 **wMaxPacketSize**インターフェイスのエンドポイント。 UFX、インターフェイスのすべてのエンドポイント キューが削除が完了し、インターフェイスのエンドポイントのキューを開始します。 ポートの種類がない場合**UsbfnStandardDownstreamPort**または**UsbfnChargingDownstreamPort**、UFX するポートの種類を変更する**UsbfnStandardDownstreamPort**し、通知Cad.sys;呼び出すことによって、クライアント ドライバー [ *EVT\_UFX\_デバイス\_ポート\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_port_change)と[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) ; 状態を更新する構成済みの状態のクラス ドライバー。

## <a name="standard-control-transfers"></a>標準コントロールの転送


呼び出された後、いつでも、既定のエンドポイント上のコントロールの転送を処理できる UFX [ *EVT\_UFX\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)でをクライアント ドライバー、既定のエンドポイントを使用して作成します。 コントロールのすべての転送にパケットを 8 バイトのセットアップで始まります。 にホストをセットアップ パケットを送信するクライアント ドライバーを呼び出す必要があります[ **UfxEndpointNotifySetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxendpointnotifysetup)します。 UFX によっては、標準コントロールの転送が完了しました。 コントロールの転送に関連付けられているデータがある場合 UFX から読み取り、適切な既定のコントロール エンドポイントを書き込みます。

## <a name="non-standard-control-transfers"></a>非標準のコントロールの転送


転送は完了して、適切なクラス ドライバーに転送 UFX がコントロールの転送を処理できない場合、 [ **IOCTL\_内部\_USBFN\_BUS\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)要求。 コントロールの転送は、コントロール エンドポイントのエンドポイント記述子として定義されている任意のエンドポイントで発生します。 既定のコントロール エンドポイント以外のエンドポイント上のコントロールの転送は、常に非標準のコントロールの転送です。 コントロール エンドポイントが既定のコントロール エンドポイントの場合は、UFX はクラスのドライバーのクラスの要求と示されているセットアップ パケットのクラス ドライバーを通知します。 コントロール エンドポイントは、インターフェイスに属する、UFX はそのインターフェイスに関連付けられたクラス ドライバーを通知します。 必要に応じて、クラス ドライバーは、コントロール エンドポイントの読み書きに必要です。

## <a name="data-transfers"></a>データ転送


送信することによってクラス ドライバーによってデータ転送を開始[ **IOCTL\_内部\_USBFN\_転送\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)、 [ **IOCTL\_内部\_USBFN\_転送\_IN\_APPEND\_0\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)、または[ **IOCTL\_内部\_USBFN\_転送\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)要求。 、それらの要求の検証後 UFX は、それをクライアント ドライバーによって処理される適切なエンドポイントのキューに転送します。 追加の検証を実行するには、クライアント ドライバーが必要です。 クライアント ドライバーでは、エンドポイントのキューでの転送要求を受信します。 クライアント ドライバーでは、このキューからバスの使用率を最大化する必要がある多くの要求を取得できます。 クライアント ドライバーは、状態が成功した要求を完了する必要があります\_成功します。 ドライバーは、要求をキャンセルするベストエフォートの試行を行う必要があり、完了ステータスの要求はキャンセル\_がキャンセルされた場合に取り消されました。 クライアント ドライバーが、状態が要求を完了すると無効なパラメーターが渡された場合\_無効な\_パラメーター。

**コントロールの転送**

コントロールの転送にパケットを 8 バイトのセットアップで始まります。 にホストをセットアップ パケットを送信するクライアント ドライバーを呼び出す必要があります[ **UfxEndpointNotifySetup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxendpointnotifysetup)します。 UFX 通知要求を完了して転送を非標準のコントロールのクラス ドライバーに通知します。 クライアントと UFX の両方を使用して、 [ **IOCTL\_内部\_USBFN\_転送\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)、 [ **IOCTL\_内部\_USBFN\_転送\_IN\_APPEND\_0\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)、または[ **IOCTL\_内部\_USBFN\_転送\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)から読み取ったり、書き込んだりする既定のコントロール エンドポイントにします。 ただし、インターフェイスでは、対応するクラス ドライバーのみを使用して他のコントロール エンドポイントを定義できます。 コントロール エンドポイントは、セットアップ パケットへの応答で停止していることができます。 クラスのドライバーの送信、 [ **IOCTL\_内部\_USBFN\_設定\_パイプ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state)エンドポイントを停止する要求。 停止が送信された後すぐに、エンドポイントでトラフィックを再開するは、ハードウェアまたはクライアント ドライバーが必要です。 コントロール エンドポイントを送信し、以前データなし、長さ 0 のパケット (ZLP) が表示されることもできます。 クライアント ドライバーと UFX これを使用して[ **IOCTL\_内部\_USBFN\_コントロール\_状態\_ハンドシェイク\_IN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_in)と[ **IOCTL\_内部\_USBFN\_コントロール\_状態\_ハンドシェイク\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_control_status_handshake_out).

**一括および割り込みの転送**

一括転送では、データ配信を保証し、大量のデータを送信するために使用します。 転送を使用して一括エンドポイントに送信できる[ **IOCTL\_内部\_USBFN\_転送\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in)、 [ **IOCTL\_内部\_USBFN\_転送\_IN\_APPEND\_0\_PKT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_in_append_zero_pkt)、または[ **IOCTL\_内部\_USBFN\_転送\_アウト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_transfer_out)します。 使用してエンドポイントを制御する一括エンドポイントが同様に停滞する[ **IOCTL\_内部\_USBFN\_設定\_パイプ\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_set_pipe_state). ホストのすべての要求への応答停止パケットを送信して、IOCTL 要求を保持するには、クライアント ドライバーが必要です。 コントロールのエンドポイントとは異なり一括停止しているエンドポイントは、停止状態が明示的にクリアされるまで停止したままです。

転送の割り込みは、一括転送に似ていますが、保証された待機時間、転送を中断します。 割り込み転送は、一括転送もストリーミング機能がないと同じインターフェイスを持っています。

**アイソクロナス転送**

クライアント ドライバーは、このバージョンでアイソクロナス転送をサポートする必要はありません。

## <a name="power-management"></a>電源管理


クライアント ドライバーでは、電源管理のすべての側面を所有します。 適切な電源状態に戻ってをなど、イベント完了の適切なエクスポート関数を呼び出す前に、要求を完了クライアント ドライバーが期待どおりのコールバック関数は非同期であるため[ **UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)します。

UFX を稼働状態にある場合、デバイスの状態 (で定義されている[ **USBFN\_デバイス\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnbase/ne-usbfnbase-_usbfn_device_state)) は**UsbfnDeviceStateSuspended**と**UsbfnDeviceStateAttached**ポートの種類を報告していないとします。 UFX がポートの種類を報告する代わりに、(で定義されている[ **USBFN\_ポート\_型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnbase/ne-usbfnbase-_usbfn_port_type)) **UsbfnStandardDownstreamPort**または**UsbfnChargingDownstreamPort**します。

UFX を入力し、呼び出すことによって動作状態を終了する[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)または[*EVT\_UFX\_デバイス\_ポート\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_port_change)実装します。 クライアント ドライバーを呼び出すと、稼動状態の間の移行が完了したら[ **UfxDeviceEventComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdeviceeventcomplete)します。

動作状態、UFX は任意のコールバックを呼び出すことができます。 UFX 作業の状態でないときに呼び出すのみ[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change) ; 動作状態を入力するには[ *EVT\_UFX\_デバイス\_リモート\_ウェイク アップ\_信号*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal) (場合により中断中にリモート ウェイクを発行するにはサポートされています)。

**デバイスを中断します。**

デバイスの中断 3 ミリ秒のバスのトラフィックがないときに発生します。 この場合、クライアント ドライバーが UFX を通知する必要がありますの中断し、再開を呼び出すことによって、検出した場合に[ **UfxDeviceNotifySuspend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifysuspend)と[ **UfxDeviceNotifyResume**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nf-ufxclient-ufxdevicenotifyresume). これらの呼び出し、UFX 呼び出しを受け取る[ *EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)しによってクラス ドライバーに通知します完了[ **IOCTL\_内部\_USBFN\_BUS\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbfnioctl/ni-usbfnioctl-ioctl_internal_usbfn_bus_event_notification)要求。 UFX が呼び出しを呼び出すことができる場合、リモート ウェイクがデバイスでサポートされているし、ホストで有効になって、 *EVT\_UFX\_デバイス\_USB\_状態\_変更*問題を中断している間、リモート ウェイク信号。

## <a name="related-topics"></a>関連トピック
[Windows での USB デバイス側のドライバー](usb-device-side-drivers-in-windows.md)  
[USB ファンクション コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)  
[UFX オブジェクトと関数の USB クライアント ドライバーによって使用されるハンドル](ufx-objects-and-handles-used-by-a-usb-function-controller.md)  



