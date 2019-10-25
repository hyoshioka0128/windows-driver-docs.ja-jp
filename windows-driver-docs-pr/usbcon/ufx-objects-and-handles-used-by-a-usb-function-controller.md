---
Description: USB 関数クラス拡張 (UFX) は、WDF オブジェクト機能を使用して、これらの USB 固有の UFX オブジェクトを定義します。
title: USB 機能クライアント ドライバーが使用する UFX オブジェクトとハンドル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a559cb9c824be474c781810481255c8910d3143b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844335"
---
# <a name="ufx-objects-and-handles-used-by-a-usb-function-client-driver"></a>USB 機能クライアント ドライバーが使用する UFX オブジェクトとハンドル


**要約**

-   UFX オブジェクトは、エンドポイントとの間の転送を処理するために、関数コントローラードライバーによって使用されます。
-   これらのオブジェクトは、WDF オブジェクトへのハンドルであり、クライアントドライバーの要求時に UFX によって作成されます。 各オブジェクトの有効期間は、UFX によって管理されます。

**適用対象**

-   Windows 10

**最終更新日**

-   2015 年 7 月

**重要な API**

-   [**UfxDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate)
-   [**UfxEndpointCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate)

USB 関数クラス拡張 (UFX) は、WDF オブジェクト機能を使用して、これらの USB 固有の UFX オブジェクトを定義します。

これらのオブジェクトは、WDF オブジェクトへのハンドルであり、関数クライアントドライバーの要求時に UFX によって作成されます。 必要に応じて、クライアントドライバーは、作成時に渡すことができるこれらのオブジェクトにコンテキストを関連付けることができます。 UFX によって作成されたすべての WDF オブジェクトは、オブジェクトの作成時に UFX によって設定されたデバイスコンテキストを2つ持つ可能性があります。クライアントドライバーによって渡され、WDF オブジェクトが作成された後に[**WdfObjectAllocateContext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext)を使用して ufx で設定されるその他のデバイスコンテキスト。

## <a name="usb-device-object"></a>USB デバイスオブジェクト


**UFXDEVICE**

コントローラーによって作成された USB デバイスを表します。 このオブジェクトは、usb プロトコル仕様に従って USB 状態を管理し、USB デバイスに関連付けられている1つ以上のエンドポイントを管理します。 関数コントローラードライバーは、 [**UfxDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxdevicecreate)メソッドを呼び出すことによって、このオブジェクトを[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック内に作成します。

[ *.EVT\_UFX\_デバイス\_ホスト\_接続*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_connect)  
ホストとの接続を開始します。

[ *.EVT\_UFX\_デバイス\_ホスト\_切断*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_host_disconnect)  
関数コントローラーとホストとの通信を無効にします。

[ *.EVT\_UFX\_デバイス\_アドレス指定される*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_addressed)  
関数コントローラーにアドレスを割り当てます。

[ *.EVT\_UFX\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)  
既定のエンドポイントオブジェクトを作成します。

[ *.EVT\_UFX\_デバイス\_既定の\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_default_endpoint_add)  
既定のエンドポイントオブジェクトを作成します。

[ *.EVT\_UFX\_デバイス\_USB\_状態\_変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_usb_state_change)  
USB デバイスの状態を更新します。

[ *.EVT\_UFX\_デバイス\_ポート\_の変更*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_change)  
USB デバイスが接続されている新しいポートの種類を更新します。

[ *.EVT\_UFX\_デバイス\_ポート\_検出*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_port_detect)  
ポートの検出を開始します。

[ *.EVT\_UFX\_デバイス\_リモート\_ウェイクアップ\_シグナル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_remote_wakeup_signal)  
関数コントローラーでリモートウェイクアップを開始します。

[ *.EVT\_UFX\_デバイス\_\_独自の\_チャージャーを検出する*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_detect)  
独自のチャージャーの検出を開始します。

[ *.EVT\_UFX\_デバイス\_専用\_チャージャー\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_reset)  
独自の充電器をリセットします。

[ *.EVT\_UFX\_デバイス\_専用\_チャージャー\_設定\_プロパティ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_proprietary_charger_set_property)  
USB 経由の充電を有効にするために使用されるチャージャー情報を設定します。

## <a name="usb-endpoint-object"></a>USB エンドポイントオブジェクト


**UFXENDPOINT**

ホストとデバイスの間の論理接続を表します。 オブジェクトは、ホストとの間でのデータの転送を行います。 すべてのデバイスオブジェクトには、1つまたは複数のエンドポイントを指定できます。 既定のエンドポイントは常にコントロールエンドポイントであり、rest はクラスドライバー固有のオブジェクトです。 関数コントローラードライバーは、 [**Ufxendpointcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nf-ufxclient-ufxendpointcreate)メソッドを呼び出すことによってコールバックを[*追加\_、.EVT\_UFX\_デバイス\_エンドポイント*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ufxclient/nc-ufxclient-evt_ufx_device_endpoint_add)にオブジェクトを作成します。

## <a name="related-topics"></a>関連トピック
[USB ファンクション コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)  



