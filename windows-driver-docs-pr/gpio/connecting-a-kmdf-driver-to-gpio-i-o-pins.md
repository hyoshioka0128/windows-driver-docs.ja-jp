---
title: KMDF ドライバーを GPIO I/O ピンに接続します。
description: どの周辺機器のカーネル モード ドライバー フレームワーク (KMDF) ドライバーでは、GPIO I/O リソースの説明を取得できます。
ms.assetid: 02F6431C-7B55-4DFB-9792-4A72F0268C76
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcf771912ecf322e67b2e6e697b2f73740312e76
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539472"
---
# <a name="connecting-a-kmdf-driver-to-gpio-io-pins"></a>KMDF ドライバーを GPIO I/O ピンに接続します。


GPIO I/O リソース、一連の 1 つまたは複数の GPIO ピンを入力またはデータのデータの出力として構成されます。 これらのピンに物理的に接続するための周辺機器のドライバーでは、オペレーティング システムから対応する GPIO I/O リソースを取得します。 周辺機器のデバイス ドライバーは、このリソースの GPIO ピンへの接続を開きし、この接続を表すハンドルを I/O 要求を送信します。

次のコード例では、周辺機器のカーネル モード ドライバー フレームワーク (KMDF) ドライバーがドライバーに、プラグ アンド プレイ (PnP) マネージャーが割り当てられている GPIO I/O リソースの説明を取得する方法を示します。

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

上記のコード例で、`DeviceExtension`変数は周辺機器のデバイスのデバイス コンテキストへのポインター。 `XyzDrvGetDeviceExtension`周辺機器のデバイス ドライバーによって、このデバイス コンテキストを取得する関数が実装されます。 このドライバーが以前に登録されてその[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック関数を呼び出して、 [ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://msdn.microsoft.com/library/windows/hardware/ff546135)メソッド。

次のコード例は、周辺機器のデバイス ドライバーが、以前に取得した GPIO リソースの説明を使用する方法を示しています。 ドライバーの GPIO I/O リソースを WDFIOTARGET ハンドルを開くためのコード例です。

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

上記のコード例で、`Device`変数は周辺機器の framework デバイス オブジェクトの WDFDEVICE ハンドルです。 **リソース\_ハブ\_作成\_パス\_FROM\_ID**関数は、GPIO I/O リソースの名前を含む文字列を作成します。 コード例では、この文字列を使用して、GPIO I/O リソースの名前を開きます。

周辺機器のデバイス ドライバーが GPIO I/O リソースを識別するハンドルを取得後、このドライバーは、GPIO ピンからデータを読み書き I/O 制御要求を送信できます。 ドライバーの GPIO I/O リソースを開くの読み取りは[ **IOCTL\_GPIO\_読み取り\_ピン**](https://msdn.microsoft.com/library/windows/hardware/hh406483)リソース内のピンからデータを読み取る I/O 制御要求。 ドライバーの GPIO I/O リソースを開くの書き込みは[ **IOCTL\_GPIO\_書き込み\_ピン**](https://msdn.microsoft.com/library/windows/hardware/hh406487)リソース内のピンにデータの書き込み I/O コントロール要求。 次のコード例では、GPIO 読み取りを実行または操作を記述する方法を示します。

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

上記のコード例で`Data`データ バッファーへのポインターは、`Size`このデータ バッファーのバイト単位のサイズと`ReadOperation`、要求された操作は、読み取り、かどうかを示します (**TRUE**) または書き込み (**FALSE**)。

## <a name="for-more-information"></a>詳細情報


詳細については**IOCTL\_GPIO\_読み取り\_ピン**、要求の出力バッファーにデータ入力ピンが、bits のマッピングを含む要求を参照してください[ **IOCTL\_GPIO\_読み取り\_ピン**](https://msdn.microsoft.com/library/windows/hardware/hh406483)します。 詳細については**IOCTL\_GPIO\_書き込み\_ピン**データの出力ピンに要求の入力バッファー内のビットのマッピングを含む要求を参照してください[ **IOCTL\_GPIO\_書き込み\_ピン**](https://msdn.microsoft.com/library/windows/hardware/hh406487)します。

カーネル モードで実行されている GPIO 周辺ドライバーを作成する方法を示すサンプル ドライバー、SimDevice サンプル ドライバーを参照してください、 [GPIO サンプル ドライバー](https://go.microsoft.com/fwlink/p/?LinkId=616032) GitHub 上のコレクション。

 

 




