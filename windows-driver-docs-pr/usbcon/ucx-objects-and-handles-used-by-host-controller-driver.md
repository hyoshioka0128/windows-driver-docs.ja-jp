---
Description: UCX では、独自の特定の USB UCX オブジェクトを定義する WDF オブジェクトの機能を拡張します。 UCX は、基になるホスト コント ローラー ドライバーに要求をキューにこれらのオブジェクトを使用します。
title: ホスト コントローラー ドライバーが使用する UCX オブジェクトとハンドル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 727421218b45a5829ba514ba7c503c090bb2601b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368778"
---
# <a name="ucx-objects-and-handles-used-by-a-host-controller-driver"></a>ホスト コントローラー ドライバーが使用する UCX オブジェクトとハンドル


**要約**

-   UCX オブジェクトは、コント ローラー、そのルート ハブおよびすべてのエンドポイントに関連する操作を処理するために、ホスト コント ローラー ドライバーによって使用されます。
-   UCX オブジェクトは、ホスト コント ローラー ドライバーによって作成され、各オブジェクトの有効期間が UCX によって管理されます。

**適用対象**

-   Windows 10

**最終更新日**

-   2015 年 7 月

**重要な API**

-   [**UcxControllerCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))
-   [**UcxRootHubCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))
-   [**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)

UCX では、独自の特定の USB UCX オブジェクトを定義する WDF オブジェクトの機能を拡張します。 UCX は、基になるホスト コント ローラー ドライバーに要求をキューにこれらのオブジェクトを使用します。

WDF のオブジェクトの詳細については、次を参照してください。 [Framework オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)します。

## <a name="host-controller-object"></a>ホスト コント ローラーのオブジェクト


**UCXCONTROLLER**

ホスト コント ローラーのドライバーによって作成されるホスト コント ローラーを表します。 ドライバーは、ホスト コント ローラーのインスタンスごとに 1 つだけのホスト コント ローラー オブジェクトを作成する必要があります。 内で作成された通常、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックを呼び出すことによって、 [ **UcxControllerCreate** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))メソッド。

ホスト コント ローラーのドライバーでは、オブジェクトを作成するとき、ドライバーは UCX によって呼び出されるコールバック関数の実装を登録します。 さらに、ドライバーはホスト コント ローラーが接続されている、ACPI など PCI バスの種類を識別してください。 用意されており、ホスト コント ローラー デバイス情報を使用して、 [ **UCX\_コント ローラー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/ns-ucxcontroller-_ucx_controller_config)に渡される構造体、 [ **UcxControllerCreate** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))呼び出します。

I/O 要求を処理するために、ホスト コント ローラー ドライバーが GUID を登録する必要があります\_DEVINTERFACE\_USB\_ホスト\_コント ローラー デバイスのインターフェイス。 ドライバーは、このインターフェイスで定義されている Ioctl を実装する必要はありません。 UCX クライアントが呼び出して UCX するには、このインターフェイスで受信した IOCTL 要求を渡す代わりに、 [ **UcxIoDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nf-ucxcontroller-ucxiodevicecontrol)します。

ここでは、ホスト コント ローラーのオブジェクトに関連付けられている UCX によって呼び出されるコールバック関数です。 ホスト コント ローラーのドライバーでは、これらの関数を実装する必要があります。

[*EVT\_UCX\_コント ローラー\_USBDEVICE\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)  
ルート ハブや新しいデバイスがバスに存在する外部のハブとの対話を使用して、ハブのドライバーが特定ときに呼び出されます。

[*EVT\_UCX\_コント ローラー\_クエリ\_USB\_機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_query_usb_capability)  
USB ホスト コント ローラーでサポートされているさまざまな機能に関する情報を収集する UCX によって呼び出されます。

[*EVT\_UCX\_コント ローラー\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_reset)  
場合によって検出されたエラーへの応答で、コント ローラー ハードウェアをリセットする UCX によって呼び出されます。

[*EVT\_UCX\_コント ローラー\_取得\_現在\_FRAMENUMBER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_current_framenumber)  
アイソクロナス転送をスケジュールするためのハブのドライバーで使用されるホスト コント ローラーから現在のフレーム数を取得するために使用します。

## <a name="root-hub-object"></a>ルート ハブ オブジェクト


**UCXROOTHUB**

