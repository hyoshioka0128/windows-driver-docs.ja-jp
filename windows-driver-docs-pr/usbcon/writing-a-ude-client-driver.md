---
Description: USB デバイスエミュレーション (UDE) クラス拡張の動作と、エミュレートされたホストコントローラーと接続されているデバイスに対してクライアントドライバーが実行する必要があるタスクについて説明します。
title: UDE クライアント ドライバーを記述する
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 84973b34e70b02981b5f0d90d9ceb8c90c7e98ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843661"
---
# <a name="write-a-ude-client-driver"></a>UDE クライアント ドライバーを記述する

**要約**

- クラス拡張とクライアントドライバーによって使用される UDE オブジェクトとハンドル。
- コントローラーの機能を照会してコントローラーをリセットする機能を備えた、エミュレートされたホストコントローラーを作成する。
- 仮想 USB デバイスを作成し、エンドポイントを使用して電源管理とデータ転送を設定します。

**適用対象:**

- Windows 10

**最終更新日時:**

- 2015 年 11 月

**重要な API**

- [エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))

USB デバイスエミュレーション (UDE) クラス拡張の動作と、エミュレートされたホストコントローラーと接続されているデバイスに対してクライアントドライバーが実行する必要があるタスクについて説明します。 この例では、一連のルーチンとコールバック関数によって、クラスドライバーとクラス拡張がそれぞれと通信する方法について説明します。 また、クライアントドライバーが実装する必要がある機能についても説明します。

## <a name="before-you-begin"></a>始める前に

