---
title: ハードウェア通知クライアント ドライバーの作成
description: このセクションでは、Microsoft によって提供される KMDF クラス拡張機能を利用する、ハードウェア通知クライアントドライバーの開発に関する一般的なガイダンスを提供します。
ms.assetid: 348950d3-fb80-4800-a606-290d473aa412
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d2b1d1b931de07e456a7249f66b33b0b5b6b332d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824900"
---
# <a name="create-a-hardware-notification-client-driver"></a>ハードウェア通知クライアント ドライバーの作成


このセクションでは、Microsoft によって提供される KMDF クラス拡張機能を利用する、ハードウェア通知クライアントドライバーの開発に関する一般的なガイダンスを提供します。

1.  Mshwnclxstub にリンクするクライアントドライバー実装用のファイルを作成し、ヘッダー hwn と hwnclx をインクルードします。

2.  必須の KMDF およびハードウェア通知クラス拡張コールバック関数のインスタンスを定義します。 具体的には、次のコード例に示すように、これらのコールバック関数を実装して登録する必要があります。

    ```cpp
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD HwnClientEvtDeviceAdd;
    HWN_CLIENT_INITIALIZE_DEVICE HwnClientInitializeDevice;
    HWN_CLIENT_UNINITIALIZE_DEVICE HwnClientUnInitializeDevice;
    HWN_CLIENT_QUERY_DEVICE_INFORMATION HwnClientQueryDeviceInformation;
    HWN_CLIENT_START_DEVICE HwnClientStartDevice;
    HWN_CLIENT_STOP_DEVICE HwnClientStopDevice;
    HWN_CLIENT_SET_STATE HwnClientSetState;
    HWN_CLIENT_GET_STATE HwnClientGetState;
    ```

3.  クライアントドライバーのエントリポイントである[*driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを実装し、初期化を行います。 ハードウェア通知クライアントドライバーでは、この関数は次の処理を行います。

    -   [**WDF\_driver\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdf_driver_config_init)を呼び出して、ドライバーの[**WDF\_driver\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/ns-wdfdriver-_wdf_driver_config)構造体を初期化します。

    -   [**Wdfdrivercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdrivercreate)を呼び出して、クライアントドライバーのフレームワークドライバーオブジェクトを作成します。

    -   クラス拡張によって使用されるコールバック関数ポインターを含む、 [**HWN\_クライアント\_登録\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/ns-hwnclx-_hwn_client_registration_packet)の内容を定義します。 必要なコールバック関数の詳細については、「[ハードウェア通知のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

    -   [HwNRegisterClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnregisterclient)を呼び出して、クライアントドライバーをクラス拡張に登録します。

4.  PnP マネージャーがデバイスの存在を報告したときにデバイスの初期化操作を実行するために、 [ *.evt\_WDF\_DRIVER\_デバイス\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)機能を実装します。 ハードウェア通知クライアントドライバーでは、この関数は次の処理を行います。

    -   [**HwNProcessAddDevicePreDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnprocessadddevicepredevicecreate)を呼び出しています。これは、kmdf がデバイスをさまざまな状態に移行するために必要なデバイス準備/リリースとエントリ/終了コールバックを提供します。

    -   [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、フレームワークデバイスオブジェクトを作成します。

    -   [**HwNProcessAddDevicePostDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nf-hwnclx-hwnprocessadddevicepostdevicecreate)を呼び出して、i/o キューを作成します。

5.  定義された[**HWN\_CLIENT\_INITIALIZE\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_initialize_device)関数を実装します。これは、ハードウェア通知コントローラーを使用するための準備として、クラス拡張によって呼び出されます。

6.  定義済みの[**HWN\_クライアント\_初期化解除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_uninitialize_device)関数を実装します。この関数は、ハードウェア通知コントローラーの初期設定を解除するためにクラス拡張によって呼び出されます。

7.  定義済みの[**HWN\_クライアント\_クエリ\_デバイス\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_query_device_information)関数を実装します。この関数は、クラス拡張機能によって呼び出されます。 この関数は、ハードウェア通知コンポーネントの属性を取得します。

8.  定義された[**HWN\_クライアント\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_start_device)関数を起動します。この関数は、クラス拡張機能によって呼び出されます。 この機能は、ハードウェア通知コントローラーを起動し、クライアントドライバーの ACPI リソースを割り当てる役割を担います。

9.  定義された[**HWN\_クライアント\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_stop_device) 、クラス拡張によって呼び出される\_デバイス関数の停止を実装します。 この機能は、ハードウェア通知コントローラーを停止し、クライアントドライバーによって使用される ACPI リソースを解放する役割を担います。

10. 定義された[**HWN\_クライアント\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_set_state)を実装します。この設定は、クラス拡張によって呼び出されます。 この機能は、ハードウェア通知コンポーネントの状態を設定する役割を担います。

11. 定義された[**HWN\_クライアント\_\_状態を取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hwnclx/nc-hwnclx-hwn_client_get_state)するように実装します。これは、クラス拡張によって呼び出されます。 この関数は、ハードウェア通知コンポーネントの現在の値を取得します。 入力バッファーが NULL の場合、つまりユーザーが特定のハードウェア通知状態を指定しなかった場合、この関数はすべてのハードウェア通知コンポーネントの状態情報を返す必要があります。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[ハードウェア通知](hardware-notifications-support.md)

[ハードウェア通知リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)