取得し、ホスト コント ローラーのルートのポートの状態を制御します。 通常内のホスト コント ローラーのドライバーによって作成された、 [ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックを呼び出すことによって、 [ **UcxRootHubCreate** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))ホスト コント ローラーのオブジェクトを作成した後のメソッドです。 ホスト コント ローラーのインスタンスごとに 1 つだけのルート ハブ オブジェクトである必要があります。 **UcxRootHubCreate**呼び出し、ドライバーがそのコールバックの実装を登録します。

[*EVT\_UCX\_ROOTHUB\_取得\_情報*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_info)  
ルート ハブのポートに USB 2.0 および USB 3.0 の数を返します。

[*EVT\_UCX\_ROOTHUB\_取得\_20PORT\_情報*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_20port_info)  
USB 2.0 接続または USB 3.0 ポートに関する情報を返す ([*EVT\_UCX\_ROOTHUB\_取得\_30PORT\_情報*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_30port_info)) のルート ハブ。

ハブのルート オブジェクトを作成および初期化した後、ハブのドライバーは割り込みと制御の転送を送信することによってルート ハブのポートと対話します。 UCX は、ホスト コント ローラーのドライバーによって実装されるこれらのコールバック関数を呼び出すことによって、これらの転送に役立ちます。

[*EVT\_UCX\_ROOTHUB\_コントロール\_URB*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)  
USB ハブでは、機能の制御の要求を処理します。

[*EVT\_UCX\_ROOTHUB\_INTERRUPT\_TX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)  
変更されたポートに関する情報を要求をハンドルします。

詳細については、次を参照してください。[ホスト コント ローラーのドライバーのコールバック関数のハブ ルート](manage-the-root-hub-in-a-host-controller-driver.md)します。

## <a name="usb-device-object"></a>USB デバイス オブジェクト


**UCXUSBDEVICE**

バスに接続されている物理的な USB デバイスを表します。 通常内のホスト コント ローラーのドライバーによって作成された、 [ *EVT\_UCX\_コント ローラー\_USBDEVICE\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add) を呼び出すことによってコールバック[**UcxUsbDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)メソッド。

ホスト コント ローラーのドライバーとコールバック関数の実装を登録するオブジェクトが作成されたときに、 [ **UcxUsbDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)呼び出します。

これらのコールバック関数は、コント ローラーと USB デバイスの現在の状態に関する情報を通知するドライバーを保持するものです。

[*EVT\_UCX\_USBDEVICE\_を有効にします。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable)  
デバイスの既定のエンドポイントへの転送を実行するため、コント ローラーを準備します。

[*EVT\_UCX\_USBDEVICE\_を無効にします。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)  
デバイスとその既定のエンドポイントに関連付けられたコント ローラーのリソースを解放します。

[*EVT\_UCX\_USBDEVICE\_アドレス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_address)  
コント ローラーに、アドレス プログラムし、セットを送信\_アドレス指定された状態にする、デバイスにアドレス転送します。

[*EVT\_UCX\_USBDEVICE\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)  
コント ローラーに既定以外のエンドポイントをプログラムやその他の既定以外のエンドポイントを解放します。

[*EVT\_UCX\_USBDEVICE\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_reset)  
コント ローラーの通知が、ドライバーが USB デバイスとコント ローラーの同期に必要なアクションを受け取る場合、デバイスがリセットされたことを。

[*EVT\_UCX\_USBDEVICE\_UPDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)  
デバイスに関連する情報のさまざまな部分のコント ローラーに通知します。

[*EVT\_UCX\_USBDEVICE\_ハブ\_情報*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_hub_info)  
通知ハブのプロパティ、UCXUSBDEVICE を処理する場合は、ハブのデバイスです。

[*EVT\_UCX\_USBDEVICE\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)  
デバイスのエンドポイントを作成するドライバーに通知します。 [*EVT\_UCX\_USBDEVICE\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)既定のエンドポイント。

ドライバーの呼び出しが想定されて中断された USB 3.0 デバイスのインターフェイスをウェイク アップのシグナルを受け取るが、 [ **UcxUsbDeviceRemoteWakeNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nf-ucxusbdevice-ucxusbdeviceremotewakenotification) UCX に通知します。

オブジェクトを作成すると後、は、オブジェクトの有効期間は UCX、によって管理され、ドライバーでは、オブジェクトは削除する必要があります。

