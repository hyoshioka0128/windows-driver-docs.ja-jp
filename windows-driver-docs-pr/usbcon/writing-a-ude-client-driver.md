---
Description: USB デバイス Emulation(UDE) クラスの拡張機能と、クライアント ドライバーが、エミュレートされたホストのコント ローラーとそれに接続されたデバイスに対して実行する必要がありますタスクの動作について説明します。
title: UDE クライアント ドライバーを記述する
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: e06d4acd349f1d132975032c9a4a76bac1e07d93
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366496"
---
# <a name="write-a-ude-client-driver"></a>UDE クライアント ドライバーを記述する

**要約**

- UDE オブジェクトとクラスの拡張機能とクライアント ドライバーによって使用されるハンドル。
- コント ローラーの機能のクエリを実行して、コント ローラーをリセットする機能をエミュレートされたホスト コント ローラーを作成します。
- 電源管理とデータのために設定すると仮想の USB デバイスの作成は、エンドポイントを介して転送します。

**適用対象:**

- Windows 10

**最終更新日。**

- 2015 年 11 月

**重要な API**

- [エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))

USB デバイス Emulation(UDE) クラスの拡張機能と、クライアント ドライバーが、エミュレートされたホストのコント ローラーとそれに接続されたデバイスに対して実行する必要がありますタスクの動作について説明します。 ルーチンとコールバック関数のセットを通じてそれぞれのクラス ドライバーとクラスの拡張機能の通信方法に関する情報を提供します。 機能についても説明を実装するために、クライアント ドライバーが必要です。

## <a name="before-you-begin"></a>始める前に

