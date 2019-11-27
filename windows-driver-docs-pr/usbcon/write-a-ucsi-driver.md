---
Description: トランスポートに依存しない方法で UCSI 仕様を実装する UCSI クラス拡張の動作について説明します。
title: UCSI クライアント ドライバーを記述する
ms.date: 09/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: b059d03672d8c08d894229997d3b31239bd95971
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841680"
---
# <a name="write-a-ucsi-client-driver"></a>UCSI クライアント ドライバーを記述する

USB タイプ c コネクタシステムソフトウェアインターフェイス (UCSI) ドライバーは、埋め込みコントローラー (EC) を備えた USB タイプ C システムのコントローラードライバーとして機能します。

次のようにシステムに接続されている EC で、UCSI 仕様で説明されているプラットフォームポリシーマネージャー (PPM) を実装しているシステムの場合:

- ACPI トランスポートでは、ドライバーを作成する必要はあり_ません_。 Microsoft が提供するインボックスドライバー (UcmUcsiCx および UcmUcsiAcpiClient) を読み込みます。 (「 [Ucsi ドライバー](ucsi.md)」を参照してください)。

- USB、PCI、I2C、UART などの非 ACPI トランスポートでは、コントローラーのクライアントドライバーを書き込む必要があります。

> USB タイプ C ハードウェアに電力配信 (PD) のステートマシンを処理する機能がない場合は、USB タイプの C ポートコントローラードライバーを記述することを検討してください。 詳細については、「 [Write a USB Type-C port controller driver](bring-up-a-usb-type-c-connector-on-a-windows-system.md)」を参照してください。

Windows 10 バージョン1809以降では、UCSI (UcmUcsiCx) の新しいクラス拡張が追加されました。これにより、トランスポートに依存しない方法で UCSI 仕様が実装されます。 最小限のコードで、UcmUcsiCx へのクライアントであるドライバーが非 ACPI トランスポート経由で USB Type-C ハードウェアと通信できます。 このトピックでは、UCSI クラス拡張機能で提供されるサービスと、クライアント ドライバーの想定される動作について説明します。