## <a name="endpoint-object"></a>Endpoint オブジェクト


**UCXENDPOINT**

USB デバイス オブジェクトのエンドポイントを表します。 Endpoint オブジェクトは、いずれかの中に、ホスト コント ローラーによって作成されます、 [ *EVT\_UCX\_USBDEVICE\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)または[ *EVT\_UCX\_USBDEVICE\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)コールバック。 Endpoint オブジェクトが作成されたときに、ドライバーは、そのコールバック関数を登録します。

ドライバーもエンドポイントごとに、framework キュー オブジェクトを作成しを呼び出して UCX にそのキューに対する WDFQUEUE を渡します[ **UcxEndpointSetWdfIoQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nf-ucxendpoint-ucxendpointsetwdfioqueue)します。 エンドポイントを作成すると後、は、オブジェクトと関連付けられているキューの有効期間は UCX、によって管理され、ドライバーを削除しないこれらのオブジェクト自体。

Endpoint オブジェクトは、ドライバーは、エンドポイントに関連する操作と UCX を支援するためにいくつかのコールバック関数を実装します。

[*EVT\_UCX\_エンドポイント\_中止*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)  
エンドポイントに関連付けられているキューを中止します。

[*EVT\_UCX\_エンドポイント\_OK\_TO\_キャンセル\_転送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)  
通知を完了するコント ローラーのドライバーには、エンドポイント上の転送が取り消されました。

[*EVT\_UCX\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)  
エンドポイントのすべての未処理 I/O 要求を完了します。

[*EVT\_UCX\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)  
エンドポイントに関連付けられているキューを開始します。

[*EVT\_UCX\_エンドポイント\_静的\_ストリーム\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)  
静的なストリームを作成します。

[*EVT\_UCX\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_reset)  
エンドポイントのコント ローラーのプログラミングをリセットするドライバーに通知します。

ホスト コント ローラーのドライバーでは、エンドポイントの USB 3.0 いいえ Ping 応答エラーを受信すると、ドライバーを呼び出す必要があります[ **UcxEndpointNoPingResponseError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nf-ucxendpoint-ucxendpointnopingresponseerror)します。 USB デバイス オブジェクトの受信で結果を呼び出す[ *EVT\_UCX\_USBDEVICE\_UPDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)します。
詳細については、次を参照してください。[ホスト コント ローラーのドライバーを構成する USB エンドポイント](configuring-usb-endpoints-in-a-host-controller-driver.md)します。

## <a name="stream-object"></a>Stream オブジェクト


**UCXSTREAMS**

1 つのエンドポイント間で、デバイスにパイプの数を表します。 ホスト コント ローラーのドライバーでストリーム オブジェクトの作成、 [ *EVT\_UCX\_エンドポイント\_静的\_ストリーム\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)コールバック呼び出して[ **UcxStaticStreamsCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)します。

中に、 [ **UcxStaticStreamsCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)呼び出し、ホスト コント ローラーのドライバーがそのコールバック関数を登録します。 ストリーム オブジェクトを作成し、UCXSTREAMS を呼び出して処理を返すかどうかは、特定のエンドポイント オブジェクトで、ドライバーを調べる[ **UcxEndpointGetStaticStreamsReferenced**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nf-ucxendpoint-ucxendpointgetstaticstreamsreferenced)します。

ドライバーが各ストリーム framework キュー オブジェクトを作成し、UCX に WDFQUEUE ハンドルを呼び出すことによって送信オブジェクトを作成すると後、 [ **UcxStaticStreamsSetStreamInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxsstreams/nf-ucxsstreams-ucxstaticstreamssetstreaminfo)します。

ストリーム オブジェクトは、ホスト コント ローラー UCX が静的なストリームを管理するを支援するためのいくつかのコールバック関数を提供します。

[*EVT\_UCX\_エンドポイント\_静的\_ストリーム\_を無効にします。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_disable)  
エンドポイントのすべてのストリームのコント ローラーのリソースをリリースします。

[*EVT\_UCX\_エンドポイント\_静的\_ストリーム\_を有効にします。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_enable)  
このエンドポイントのすべてのストリームのコント ローラーのハードウェアを有効にします。

オブジェクトと関連付けられているキューの有効期間は UCX、によって管理され、ドライバーは、オブジェクトを削除する必要があります。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  



