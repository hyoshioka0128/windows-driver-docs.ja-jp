---
Description: トランスポートで UCSI 仕様を実装する UCSI クラスの拡張機能の動作を記述に依存しない方法です。
title: UCSI クライアント ドライバーを記述する
ms.date: 09/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 625212799bed9e6bec50495c7556736d8a6f20ad
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136129"
---
# <a name="write-a-ucsi-client-driver"></a>UCSI クライアント ドライバーを記述する

USB タイプ C コネクタ システム ソフトウェア インターフェイス (UCSI) ドライバーは、埋め込みコント ローラー (EC) を備えた USB 型-c システムのコント ローラーのドライバーとして機能します。

実装する場合、システムをプラットフォーム ポリシー マネージャー (PPM) UCSI 仕様」の説明に従って、EC 内に接続されているシステム上。

- ACPI トランスポート_いない_ドライバーを作成する必要があります。 (UcmUcsiCx.sys および UcmUcsiAcpiClient.sys)、Microsoft によって提供されるインボックス ドライバーを読み込みます。 (を参照してください[UCSI ドライバー](ucsi.md))。

- USB、PCI、I2C UART などの非 ACPI トランスポートでは、コント ローラーのクライアント ドライバーを記述する必要があります。

> USB タイプ-c ハードウェアが電力 (PD) の配信のステート マシンを処理する機能を持たない場合は、型-C# の USB ポートのコント ローラー ドライバーの作成を検討してください。 詳細については、[型-C# の USB ポート コント ローラー ドライバー](bring-up-a-usb-type-c-connector-on-a-windows-system.md)を参照してください。

以降では、Windows 10、バージョンは 1809、UCSI (UcmUcsiCx.sys) の新しいクラスの拡張機能が追加されました、UCSI 仕様を実装するトランスポートに依存しない方法です。 最小限のコードで、UcmUcsiCx へのクライアントであるドライバーが非 ACPI トランスポート経由で USB Type-C ハードウェアと通信できます。 このトピックでは、UCSI クラス拡張機能で提供されるサービスと、クライアント ドライバーの想定される動作について説明します。