**公式の仕様**
-   [UCSI の Intel BIOS 実装](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 3.1 および USB タイプ-C 仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [UCSI ドライバー](ucsi.md)

適用対象:

- Windows 10 Version 1809

**WDF のバージョン**

-   KMDF バージョン1.27


**重要な API**

[UcmUcsiCx クラス拡張機能のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

**サンプル**

[UcmUcsiCx クライアント ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

ACPI 部分を、必要なバスの実装に置き換えます。

## <a name="ucsi-class-extension-architecture"></a>UCSI クラス拡張アーキテクチャ
UCSI クラス拡張、UcmUcsiCx では、非 ACPI トランスポートを使用して、埋め込みコントローラーと通信するドライバーを記述できます。 コントローラードライバーは、UcmUcsiCx するクライアントドライバーです。 UcmUcsiCx は、クライアントを USB コネクタマネージャー (UCM) に変換します。 そのため、UcmUcsiCx は独自のポリシー決定を行いません。 代わりに、UCM によって提供されるポリシーを実装します。 UcmUcsiCx は、クライアントドライバーからのプラットフォームポリシーマネージャー (PPM) 通知を処理するためのステートマシンを実装し、UCM ポリシーの決定を実装するコマンドを送信して、より信頼性の高い問題の検出とエラー処理を可能にします。

![UCSI クラス拡張アーキテクチャ](images/ucsicxarch.png)

**OS ポリシーマネージャー (OPM)**

OS ポリシーマネージャー (OPM) は、UCSI 仕様で説明されているように、PPM と対話するためのロジックを実装します。 OPM の責任は次のとおりです。

- UCM ポリシーを UCSI コマンドに変換し、UCM 通知に UCSI 通知を変換します。
- PPM の初期化、エラーの検出、および復旧のメカニズムに必要な UCSI コマンドを送信しています。

**UCSI コマンドの処理** 

一般的な操作には、UCSI-complicant ハードウェアによって実行されるいくつかのコマンドが含まれます。 たとえば、GET_CONNECTOR_STATUS のコマンドを考えてみましょう。

1. PPM ファームウェアは、connect 変更通知を UcmUcsiCx/client ドライバーに送信します。
2. 応答として、UcmUcsiCx/クライアントドライバーは、GET_CONNECTOR_STATUS コマンドを PPM ファームウェアに送り返します。  
3. PPM ファームウェアは GET_CONNECTOR_STATUS を実行し、コマンド完了通知を非同期的に UcmUcsiCx/クライアントドライバーに送信します。 この通知には、実際の接続状態に関するデータが含まれています。
4. UcmUcsiCx/client ドライバーは、その状態情報を処理し、PPM ファームウェアに ACK_CC_CI を送信します。
5. PPM ファームウェアは ACK_CC_CI を実行し、コマンド完了通知を非同期的に UcmUcsiCx/クライアントドライバーに送信します。
6. UcmUcsiCx/client ドライバーは、GET_CONNECTOR_STATUS コマンドが完了したと見なします。

**プラットフォームポリシーマネージャー (PPM) との通信**

UcmUcsiCx は、OPM から PPM ファームウェアへの UCSI コマンドの送信と、PPM ファームウェアからの通知の受信の詳細を抽象化します。 PPM コマンドを WDFREQUEST オブジェクトに変換し、クライアントドライバーに転送します。

- PPM の通知

    クライアントドライバーは、ファームウェアからの PPM の通知について UcmUcsiCx に通知します。 このドライバーは、CCI を含む UCSI データブロックを提供します。 UcmUcsiCx は、データに基づいて適切なアクションを実行する OPM およびその他のコンポーネントに通知を転送します。

- クライアントドライバーへの Ioctl

    UcmUcsiCx は、(IOCTL 要求を介して) UCSI コマンドをクライアントドライバーに送信して、PPM ファームウェアに送信します。 ドライバーは、UCSI コマンドをファームウェアに送信した後に、要求を完了する役割を担います。


**電源遷移の処理**

クライアントドライバーは、電源ポリシーの所有者です。  

S0 がアイドル状態になったためにクライアントドライバーが Dx 状態になると、WDF は、UcmUcsiCx が UCSI コマンドを含む IOCTL をクライアントドライバーの電源管理キューに送信するときに、ドライバーを D0 にします。 S0 がアイドル状態の場合、PPM の通知が引き続き有効になっているため、ファームウェアから PPM の通知がある場合は、S0 のクライアントドライバーが電源状態に再入力する必要があります。  

## <a name="before-you-begin"></a>開始する前に...

-   ハードウェアまたはファームウェアが PD ステートマシンとトランスポートのどちらを実装しているかに応じて、書き込む必要があるドライバーの種類を決定します。

    正しいクラス拡張機能を選択するかどうかを判断 ![には](images/drivers-c.png) 「 [USB タイプ-C コネクタ用の Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)」を参照してください。  

-   デスクトップエディション (Home、Pro、Enterprise、および教育) 用の Windows 10 をインストールします。

-   開発用コンピューターに最新の Windows Driver Kit (WDK) を[インストール](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)します。 キットには、クライアントドライバーを記述するために必要なヘッダーファイルとライブラリが用意されています。具体的には、次のものが必要です。

    -   スタブライブラリ (UcmUcsiCxStub)。 ライブラリは、クライアントドライバーによって行われた呼び出しを変換し、クラス拡張に渡します。
    -   ヘッダーファイル Ucmucsicx。
    - クライアントドライバーはカーネルモードで実行され、KMDF 1.27 ライブラリにバインドされます。

-   Windows Driver Foundation (WDF) について理解を深めます。 推奨される読み取り: 小額 Orwick および Guy Smith によって作成され[た Windows Driver Foundation を使用したドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)。

## <a name="1-register-your-client-driver-with-ucmucsicx"></a>1. クライアントドライバーを UcmUcsiCx に登録します。

[**EVT_WDF_DRIVER_DEVICE_ADD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)の実装では、 

1. プラグアンドプレイと電源管理のイベントコールバック関数 ([**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)) を設定した後、 [**UcmUcsiDeviceInitInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitinitialize)を呼び出して、不透明な構造体を[**WDFDEVICE_INIT**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)初期化します。 この呼び出しにより、クライアントドライバーがフレームワークに関連付けられます。

2. フレームワークデバイスオブジェクト (WDFDEVICE) を作成した後、 [**UcmUcsiDeviceInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitialize.md)を呼び出して、UcmUcsiCx にクライアントのダイバーを登録します。

## <a name="2-create-the-ppm-object-with-ucmucsicx"></a>2. UcmUcsiCx を使用して PPM オブジェクトを作成する

[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)の実装では、生のリソースと変換されたリソースの一覧を受け取ったら、リソースを使用してハードウェアを準備します。 たとえば、トランスポートが I2C の場合は、ハードウェアリソースを読み取り、通信チャネルを開きます。 次に、PPM オブジェクトを作成します。 オブジェクトを作成するには、特定の構成オプションを設定する必要があります。

1. デバイス上のコネクタコレクションへのハンドルを指定します。 
   1. [**UcmUcsiConnectorCollectionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectioncreate)を呼び出して、コネクタコレクションを作成します。
   2. UcmUcsiConnectorCollectionAddConnector を呼び出して、デバイス上のコネクタを列挙し、コレクションに追加します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectionaddconnector)

      ```cpp
      // Create the connector collection.

      UCMUCSI_CONNECTOR_COLLECTION* ConnectorCollectionHandle;

      status = UcmUcsiConnectorCollectionCreate(Device, //WDFDevice
               WDF_NO_OBJECT_ATTRIBUTES,
               ConnectorCollectionHandle);

      // Enumerate the connectors on the device.
      // ConnectorId of 0 is reserved for the parent device.
      // In this example, we assume the parent has no children connectors.

      UCMUCSI_CONNECTOR_INFO_INIT(&connectorInfo);
      connectorInfo.ConnectorId = 0;

      status = UcmUcsiConnectorCollectionAddConnector ( &ConnectorCollectionHandle,
                   &connectorInfo);
      ```
2. デバイスコントローラーを有効にするかどうかを決定します。

3. PPM オブジェクトを構成して作成します。
   1. 手順 1. で作成したコネクタハンドルを指定して、 [**UCMUCSI_PPM_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/ns-ucmucsippm-_ucmucsi_ppm_config)構造体を初期化します。
   2. **UsbDeviceControllerEnabled**メンバーを、手順 2. で決定したブール値に設定します。
   3. WDF_OBJECT_ATTRIBUTES でイベントコールバックを設定します。
   4. 構成されているすべての構造体を渡して[**UcmUcsiPpmCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmcreate)を呼び出します。

      ```cpp
      UCMUCSIPPM ppmObject = WDF_NO_HANDLE;
      PUCMUCSI_PPM_CONFIG UcsiPpmConfig;
      WDF_OBJECT_ATTRIBUTES attrib;

      UCMUCSI_PPM_CONFIG_INIT(UcsiPpmConfig, ConnectorCollectionHandle);

      UcsiPpmConfig->UsbDeviceControllerEnabled = TRUE;

      WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attrib, Ppm);
      attrib->EvtDestroyCallback = &EvtObjectContextDestroy;

      status = UcmUcsiPpmCreate(wdfDevice, UcsiPpmConfig, &attrib, &ppmObject);
      ```
      ## <a name="3-set-up-io-queues"></a>3. IO キューを設定する

UcmUcsiCx は、PPM のファームウェアに送信するために、UCSI コマンドをクライアントドライバーに送信します。 これらのコマンドは、これらの IOCTL 要求の形式で WDF キューに送信されます。

-  [IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)
-  [IOCTL_UCMUCSI_PPM_GET_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_get_ucsi_data_block)

クライアントドライバーは、 [**UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)を呼び出して、そのキューを作成し、UcmUcsiCx に登録する役割を担います。 キューは、電源管理されている必要があります。

UcmUcsiCx は、WDF キューに未処理の要求が1つだけ存在することを保証します。 クライアントドライバーは、UCSI コマンドをファームウェアに送信した後に、WDF 要求を完了する役割も担います。

通常、ドライバーは[**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)の実装にキューを設定します。

```cpp
WDFQUEUE UcsiCommandRequestQueue = WDF_NO_HANDLE;
WDF_OBJECT_ATTRIBUTES attrib;
WDF_IO_QUEUE_CONFIG queueConfig;

WDF_OBJECT_ATTRIBUTES_INIT(&attrib);
attrib.ParentObject = GetObjectHandle();

// In this example, even though the driver creates a sequential queue, 
// UcmUcsiCx guarantees that will not send another request 
// until the previous one has been completed.


WDF_IO_QUEUE_CONFIG_INIT(&queueConfig, WdfIoQueueDispatchSequential);

// The queue must be power-managed.

queueConfig.PowerManaged = WdfTrue;
queueConfig.EvtIoDeviceControl = EvtIoDeviceControl;

status = WdfIoQueueCreate(device, &queueConfig, &attrib, &UcsiCommandRequestQueue);

UcmUcsiPpmSetUcsiCommandRequestQueue(ppmObject, UcsiCommandRequestQueue);
```

また、クライアントドライバーは、 [**UcmUcsiPpmStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmstart)を呼び出して、ドライバーが IOCTL 要求を受信する準備ができていることを UcmUcsiCx に通知する必要もあります。  [**UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)を使用して、ucsi コマンドを受け取るための WDFQUEUE ハンドルを作成した後で、 [**EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)でその呼び出しを行うことをお勧めします。
逆に、ドライバーが他の要求を処理したくない場合は、 [**UcmUcsiPpmStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmstop)を呼び出す必要があります。 これは[**EVT_WDF_DEVICE_RELEASE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)の実装に含まれています。

## <a name="4-handle-the-ioctl-requests"></a>4. IOCTL 要求を処理する

USB タイプ C パートナーがコネクタに接続されている場合に発生するイベントのシーケンス例を考えてみましょう。

1. PPM ファームウェアによって添付イベントが特定され、クライアントドライバーに通知が送信されます。
2. クライアントドライバーは、 [**UcmUcsiPpmNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippm/nf-ucmucsippm-ucmucsippmnotification)を呼び出して、その通知を UcmUcsiCx に送信します。
3. UcmUcsiCx notfies OPM state machine; Get Connector Status コマンドを UcmUcsiCx に送信します。
4. UcmUcsiCx は要求を作成し、 [IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)をクライアントドライバーに送信します。
5. クライアントドライバーはその要求を処理し、コマンドを PPM ファームウェアに送信します。 ドライバーはこの要求を非同期に完了し、別の通知を UcmUcsiCx に送信します。
6. コマンドの完了通知が成功すると、OPM ステートマシンは、(コネクタステータス情報を含む) ペイロードを読み取り、タイプ C attach イベントの UCM に通知します。

この例では、ペイロードは、ファームウェアとポートパートナー間の電力配信ネゴシエーション状態の変更が成功したことを示しています。 OPM ステートマシンが別の UCSI コマンドを送信します: Get PDOs。
Get the Connector Status コマンドと同様に、Get PDOs コマンドが正常に完了すると、OPM ステートマシンはこのイベントの UCM に通知します。

クライアントドライバーの[EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)のハンドラーは、次のコード例のようになります。 要求の処理の詳細については、「[要求ハンドラー](https://docs.microsoft.com/windows-hardware/drivers/wdf/request-handlers) 」を参照してください。

```cpp
void EvtIoDeviceControl(
    _In_ WDFREQUEST Request,
    _In_ ULONG IoControlCode
    )
{
...
    switch (IoControlCode)
    {
    case IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK:
        EvtSendData(Request);
        break;

    case IOCTL_UCMUCSI_PPM_GET_UCSI_DATA_BLOCK:
        EvtReceiveData(Request);
        break;

    default:
        status = STATUS_NOT_SUPPORTED;
        goto Exit;
    }

    status = STATUS_SUCCESS;

Exit:

    if (!NT_SUCCESS(status))
    {
        WdfRequestComplete(Request, status);
    }

}

VOID EvtSendData(
    WDFREQUEST Request
    )
{
    NTSTATUS status;
    PUCMUCSI_PPM_SEND_UCSI_DATA_BLOCK_IN_PARAMS inParams;

    status = WdfRequestRetrieveInputBuffer(Request, sizeof(*inParams),
        reinterpret_cast<PVOID*>(&inParams), nullptr);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    // Build a UCSI command request and send to the PPM firmware.

Exit:
    WdfRequestComplete(Request, status);
}

VOID EvtReceiveData(
    WDFREQUEST Request
    )
{

    NTSTATUS status;

    PUCMUCSI_PPM_GET_UCSI_DATA_BLOCK_IN_PARAMS inParams;
    PUCMUCSI_PPM_GET_UCSI_DATA_BLOCK_OUT_PARAMS outParams;

    status = WdfRequestRetrieveInputBuffer(Request, sizeof(*inParams),
        reinterpret_cast<PVOID*>(&inParams), nullptr);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    status = WdfRequestRetrieveOutputBuffer(Request, sizeof(*outParams),
        reinterpret_cast<PVOID*>(&outParams), nullptr);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    // Receive data from the PPM firmware.
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }
    WdfRequestSetInformation(Request, sizeof(*outParams));

Exit:
    WdfRequestComplete(Request, status);
}
```