- 最新の Windows Driver Kit (WDK) 開発用コンピューターを[インストール](https://go.microsoft.com/fwlink/p/?LinkID=733614)します。 このキットには、UDE クライアントドライバーを作成するために必要なヘッダーファイルとライブラリが用意されています。具体的には、次のものが必要です。
  - スタブライブラリ (Udecxstub .lib)。 ライブラリは、クライアントドライバーによって行われた呼び出しを変換し、UdeCx に渡します。
  - ヘッダーファイル Udecx。
- 対象のコンピューターに Windows 10 をインストールします。
- UDE について理解を深めます。 「[アーキテクチャ: USB デバイスエミュレーション (UDE)](usb-emulated-device--ude--architecture.md)」を参照してください。
- Windows Driver Foundation (WDF) について理解を深めます。 推奨される読み取り: 小額 Orwick および Guy Smith によって作成され[た Windows Driver Foundation を使用したドライバーの開発]( https://go.microsoft.com/fwlink/p/?LinkId=691676)。

## <a name="ude-objects-and-handles"></a>UDE オブジェクトとハンドル

UDE クラス拡張機能とクライアントドライバーは、エミュレートされたホストコントローラーと仮想デバイスを表す特定の WDF オブジェクトを使用します。これには、デバイスとホスト間でデータを転送するために使用されるエンドポイントと URBs が含まれます。 クライアントドライバーはオブジェクトの作成を要求し、オブジェクトの有効期間はクラス拡張によって管理されます。

- **エミュレートされたホストコントローラーオブジェクト (WDFDEVICE)**

    は、エミュレートされたホストコントローラーを表します。は、UDE クラス拡張とクライアントドライバーの間のメインハンドルです。

- **UDE デバイスオブジェクト (UDECXUSBDEVICE)**

    エミュレートされたホストコントローラー上のポートに接続されている仮想 USB デバイスを表します。

- **UDE エンドポイントオブジェクト (UDECXUSBENDPOINT)**

    USB デバイスのシーケンシャルデータパイプを表します。 エンドポイントでデータを送受信するためのソフトウェア要求を受信するために使用されます。

## <a name="initialize-the-emulated-host-controller"></a>エミュレートされたホストコントローラーを初期化します

エミュレートされたホストコントローラーの WDFDEVICE ハンドルをクライアントドライバーが取得するシーケンスの概要を次に示します。 ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数でこれらのタスクを実行することをお勧めします。

1. フレームワークによって渡された[wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)への参照を渡すことによって、 [**Udecxinitializewdfdeviceinit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxinitializewdfdeviceinit)を呼び出します。
2. このデバイスが他の USB ホストコントローラーと同様に表示されるように、 [Wdfdevice\_INIT](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdfdevice_init)構造体をセットアップ情報で初期化します。 たとえば、FDO 名とシンボリックリンクを割り当てる場合は、アプリケーションが次のハンドルを開くことができるように、Microsoft が提供する GUID\_DEVINTERFACE\_USB\_ホスト\_コントローラー GUID としてデバイスインターフェイスを登録します。ドライブ.
3. [**WdfDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)を呼び出して、フレームワークデバイスオブジェクトを作成します。
4. [**Udecxwdfdeviceaddusbdeviceemulation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)を呼び出し、クライアントドライバーのコールバック関数を登録します。

    ここでは、UDE クラス拡張によって呼び出される、ホストコントローラーオブジェクトに関連付けられているコールバック関数を示します。 これらの関数は、クライアントドライバーによって実装される必要があります。

    [ *.EVT\_UDECX\_WDF\_デバイス\_クエリ\_USB\_機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)  
    クライアントドライバーがクラス拡張に報告する必要があるホストコントローラーによってサポートされる機能を決定します。

    [ *.EVT\_UDECX\_WDF\_デバイス\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)  
    (省略可能)。 ホストコントローラーまたは接続されているデバイスをリセットします。

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


## <a name="handle-user-mode-ioctl-requests-sent-to-the-host-controller"></a>ホストコントローラーに送信されたユーザーモードの IOCTL 要求を処理します

初期化中に、UDE クライアントドライバーは、USB\_ホスト\_コントローラーのデバイスインターフェイス GUID\_DEVINTERFACE\_GUID を公開します。 これにより、ドライバーは、その GUID を使用してデバイスハンドルを開くアプリケーションから IOCTL 要求を受け取ることができます。 IOCTL 制御コードの一覧については、「デバイスインターフェイス GUID を使用した[アプリケーションとサービスの Usb ioctl](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#um-ioctl) : GUID\_devinterface\_USB\_HOST\_CONTROLLER」を参照してください。

これらの要求を処理するために、クライアントドライバーは[*Evtiodevicecontrol*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_device_control)イベントコールバックを登録します。 の実装では、要求を処理するのではなく、ドライバーが UDE クラス拡張に要求を転送して処理できるようにすることができます。 要求を転送するには、ドライバーで[**Udecxwdfdevicetryhandleuserioctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdevicetryhandleuserioctl)を呼び出す必要があります。 受信した IOCTL 制御コードが、デバイス記述子の取得などの標準要求に対応する場合、クラス拡張は、要求を処理して正常に完了します。 この場合、 **Udecxwdfdevicetryhandleuserioctl**は戻り値として TRUE で完了します。 それ以外の場合、呼び出しは FALSE を返し、ドライバーは要求を完了する方法を決定する必要があります。 最も単純な実装では、ドライバーは[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出すことによって、適切なエラーコードを使用して要求を完了できます。

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

## <a name="report-the-capabilities-of-the-host-controller"></a>ホストコントローラーの機能を報告する


上位レイヤードライバーが USB ホストコントローラーの機能を使用できるようにするには、そのドライバーがコントローラーによってサポートされているかどうかを判断する必要があります。 ドライバーは、 [**WdfUsbTargetDeviceQueryUsbCapability**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)および[**USBD\_queryusbcapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))を呼び出すことによって、このようなクエリを行います。 これらの呼び出しは、USB デバイスエミュレーション (UDE) クラス拡張に転送されます。 クラス拡張は、要求を取得すると、クライアントドライバーの[ *.evt\_UDECX\_WDF\_デバイス\_クエリ\_USB\_機能*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_query_usb_capability)の実装を呼び出します。 この呼び出しは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)の完了後にのみ行われます。通常は、 [*EvtDeviceReleaseHardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_release_hardware)の後ではなく、 [*evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)で実行されます。 これはコールバック関数が必要です。

実装では、クライアントドライバーは、要求された機能をサポートしているかどうかを報告する必要があります。 一部の機能は、静的ストリームなどの UDE ではサポートされていません。

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

## <a name="create-a-virtual-usb-device"></a>仮想 USB デバイスを作成する

仮想 USB デバイスは、USB デバイスに似た動作をします。 複数のインターフェイスを持つ構成をサポートし、各インターフェイスが別の設定をサポートします。 各設定には、データ転送に使用されるエンドポイントをもう1つ含めることができます。 すべての記述子 (デバイス、構成、インターフェイス、エンドポイント) は、デバイスが実際の USB デバイスと同じように情報を報告できるように、UDE クライアントドライバーによって設定されます。

> [!NOTE]
> UDE クライアントドライバーが外部ハブをサポートしていない

クライアントドライバーが UDE デバイスオブジェクトの UDECXUSBDEVICE ハンドルを作成するシーケンスの概要を次に示します。 ドライバーは、エミュレートされたホストコントローラーの WDFDEVICE ハンドルを取得した後に、これらの手順を実行する必要があります。 ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数でこれらのタスクを実行することをお勧めします。

1. デバイスを作成するために必要な初期化パラメーターへのポインターを取得するには、 [**Udecxusbdeviceinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitallocate)を呼び出します。 この構造体は、UDE クラス拡張によって割り当てられます。
2. [**Udecx\_USB\_デバイス\_\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/ns-udecxusbdevice-_udecx_usb_device_state_change_callbacks)のメンバーを設定して\_コールバックを変更し、 [**Udecxusbdeviceinitsetstatechangecallバッキング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)を呼び出すことによって、イベントコールバック関数を登録します。 Ude デバイスオブジェクトに関連付けられているコールバック関数は、UDE クラス拡張機能によって呼び出されます。

    これらの関数は、エンドポイントを作成または構成するためにクライアントドライバーによって実装されます。

   - [ *.EVT\_UDECX\_USB\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)
   - [ *.EVT\_UDECX\_USB\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)
   - [ *.EVT\_UDECX\_USB\_デバイス\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)

     <!-- -->

   - [ *.EVT\_UDECX\_USB\_デバイス\_D0\_ENTRY*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)
   - [ *.EVT\_UDECX\_USB\_デバイス\_D0\_終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)
   - [ *.EVT\_UDECX\_USB\_デバイス\_設定\_関数\_中断\_と\_ウェイク*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)

3. [**Udecxusbdeviceinitsetspeed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetspeed)を呼び出して、usb デバイスの速度と、デバイス、usb 2.0、SuperSpeed デバイスの種類を設定します。
4. デバイスがサポートするエンドポイントの種類を指定するには、 [**Udecxusbdeviceinitsetendpointstype**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetendpointstype)を呼び出します。 simple または dynamic です。 クライアントドライバーが単純なエンドポイントを作成することを選択した場合、ドライバーはデバイスに接続する前にすべてのエンドポイントオブジェクトを作成する必要があります。 デバイスに必要な構成は1つだけであり、インターフェイスの設定はインターフェイスごとに1つだけである必要があります。 動的エンドポイントの場合、ドライバーは、デバイスを接続した後に、デバイスを接続した後に、\_\_デバイスを接続した後で、 [ *\_デバイス\_エンドポイント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)イベントコールバックを構成することにより、いつでもエンドポイントを作成できます。 「[動的エンドポイントの作成](#create-dynamic-endpoints)」を参照してください。
5. これらのメソッドのいずれかを呼び出して、必要な記述子をデバイスに追加します。

   - [**UdecxUsbDeviceInitAddDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptor)
   - [**Udecxusbdeviceinitadd記述子 Withindex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitadddescriptorwithindex)
   - [**UdecxUsbDeviceInitAddStringDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptor)
   - [**Udecxusbdeviceinitaddstring記述子 Raw**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitaddstringdescriptorraw)

     UDE クラス拡張が、前のいずれかのメソッドを使用して初期化時にクライアントドライバーによって提供された標準記述子の要求を受け取った場合、クラス拡張は自動的に要求を完了します。 クラス拡張は、その要求をクライアントドライバーに転送しません。 この設計により、ドライバーが制御要求を処理するために必要な要求の数が減ります。 さらに、セットアップパケットを広範囲に解析し、 **Wlength**および**transferbufferlength**を正しく処理する必要がある記述子ロジックをドライバーに実装する必要もなくなりました。 この一覧には、標準要求が含まれています。 クライアントドライバーは、これらの要求を確認する必要はありません (前のメソッドが記述子を追加するために呼び出された場合のみ)。

   - USB\_要求\_\_記述子を取得します
   - USB\_要求\_設定\_構成
   - USB\_要求\_\_インターフェイス
   - USB\_要求\_\_アドレスを設定します
   - USB\_要求\_\_機能の設定
   - USB\_機能\_機能\_中断
   - リモート\_ウェイクアップ\_USB\_機能
   - USB\_要求\_\_機能をクリア
   - USB\_機能\_エンドポイント\_停止
   - USB\_要求\_設定\_SEL
   - USB\_要求\_ISOCH\_遅延

     ただし、インターフェイス、クラス固有、またはベンダー定義の記述子に対する要求では、UDE クラス拡張機能によってそれらがクライアントドライバーに転送されます。 ドライバーは、これらの GET\_記述子要求を処理する必要があります。

6. [**UdecxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate)を呼び出して ude デバイスオブジェクトを作成し、UDECXUSBDEVICE ハンドルを取得します。
7. [**Udecxusbendpointcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)を呼び出して、静的なエンドポイントを作成します。 「[単純なエンドポイントの作成](#create-simple-endpoints)」を参照してください。
8. [**Udecxusbdeviceplugin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugin)を呼び出して、デバイスが接続されていること、およびエンドポイントで i/o 要求を受信できることを ude クラス拡張に示します。 この呼び出しの後、クラス拡張は、エンドポイントおよび USB デバイスでコールバック関数を呼び出すこともできます。
    **メモ** USB デバイスを実行時に削除する必要がある場合、クライアントドライバーは[**UdecxUsbDevicePlugOutAndDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceplugoutanddelete)を呼び出すことができます。 デバイスを使用する必要がある場合は、 [**UdecxUsbDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicecreate)を呼び出してドライバーを作成する必要があります。

この例では、記述子宣言はグローバル変数と見なされます。これは、次の例のように、HID デバイスの場合と同じように宣言されています。

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

次に示すのは、クライアントドライバーが、コールバック関数の登録、デバイス速度の設定、エンドポイントの種類の指定、最後にいくつかのデバイス記述子の設定を行って、初期化パラメーターを指定している例です。

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


UDE クラス拡張は、デバイスを低電力状態に送信する要求を受信したとき、または動作状態に戻すときに、クライアントドライバーのコールバック関数を呼び出します。 これらのコールバック関数は、wake をサポートする USB デバイスに必要です。 クライアントドライバーは、 [**Udecxusbdeviceinitsetstatechangecallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)の前の呼び出しで、によって実装を登録しました。

詳細については、「 [USB デバイスの電源状態](comparing-usb-device-states-to-wdm-device-states.md)」を参照してください。

[ *.EVT\_UDECX\_USB\_デバイス\_D0\_ENTRY*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_entry)  
クライアントドライバーは、デバイスを Dx 状態から D0 状態に移行します。

[ *.EVT\_UDECX\_USB\_デバイス\_D0\_終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)  
クライアントドライバーは、デバイスを D0 状態から Dx 状態に移行します。

[ *.EVT\_UDECX\_USB\_デバイス\_設定\_関数\_中断\_と\_ウェイク*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)  
クライアントドライバーは、仮想 USB 3.0 デバイスの指定されたインターフェイスの機能の状態を変更します。

USB 3.0 デバイスでは、個々の機能が低電力状態に入ることができます。 各関数は、ウェイクアップ信号を送信することもできます。 UDE クラスの拡張機能は、 [ *.evt\_UDECX\_USB\_\_デバイス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_set_function_suspend_and_wake)を呼び出すことによってクライアントドライバーに通知し、\_\_を中断\_および\_ウェイクします。 このイベントは、関数の電源状態の変更を示し、関数が新しい状態から復帰できるかどうかをクライアントドライバーに通知します。 関数では、クラス拡張は、ウェイクアップしている関数のインターフェイス番号を渡します。
クライアントドライバーは、低リンクの電源状態、機能の中断、またはその両方から、仮想 USB デバイス自体のウェイクアップを開始する操作をシミュレートできます。 USB 2.0 デバイスの場合、ドライバーは[**Udecxusbデバイス Ignalwake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalwake)を呼び出す必要があります。これは、最新の[ *.evt\_udecx\_USB\_デバイス\_D0\_終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_d0_exit)します。 USB 3.0 デバイスの場合は、USB 3.0 ウェイク機能が機能ごとに使用されるため、ドライバーは[**Udecxusbデバイス Ignalfunctionwake**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdevicesignalfunctionwake)を呼び出す必要があります。 デバイス全体の電源が入っていない場合、またはそのような状態になっている場合は、 **Udecxusb装置 Ignalfunctionwake**によってデバイスがウェイクアップされます。

## <a name="create-simple-endpoints"></a>単純なエンドポイントを作成する


クライアントドライバーは、USB デバイスとの間のデータ転送を処理するために、UDE エンドポイントオブジェクトを作成します。 ドライバーは、UDE デバイスを作成した後、デバイスを接続先として報告する前に、単純なエンドポイントを作成します。

ここでは、クライアントドライバーが UDE エンドポイントオブジェクトの UDECXUSBENDPOINT ハンドルを作成するシーケンスの概要について説明します。 ドライバーは、仮想 USB デバイスの UDECXUSBDEVICE ハンドルを取得した後に、これらの手順を実行する必要があります。 ドライバーは、 [*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバック関数でこれらのタスクを実行することをお勧めします。

1. [**Udecxusbsimpleendpointinitallocate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbsimpleendpointinitallocate)を呼び出して、クラス拡張によって割り当てられた初期化パラメーターへのポインターを取得します。
2. [**Udecxusbendpointinitsetendpointaddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress)を呼び出して、初期化パラメーターのエンドポイントアドレスを設定します。
3. [**Udecxusbendpointinitsetcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)を呼び出して、クライアントドライバーで実装されているコールバック関数を登録します。

    これらの関数は、エンドポイントでキューと要求を処理するためにクライアントドライバーによって実装されます。

    [ *.EVT\_UDECX\_USB\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)  
    仮想 USB デバイスのエンドポイントをリセットします。

    [ *.EVT\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)  
    (省略可能)。 I/o 要求の処理を開始します

    [ *.EVT\_UDECX\_USB\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)  
    (省略可能)。 エンドポイントのキューへの i/o 要求のキューを停止し、未処理の要求をキャンセルします。

4. [**Udecxusbendpointcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)を呼び出して、エンドポイントオブジェクトを作成し、udecxusbendpoint ハンドルを取得します。
5. [**Udecxusbendpointsetwdfioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue)を呼び出して、フレームワークキューオブジェクトをエンドポイントに関連付けます。 該当する場合は、適切な属性を設定することによって、エンドポイントオブジェクトをキューの WDF 親オブジェクトに設定できます。

    すべてのエンドポイントオブジェクトには、転送要求を処理するためのフレームワークキューオブジェクトがあります。 クラス拡張によって受信される転送要求ごとに、フレームワークの要求オブジェクトをキューに格納します。 キューの状態 (開始済み、削除済み) は UDE クラス拡張によって管理され、クライアントドライバーはその状態を変更することはできません。 各要求オブジェクトには、転送の詳細を含む USB 要求ブロック ([**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)) が含まれています。

この例では、クライアントドライバーが既定のコントロールエンドポイントを作成します。

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

## <a name="create-dynamic-endpoints"></a>動的エンドポイントの作成


クライアントドライバーは、UDE クラス拡張の要求時に (ハブドライバーとクライアントドライバーに代わって) 動的エンドポイントを作成できます。 クラス拡張は、次のいずれかのコールバック関数を呼び出すことによって要求を行います。

[ *.EVT\_UDECX\_USB\_デバイス\_既定\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_default_endpoint_add)  
クライアントドライバーは、既定のコントロールエンドポイント (エンドポイント 0) を作成します。

[ *.EVT\_UDECX\_USB\_デバイス\_エンドポイント\_追加*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoint_add)  
クライアントドライバーは、動的エンドポイントを作成します。

[ *.EVT\_UDECX\_USB\_デバイス\_エンドポイント\_構成*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)  
クライアントドライバーは、別の設定を選択するか、現在のエンドポイントを無効にするか、動的エンドポイントを追加して、構成を変更します。

クライアントドライバーは、 [**Udecxusbdeviceinitsetstatechangecallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nf-udecxusbdevice-udecxusbdeviceinitsetstatechangecallbacks)の呼び出し中に、前のコールバックを登録しました。 「[仮想 USB デバイス](#create-a-virtual-usb-device)を作成する」を参照してください。
このメカニズムにより、クライアントドライバーはデバイスの USB 構成とインターフェイスの設定を動的に変更できます。 たとえば、エンドポイントオブジェクトが必要な場合、または既存のエンドポイントオブジェクトを解放する必要がある場合、クラス拡張は、[*構成\_\_エンドポイント\_UDECX\_USB\_デバイス*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbdevice/nc-udecxusbdevice-evt_udecx_usb_device_endpoints_configure)を呼び出します。

コールバック関数の実装において、クライアントドライバーがエンドポイントオブジェクトの UDECXUSBENDPOINT ハンドルを作成するシーケンスの概要を次に示します。

1. [**Udecxusbendpointinitsetendpointaddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetendpointaddress)を呼び出して、初期化パラメーターのエンドポイントアドレスを設定します。
2. [**Udecxusbendpointinitsetcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)を呼び出して、クライアントドライバーで実装されているコールバック関数を登録します。 単純なエンドポイントと同様に、ドライバーは次のコールバック関数を登録できます。
    - [ *.Evt\_UDECX\_USB\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)(必須)。
    - [ *.EVT\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)
    - [ *.EVT\_UDECX\_USB\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)

3. [**Udecxusbendpointcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointcreate)を呼び出して、エンドポイントオブジェクトを作成し、udecxusbendpoint ハンドルを取得します。
4. [**Udecxusbendpointsetwdfioqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointsetwdfioqueue)を呼び出して、フレームワークキューオブジェクトをエンドポイントに関連付けます。

この実装例では、クライアントドライバーは動的な既定のコントロールエンドポイントを作成します。

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

## <a name="perform-error-recovery-by-resetting-an-endpoint"></a>エンドポイントをリセットしてエラー回復を実行する


場合によっては、エンドポイントの停止条件など、さまざまな理由によりデータ転送が失敗することがあります。 転送が失敗した場合、エンドポイントは、エラー状態がクリアされるまで要求を処理できません。 UDE クラス拡張機能でデータ転送が失敗すると、クライアントドライバーの[ *.evt\_UDECX\_USB\_エンドポイント\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_reset)コールバック関数が呼び出されます。これは、前回のへ[**の呼び出しで登録されたドライバーです。UdecxUsbEndpointInitSetCallbacks バック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)。 実装では、ドライバーがパイプの停止状態をクリアし、その他の必要な手順を実行してエラー状態をクリアすることができます。

この呼び出しは非同期です。 リセット操作でクライアントが終了した後、ドライバーは、 [**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出すことによって、適切なエラーコードを使用して要求を完了する必要があります。 この呼び出しにより、UDE クライアントの拡張機能に、状態を持つリセット操作の完了が通知されます。

**メモ** エラー回復に複雑なソリューションが必要な場合は、クライアントドライバーにホストコントローラーをリセットするオプションがあります。 このロジックは、ドライバーによって[**Udecxwdfdeviceaddusbdeviceエミュレーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nf-udecxwdfdevice-udecxwdfdeviceaddusbdeviceemulation)呼び出しに登録されていた[ *\_udecx\_WDF\_デバイス\_リセット*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxwdfdevice/nc-udecxwdfdevice-evt_udecx_wdf_device_reset)コールバック関数に、.evt で実装できます。 該当する場合、ドライバーはホストコントローラーとすべてのダウンストリームデバイスをリセットできます。 クライアントドライバーがコントローラーをリセットする必要がなく、すべてのダウンストリームデバイスをリセットする必要がある場合、ドライバーでは、登録時に構成パラメーターに**Udewdfdeviceresetactionresetを**指定する必要があります。 この場合、クラス拡張は、接続されている各デバイスに対して、 *.evt\_UDECX\_WDF\_デバイス\_リセット*を呼び出します。

## <a name="implement-queue-state-management"></a>キュー状態管理の実装

UDE エンドポイントオブジェクトに関連付けられているフレームワークキューオブジェクトの状態は、UDE クラス拡張によって管理されます。 ただし、クライアントドライバーがエンドポイントキューから他の内部キューに要求を転送する場合、クライアントは、エンドポイントの i/o フローの変更を処理するロジックを実装する必要があります。 これらのコールバック関数は、 [**Udecxusbendpointinitsetcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)に登録されます。

### <a name="endpoint-purge-operation"></a>エンドポイントの消去操作

次の例に示すように、エンドポイントごとに1つのキューを持つ UDE クライアントドライバーは、 [*USB\_エンド\_ポイントを\_\_UDECX*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)を実装できます。

[ *.Evt\_UDECX\_USB\_エンドポイント\_消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)の実装では、クライアントドライバーは、エンドポイントのキューから転送されたすべての i/o が完了していることを確認する必要があります。また、新しく転送された i/o も、クライアントに対して失敗します。ドライバーの[ *.evt\_UDECX\_USB\_エンドポイント\_開始*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)が呼び出されます。 これらの要件は、 [**UdecxUsbEndpointPurgeComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointpurgecomplete)を呼び出すことによって満たされます。これにより、転送されたすべての i/o が完了し、今後の転送 i/o が失敗します。

### <a name="endpoint-start-operation"></a>エンドポイントの開始操作

[ *.Evt\_UDECX\_USB\_エンドポイント\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_start)実装を開始するために、クライアントドライバーはエンドポイントのキュー、およびエンドポイントの転送 i/o を受信するすべてのキューでの i/o 処理を開始する必要があります。 エンドポイントが作成された後は、このコールバック関数が戻るまで i/o は受信されません。 このコールバックは、 [ *.evt\_UDECX\_USB\_エンドポイント\_の消去*](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nc-udecxusbendpoint-evt_udecx_usb_endpoint_purge)の完了後に、エンドポイントを処理 i/o の状態に戻します。


## <a name="handling-data-transfer-requests-urbs"></a>データ転送要求の処理 (URBs)


クライアントデバイスのエンドポイントに送信された USB i/o 要求を処理するには、キューをに関連付けているときに、 [**Udecxusbendpointinitsetcallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxusbendpoint/nf-udecxusbendpoint-udecxusbendpointinitsetcallbacks)で使用されるキューオブジェクトの[EVT_WDF_IO_QUEUE_IO_INTERNAL_DEVICE_CONTROL](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_internal_device_control)コールバックをインターセプトします。終点. このコールバックでは、 [IOCTL\_内部\_USB](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb)のプロセス i/o は\_URB iocontrolcode を送信\_ます (「 [urb 処理メソッド](#urb-handling-methods)」のサンプルコードを参照してください)。


## <a name="urb-handling-methods"></a>URB の処理方法


内部\_USB を\_介した URBs の処理の一環として、仮想デバイス上のエンドポイントに関連付けられているキューの[\_URB を送信\_](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_internal_usb_submit_urb) 、ude クライアントドライバーは、次のような方法で i/o 要求の転送バッファーへのポインターを取得することができます。メソッド

これらの関数は、エンドポイントでキューと要求を処理するためにクライアントドライバーによって実装されます。

[**UdecxUrbRetrieveControlSetupPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbretrievecontrolsetuppacket)  
指定されたフレームワーク要求オブジェクトから USB コントロールのセットアップパケットを取得します。

[**UdecxUrbRetrieveBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbretrievebuffer)  
エンドポイントキューに送信された、指定されたフレームワーク要求オブジェクトからの URB の転送バッファーを取得します。

[**UdecxUrbSetBytesCompleted 完了しました**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbsetbytescompleted)  
フレームワークの要求オブジェクト内に含まれる URB に転送されるバイト数を設定します。

[**UdecxUrbComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbcomplete)  
USB 固有の完了ステータスコードを使用して、URB 要求を完了します。

[**UdecxUrbCompleteWithNtStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/udecxurb/nf-udecxurb-udecxurbcompletewithntstatus)  
NTSTATUS コードを使用して URB 要求を完了します。

以下は、USB 出力転送の URB に対する一般的な i/o 処理のフローです。

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

クライアントドライバーは、DPC とは別ので i/o 要求を完了できます。 次のベストプラクティスに従ってください。

- 既存の USB ドライバーとの互換性を確保するために、UDE クライアントは、ディスパッチ\_レベルで[**Wdfrequestcomplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)を呼び出す必要があります。
- [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)がエンドポイントのキューに追加され、呼び出し元のドライバーのスレッドまたは DPC でドライバーが同期的に処理を開始する場合、要求を同期的に完了することはできません。 この目的には別の DPC が必要です。これは、 [**Wdfdpcenqueue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdpc/nf-wdfdpc-wdfdpcenqueue)を呼び出してドライバーをキューに置いています。
- UDE クラス拡張機能が[*EvtIoCanceledOnQueue*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nc-wdfio-evt_wdf_io_queue_io_canceled_on_queue)または[*Evtrequestcancel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_cancel)を呼び出すと、クライアントドライバーは、呼び出し元のスレッドまたは dpc とは別の dpc で受信した URB を完了する必要があります。 これを行うには、ドライバーが[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)キューの*EvtIoCanceledOnQueue*コールバックを提供する必要があります。
