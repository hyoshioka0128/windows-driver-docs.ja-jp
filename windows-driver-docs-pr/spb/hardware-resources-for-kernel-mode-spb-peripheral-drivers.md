---
title: カーネルモード SPB 周辺機器ドライバーのハードウェア リソース
description: SPB の周辺機器用の KMDF ドライバーのコード例を示し、ハードウェアリソースを取得します。
ms.assetid: ABFFCBEC-16AB-44AF-BEF6-34AEE612EAF7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 054bc2f739205b86cb22239457d927216f59c36b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845237"
---
# <a name="hardware-resources-for-kernel-mode-spb-peripheral-drivers"></a>カーネルモード SPB 周辺機器ドライバーのハードウェア リソース


このトピックのコード例では、[単純な周辺機器バス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) 上の周辺機器の[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)(kmdf) ドライバーが、デバイスを操作するために必要なハードウェアリソースを取得する方法を示します。 これらのリソースには、デバイスへの論理接続を確立するためにドライバーが使用する情報が含まれています。 その他のリソースには、割り込みと1つ以上の GPIO 入力ピンまたは出力ピンが含まれる場合があります。 (GPIO pin は、入力または出力として構成されている汎用 i/o コントローラーデバイスの pin です。詳細については、「[汎用 i/o (GPIO) ドライバー](https://developer.microsoft.com/windows/hardware)」を参照してください)。メモリマップトデバイスの場合とは異なり、SPB に接続されている周辺機器は、レジスタをにマップするためにシステムメモリアドレスのブロックを必要としません。

このドライバーは、一連のプラグアンドプレイおよび電源管理イベントのコールバック関数を実装します。 これらの関数を KMDF に登録するために、ドライバーの[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベントコールバック関数は[**WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)メソッドを呼び出します。 このフレームワークは、電源管理イベントコールバック関数を呼び出して、周辺機器の電源状態の変化をドライバーに通知します。 これらの関数には、デバイスをドライバーからアクセスできるようにするために必要なすべての操作を実行する[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)関数が含まれています。

電源が周辺機器に復元されると、ドライバーフレームワークは、このデバイスが使用できるように準備する必要があることを SPB 周辺機器に通知するために、 *Evtdevicepreparehardware*関数を呼び出します。 この呼び出し中に、ドライバーは入力パラメーターとして2つのハードウェアリソースリストを受け取ります。 *Resourcesraw*パラメーターは、[*生のリソース*](https://docs.microsoft.com/windows-hardware/drivers/wdf/raw-and-translated-resources)のリストへの WDFCMRESLIST オブジェクトハンドルで、 *ResourcesTranslated*パラメーターは翻訳された[*リソース*](https://docs.microsoft.com/windows-hardware/drivers/wdf/raw-and-translated-resources)の一覧への WDFCMRESLIST オブジェクトハンドルです。 変換されたリソースには、周辺機器への論理接続を確立するためにドライバーが必要とする*接続 ID*が含まれます。 詳細については、「[SPB 接続周辺機器の接続 ID](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)」を参照してください。

次のコード例では、 *EvtdeviceResourcesTranslated hardware*関数が、このパラメーターから接続 ID を取得する方法を示します。

```cpp
BOOLEAN fConnectionIdFound = FALSE;
LARGE_INTEGER connectionId = 0;
ULONG resourceCount;
NTSTATUS status = STATUS_SUCCESS;

resourceCount = WdfCmResourceListGetCount(ResourcesTranslated);

// Loop through the resources and save the relevant ones.

for (ULONG ix = 0; ix < resourceCount; ix++)
{
    PCM_PARTIAL_RESOURCE_DESCRIPTOR pDescriptor;

    pDescriptor = WdfCmResourceListGetDescriptor(ResourcesTranslated, ix);

    if (pDescriptor == NULL)
    {
        status = E_POINTER;
        break;
    }

    // Determine the resource type.
    switch (pDescriptor->Type)
    {
    case CmResourceTypeConnection:
        {
            // Check against the expected connection types.

            UCHAR Class = pDescriptor->u.Connection.Class;
            UCHAR Type = pDescriptor->u.Connection.Type;

            if (Class == CM_RESOURCE_CONNECTION_CLASS_SERIAL)
            {
                if (Type == CM_RESOURCE_CONNECTION_TYPE_SERIAL_I2C)
                {
                    if (fConnectionIdFound == FALSE)
                    {
                        // Save the SPB connection ID.

                        connectionId.LowPart = pDescriptor->u.Connection.IdLowPart;
                        connectionId.HighPart = pDescriptor->u.Connection.IdHighPart;
                        fConnectionIdFound = TRUE;
                    }
                }
            }

            if (Class == CM_RESOURCE_CONNECTION_CLASS_GPIO)
            {
                // Check for GPIO pin resource.
                ...
            }
        }
        break;

    case CmResourceTypeInterrupt:
        {
            // Check for interrupt resource.
            ...
        }
        break;

    default:
        // Don't care about other resource descriptors.
        break;
    }
}
```

上記のコード例では、SPB に接続されている周辺機器の接続 ID を `connectionId`という名前の変数にコピーします。

次のコード例では、周辺機器への論理接続を開くために使用できるデバイスパス名にこの接続 ID を組み込む方法を示します。 このデバイスパス名は、周辺機器にアクセスするために必要なパラメーターの取得元となるシステムコンポーネントとして、リソースハブを識別します。

```cpp
// Use the connection ID to create the full device path name.
 
DECLARE_UNICODE_STRING_SIZE(szDeviceName, RESOURCE_HUB_PATH_SIZE);

status = RESOURCE_HUB_CREATE_PATH_FROM_ID(&szDeviceName,
                                          connectionId.LowPart,
                                          connectionId.HighPart);

if (!NT_SUCCESS(status))
{
     // Error handling
     ...
}
```

前のコード例では、 **DECLARE\_unicode\_string\_SIZE**マクロは、デバイスを格納するのに十分な大きさのバッファーを持つ、初期化された[**unicode\_文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_unicode_string)`szDeviceName` 変数の宣言を作成します。リソースハブで使用される形式のパス名。 このマクロは、Ntdef .h ヘッダーファイルで定義されています。 **リソース\_ハブの\_パス\_サイズ**定数は、デバイスパス名のバイト数を指定します。 **リソース\_ハブ\_\_ID マクロから\_パス\_を作成**すると、接続 ID からデバイスパス名が生成されます。 **リソース\_ハブ\_パス\_サイズ**と**リソース\_ハブ\_\_ID から\_パス\_を作成**するには、Reshub ヘッダーファイルで定義します。

次のコード例では、デバイスパス名を使用して、SPB に接続されている周辺機器にファイルハンドル (`SpbIoTarget`) を開きます。

```cpp
// Open the SPB peripheral device as a remote I/O target.
 
WDF_IO_TARGET_OPEN_PARAMS openParams;
WDF_IO_TARGET_OPEN_PARAMS_INIT_OPEN_BY_NAME(&openParams,
                                            &szDeviceName,
                                            (GENERIC_READ | GENERIC_WRITE));

openParams.ShareAccess = 0;
openParams.CreateDisposition = FILE_OPEN;
openParams.FileAttributes = FILE_ATTRIBUTE_NORMAL;

status = WdfIoTargetOpen(SpbIoTarget, &openParams);

if (!NT_SUCCESS(status))
{
    // Error handling
    ...
}
```

前のコード例では、 [**WDF\_io\_ターゲット\_open\_PARAMS\_\_NAME 関数によって open\_によって**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_open_by_name)、open\_に初期化[**されます。\_PARAMS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/ns-wdfiotarget-_wdf_io_target_open_params)構造体を使用すると、ドライバーはデバイスの名前を指定することによって、周辺機器への論理接続を開くことができます。\_\_\_ `SpbIoTarget` 変数は、フレームワークの i/o ターゲットオブジェクトへの WDFIOTARGET ハンドルです。 このハンドルは、この例では示されていない[**Wdfiotargetcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate)メソッドの以前の呼び出しから取得されました。 [**WdfIoTargetOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)メソッドへの呼び出しが成功した場合、ドライバーは `SpbIoTarget` ハンドルを使用して、周辺機器に i/o 要求を送信できます。

*Evtdriverdeviceadd*イベントコールバック関数では、SPB 周辺ドライバーは[**Wdfrequestcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)メソッドを呼び出して、ドライバーで使用するフレームワーク要求オブジェクトを割り当てることができます。 その後、オブジェクトが不要になったときに、ドライバーは[**Wdfobjectdelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)メソッドを呼び出してオブジェクトを削除します。 このドライバーは、 **Wdfrequestcreate**呼び出しから取得したフレームワーク要求オブジェクトを複数回再利用して、周辺機器に i/o 要求を送信できます。 読み取り、書き込み、または IOCTL 要求の場合、ドライバーは、同期メソッド[**Wdfiotargetsendreadsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)、または[**Wdfiotargetsendioctlを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)呼び出して要求を送信します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)

次のコード例では、ドライバーは**WdfIoTargetSendWriteSynchronously**を呼び出して、 [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求を SPB に接続されている周辺機器に同期的に送信します。 この例の先頭で、`pBuffer` 変数は、周辺機器に書き込まれるデータを含む非ページバッファーを指し、`dataSize` 変数はこのデータのサイズ (バイト単位) を指定します。

```cpp
ULONG_PTR bytesWritten;
NTSTATUS status;

// Describe the input buffer.

WDF_MEMORY_DESCRIPTOR memoryDescriptor;
WDF_MEMORY_DESCRIPTOR_INIT_BUFFER(&memoryDescriptor, pBuffer, dataSize);

// Configure the write request to time out after 2 seconds.

WDF_REQUEST_SEND_OPTIONS requestOptions;
WDF_REQUEST_SEND_OPTIONS_INIT(&requestOptions, WDF_REQUEST_SEND_OPTION_TIMEOUT);
requestOptions.Timeout = WDF_REL_TIMEOUT_IN_SEC(2);

// Send the write request synchronously.

status = WdfIoTargetSendWriteSynchronously(SpbIoTarget,
                                           SpbRequest,
                                           &memoryDescriptor,
                                           NULL,
                                           &requestOptions,
                                           &bytesWritten);
if (!NT_SUCCESS(status))
{
    // Error handling
    ...
}
```

上記のコード例では、次のことを行います。

1.  [**WDF\_memory\_descriptor\_INIT\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)関数呼び出しは、入力バッファーを記述する[**WDF `memoryDescriptor` MEMORY\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)構造体である\_変数を初期化します。 以前は、ドライバーは[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)などのルーチンを呼び出して、非ページプールからバッファーを割り当て、書き込みデータをこのバッファーにコピーしました。
2.  [**WDF\_request\_send\_OPTIONS\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdf_request_send_options_init)関数呼び出しによって、`requestOptions` 変数が初期化されます。この変数は、オプションの設定を含む[**WDF\_OPTIONS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/ns-wdfrequest-_wdf_request_send_options)構造を送信\_の要求です。書き込み要求の場合。\_ この例では、構造体によって、2秒後に完了しなかった場合にタイムアウトするように要求が構成されます。
3.  **WdfIoTargetSendWriteSynchronously**メソッドを呼び出すと、書き込み要求が SPB 接続周辺機器に送信されます。 メソッドは、書き込み操作が完了するかタイムアウトした後に、同期的に戻ります。必要に応じて、別のドライバースレッドが[**Wdfrequestcancelの要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)を呼び出して要求を取り消すことができます。

**WdfIoTargetSendWriteSynchronously**呼び出しでは、ドライバーは `SpbRequest`という名前の変数を提供します。これは、ドライバーによって以前に作成されたフレームワーク要求オブジェクトへのハンドルです。 **WdfIoTargetSendWriteSynchronously**呼び出しの後、通常、ドライバーは[**WdfRequestReuse**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestreuse)メソッドを呼び出して、フレームワーク要求オブジェクトを再度使用するように準備する必要があります。

 

 