**公式の仕様**
-   [UCSI の Intel BIOS の実装](https://go.microsoft.com/fwlink/p/?LinkId=760658)
-   [USB 3.1 と USB 型-C# の仕様](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [UCSI ドライバー](ucsi.md)

適用対象:

- Windows 10 Version 1809

**WDF のバージョン**

-   KMDF 1.27 のバージョン


**重要な API**

[UcmUcsiCx クラス拡張機能のリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

**サンプル**

[UcmUcsiCx クライアント ドライバーのサンプル](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmUcsiAcpiSample)

必須のバスの実装では、ACPI 部分を置き換えます。

## <a name="ucsi-class-extension-architecture"></a>UCSI クラスの拡張機能アーキテクチャ
UCSI クラスの拡張、UcmUcsiCx、非 ACPI のトランスポートを使用して、その埋め込みコント ローラーと通信するドライバーを作成することができます。 コント ローラー ドライバーは、UcmUcsiCx にクライアント ドライバーです。 UcmUcsiCx は、さらに、USB コネクタ マネージャー (UCM) にクライアントです。 そのため、UcmUcsiCx には、独自のポリシーの決定はすべてのことはありません。 代わりに、UCM によって提供されるポリシーを実装します。 UcmUcsiCx では、クライアント ドライバーからプラットフォーム ポリシー マネージャー (PPM) 通知の処理用にステート マシンを実装しより信頼性の高い問題の検出とエラー処理のことができます UCM ポリシーの決定を実装するためのコマンドを送信します。

![UCSI クラスの拡張機能アーキテクチャ](images/ucsicxarch.png)

**OS Policy Manager (OPM)**

UCSI 仕様」の説明に従って、OS ポリシー マネージャー (OPM) は PPM、対話するためのロジックを実装します。 OPM は責任を負います。

- UCM ポリシーに UCSI コマンドおよび UCSI 通知 UCM 通知に変換します。
- UCSI コマンドの PPM、エラー、および復旧メカニズムの検出を初期化するために必要な送信します。

**UCSI コマンドの処理** 

標準的な操作では、いくつかのコマンドを UCSI complicant ハードウェアによって完了する必要があります。 たとえば、GET_CONNECTOR_STATUS コマンドについて考えてみましょう。

1. PPM ファームウェア UcmUcsiCx/クライアント ドライバーに接続の変更通知を送信します。
2. 応答では、UcmUcsiCx/クライアント ドライバーは、PPM ファームウェアに GET_CONNECTOR_STATUS コマンドを送信します。  
3. PPM ファームウェアは GET_CONNECTOR_STATUS を実行し、非同期的に UcmUcsiCx/クライアント ドライバーにコマンドの完了通知を送信します。 通知にはに関するデータが含まれている状態を実際に接続します。
4. UcmUcsiCx/クライアント ドライバーでは、その状態情報を処理し、ACK_CC_CI を PPM ファームウェアに送信します。
5. PPM ファームウェアは ACK_CC_CI を実行し、非同期的に UcmUcsiCx/クライアント ドライバーにコマンドの完了通知を送信します。
6. UcmUcsiCx/クライアント ドライバーでは、GET_CONNECTOR_STATUS コマンドが完了すると見なします。

**プラットフォーム ポリシー マネージャー (PPM) との通信**

UcmUcsiCx は OPM から PPM ファームウェアに UCSI コマンドを送信して、PPM ファームウェアから通知を受信の詳細を抽象化します。 WDFREQUEST オブジェクトへの PPM コマンドを変換し、クライアント ドライバーに転送します。

- PPM 通知

    クライアント ドライバーでは、ファームウェアの PPM 通知に関する UcmUcsiCx を通知します。 ドライバーは、CCI を含む UCSI データ ブロックを提供します。 UcmUcsiCx は、OPM やデータに基づく適切なアクションを実行する他のコンポーネントに通知を転送します。

- クライアント ドライバーに Ioctl

    UcmUcsiCx は、PPM ファームウェアに送信するクライアント ドライバー (IOCTL 要求) を通じて UCSI コマンドを送信します。 ドライバーは、ファームウェアに UCSI のコマンドは、送信後に、要求を完了します。


**電源の移行の処理**

クライアント ドライバーは、電源ポリシー所有者です。  

場合は、クライアント ドライバーが Dx 状態に入る S0 アイドル状態のため、WDF は、UcmUcsiCx 送信すると、クライアント ドライバーの電源管理対象のキューに UCSI コマンドを含む IOCTL D0 にドライバーをもたらします。 S0 アイドル状態で、クライアント ドライバーは、S0 アイドル状態の PPM 通知が引き続き有効であるため、ファームウェアの PPM 通知がある場合に、電源の状態を再入力する必要があります。  

## <a name="before-you-begin"></a>開始する前にしています.

-   によって、ハードウェアまたはファームウェア PD ステート マシン、およびトランスポートを実装するかどうかを記述する必要があるドライバーの種類を決定します。

    ![適切なクラスの拡張機能を選択するための意思決定](images/drivers-c.png)詳細については、[型-C# の USB コネクタ用の開発の Windows ドライバー](developing-windows-drivers-for-usb-type-c-connectors.md)を参照してください。  

-   デスクトップ エディション (Home、Pro、Enterprise、および教育機関向け) の場合は、Windows 10 をインストールします。

-   [インストール](https://developer.microsoft.com/windows/hardware/windows-driver-kit)開発用コンピューターに最新 Windows Driver Kit (WDK)。 このキットが必要なヘッダー ファイルとライブラリを具体的には、クライアント ドライバーを記述するため、必要があります。

    -   スタブ ライブラリは、(UcmUcsiCxStub.lib)。 ライブラリでは、クライアント ドライバーによって行われた呼び出しを変換し、クラスの拡張機能に渡します。
    -   ヘッダー ファイルでは、Ucmucsicx.h します。
    - クライアント ドライバーでは、カーネル モードで実行され、KMDF 1.27 ライブラリにバインドします。

-   Windows Driver Foundation (WDF) を理解します。 参考資料。[Windows Driver Foundation でのドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)少額 Orwick と Guy Smith によって書き込まれた、します。

## <a name="1-register-your-client-driver-with-ucmucsicx"></a>1.UcmUcsiCx をクライアント ドライバーに登録します。

[ **EVT_WDF_DRIVER_DEVICE_ADD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)の実装 

1. 設定した後、プラグ アンド プレイと電源管理イベントのコールバック関数 ([**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks))、呼び出す[ **UcmUcsiDeviceInitInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitinitialize)初期化するために、 [ **WDFDEVICE_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)非透過構造体。 呼び出しは、クライアント ドライバーをフレームワークに関連付けます。

2. Framework デバイス オブジェクト (WDFDEVICE) を作成すると、呼び出す[ **UcmUcsiDeviceInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsidevice/nf-ucmucsidevice-ucmucsideviceinitialize.md) UcmUcsiCx クライアント ドライバーに登録します。

## <a name="2-create-the-ppm-object-with-ucmucsicx"></a>2.UcmUcsiCx で PPM オブジェクトを作成します。

実装で[ **EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)、生と翻訳されたリソースの一覧を受信した後、リソースを使用して、ハードウェアを準備します。 たとえば、トランスポートが I2C の場合は、通信チャネルを開くためのハードウェア リソースを読み取り。 次に、PPM オブジェクトを作成します。 オブジェクトを作成するには、特定の構成オプションを設定する必要があります。

1. デバイス上には、コネクタのコレクションを識別するハンドルを提供します。 
   1. コネクタのコレクションを呼び出すことによって作成[ **UcmUcsiConnectorCollectionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectioncreate)します。
   2. デバイスのコネクタを列挙し、呼び出すことによって、コレクションに追加[ **UcmUcsiConnectorCollectionAddConnector**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsiconnectorcollectionaddconnector)

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
2. デバイス コント ローラーを有効にするかどうかを決定します。

3. 構成し、PPM オブジェクトを作成します。
   1. 初期化を[ **UCMUCSI_PPM_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/ns-ucmucsippm-_ucmucsi_ppm_config)手順 1 で作成したコネクタのハンドルを提供することで、構造体。
   2. 設定**UsbDeviceControllerEnabled**メンバーを手順 2. で決定するブール値。
   3. WDF_OBJECT_ATTRIBUTES でイベントのコールバックを設定します。
   4. 呼び出す[ **UcmUcsiPpmCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmcreate)で構成されているすべての構造体の受け渡し。

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
      ## <a name="3-set-up-io-queues"></a>3.IO キューを設定します。

UcmUcsiCx は、PPM ファームウェアに送信するクライアント ドライバーに UCSI コマンドを送信します。 コマンドは、WDF キュー内のこれらの IOCTL 要求の形式で送信されます。

-  [IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)
-  [IOCTL_UCMUCSI_PPM_GET_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_get_ucsi_data_block)

クライアント ドライバーは、作成して呼び出すことによって UcmUcsiCx にそのキューを登録する責任を負います[ **UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)します。 キューは、電源管理対象にする必要があります。

あること多くて 1 つの未処理の要求、WDF キューで UcmUcsiCx が保証されます。 クライアント ドライバーも担当のファームウェアに UCSI のコマンドは、送信後、WDF 要求を完了します。

キューの実装でのドライバーを設定する通常[ **EVT_WDF_DEVICE_PREPARE_HARDWARE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)します。

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

また、クライアント ドライバーを呼び出す必要がありますも[ **UcmUcsiPpmStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmstart)ドライバーが、IOCTL を受信する準備が UcmUcsiCx に通知を要求します。  その呼び出しを行うことをお勧めで[ **EVT_WDF_DEVICE_PREPARE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)を通じて、コマンドの受信 UCSI WDFQUEUE ハンドルを作成した後[ **UcmUcsiPpmSetUcsiCommandRequestQueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmsetucsicommandrequestqueue)します。
逆に、要求を処理する場合は、ドライバーは、呼び出す必要があります[ **UcmUcsiPpmStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmstop)します。 これは、 [ **EVT_WDF_DEVICE_RELEASE_HARDWARE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)実装します。

## <a name="4-handle-the-ioctl-requests"></a>4.IOCTL 要求を処理します。

USB タイプ-c パートナーがコネクタに接続されているときに発生するこの例一連のイベントを検討してください。

1. PPM ファームウェアでは、添付イベントを決定し、クライアント ドライバーに通知を送信します。
2. クライアント ドライバー呼び出し[ **UcmUcsiPpmNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippm/nf-ucmucsippm-ucmucsippmnotification) UcmUcsiCx にその通知を送信します。
3. UcmUcsiCx notfies OPM ステート マシンと UcmUcsiCx にコネクタの状態の取得コマンドを送信します。
4. 要求を作成し、UcmUcsiCx [IOCTL_UCMUCSI_PPM_SEND_UCSI_DATA_BLOCK](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ucmucsippmrequests/ni-ucmucsippmrequests-ioctl_ucmucsi_ppm_send_ucsi_data_block)クライアント ドライバーにします。
5. クライアント ドライバーでは、その要求を処理し、PPM ファームウェアにコマンドを送信します。 ドライバーは、この要求を非同期的に完了して、UcmUcsiCx を別の通知を送信します。
6. コマンドが正常に完了の通知では、OPM ステート マシンは (コネクタの状態情報を含む) ペイロードを読み取るし、種類 C の UCM 添付イベントを通知します。

この例で、ファームウェア、ポート、パートナーとの間電源配信ネゴシエーションのステータスの変更が成功したことをペイロードも表示されます。 OPM ステート マシンは、別の UCSI コマンドを送信します。Pdo を取得します。
コネクタの状態の取得のコマンドを取得 Pdo コマンドが正常に終了したときと同様に、OPM ステート マシンは、このイベントの UCM を通知します。

クライアント ドライバーのハンドラーを[EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)は次のコード例に似ています。 要求の処理方法の詳細については、次を参照してください[要求ハンドラー。](https://docs.microsoft.com/windows-hardware/drivers/wdf/request-handlers)

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
