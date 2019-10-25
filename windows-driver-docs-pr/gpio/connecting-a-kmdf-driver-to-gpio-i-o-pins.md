---
title: KMDF ドライバーの GPIO I/O ピンへの接続
description: 周辺機器用のカーネルモードドライバーフレームワーク (KMDF) ドライバーが、GPIO i/o リソースの説明を取得する方法。
ms.assetid: 02F6431C-7B55-4DFB-9792-4A72F0268C76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 076ada4fa04dde1ef95ad0ac85880b21e97ddbcb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825053"
---
# <a name="connecting-a-kmdf-driver-to-gpio-io-pins"></a>KMDF ドライバーの GPIO I/O ピンへの接続


GPIO i/o リソースは、データ入力またはデータ出力として構成される1つ以上の GPIO ピンのセットです。 これらのピンに物理的に接続する周辺機器のドライバーは、対応する GPIO i/o リソースをオペレーティングシステムから取得します。 周辺機器ドライバーは、このリソースの GPIO ピンへの接続を開き、この接続を表すハンドルに i/o 要求を送信します。

次のコード例は、周辺機器のカーネルモードドライバーフレームワーク (KMDF) ドライバーが、プラグアンドプレイ (PnP) マネージャーがドライバーに割り当てた GPIO i/o リソースの説明を取得する方法を示しています。

```cpp
NTSTATUS
  EvtDevicePrepareHardware(
    _In_ WDFDEVICE Device,
    _In_ WDFCMRESLIST ResourcesRaw,
    _In_ WDFCMRESLIST ResourcesTranslated
    )
{
    int ResourceCount, Index;
    PCM_PARTIAL_RESOURCE_DESCRIPTOR Descriptor;
    XYZ_DEVICE_CONTEXT *DeviceExtension;

    ...

    DeviceExtension = XyzDrvGetDeviceExtension(Device);
    ResourceCount = WdfCmResourceListGetCount(ResourcesTranslated);
    for (Index = 0; Index < ResourceCount; Index += 1) {
        Descriptor = WdfCmResourceListGetDescriptor(ResourcesTranslated, Index);
        switch (Descriptor->Type) {

        //
        // GPIO I/O descriptors
        //

        case CmResourceTypeConnection:

            //
            // Check against expected connection type.
            //

            if ((Descriptor->u.Connection.Class == CM_RESOURCE_CONNECTION_CLASS_GPIO) &&
                (Descriptor->u.Connection.Type == CM_RESOURCE_CONNECTION_TYPE_GPIO_IO)) {

                DeviceExtension->ConnectionId.LowPart = Descriptor->u.Connection.IdLowPart;
                DeviceExtension->ConnectionId.HighPart = Descriptor->u.Connection.IdHighPart;

        ...

}
```