- [インストール](https://go.microsoft.com/fwlink/p/?LinkID=733614)最新 Windows Driver Kit (WDK)、開発用コンピューター。 このキットが必要なヘッダー ファイルとライブラリを具体的には、UDE クライアント ドライバーを記述するため、必要があります。
  - スタブ ライブラリは、(Udecxstub.lib)。 ライブラリは、クライアント ドライバーによって行われた呼び出しを変換し、UdeCx まで渡したりします。
  - ヘッダー ファイルでは、Udecx.h します。
- Windows 10 をターゲット コンピューターにインストールします。
- UDE の把握します。 参照してください[アーキテクチャ。USB デバイス Emulation(UDE)](usb-emulated-device--ude--architecture.md)します。
- Windows Driver Foundation (WDF) を理解します。 参考資料。[Windows Driver Foundation でのドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)少額 Orwick と Guy Smith によって書き込まれた、します。

## <a name="ude-objects-and-handles"></a>UDE オブジェクトとハンドル

UDE クラスの拡張機能と、クライアント ドライバーは、エミュレートされたホスト コント ローラーとそのエンドポイントと、デバイスとホスト間のデータ転送に使用する翻訳を含む、仮想デバイスを表す特定の WDF オブジェクトを使用します。 クライアント ドライバーは、オブジェクトの作成を要求し、クラスの拡張機能によって、オブジェクトの有効期間を管理します。

- **エミュレートされたホスト コント ローラーのオブジェクト (WDFDEVICE)**

    エミュレートされたホスト コント ローラーを表し、UDE クラスの拡張機能と、クライアント ドライバーとの間の主要なハンドルです。

- **UDE デバイス オブジェクト (UDECXUSBDEVICE)**

    エミュレートされたホスト コント ローラー上のポートに接続されている仮想の USB デバイスを表します。

- **UDE エンドポイント オブジェクト (UDECXUSBENDPOINT)**

    USB デバイスのパイプをシーケンシャルにデータを表します。 ソフトウェアの要求を送信または受信エンドポイントでのデータを受信するために使用します。

## <a name="initialize-the-emulated-host-controller"></a>エミュレートされたホスト コント ローラーを初期化します。

クライアント ドライバーが、エミュレートされたホスト コント ローラーの WDFDEVICE ハンドルを取得するシーケンスの概要を次に示します。 ドライバーがこれらのタスクを実行することをお勧めします。 その[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

1. 呼び出す[ **UdecxInitializeWdfDeviceInit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxinitializewdfdeviceinit)への参照を渡すことによって[WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)フレームワークによって渡されます。
2. 初期化、 [WDFDEVICE\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)このデバイスが他の USB ホスト コント ローラーに似ていますが表示されるようにセットアップ情報を含む構造体します。 たとえば、FDO 名とシンボリック リンクを割り当て、Microsoft から提供された GUID を持つデバイスのインターフェイスを登録\_DEVINTERFACE\_USB\_ホスト\_デバイス インターフェイスの GUID としてコント ローラーの GUID をアプリケーションでは、デバイスを識別するハンドルを開くことができます。
3. 呼び出す[ **WdfDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdevicecreate) framework デバイス オブジェクトを作成します。
4. 呼び出す[ **UdecxWdfDeviceAddUsbDeviceEmulation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)し、クライアント ドライバーのコールバック関数を登録します。

    ここでは、ホスト コント ローラーのオブジェクトに関連付けられている UDE クラスの拡張機能によって呼び出されるコールバック関数です。 クライアント ドライバーでは、これらの関数を実装する必要があります。

    [*EVT\_UDECX\_WDF\_デバイス\_クエリ\_USB\_機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)  
    クライアント ドライバーは、クラスの拡張機能に報告する必要があります、ホスト コント ローラーでサポートされている機能を決定します。

    [*EVT\_UDECX\_WDF\_デバイス\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)  
    (省略可能)。 ホスト コント ローラーや接続されたデバイスをリセットします。

    ```cpp

    EVT_WDF_DRIVER_DEVICE_ADD                 Controller_WdfEvtDeviceAdd;

    #define BASE_DEVICE_NAME                  L"\\Device\\USBFDO-"
    #define BASE_SYMBOLIC_LINK_NAME           L"\\DosDevices\\HCD"

    #define DeviceNameSize                    sizeof(BASE_DEVICE_NAME)+MAX_SUFFIX_SIZE
    #define SymLinkNameSize                   sizeof(BASE_SYMBOLIC_LINK_NAME)+MAX_SUFFIX_SIZE

    NTSTATUS
    Controller_WdfEvtDeviceAdd(
        _In_
            WDFDRIVER Driver,
        _Inout_
            PWDFDEVICE_INIT WdfDeviceInit
        )
    {
        NTSTATUS                            status;
        WDFDEVICE                           wdfDevice;
        WDF_PNPPOWER_EVENT_CALLBACKS        wdfPnpPowerCallbacks;
        WDF_OBJECT_ATTRIBUTES               wdfDeviceAttributes;
        WDF_OBJECT_ATTRIBUTES               wdfRequestAttributes;
        UDECX_WDF_DEVICE_CONFIG             controllerConfig;
        WDF_FILEOBJECT_CONFIG               fileConfig;
        PWDFDEVICE_CONTEXT                  pControllerContext;
        WDF_IO_QUEUE_CONFIG                 defaultQueueConfig;
        WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS
                                            idleSettings;
        UNICODE_STRING                      refString;
        ULONG instanceNumber;
        BOOLEAN isCreated;

        DECLARE_UNICODE_STRING_SIZE(uniDeviceName, DeviceNameSize);
        DECLARE_UNICODE_STRING_SIZE(uniSymLinkName, SymLinkNameSize);

        UNREFERENCED_PARAMETER(Driver);

        ...

        WdfDeviceInitSetPnpPowerEventCallbacks(WdfDeviceInit, &wdfPnpPowerCallbacks);

        WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&wdfRequestAttributes, REQUEST_CONTEXT);
        WdfDeviceInitSetRequestAttributes(WdfDeviceInit, &wdfRequestAttributes);



    // To distinguish I/O sent to GUID_DEVINTERFACE_USB_HOST_CONTROLLER, we will enable
    // enable interface reference strings by calling WdfDeviceInitSetFileObjectConfig
    // with FileObjectClass WdfFileObjectWdfXxx.

    WDF_FILEOBJECT_CONFIG_INIT(&fileConfig,
                                WDF_NO_EVENT_CALLBACK,
                                WDF_NO_EVENT_CALLBACK,
                                WDF_NO_EVENT_CALLBACK // No cleanup callback function
                                );

    ...

    WdfDeviceInitSetFileObjectConfig(WdfDeviceInit,
                                        &fileConfig,
                                        WDF_NO_OBJECT_ATTRIBUTES);

    ...

    // Do additional setup required for USB controllers.

    status = UdecxInitializeWdfDeviceInit(WdfDeviceInit);

    ...

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&wdfDeviceAttributes, WDFDEVICE_CONTEXT);
    wdfDeviceAttributes.EvtCleanupCallback = _ControllerWdfEvtCleanupCallback;


    // Call WdfDeviceCreate with a few extra compatibility steps to ensure this device looks
    // exactly like other USB host controllers.


    isCreated = FALSE;

    for (instanceNumber = 0; instanceNumber < ULONG_MAX; instanceNumber++) {

        status = RtlUnicodeStringPrintf(&uniDeviceName,
                                        L"%ws%d",
                                        BASE_DEVICE_NAME,
                                        instanceNumber);

        ...

        status = WdfDeviceInitAssignName(*WdfDeviceInit, &uniDeviceName);

        ...

        status = WdfDeviceCreate(WdfDeviceInit, WdfDeviceAttributes, WdfDevice);

        if (status == STATUS_OBJECT_NAME_COLLISION) {


            // This is expected to happen at least once when another USB host controller
            // already exists on the system.

        ...

        } else if (!NT_SUCCESS(status)) {

        ...

        } else {

            isCreated = TRUE;
            break;
        }
    }

    if (!isCreated) {

        ...
    }


    // Create the symbolic link (also for compatibility).
    status = RtlUnicodeStringPrintf(&uniSymLinkName,
                                    L"%ws%d",
                                    BASE_SYMBOLIC_LINK_NAME,
                                    instanceNumber);
    ...

    status = WdfDeviceCreateSymbolicLink(*WdfDevice, &uniSymLinkName);

    ...

    // Create the device interface.

    RtlInitUnicodeString(&refString,
                         USB_HOST_DEVINTERFACE_REF_STRING);

    status = WdfDeviceCreateDeviceInterface(wdfDevice,
                                            (LPGUID)&GUID_DEVINTERFACE_USB_HOST_CONTROLLER,
                                            &refString);

    ...

    UDECX_WDF_DEVICE_CONFIG_INIT(&controllerConfig, Controller_EvtUdecxWdfDeviceQueryUsbCapability);

    status = UdecxWdfDeviceAddUsbDeviceEmulation(wdfDevice,
                                               &controllerConfig);


    // Create default queue. It only supports USB controller IOCTLs. (USB I/O will come through
    // in separate USB device queues.)
    // Shown later in this topic.

    WDF_IO_QUEUE_CONFIG_INIT_DEFAULT_QUEUE(&defaultQueueConfig, WdfIoQueueDispatchSequential);
    defaultQueueConfig.EvtIoDeviceControl = ControllerEvtIoDeviceControl;
    defaultQueueConfig.PowerManaged = WdfFalse;

    status = WdfIoQueueCreate(wdfDevice,
                              &defaultQueueConfig,
                              WDF_NO_OBJECT_ATTRIBUTES,
                              &pControllerContext->DefaultQueue);

    ...

    // Initialize virtual USB device software objects.
    // Shown later in this topic.

    status = Usb_Initialize(wdfDevice);

    ...

    exit:

        return status;
    }
    ```


## <a name="handle-user-mode-ioctl-requests-sent-to-the-host-controller"></a>ホスト コント ローラーに送信されたユーザー モードの IOCTL 要求を処理します。

初期化中に、UDE クライアント ドライバーは、GUID を公開する\_DEVINTERFACE\_USB\_ホスト\_コント ローラー デバイス インターフェイスの GUID。 これにより、その GUID を使用してデバイスのハンドルを開いているアプリケーションから IOCTL 要求を受信するドライバーができます。 IOCTL 制御コードの一覧は、次を参照してください。[アプリケーションとサービス用の USB Ioctl](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#um-ioctl)デバイスとインターフェイスの GUID。GUID\_DEVINTERFACE\_USB\_ホスト\_コント ローラー。

クライアント ドライバーはそれらの要求を処理するために登録、 [ *EvtIoDeviceControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)イベント コールバック。 実装では、要求を処理する代わりに、ドライバー、UDE クラスの拡張処理のために要求を転送できます。 要求を転送するように、ドライバーを呼び出す必要があります[ **UdecxWdfDeviceTryHandleUserIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdevicetryhandleuserioctl)します。 受信 IOCTL 制御コードがデバイスの記述子の取得などの標準の要求に対応している場合、クラス拡張は処理し、要求が正常に完了します。 この場合、 **UdecxWdfDeviceTryHandleUserIoctl**戻り値として TRUE になって完了します。 それ以外の場合、呼び出しは、FALSE と、ドライバーは、要求を完了する方法を決定する必要がありますを返します。 最も単純な実装でドライバーは、呼び出すことによって適切なエラー コードを使用して要求を完了できます[ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。

```cpp

EVT_WDF_IO_QUEUE_IO_DEVICE_CONTROL        Controller_EvtIoDeviceControl;


VOID
Controller_EvtIoDeviceControl(
    _In_
        WDFQUEUE Queue,
    _In_
        WDFREQUEST Request,
    _In_
        size_t OutputBufferLength,
    _In_
        size_t InputBufferLength,
    _In_
        ULONG IoControlCode
)
{
    BOOLEAN handled;
    NTSTATUS status;
    UNREFERENCED_PARAMETER(OutputBufferLength);
    UNREFERENCED_PARAMETER(InputBufferLength);

    handled = UdecxWdfDeviceTryHandleUserIoctl(WdfIoQueueGetDevice(Queue),
                                                Request);

    if (handled) {

        goto exit;
    }

    // Unexpected control code.
    // Fail the request.


    status = STATUS_INVALID_DEVICE_REQUEST;

    WdfRequestComplete(Request, status);

exit:

    return;
}
```

## <a name="report-the-capabilities-of-the-host-controller"></a>ホスト コント ローラーの機能を報告します。


上位レイヤー ドライバーでは、USB ホスト コント ローラーの機能を使用できます、前に、ドライバーがコント ローラーで、これらの機能がサポートされているかどうかを決定する必要があります。 ドライバーは、呼び出すことによってこのようなクエリを行う[ **WdfUsbTargetDeviceQueryUsbCapability** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)と[ **USBD\_QueryUsbCapability** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)). これらの呼び出しは、USB デバイス Emulation(UDE) クラスの拡張機能に転送されます。 クラスの拡張機能に要求を取得するには、クライアント ドライバーが呼び出す[ *EVT\_UDECX\_WDF\_デバイス\_クエリ\_USB\_機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)実装します。 この呼び出し後にのみ[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)が完了したら、通常[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 後ではなく、[*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)します。 これは、コールバック関数が必要です。

実装では、クライアント ドライバーは、要求された機能がサポートしているかどうかを報告する必要があります。 静的ストリームなど、特定の機能は UDE によってサポートされていません。

```cpp
NTSTATUS
Controller_EvtControllerQueryUsbCapability(
    WDFDEVICE     UdeWdfDevice,
    PGUID         CapabilityType,
    ULONG         OutputBufferLength,
    PVOID         OutputBuffer,
    PULONG        ResultLength
)

{
    NTSTATUS status;

    UNREFERENCED_PARAMETER(UdeWdfDevice);
    UNREFERENCED_PARAMETER(OutputBufferLength);
    UNREFERENCED_PARAMETER(OutputBuffer);

    *ResultLength = 0;

    if (RtlCompareMemory(CapabilityType,
                         &GUID_USB_CAPABILITY_CHAINED_MDLS,
                         sizeof(GUID)) == sizeof(GUID)) {

        //
        // TODO: Is GUID_USB_CAPABILITY_CHAINED_MDLS supported?
        // If supported, status = STATUS_SUCCESS
        // Otherwise, status = STATUS_NOT_SUPPORTED
    }

    else {

        status = STATUS_NOT_IMPLEMENTED;
    }

    return status;
}
```

## <a name="create-a-virtual-usb-device"></a>仮想の USB デバイスを作成します。

仮想の USB デバイスは、USB デバイスのような動作します。 複数のインターフェイスの構成をサポートし、各インターフェイスの代替設定をサポートしています。 各設定には、1 つのエンドポイントにデータ転送に使用されることができます。 すべての記述子 (デバイス、構成、インターフェイス、エンドポイント) は、デバイスが実際の USB デバイスのような情報を通報できるように、UDE クライアント ドライバーによって設定されます。

> [!NOTE]
> UDE クライアント ドライバーは外部ハブをサポートしていません

クライアント ドライバーが UDE デバイス オブジェクトの UDECXUSBDEVICE ハンドルを作成し、シーケンスの概要を次に示します。 ドライバーは、エミュレートされたホスト コント ローラーの WDFDEVICE ハンドルが取得した後、これらの手順を実行する必要があります。 ドライバーがこれらのタスクを実行することをお勧めします。 その[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

1. 呼び出す[ **UdecxUsbDeviceInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitallocate)デバイスを作成するために必要な初期化パラメーターへのポインターを取得します。 この構造体は、UDE クラスの拡張機能によって割り当てられます。
2. メンバーを設定してイベントのコールバック関数を登録[ **UDECX\_USB\_デバイス\_状態\_変更\_コールバック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/ns-udecxusbdevice-_udecx_usb_device_state_change_callbacks)と呼び出して[ **UdecxUsbDeviceInitSetStateChangeCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)します。 ここでは、UDE デバイス オブジェクトに関連付けられている、UDE クラスの拡張機能によって呼び出されるコールバック関数です。

    これらの関数は、作成するか、エンドポイントを構成するクライアント ドライバーによって実装されます。

   - [*EVT\_UDECX\_USB\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)
   - [*EVT\_UDECX\_USB\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)
   - [*EVT\_UDECX\_USB\_デバイス\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)

     <!-- -->

   - [*EVT\_UDECX\_USB\_デバイス\_D0\_エントリ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)
   - [*EVT\_UDECX\_USB\_デバイス\_D0\_終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)
   - [*EVT\_UDECX\_USB\_デバイス\_設定\_関数\_SUSPEND\_AND\_WAKE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)

3. 呼び出す[ **UdecxUsbDeviceInitSetSpeed** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetspeed) USB デバイスの速度ともデバイス、USB 2.0 または SuperSpeed デバイスの種類を設定します。
4. 呼び出す[ **UdecxUsbDeviceInitSetEndpointsType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetendpointstype)デバイスをサポートするエンドポイントの種類を指定する: 単純型または動的です。 クライアント ドライバーが単純なエンドポイントを作成することを選択する場合、ドライバーは、デバイスを接続する前にエンドポイントのすべてのオブジェクトを作成する必要があります。 デバイスは、インターフェイスあたり 1 つだけの構成とインターフェイスの 1 つだけ設定が必要です。 動的のエンドポイントの場合、ドライバーは、受信したときに、デバイスを接続した後、いつでもにエンドポイントを作成できます、 [ *EVT\_UDECX\_USB\_デバイス\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)イベント コールバック。 参照してください[動的エンドポイントを作成する](#create-dynamic-endpoints)します。
5. これらのデバイスに必要な記述子を追加するメソッドを呼び出します。

   - [**UdecxUsbDeviceInitAddDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptor)
   - [**UdecxUsbDeviceInitAddDescriptorWithIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptorwithindex)
   - [**UdecxUsbDeviceInitAddStringDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptor)
   - [**UdecxUsbDeviceInitAddStringDescriptorRaw**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptorraw)

     UDE クラスの拡張機能は、クライアント ドライバーが、上記の方法のいずれかを使用して初期化中に提供する標準的な記述子の要求を受信した場合、クラス拡張は自動的に要求を完了します。 クラスの拡張機能は、クライアント ドライバーには、その要求を転送しません。 この設計では、ドライバーがに対する制御要求を処理する必要がある要求の数を減らします。 さらに、セットアップのパケットの広範な解析および処理を必要とする記述子ロジックを実装するために、ドライバーの必要もありません**wLength**と**TransferBufferLength**正しくします。 この一覧には、標準的な要求が含まれています。 クライアント ドライバーは (記述子を追加する前のメソッドが呼び出された) 場合のみ、これらの要求を確認する必要はありません。

   - USB\_要求\_取得\_記述子
   - USB\_要求\_設定\_構成
   - USB\_要求\_設定\_インターフェイス
   - USB\_要求\_設定\_アドレス
   - USB\_要求\_設定\_機能
   - USB\_機能\_関数\_中断
   - USB\_機能\_リモート\_ウェイク アップ
   - USB\_要求\_クリア\_機能
   - USB\_機能\_エンドポイント\_失速
   - USB\_要求\_設定\_SEL
   - USB\_要求\_アイソクロナス\_遅延

     ただし、インターフェイス、クラス固有またはベンダー定義の記述子の要求、UDE クラスの拡張機能に転送クライアント ドライバー。 ドライバーは、GET を処理する必要があります\_記述子要求。

6. 呼び出す[ **UdecxUsbDeviceCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate) UDE デバイス オブジェクトを作成および UDECXUSBDEVICE ハンドルを取得します。
7. 静的なエンドポイントを呼び出すことによって作成[ **UdecxUsbEndpointCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)します。 参照してください[単純なエンドポイントを作成する](#create-simple-endpoints)します。
8. 呼び出す[ **UdecxUsbDevicePlugIn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugin)をデバイスが接続されているし、エンドポイント上の I/O 要求を受信できる UDE クラスの拡張機能を示します。 この呼び出しの後、クラス拡張もエンドポイントおよび USB デバイスのコールバック関数を呼び出すことができます。
    **注**クライアント ドライバーを呼び出すことができる場合、USB デバイスは、実行時に削除する必要があります、 [ **UdecxUsbDevicePlugOutAndDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugoutanddelete)します。 ドライバーは、デバイスを使用する場合、その必要がありますを呼び出して作成[ **UdecxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate)します。

この例では、記述子の宣言は、グローバル変数、例と同様、HID デバイスは、ここに示すように宣言すると見なされます。

```cpp
const UCHAR g_UsbDeviceDescriptor[] = {
    // Device Descriptor
    0x12, // Descriptor Size
    0x01, // Device Descriptor Type
    0x00, 0x03, // USB 3.0
    0x00, // Device class
    0x00, // Device sub-class
    0x00, // Device protocol
    0x09, // Maxpacket size for EP0 : 2^9
    0x5E, 0x04, // Vendor ID
    0x39, 0x00, // Product ID
    0x00, // LSB of firmware version
    0x03, // MSB of firmware version
    0x01, // Manufacture string index
    0x03, // Product string index
    0x00, // Serial number string index
    0x01 // Number of configurations
};
```

クライアント ドライバーが、コールバック関数を登録し、デバイスの速度を設定し、エンドポイントの種類を示す最後にいくつかのデバイス記述子の設定の初期化パラメーターを指定する例を示します。

```cpp

NTSTATUS
Usb_Initialize(
    _In_
        WDFDEVICE WdfDevice
    )
{
    NTSTATUS                                status;
    PUSB_CONTEXT                            usbContext;    //Client driver declared context for the host controller object
    PUDECX_USBDEVICE_CONTEXT                deviceContext; //Client driver declared context for the UDE device object
    UDECX_USB_DEVICE_STATE_CHANGE_CALLBACKS callbacks;
    WDF_OBJECT_ATTRIBUTES                   attributes;

    UDECX_USB_DEVICE_PLUG_IN_OPTIONS        pluginOptions;


    usbContext = WdfDeviceGetUsbContext(WdfDevice);

    usbContext->UdecxUsbDeviceInit = UdecxUsbDeviceInitAllocate(WdfDevice);

    if (usbContext->UdecxUsbDeviceInit == NULL) {

        ...
        goto exit;
    }


    // State changed callbacks

    UDECX_USB_DEVICE_CALLBACKS_INIT(&callbacks);
#ifndef SIMPLEENDPOINTS
    callbacks.EvtUsbDeviceDefaultEndpointAdd = UsbDevice_EvtUsbDeviceDefaultEndpointAdd;
    callbacks.EvtUsbDeviceEndpointAdd = UsbDevice_EvtUsbDeviceEndpointAdd;
    callbacks.EvtUsbDeviceEndpointsConfigure = UsbDevice_EvtUsbDeviceEndpointsConfigure;
#endif
    callbacks.EvtUsbDeviceLinkPowerEntry = UsbDevice_EvtUsbDeviceLinkPowerEntry;
    callbacks.EvtUsbDeviceLinkPowerExit = UsbDevice_EvtUsbDeviceLinkPowerExit;
    callbacks.EvtUsbDeviceSetFunctionSuspendAndWake = UsbDevice_EvtUsbDeviceSetFunctionSuspendAndWake;

    UdecxUsbDeviceInitSetStateChangeCallbacks(usbContext->UdecxUsbDeviceInit, &callbacks);


    // Set required attributes.

    UdecxUsbDeviceInitSetSpeed(usbContext->UdecxUsbDeviceInit, UdecxUsbLowSpeed);

#ifdef SIMPLEENDPOINTS
    UdecxUsbDeviceInitSetEndpointsType(usbContext->UdecxUsbDeviceInit, UdecxEndpointTypeSimple);
#else
    UdecxUsbDeviceInitSetEndpointsType(usbContext->UdecxUsbDeviceInit, UdecxEndpointTypeDynamic);
#endif


    // Add device descriptor
    //
    status = UdecxUsbDeviceInitAddDescriptor(usbContext->UdecxUsbDeviceInit,
                                           (PUCHAR)g_UsbDeviceDescriptor,
                                           sizeof(g_UsbDeviceDescriptor));

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

#ifdef USB30

    // Add BOS descriptor for a SuperSpeed device

    status = UdecxUsbDeviceInitAddDescriptor(pUsbContext->UdecxUsbDeviceInit,
                                           (PUCHAR)g_UsbBOSDescriptor,
                                           sizeof(g_UsbBOSDescriptor));

    if (!NT_SUCCESS(status)) {

        goto exit;
    }
#endif


    // String descriptors

    status = UdecxUsbDeviceInitAddDescriptorWithIndex(usbContext->UdecxUsbDeviceInit,
                                                    (PUCHAR)g_LanguageDescriptor,
                                                    sizeof(g_LanguageDescriptor),
                                                    0);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    status = UdecxUsbDeviceInitAddStringDescriptor(usbContext->UdecxUsbDeviceInit,
                                                 &g_ManufacturerStringEnUs,
                                                 g_ManufacturerIndex,
                                                 US_ENGLISH);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&attributes, UDECX_USBDEVICE_CONTEXT);

    status = UdecxUsbDeviceCreate(&usbContext->UdecxUsbDeviceInit,
                                &attributes,
                                &usbContext->UdecxUsbDevice);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

#ifdef SIMPLEENDPOINTS
   // Create the default control endpoint
   // Shown later in this topic.

    status = UsbCreateControlEndpoint(WdfDevice);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

#endif

    UDECX_USB_DEVICE_PLUG_IN_OPTIONS_INIT(&pluginOptions);
#ifdef USB30
    pluginOptions.Usb30PortNumber = 2;
#else
    pluginOptions.Usb20PortNumber = 1;
#endif
    status = UdecxUsbDevicePlugIn(usbContext->UdecxUsbDevice, &pluginOptions);

exit:

    if (!NT_SUCCESS(status)) {

        UdecxUsbDeviceInitFree(usbContext->UdecxUsbDeviceInit);
        usbContext->UdecxUsbDeviceInit = NULL;

    }

    return status;
}
```

## <a name="power-management-of-the-usb-device"></a>USB デバイスの電源管理


UDE クラスの拡張機能は、低電力状態または動作状態に戻して、デバイスの送信要求を受信したときに、クライアント ドライバーのコールバック関数を呼び出します。 これらのコールバック関数は、USB デバイスのスリープ解除をサポートする必要があります。 クライアント ドライバーでは、以前の呼び出しにによってその実装が登録されている[ **UdecxUsbDeviceInitSetStateChangeCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)します。

詳細については、次を参照してください。 [USB デバイスの電源状態](comparing-usb-device-states-to-wdm-device-states.md)します。

[*EVT\_UDECX\_USB\_デバイス\_D0\_エントリ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)  
クライアント ドライバーでは、Dx 状態から d0 へのデバイスを移行します。

[*EVT\_UDECX\_USB\_デバイス\_D0\_終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)  
クライアント ドライバーでは、Dx 状態 D0 状態からデバイスを移行します。

[*EVT\_UDECX\_USB\_デバイス\_設定\_関数\_SUSPEND\_AND\_WAKE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)  
クライアント ドライバーでは、仮想の USB 3.0 デバイスの指定したインターフェイスの関数の状態を変更します。

USB 3.0 デバイスは、低電力状態を入力する個々 の関数を使用します。 各関数は、ウェイク信号を送信できるもあります。 UDE クラスの拡張機能を呼び出すことによって、クライアント ドライバーに通知[ *EVT\_UDECX\_USB\_デバイス\_設定\_関数\_SUSPEND\_AND\_WAKE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)します。 このイベントは、関数の電源状態の変更を示し、関数が新しい状態から復帰がかどうかのクライアント ドライバーに通知。 関数では、クラス拡張は、ウェイク アップは関数のインターフェイスの数を渡します。
クライアント ドライバーは、仮想 USB デバイスを開始する、関数リンクが低電力状態からのスリープ解除すると、独自の中断、またはその両方の操作をシミュレートできます。 USB 2.0 デバイスの場合、ドライバーを呼び出す必要があります[ **UdecxUsbDeviceSignalWake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalwake)、ドライバー、最新のデバイスのスリープ解除を有効になっている場合は、 [ *EVT\_UDECX\_USB\_デバイス\_D0\_終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)します。 USB 3.0 デバイスの場合、ドライバーを呼び出す必要があります[ **UdecxUsbDeviceSignalFunctionWake** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalfunctionwake) USB 3.0 ウェイク アップ機能関数であるためです。 デバイス全体が低電力状態の場合、またはこのような状態では場合、 **UdecxUsbDeviceSignalFunctionWake**デバイスのスリープします。

## <a name="create-simple-endpoints"></a>単純なエンドポイントを作成します。


クライアント ドライバーでは、UDE エンドポイントのオブジェクトと、USB デバイスからのデータ転送を処理するために作成します。 ドライバーは、UDE デバイスを作成した後、接続されているように、デバイスを報告する前に、単純なエンドポイントを作成します。

クライアント ドライバーが UDE エンドポイント オブジェクトの UDECXUSBENDPOINT ハンドルを作成し、シーケンスの概要を次に示します。 ドライバーは、仮想の USB デバイスの UDECXUSBDEVICE ハンドルが取得した後、これらの手順を実行する必要があります。 ドライバーがこれらのタスクを実行することをお勧めします。 その[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数。

1. 呼び出す[ **UdecxUsbSimpleEndpointInitAllocate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbsimpleendpointinitallocate)クラスの拡張機能によって割り当てられた初期化パラメーターへのポインターを取得します。
2. 呼び出す[ **UdecxUsbEndpointInitSetEndpointAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress)初期化パラメーターで、エンドポイント アドレスを設定します。
3. 呼び出す[ **UdecxUsbEndpointInitSetCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)クライアント ドライバーによって実装されるコールバック関数を登録します。

    これらの関数は、キュー、およびエンドポイントに要求を処理するために、クライアント ドライバーによって実装されます。

    [*EVT\_UDECX\_USB\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)  
    仮想の USB デバイスのエンドポイントをリセットします。

    [*EVT\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)  
    (省略可能)。 I/O 要求の処理を開始します。

    [*EVT\_UDECX\_USB\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)  
    (省略可能)。 エンドポイントのキューへの I/O 要求のキューを停止し、未処理の要求をキャンセルします。

4. 呼び出す[ **UdecxUsbEndpointCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate) endpoint オブジェクトを作成および UDECXUSBENDPOINT ハンドルを取得します。
5. 呼び出す[ **UdecxUsbEndpointSetWdfIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue)にフレームワークのキュー オブジェクトをエンドポイントに関連付けます。 該当する場合は、エンドポイントにオブジェクトを適切な属性の設定によって、キューの WDF の親オブジェクトを設定できます。

    エンドポイントのすべてのオブジェクトでは、転送要求を処理するために、フレームワークのキュー オブジェクトがあります。 クラスの拡張機能が受け取る転送要求ごとに、フレームワークの要求オブジェクトをキューします。 キューの状態 (開始、削除) は、UDE によって管理されるクラスの拡張機能と、クライアント ドライバーする必要がありますいないその状態を変更します。 各要求オブジェクトには、USB 要求のブロックが含まれています ([**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb))、転送の詳細を格納しています。

この例では、クライアント ドライバーは、既定のコントロール エンドポイントを作成します。

```cpp
EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL IoEvtControlUrb;
EVT_UDECX_USB_ENDPOINT_RESET UsbEndpointReset;
EVT_UDECX_USB_ENDPOINT_PURGE UsEndpointEvtPurge;
EVT_UDECX_USB_ENDPOINT_START UsbEndpointEvtStart;

NTSTATUS
UsbCreateControlEndpoint(
    _In_
        WDFDEVICE WdfDevice
    )
{
    NTSTATUS                      status;
    PUSB_CONTEXT                  pUsbContext;
    WDF_IO_QUEUE_CONFIG           queueConfig;
    WDFQUEUE                      controlQueue;
    UDECX_USB_ENDPOINT_CALLBACKS  callbacks;
    PUDECXUSBENDPOINT_INIT        endpointInit;

    pUsbContext = WdfDeviceGetUsbContext(WdfDevice);
    endpointInit = NULL;

    WDF_IO_QUEUE_CONFIG_INIT(&queueConfig, WdfIoQueueDispatchSequential);

    queueConfig.EvtIoInternalDeviceControl = IoEvtControlUrb;

    status = WdfIoQueueCreate (Device,
                               &queueConfig,
                               WDF_NO_OBJECT_ATTRIBUTES,
                               &controlQueue);


    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    endpointInit = UdecxUsbSimpleEndpointInitAllocate(pUsbContext->UdecxUsbDevice);

    if (endpointInit == NULL) {

        status = STATUS_INSUFFICIENT_RESOURCES;
        goto exit;
    }

    UdecxUsbEndpointInitSetEndpointAddress(endpointInit, USB_DEFAULT_ENDPOINT_ADDRESS);

    UDECX_USB_ENDPOINT_CALLBACKS_INIT(&callbacks, UsbEndpointReset);
    UdecxUsbEndpointInitSetCallbacks(endpointInit, &callbacks);

    callbacks.EvtUsbEndpointStart = UsbEndpointEvtStart;
    callbacks.EvtUsbEndpointPurge = UsEndpointEvtPurge;

    status = UdecxUsbEndpointCreate(&endpointInit,
        WDF_NO_OBJECT_ATTRIBUTES,
        &pUsbContext->UdecxUsbControlEndpoint);

    if (!NT_SUCCESS(status)) {
        goto exit;
    }

    UdecxUsbEndpointSetWdfIoQueue(pUsbContext->UdecxUsbControlEndpoint,
        controlQueue);

exit:

    if (endpointInit != NULL) {

        NT_ASSERT(!NT_SUCCESS(status));
        UdecxUsbEndpointInitFree(endpointInit);
        endpointInit = NULL;
    }

    return status;
}
```

## <a name="create-dynamic-endpoints"></a>動的エンドポイントを作成します。


クライアント ドライバーでは、(ハブのドライバーとクライアント ドライバーで) に代わって、UDE クラスの拡張機能の要求で動的エンドポイントを作成できます。 クラスの拡張機能は、これらのコールバック関数を呼び出すことによって、要求を行います。

[*EVT\_UDECX\_USB\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)  
クライアント ドライバーは、既定のコントロール エンドポイント (エンドポイント 0) を作成します。

[*EVT\_UDECX\_USB\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)  
クライアント ドライバーでは、動的エンドポイントを作成します。

[*EVT\_UDECX\_USB\_デバイス\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)  
クライアント ドライバーでは、代替の設定を選択する、現在のエンドポイントを無効にする、または動的エンドポイントを追加で構成を変更します。

クライアント ドライバーでは、呼び出し中に、上記のコールバックが登録されている[ **UdecxUsbDeviceInitSetStateChangeCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)します。 作成するを参照[仮想の USB デバイス](#create-a-virtual-usb-device)します。
このメカニズムにより、クライアント ドライバーを USB 構成とデバイスのインターフェイスの設定を動的に変更します。 たとえば、エンドポイント オブジェクトが必要ですか、既存の endpoint オブジェクトを解放する必要があります、クラス拡張機能から呼び出さ、 [ *EVT\_UDECX\_USB\_デバイス\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)します。

クライアント ドライバーがコールバック関数の実装内でエンドポイント オブジェクト UDECXUSBENDPOINT ハンドルを作成し、シーケンスの概要を次に示します。

1. 呼び出す[ **UdecxUsbEndpointInitSetEndpointAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress)初期化パラメーターで、エンドポイント アドレスを設定します。
2. 呼び出す[ **UdecxUsbEndpointInitSetCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)クライアント ドライバーによって実装されるコールバック関数を登録します。 単純なエンドポイントと同様に、ドライバーを登録できますこれらのコールバック関数。
    - [*EVT\_UDECX\_USB\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset) (必須)。
    - [*EVT\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)
    - [*EVT\_UDECX\_USB\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)

3. 呼び出す[ **UdecxUsbEndpointCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate) endpoint オブジェクトを作成および UDECXUSBENDPOINT ハンドルを取得します。
4. 呼び出す[ **UdecxUsbEndpointSetWdfIoQueue** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue)にフレームワークのキュー オブジェクトをエンドポイントに関連付けます。

この実装の例では、クライアント ドライバーは、動的な既定のコントロール エンドポイントを作成します。

```cpp
NTSTATUS
UsbDevice_EvtUsbDeviceDefaultEndpointAdd(
    _In_
        UDECXUSBDEVICE            UdecxUsbDevice,
    _In_
        PUDECXUSBENDPOINT_INIT    UdecxUsbEndpointInit
)
{
    NTSTATUS                    status;
    PUDECX_USBDEVICE_CONTEXT    deviceContext;
    WDFQUEUE                    controlQueue;
    WDF_IO_QUEUE_CONFIG         queueConfig;
    UDECX_USB_ENDPOINT_CALLBACKS  callbacks;

    deviceContext = UdecxDeviceGetContext(UdecxUsbDevice);

    WDF_IO_QUEUE_CONFIG_INIT(&queueConfig, WdfIoQueueDispatchSequential);

    queueConfig.EvtIoInternalDeviceControl = IoEvtControlUrb;

    status = WdfIoQueueCreate (deviceContext->WdfDevice,
                               &queueConfig,
                               WDF_NO_OBJECT_ATTRIBUTES,
                               &controlQueue);

    if (!NT_SUCCESS(status)) {

        goto exit;
    }

    UdecxUsbEndpointInitSetEndpointAddress(UdecxUsbEndpointInit, USB_DEFAULT_DEVICE_ADDRESS);

    UDECX_USB_ENDPOINT_CALLBACKS_INIT(&callbacks, UsbEndpointReset);
    UdecxUsbEndpointInitSetCallbacks(UdecxUsbEndpointInit, &callbacks);

    status = UdecxUsbEndpointCreate(UdecxUsbEndpointInit,
        WDF_NO_OBJECT_ATTRIBUTES,
        &deviceContext->UdecxUsbControlEndpoint);

    if (!NT_SUCCESS(status)) {
        goto exit;
    }

    UdecxUsbEndpointSetWdfIoQueue(deviceContext->UdecxUsbControlEndpoint,
        controlQueue);


exit:

    return status;
}
```

## <a name="perform-error-recovery-by-resetting-an-endpoint"></a>エンドポイントをリセットすることで、エラーからの回復を実行します。


データ転送は、エンドポイントの停止条件などのさまざまな理由により失敗します。 場合は、失敗した転送エラー状態がクリアされるまで、エンドポイントが要求を処理することはできません。 UDE クラスの拡張機能には、失敗したデータ転送が発生した、クライアント ドライバーが呼び出されます[ *EVT\_UDECX\_USB\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)コールバック関数は、以前の呼び出しに登録されているドライバー [ **UdecxUsbEndpointInitSetCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)します。 実装では、ドライバーは、パイプの停止の状態をクリアし、エラー状態をクリアするために必要なその他の手順を実行できます。

この呼び出しは非同期です。 ドライバーが呼び出すことによって適切なエラー コードを使用して要求を完了する必要があります、クライアントが、リセット操作が完了したら、 [ **WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)します。 その呼び出しは、状態のリセット操作の完了に関する UDE クライアントの拡張機能を通知します。

**注**クライアント ドライバーが、ホスト コント ローラーをリセットする際のオプションで複雑なソリューションがエラーからの回復に必要な場合。 このロジックを実装することができます、 [ *EVT\_UDECX\_WDF\_デバイス\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)ドライバーがそのに登録されているコールバック関数[**UdecxWdfDeviceAddUsbDeviceEmulation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)呼び出します。 該当する場合、ドライバーは、ホスト コント ローラーおよびすべてのダウン ストリーム デバイスをリセットできます。 ドライバーを指定する必要があるかどうか、クライアント ドライバーでは、コント ローラーをリセットが、すべてのダウン ストリーム デバイスをリセットする必要はありません、 **UdeWdfDeviceResetActionResetEachUsbDevice**登録時に構成パラメーターにします。 クラスの拡張機能を呼び出す場合、 *EVT\_UDECX\_WDF\_デバイス\_リセット*接続されたデバイスごとにします。

## <a name="implement-queue-state-management"></a>キューの状態管理を実装します。

UDE エンドポイントのオブジェクトに関連付けられているフレームワークのキュー オブジェクトの状態は、UDE クラスの拡張機能によって管理されます。 ただし、クライアント ドライバーでは、他の内部キューにエンドポイントのキューから要求を転送するクライアントする必要があります、エンドポイントの I/O のフローでの変更を処理するロジックを実装します。 これらのコールバック関数に登録されている[ **UdecxUsbEndpointInitSetCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)します。

### <a name="endpoint-purge-operation"></a>エンドポイントの消去操作

エンドポイントごとに 1 つのキューで UDE クライアント ドライバーを実装できます[ *EVT\_UDECX\_USB\_エンドポイント\_パージ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)この例で示すようにします。

[ *EVT\_UDECX\_USB\_エンドポイント\_パージ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)実装で、クライアント ドライバーはから転送されるすべての I/O を確認する必要なエンドポイントのキューが完了し、その新しく転送された I/O は、クライアント ドライバーのまでも失敗[ *EVT\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)が呼び出されます。 呼び出すことによってこれらの要件が満たされて[ **UdecxUsbEndpointPurgeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointpurgecomplete)I/O がすべて転送されることを確認することが完了し、将来の I/O の転送が失敗しました。

### <a name="endpoint-start-operation"></a>エンドポイントの操作の開始

[ *EVT\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)実装で、クライアント ドライバーは、エンドポイントの上の I/O の処理を開始するために必要キュー、およびエンドポイントの転送された I/O を受信するすべてのキュー。 エンドポイントが作成された後、このコールバック関数から制御が戻た後までのすべての I/O は受信しません。 このコールバックは、後の I/O の処理の状態のエンドポイントを返します[ *EVT\_UDECX\_USB\_エンドポイント\_パージ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)が完了するとします。


## <a name="handling-data-transfer-requests-urbs"></a>処理データの転送要求 (翻訳)


クライアント デバイスのエンドポイントに送信された USB I/O 要求を処理するには、インターセプト、 [EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)と共に使用するキュー オブジェクトに対してコールバック[ **UdecxUsbEndpointInitSetCallbacks** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)エンドポイント、キューに関連付けるとき。 プロセスの I/O は、そのコールバックで、 [IOCTL\_内部\_USB\_送信\_URB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) IoControlCode (下のサンプル コードを参照してください[メソッドを処理するURB](#urb-handling-methods)。).


## <a name="urb-handling-methods"></a>URB 処理メソッド


一部としての処理を使用して翻訳[IOCTL\_内部\_USB\_送信\_URB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) A UDE クライアント ドライバーの仮想デバイス上のエンドポイントに関連付けられているキューへのポインターを取得できます、これらのメソッドを使用して、I/O 要求のバッファーを転送します。

これらの関数は、キュー、およびエンドポイントに要求を処理するために、クライアント ドライバーによって実装されます。

[**UdecxUrbRetrieveControlSetupPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbretrievecontrolsetuppacket)  
指定のフレームワークの要求オブジェクトから USB コントロール セットアップ パケットを取得します。

[**UdecxUrbRetrieveBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbretrievebuffer)  
エンドポイントのキューに送信される指定のフレームワークの要求オブジェクトから、URB の転送のバッファーを取得します。

[**UdecxUrbSetBytesCompleted**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbsetbytescompleted)  
フレームワークの要求オブジェクト内に含まれる URB に転送されたバイト数を設定します。

[**UdecxUrbComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbcomplete)  
USB に固有の完了ステータス コードと URB 要求を完了します。

[**UdecxUrbCompleteWithNtStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/udecxurb/nf-udecxurb-udecxurbcompletewithntstatus)  
NTSTATUS コードで URB 要求を完了します。

一般的な I/O が USB を転送の URB の処理の流れを次に示します。

```cpp
static VOID
IoEvtSampleOutUrb(
    _In_ WDFQUEUE Queue,
    _In_ WDFREQUEST Request,
    _In_ size_t OutputBufferLength,
    _In_ size_t InputBufferLength,
    _In_ ULONG IoControlCode
)
{
    PENDPOINTQUEUE_CONTEXT pEpQContext;
    NTSTATUS status = STATUS_SUCCESS;
    PUCHAR transferBuffer;
    ULONG transferBufferLength = 0;

    UNREFERENCED_PARAMETER(OutputBufferLength);
    UNREFERENCED_PARAMETER(InputBufferLength);

    // one possible way to get context info
    pEpQContext = GetEndpointQueueContext(Queue);

    if (IoControlCode != IOCTL_INTERNAL_USB_SUBMIT_URB)
    {
        LogError(TRACE_DEVICE, "WdfRequest %p Incorrect IOCTL %x, %!STATUS!",
            Request, IoControlCode, status);
        status = STATUS_INVALID_PARAMETER;
        goto exit;
    }

    status = UdecxUrbRetrieveBuffer(Request, &transferBuffer, &transferBufferLength);
    if (!NT_SUCCESS(status))
    {
        LogError(TRACE_DEVICE, "WdfRequest %p unable to retrieve buffer %!STATUS!",
            Request, status);
        goto exit;
    }

    if (transferBufferLength >= 1)
    {
        //consume one byte of output data
        pEpQContext->global_storage = transferBuffer[0];
    }

exit:
    // writes never pended, always completed
    UdecxUrbSetBytesCompleted(Request, transferBufferLength);
    UdecxUrbCompleteWithNtStatus(Request, status);
    return;
}
```

クライアント ドライバーでは、DPC とは別に、I/O 要求を完了できます。 これらのベスト プラクティスに従います。

- 既存の USB ドライバーとの互換性を確実には、UDE クライアントが呼び出す必要があります[ **WdfRequestComplete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcomplete)ディスパッチで\_レベル。
- 場合、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)エンドポイントのキューおよび、呼び出し元のドライバーのスレッドまたは DPC、要求で同期的に処理を開始する必要があります同期的に完了できませんドライバーに追加されました。 個別の DPC が必要なドライバーを呼び出すことによってキューに入れるため、 [ **WdfDpcEnqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdpc/nf-wdfdpc-wdfdpcenqueue)します。
- UDE クラスの拡張機能を呼び出すときに[ *EvtIoCanceledOnQueue* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)または[ *EvtRequestCancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)、クライアント ドライバーが完了する必要があります、呼び出し元のスレッドまたは DPC から個別の DPC に URB を受け取りました。 これを行うには、ドライバーが提供する必要があります、 *EvtIoCanceledOnQueue*コールバックをその[ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)キュー。
