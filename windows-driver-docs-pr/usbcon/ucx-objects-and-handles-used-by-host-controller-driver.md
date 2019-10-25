---
Description: UCX は、WDF オブジェクト機能を拡張して、独自の USB 固有の UCX オブジェクトを定義します。 UCX は、これらのオブジェクトを使用して、基になるホストコントローラードライバーへの要求をキューに置いています。
title: ホスト コントローラー ドライバーが使用する UCX オブジェクトとハンドル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cea15160b2da02d540a0689aabe7b7c3882eb65
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844339"
---
# <a name="ucx-objects-and-handles-used-by-a-host-controller-driver"></a>ホスト コントローラー ドライバーが使用する UCX オブジェクトとハンドル


**要約**

-   UCX オブジェクトは、コントローラー、ルートハブ、およびすべてのエンドポイントに関連する操作を処理するために、ホストコントローラードライバーによって使用されます。
-   UCX オブジェクトはホストコントローラードライバーによって作成され、各オブジェクトの有効期間は UCX によって管理されます。

**適用対象**

-   Windows 10

**最終更新日**

-   2015 年 7 月

**重要な API**

-   [**Ucxコントローラーの作成**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))
-   [**UcxRootHubCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))
-   [**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)

UCX は、WDF オブジェクト機能を拡張して、独自の USB 固有の UCX オブジェクトを定義します。 UCX は、これらのオブジェクトを使用して、基になるホストコントローラードライバーへの要求をキューに置いています。

WDF オブジェクトの詳細については、「[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)」を参照してください。

## <a name="host-controller-object"></a>ホストコントローラーオブジェクト


**UCXCONTROLLER**

ホストコントローラードライバーによって作成されたホストコントローラーを表します。 ドライバーは、ホストコントローラーインスタンスごとに1つのホストコントローラーオブジェクトのみを作成する必要があります。 通常は、 [**Ucxコントローラーの create**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))メソッドを呼び出すことによって、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック内に作成されます。

ホストコントローラードライバーによってオブジェクトが作成されると、このドライバーは UCX によって呼び出されるコールバック関数の実装を登録します。 また、ドライバーは、ホストコントローラーが接続されているバスの種類 (ACPI や PCI など) を識別する必要があります。 また、 [**Ucxcontroller create**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188033(v=vs.85))呼び出しに渡される[**UCX\_controller\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/ns-ucxcontroller-_ucx_controller_config)構造体を使用して、ホストコントローラーデバイス情報を提供します。

I/o 要求を処理するには、ホストコントローラードライバーが GUID\_DEVINTERFACE\_USB\_ホスト\_コントローラーデバイスインターフェイスに登録する必要があります。 ドライバーは、このインターフェイスで定義されている Ioctl を実装する必要はありません。 代わりに、UCX クライアントは[**Ucxiodevicecontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nf-ucxcontroller-ucxiodevicecontrol)を呼び出して、このインターフェイスで受け取った IOCTL 要求を ucx に渡します。

次に、UCX によって呼び出されるホストコントローラーオブジェクトに関連付けられているコールバック関数を示します。 これらの関数は、ホストコントローラードライバーによって実装される必要があります。

[ *.EVT\_UCX\_コントローラー\_USBDEVICE\_ADD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)  
ハブドライバーがルートハブや外部ハブとの対話によって、新しいデバイスがバス上に存在することを確認したときに呼び出されます。

[ *.EVT\_UCX\_CONTROLLER\_クエリ\_USB\_機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_query_usb_capability)  
UCX によって呼び出され、USB ホストコントローラーによってサポートされるさまざまな機能に関する情報を収集します。

[ *.EVT\_UCX\_コントローラー\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_reset)  
UCX によって呼び出され、コントローラーハードウェアをリセットします。これは、検出されたエラーへの応答として発生する可能性があります。

[ *.EVT\_UCX\_CONTROLLER\_\_現在の\_を取得する*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_get_current_framenumber)  
ホストコントローラーから現在のフレーム番号を取得するために使用します。これは、アイソクロナス転送をスケジュールするためにハブドライバーによって使用されます。

## <a name="root-hub-object"></a>ルートハブオブジェクト


**UCXROOTHUB**

