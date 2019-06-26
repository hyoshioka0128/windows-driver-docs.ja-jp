---
title: カーネルモード SPB 周辺機器ドライバーのハードウェア リソース
description: KMDF ドライバー、SPB 上周辺機器のデバイス用のコード例と、ハードウェア リソースを取得します。
ms.assetid: ABFFCBEC-16AB-44AF-BEF6-34AEE612EAF7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca4240eac03c58d1a86ff9663115359e983cfa95
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368416"
---
# <a name="hardware-resources-for-kernel-mode-spb-peripheral-drivers"></a>カーネルモード SPB 周辺機器ドライバーのハードウェア リソース


コード例では、このトピックの「表示方法、[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)上周辺機器のデバイス用の (KMDF) ドライバーを[シンプルな周辺機器のバス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) ために必要なハードウェア リソースを取得しますデバイスを動作します。 これらのリソースに含まれるは、ドライバーがデバイスへの論理接続を確立するために使用する情報です。 その他のリソースは、割り込みと 1 つを含めることができます、または複数の GPIO 入力または出力ピンです。 (GPIO ピンは、詳細については、入力または出力として構成されている汎用的な I/O コント ローラー デバイスの暗証番号 (pin) を参照してください[汎用入出力 (GPIO) ドライバー](https://developer.microsoft.com/windows/hardware))。メモリが割り当てられているデバイスとは異なり、SPB に接続されている周辺機器は、レジスタにマップするシステムのメモリ アドレスのブロックを必要としません。

このドライバーは、一連のプラグ アンド プレイと電源管理イベントのコールバック関数を実装します。 これらを登録する関数、KMDF ドライバーの[ *EvtDriverDeviceAdd* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)イベント コールバック関数の呼び出し、 [ **WdfDeviceInitSetPnpPowerEventCallbacks**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceinitsetpnppowereventcallbacks)メソッド。 フレームワークは、周辺機器の電源状態の変更のドライバーに通知する電源管理イベントのコールバック関数を呼び出します。 これらの関数に含まれるが、 [ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)関数で、デバイスをドライバーにアクセスできるようにするために必要なすべての操作を実行します。

周辺機器に電力が復元されると、ドライバー、フレームワークが呼び出す、 *EvtDevicePrepareHardware*関数を使用するためにこのデバイスを準備する必要があります SPB 周辺ドライバーに通知します。 この呼び出し中には、ドライバーは、入力パラメーターとして 2 つのハードウェア リソースのリストを受け取ります。 *ResourcesRaw*パラメーターの一覧に WDFCMRESLIST オブジェクト ハンドルは、 [*生リソース*](https://docs.microsoft.com/windows-hardware/drivers/wdf/raw-and-translated-resources)、および*ResourcesTranslated*パラメーターの一覧に WDFCMRESLIST オブジェクト ハンドルは、 [*リソースを翻訳*](https://docs.microsoft.com/windows-hardware/drivers/wdf/raw-and-translated-resources)します。 翻訳済みのリソースが含まれて、*接続 ID*周辺機器のデバイスへの論理接続を確立するために、ドライバーが必要です。 詳細については、「[SPB 接続周辺機器の接続 ID](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)」を参照してください。

次のコード例に示す方法、 *EvtDevicePrepareHardware*関数からの接続 ID の取得、 *ResourcesTranslated*パラメーター。

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

上記のコード例では、sp B に接続されている周辺機器の接続 ID をコピーという名前の変数に`connectionId`します。

次のコード例では、周辺機器のデバイスへの論理接続を開くために使用するデバイスのパス名にこの接続の ID を組み込む方法を示します。 このデバイスのパス名では、周辺機器のデバイスへのアクセスに必要なパラメーターの取得元となるシステム コンポーネントとして、リソースのハブを識別します。

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

上記のコード例で、 **DECLARE\_UNICODE\_文字列\_サイズ**マクロは、初期化の宣言を作成します[ **UNICODE\_ 。文字列**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_unicode_string)という名前の変数`szDeviceName`リソース ハブによって使用される形式でデバイスのパス名を格納するのに十分な大きさのバッファーを持ちます。 このマクロは、Ntdef.h ヘッダー ファイルで定義されます。 **リソース\_ハブ\_パス\_サイズ**定数は、デバイスのパス名でのバイト数を指定します。 **リソース\_ハブ\_作成\_パス\_FROM\_ID**マクロの接続 id からデバイスのパス名を生成します。 **リソース\_ハブ\_パス\_サイズ**と**リソース\_ハブ\_作成\_パス\_FROM\_ID**はReshub.h ヘッダー ファイルで定義します。

次のコード例はデバイスのパス名を使用してファイル ハンドルを開く (という名前の`SpbIoTarget`) SPB に接続されている周辺機器にします。

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

上記のコード例で、 [ **WDF\_IO\_ターゲット\_オープン\_PARAMS\_INIT\_オープン\_BY\_名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdf_io_target_open_params_init_open_by_name)関数を初期化します、 [ **WDF\_IO\_ターゲット\_を開く\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/ns-wdfiotarget-_wdf_io_target_open_params)ドライバーを開けるように構成します。デバイスの名前を指定することによって、周辺機器への論理接続します。 `SpbIoTarget`変数は、I/O のフレームワーク ターゲット オブジェクトの WDFIOTARGET ハンドルです。 このハンドルは、以前の呼び出しから取得された、 [ **WdfIoTargetCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate)メソッドで、この例では表示されません。 場合に呼び出し、 [ **WdfIoTargetOpen** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)メソッドが成功すると、ドライバーを使用して、`SpbIoTarget`周辺機器への I/O 要求を送信するハンドル。

*EvtDriverDeviceAdd*イベント コールバック関数、SPB の周辺機器のドライバーが呼び出すことができます、 [ **WdfRequestCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcreate)メソッドを使用するため、framework 要求オブジェクトを割り当てるドライバー。 後で、オブジェクトが不要になったときに、ドライバーを呼び出す、 [ **WdfObjectDelete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nf-wdfobject-wdfobjectdelete)オブジェクトを削除するメソッド。 ドライバーがから取得したフレームワーク要求オブジェクトを再利用できる、 **WdfRequestCreate**周辺機器への送信 I/O 要求を複数回を呼び出します。 ドライバーの呼び出しを読み取り、書き込み、または IOCTL 要求、 [ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)、 [ **WdfIoTargetSendWriteSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)、または[ **WdfIoTargetSendIoctlSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)メソッド要求を送信します。

次のコード例で、ドライバーを呼び出す**WdfIoTargetSendWriteSynchronously**同期的に送信する、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)sp B に接続されている周辺機器を要求します。 この例の開始時、`pBuffer`周辺機器のデバイスに書き込まれるデータを格納している非ページのバッファーを指す変数と`dataSize`変数は、このデータのバイト単位のサイズを指定します。

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

上記のコード例は、次のこと。

1.  [ **WDF\_メモリ\_記述子\_INIT\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/nf-wdfmemory-wdf_memory_descriptor_init_buffer)関数呼び出しを初期化します、 `memoryDescriptor` になっている変数[ **WDF\_メモリ\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfmemory/ns-wdfmemory-_wdf_memory_descriptor)入力バッファーを記述する構造体。 以前は、ドライバーと呼ばれるルーチンなど[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)非ページ プールからバッファーを割り当て、このバッファーに書き込みデータをコピーします。
2.  [ **WDF\_要求\_送信\_オプション\_INIT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdf_request_send_options_init)関数呼び出しを初期化します、 `requestOptions` になっている変数[ **WDF\_要求\_送信\_オプション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/ns-wdfrequest-_wdf_request_send_options)書き込み要求のオプションの設定を含む構造体。 この例では、構造体は、2 秒後に完了しない場合に、要求がタイムアウトするを構成します。
3.  呼び出し、 **WdfIoTargetSendWriteSynchronously**メソッド SPB に接続されている周辺機器への書き込み要求を送信します。 書き込み操作が完了するか、タイムアウト後、このメソッドは同期的に返します。ドライバーの別のスレッドを呼び出すことができます必要に応じて、 [ **WdfRequestCancelSentRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)要求をキャンセルします。

**WdfIoTargetSendWriteSynchronously**呼び出し、という名前の変数に、ドライバーで指定されています`SpbRequest`、これは、ドライバーが以前に作成したフレームワーク要求オブジェクトを識別するハンドル。 後に、 **WdfIoTargetSendWriteSynchronously**呼び出し、ドライバーは呼び出す必要があります通常、 [ **WdfRequestReuse** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestreuse)するフレームワークの要求オブジェクトを準備する方法もう一度使用します。

 

 