前のコード例では、`DeviceExtension` 変数は、周辺機器のデバイスコンテキストへのポインターです。 このデバイスコンテキストを取得する `XyzDrvGetDeviceExtension` 関数は、周辺機器ドライバーによって実装されます。 このドライバーは、 [**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)メソッドを呼び出して、以前に[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数を登録しました。

次のコード例では、周辺機器ドライバーが、前のコード例で取得した GPIO リソースの説明を使用して、ドライバーの GPIO i/o リソースへの WDFIOTARGET ハンドルを開く方法を示します。

```cpp
NTSTATUS IoRoutine(WDFDEVICE Device, BOOLEAN ReadOperation) 
{
    WDFIOTARGET IoTarget;
    XYZ_DEVICE_CONTEXT *DeviceExtension;
    UNICODE_STRING ReadString;
    WCHAR ReadStringBuffer[100];;
    BOOL DesiredAccess;
    NTSTATUS Status;
    WDF_OBJECT_ATTRIBUTES ObjectAttributes;
    WDF_IO_TARGET_OPEN_PARAMS OpenParams

    DeviceExtension = XyzDrvGetDeviceExtension(Device);
    RtlInitEmptyUnicodeString(&ReadString,
                              ReadStringBuffer,
                              sizeof(ReadStringBuffer));

    Status = RESOURCE_HUB_CREATE_PATH_FROM_ID(&ReadString,
                                              DeviceExtension->ConnectionId.LowPart,
                                              DeviceExtension->ConnectionId.HighPart);

    NT_ASSERT(NT_SUCCESS(Status));

    WDF_OBJECT_ATTRIBUTES_INIT(&ObjectAttributes);
    ObjectAttributes.ParentObject = Device;

    Status = WdfIoTargetCreate(Device, &ObjectAttributes, &IoTarget);
    if (!NT_SUCCESS(Status)) {
        goto IoErrorEnd;
    }   

    if (ReadOperation != FALSE) {
        DesiredAccess = GENERIC_READ;
    } else {
        DesiredAccess = GENERIC_WRITE;
    }

    WDF_IO_TARGET_OPEN_PARAMS_INIT_OPEN_BY_NAME(&OpenParams, ReadString, DesiredAccess);

    Status = WdfIoTargetOpen(IoTarget, &OpenParams);
    if (!NT_SUCCESS(Status)) {
        goto IoErrorEnd;
    }
    ...
```

前のコード例では、`Device` 変数は、周辺機器のフレームワークデバイスオブジェクトを表す WDFDEVICE ハンドルです。 **リソース\_ハブ\_\_ID 関数から\_パス\_を作成**し、GPIO i/o リソースの名前を含む文字列を作成します。 このコード例では、この文字列を使用して、名前で GPIO i/o リソースを開きます。

周辺機器ドライバーが GPIO i/o リソースへのハンドルを取得した後、このドライバーは、GPIO ピンに対してデータの読み取りまたは書き込みを行う i/o 制御要求を送信できます。 読み取り用の GPIO i/o リソースを開くドライバーは、 [**IOCTL\_gpio\_読み取り\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)の i/o 制御要求を使用して、リソース内のピンからデータを読み取ります。 書き込み用の GPIO i/o リソースを開くドライバーは、 [**IOCTL\_gpio\_書き込み\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)の i/o 制御要求を使用して、リソース内のピンにデータを書き込みます。 次のコード例は、GPIO の読み取りまたは書き込み操作を実行する方法を示しています。

```cpp
    WDF_OBJECT_ATTRIBUTES RequestAttributes;
    WDF_OBJECT_ATTRIBUTES Attributes;
    WDF_REQUEST_SEND_OPTIONS SendOptions;
    WDFREQUEST IoctlRequest;
    WDFIOTARGET IoTarget;
    WDFMEMORY WdfMemory;
    NTSTATUS Status;

    WDF_OBJECT_ATTRIBUTES_INIT(&RequestAttributes);
    Status = WdfRequestCreate(&RequestAttributes, IoTarget, &IoctlRequest);
    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    //
    // Set up a WDF memory object for the IOCTL request.
    //

    WDF_OBJECT_ATTRIBUTES_INIT(&Attributes);
    Attributes.ParentObject = IoctlRequest;
    Status = WdfMemoryCreatePreallocated(&Attributes, Data, Size, &WdfMemory);
    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    //
    // Format the request.
    //

    if (ReadOperation != FALSE) {
        Status = WdfIoTargetFormatRequestForIoctl(IoTarget,
                                                  IoctlRequest,
                                                  IOCTL_GPIO_READ_PINS,
                                                  NULL,
                                                  0,
                                                  WdfMemory,
                                                  0);

    } else {
        Status = WdfIoTargetFormatRequestForIoctl(IoTarget,
                                                  IoctlRequest,
                                                  IOCTL_GPIO_WRITE_PINS,
                                                  WdfMemory,
                                                  0,
                                                  WdfMemory,
                                                  0);
    }

    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    //
    // Send the request synchronously (with a 60-second time-out).
    //

    WDF_REQUEST_SEND_OPTIONS_INIT(&SendOptions,
                                  WDF_REQUEST_SEND_OPTION_SYNCHRONOUS);
    WDF_REQUEST_SEND_OPTIONS_SET_TIMEOUT(&SendOptions,
                                         WDF_REL_TIMEOUT_IN_SEC(60));

    Status = WdfRequestAllocateTimer(IoctlRequest);
    if (!NT_SUCCESS(Status)) {
        goto RwErrorExit;
    }

    if (!WdfRequestSend(IoctlRequest, IoTarget, &SendOptions)) {
        Status = WdfRequestGetStatus(IoctlRequest);
    }

    ...
```

上のコード例では、`Data` はデータバッファーへのポインターであり、`Size` はこのデータバッファーのサイズ (バイト単位) で、要求された操作が読み取り (**TRUE**) または書き込み (**FALSE**) であるかどうかを `ReadOperation` 示します。

## <a name="for-more-information"></a>詳細情報


要求出力バッファーのビットへのデータ入力ピンのマッピングなど、 **ioctl\_GPIO\_読み取り\_** の要求の詳細については、「 [**ioctl\_GPIO\_read\_pin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_read_pins)」を参照してください。 **Ioctl\_\_gpio**の詳細については、要求入力バッファー内のビットとデータ出力ピンのマッピングなど、\_の要求を書き込みます。また、「 [**ioctl\_GPIO\_書き込み\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpio/ni-gpio-ioctl_gpio_write_pins)」を参照してください。

カーネルモードで実行される GPIO 周辺ドライバーの作成方法を示すサンプルドライバーについては、GitHub の「 [gpio sample drivers](https://go.microsoft.com/fwlink/p/?LinkId=616032)コレクション」の「デバイスサンプルドライバーの簡略化」を参照してください。

 

 