ホストコントローラーのルートポートの状態を取得および制御します。 ホストコントローラーオブジェクトの作成後に[**UcxRootHubCreate**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188048(v=vs.85))メソッドを呼び出すことによって、通常は[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック内でホストコントローラードライバーによって作成されます。 ホストコントローラーインスタンスごとに1つのルートハブオブジェクトしか存在できません。 **UcxRootHubCreate**呼び出しでは、ドライバーによってコールバック実装が登録されます。

[ *.EVT\_UCX\_ROOTHUB\_\_情報の取得*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_info)  
ルートハブの USB 2.0 および USB 3.0 ポートの数を返します。

[ *.EVT\_UCX\_ROOTHUB\_\_20PORT\_情報を取得する*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_20port_info)  
ルートハブの USB 2.0 または USB 3.0 ポート ([ *.evt\_UCX\_ROOTHUB\_GET\_30PORT\_INFO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_get_30port_info)) に関する情報を返します。

ルートハブオブジェクトが作成され、初期化されると、ハブドライバーは、割り込みおよび制御転送を送信することによって、ルートハブポートとやり取りします。 UCX は、ホストコントローラードライバーによって実装されているこれらのコールバック関数を呼び出すことによって、これらの転送を支援します。

[ *.EVT\_UCX\_ROOTHUB\_制御\_URB*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_control_urb)  
USB ハブによる機能コントロール要求を処理します。

[ *.EVT\_UCX\_ROOTHUB\_INTERRUPT\_TX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxroothub/nc-ucxroothub-evt_ucx_roothub_interrupt_tx)  
変更されたポートに関する情報の要求を処理します。

詳細については、「[ホストコントローラードライバーのルートハブのコールバック関数](manage-the-root-hub-in-a-host-controller-driver.md)」を参照してください。

## <a name="usb-device-object"></a>USB デバイスオブジェクト


**UCXUSBDEVICE**

バスに接続されている物理 USB デバイスを表します。 通常は、ホストコントローラードライバーによって作成されます。 [**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)メソッドを呼び出すことによってコールバックを[*追加\_\_usbdevice\_コントローラー\_UCX コントローラー*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxcontroller/nc-ucxcontroller-evt_ucx_controller_usbdevice_add)です。

オブジェクトが作成されると、ホストコントローラードライバーは、コールバック関数の実装を[**UcxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdevicecreate)呼び出しで登録します。

これらのコールバック関数は、USB デバイスの現在の状態に関する情報をコントローラーとドライバーに通知することを目的としています。

[ *.EVT\_UCX\_USBDEVICE\_ENABLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_enable)  
デバイスの既定のエンドポイントへの転送を実行するためのコントローラーを準備します。

[ *.EVT\_UCX\_USBDEVICE\_DISABLE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_disable)  
デバイスとその既定のエンドポイントに関連付けられたコントローラーリソースを解放します。

[ *.EVT\_UCX\_USBDEVICE\_アドレス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_address)  
アドレスをコントローラーにプログラムし、デバイスに\_アドレス転送を送信して、アドレス指定された状態にします。

[ *.EVT\_UCX\_USBDEVICE\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoints_configure)  
既定以外のエンドポイントをコントローラーにプログラムするか、既定以外の他のエンドポイントを解放します。

[ *.EVT\_UCX\_USBDEVICE\_RESET*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_reset)  
デバイスがリセットされたことを示すコントローラー通知。この場合、ドライバーはコントローラーを USB デバイスと同期するために必要な操作を実行します。

[ *.EVT\_UCX\_USBDEVICE\_更新*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)  
デバイスに関連するさまざまな情報をコントローラーに通知します。

[ *.EVT\_UCX\_USBDEVICE\_HUB\_情報*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_hub_info)  
UCXUSBDEVICE ハンドルがハブデバイス用の場合、ハブのプロパティに関する通知。

[ *.EVT\_UCX\_USBDEVICE\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)  
デバイスのエンドポイントを作成するようにドライバーに通知します。 [ *.Evt\_UCX\_USBDEVICE\_既定の\_エンドポイント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)既定のエンドポイントに追加します。

中断された USB 3.0 デバイス上のインターフェイスがウェイクアップ状態になった場合、ドライバーは[**UcxUsbDeviceRemoteWakeNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nf-ucxusbdevice-ucxusbdeviceremotewakenotification)を呼び出して ucx に通知する必要があります。

オブジェクトが作成された後、オブジェクトの有効期間は UCX によって管理され、ドライバーはオブジェクトを削除しないようにする必要があります。

## <a name="endpoint-object"></a>エンドポイントオブジェクト


**UCXENDPOINT**

USB デバイスオブジェクトのエンドポイントを表します。 エンドポイントオブジェクトは、 [ *.evt\_ucx\_usbdevice\_既定の\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_default_endpoint_add)または[ *.evt\_UCX\_USBDEVICE\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_endpoint_add)するときに、ホストコントローラーによって作成されます。コール. エンドポイントオブジェクトが作成されると、ドライバーはそのコールバック関数を登録します。

また、ドライバーは、各エンドポイントのフレームワークキューオブジェクトを作成し、 [**Ucxendpointsetwdfioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointsetwdfioqueue)を呼び出して、そのキューの WDFQUEUE を ucx に渡します。 エンドポイントが作成された後、オブジェクトとそれに関連付けられているキューの有効期間は UCX によって管理され、ドライバーはこれらのオブジェクト自体を削除することはできません。

エンドポイントオブジェクトは、ドライバーが、エンドポイントに関連する操作で UCX をサポートできるようにするいくつかのコールバック関数を実装します。

[ *.EVT\_UCX\_エンドポイント\_ABORT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_abort)  
エンドポイントに関連付けられているキューを中止します。

[ *.EVT\_UCX\_エンドポイント\_OK\_\_のキャンセル\_転送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_ok_to_cancel_transfers)  
エンドポイントで取り消された転送を完了できることをコントローラードライバーに通知します。

[ *.EVT\_UCX\_エンドポイント\_PURGE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_purge)  
エンドポイントで未処理の i/o 要求をすべて完了します。

[ *.EVT\_UCX\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_start)  
エンドポイントに関連付けられているキューを開始します。

[ *.EVT\_UCX\_エンドポイント\_静的\_ストリーム\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)  
静的ストリームを作成します。

[ *.EVT\_UCX\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_reset)  
コントローラーのエンドポイントのプログラミングをリセットするようにドライバーに通知します。

ホストコントローラードライバーが、エンドポイントで USB 3.0 No Ping 応答エラーを受信した場合、ドライバーは[**Ucxendpointnoping Responseerror**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointnopingresponseerror)を呼び出す必要があります。 この呼び出しの結果、USB デバイスオブジェクトが[ *.evt\_UCX\_USBDEVICE\_更新プログラム*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxusbdevice/nc-ucxusbdevice-evt_ucx_usbdevice_update)に送信されます。
詳細については、「[ホストコントローラードライバーでの USB エンドポイントの構成](configuring-usb-endpoints-in-a-host-controller-driver.md)」を参照してください。

## <a name="stream-object"></a>Stream オブジェクト


**UCXSTREAMS**

1つのエンドポイントにわたるデバイスへのパイプの数を表します。 ホストコントローラードライバーは、 [**UcxStaticStreamsCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)を呼び出すことによってコールバックを[*追加\_静的\_ストリーム\_\_エンドポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_add)にストリームオブジェクトを作成し\_します。

[**UcxStaticStreamsCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamscreate)の呼び出し中に、ホストコントローラードライバーによってコールバック関数が登録されます。 特定のエンドポイントオブジェクトの場合、ドライバーは、ストリームオブジェクトが作成されているかどうかを判断し、 [**Ucxendpointgetstaticstreams参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nf-ucxendpoint-ucxendpointgetstaticstreamsreferenced)を呼び出すことによって UCXSTREAMS ハンドルを返します。

オブジェクトが作成されると、ドライバーは各ストリームのフレームワークキューオブジェクトを作成し、 [**Ucxstaticstreamssetstreaminfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxsstreams/nf-ucxsstreams-ucxstaticstreamssetstreaminfo)を呼び出して、WDFQUEUE ハンドルを ucx に送信します。

Stream オブジェクトには、静的ストリームを管理する UCX を支援するための、ホストコントローラーのコールバック関数がいくつか用意されています。

[ *.EVT\_UCX\_エンドポイント\_静的\_ストリーム\_無効にする*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_disable)  
エンドポイントのすべてのストリームの Release controller リソース。

[ *.EVT\_UCX\_エンドポイント\_静的\_ストリームを有効にする\_有効にする*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucxendpoint/nc-ucxendpoint-evt_ucx_endpoint_static_streams_enable)  
このエンドポイントのすべてのストリームのコントローラーハードウェアを有効にします。

オブジェクトと関連付けられたキューの有効期間は UCX によって管理され、ドライバーはオブジェクトを削除しないようにする必要があります。

## <a name="related-topics"></a>関連トピック
[USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)  



