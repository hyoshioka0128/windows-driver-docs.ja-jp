---
title: ユーザーモード SPB 周辺機器ドライバーのハードウェア リソース
description: SPB の周辺機器のデバイスの UMDF ドライバーのコード例と、ハードウェア リソースを取得します。
ms.assetid: 4D240011-1F4E-4C1E-8258-A2CF44BD3F06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30790a81a977f80bffc52f468912d3268a661d4f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373760"
---
# <a name="hardware-resources-for-user-mode-spb-peripheral-drivers"></a>ユーザーモード SPB 周辺機器ドライバーのハードウェア リソース


コード例では、このトピックの「表示方法、[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)上周辺機器のデバイス用の (UMDF) ドライバー、[シンプルな周辺機器のバス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) が動作するために必要なハードウェア リソースを取得しますデバイスです。 これらのリソースに含まれるは、ドライバーがデバイスへの論理接続を確立するために使用する情報です。 その他のリソースは、割り込みを含めることができ、1 つまたは複数の GPIO 入力または出力ピンです。 (GPIO ピンは、詳細については、入力または出力として構成されている汎用的な I/O コント ローラー デバイスの暗証番号 (pin) を参照してください[GPIO コント ローラー ドライバー](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview))。メモリが割り当てられているデバイスとは異なり、SPB に接続されている周辺機器は、レジスタにマップするシステムのメモリ アドレスのブロックを必要としません。

このドライバーは、実装、 [ **IPnpCallbackHardware2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware2)インターフェイス、および、UMDF ドライバーの呼び出し中にこのインターフェイスに登録[ **IDriverEntry::OnDeviceAdd** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッド。 フレームワークでメソッドを呼び出します、 **IPnpCallbackHardware2**インターフェイス、デバイスの電源状態の変化のドライバーに通知します。

SPB に接続されている周辺機器に電力が復元されると、ドライバー、フレームワークが呼び出す、 [ **IPnpCallbackHardware2::OnPrepareHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)このデバイスにする必要があるドライバーに通知するメソッド使用できるように準備します。 この呼び出し中には、ドライバーは、入力パラメーターとして 2 つのハードウェア リソースのリストを受け取ります。 *PWdfResourcesRaw*パラメーターが指す生のリソースの一覧と*pWdfResourcesTranslated*パラメーターは変換されたリソースの一覧を指します。 両方のパラメーターがへのポインター [ **IWDFCmResourceList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfcmresourcelist)オブジェクト。 翻訳済みのリソースが含まれて、*接続 ID* SPB 周辺ドライバーは、SPB に接続されている周辺機器への論理接続を確立する必要があります。 詳細については、次を参照してください。 [SPB の周辺機器の接続 Id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)します。

そのリソースの一覧で接続 Id を受信する周辺 UMDF ドライバーを有効にするドライバーをインストールする INF ファイルは、WDF 固有で、次のディレクティブを含める必要があります**DDInstall**セクション。

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**このディレクティブの詳細については、次を参照してください。 [INF ファイルで WDF ディレクティブを指定する](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)します。

次のコード例は、ドライバーの**OnPrepareHardware**メソッドからの接続 ID の取得、 *pWdfResourcesTranslated*パラメーター。

```cpp
BOOLEAN fConnectIdFound = FALSE;
BOOLEAN fDuplicateFound = FALSE;
LARGE_INTEGER connectionId = 0;
ULONG resourceCount;

resourceCount = pWdfResourcesTranslated->GetCount();

// Loop through the resources and save the relevant ones.
for (ULONG ix = 0; ix < resourceCount; ix++)
{
    PCM_PARTIAL_RESOURCE_DESCRIPTOR pDescriptor;

    pDescriptor = pWdfResourcesTranslated->GetDescriptor(ix);

    if (pDescriptor == NULL)
    {
        hr = E_POINTER;
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
                    if (fConnIdFound == FALSE)
                    {
                        // Save the SPB connection ID.
                        connectionId.LowPart = pDescriptor->u.Connection.IdLowPart;
                        connectionId.HighPart = pDescriptor->u.Connection.IdHighPart;
                        fConnectIdFound = TRUE;
                    }
                    else
                    {
                        fDuplicateFound = TRUE;
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
            // Check for interrupt resources.
            ...
        }
        break;

    default:
        // Ignore all other resource descriptors.
        break;
    }
}
```

上記のコード例では、sp B に接続されている周辺機器の接続 ID をコピーという名前の変数に`connectionId`します。 次のコード例では、周辺機器のデバイスを識別するために使用できるデバイスのパス名に、接続 ID を組み込む方法を示します。

```cpp
WCHAR szTargetPath[100];
HRESULT hres;

// Create the device path using the well-known resource hub
// path name and the connection ID.
//
// TODO: Replace this hardcoded string with the appropriate
//       helper method from Reshub.h when available.
hres = StringCbPrintfW(&szTargetPath[0],
                       sizeof(szTargetPath),
                       L"\\\\.\\RESOURCE_HUB\\%0*I64x",
                       (size_t)(sizeof(LARGE_INTEGER) * 2),
                       connectionId.QuadPart);
if (FAILED(hres))
{
     // Error handling
     ...
}
```

上記のコード例に SPB に接続されている周辺機器のパス名を書き込みます、`szTargetPath`配列。 次のコード例では、このデバイスのパス名を使用して、sp B に接続されている周辺機器へのファイル ハンドルを開きます。

```cpp
UMDF_IO_TARGET_OPEN_PARAMS openParams;

openParams.dwShareMode = 0;
openParams.dwCreationDisposition = OPEN_EXISTING;
openParams.dwFlagsAndAttributes = FILE_FLAG_OVERLAPPED;
hres = pRemoteTarget->OpenFileByName(&szTargetPath[0],
                                     (GENERIC_READ | GENERIC_WRITE),
                                     &openParams);
if (FAILED(hres))
{
    // Error handling
    ...
}
```

上記のコード例で、`pRemoteTarget`変数がへのポインター、 [ **IWDFRemoteTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfremotetarget)オブジェクト。 場合に呼び出し、 [ **IWDFRemoteTarget::OpenFileByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) SPB に接続されている周辺機器を使用できますのメソッドが成功、ドライバー、 **IWDFRemoteTarget**オブジェクトを周辺機器への I/O 要求を送信します。 ドライバーは、周辺機器を読み取り、書き込み、または IOCTL 要求を送信する前に、ドライバーを呼び出す、 [ **IWDFRemoteTarget::FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)、 [ **IWDFRemoteTarget::FormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)、または[ **IWDFRemoteTarget::FormatRequestForIoctl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl) I/O 要求の書式を指定するメソッド。 **IWDFRemoteTarget**インターフェイスからこれらの 3 つのメソッドを継承する、 [ **IWDFIoTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイス。 次に、ドライバーを呼び出し、 [ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send) SPB に接続されている周辺機器に I/O 要求を送信する方法。

SPB の周辺機器のドライバーを呼び出す次のコード例で、**送信**を送信する方法、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)への要求、周辺機器の SPB 接続します。

```cpp
HRESULT hres;
IWDFMemory *pInputMemory = NULL;
IWDFRemoteTarget *pWdfIoRequest = NULL;

// Create a new I/O request.
if (SUCCEEDED(hres))
{
    hres = pWdfDevice->CreateRequest(NULL, 
                                     pWdfDevice, 
                                     &pWdfIoRequest);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

// Allocate memory for the input buffer.
if (SUCCEEDED(hres))
{
    hres = pWdfDriver->CreatePreallocatedWdfMemory(pInBuffer, 
                                                   inBufferSize, 
                                                   NULL,
                                                   pWdfIoRequest,
                                                   &pInputMemory);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }

    // After this call, the parent holds the only reference.
    pWdfMemory->Release();
}

// Format the I/O request for a write operation.
if (SUCCEEDED(hres))
{
    hres = pRemoteTarget->FormatRequestForWrite(pWdfIoRequest,
                                                NULL,
                                                pInputMemory, 
                                                NULL, 
                                                0);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

// Send the request to the SPB controller.
if (SUCCEEDED(hres))
{
    ULONG Flags = fSynchronous ? WDF_REQUEST_SEND_OPTION_SYNCHRONOUS : 0;

    // Set the I/O completion callback.
    if (!fSynchronous)
    {
        pWdfIoRequest->SetCompletionCallback(pCallback, NULL);
    }

    hres = pWdfIoRequest->Send(pRemoteTarget, Flags, 0);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

if (fSynchronous || FAILED(hres))
{
    pWdfIoRequest->DeleteWdfObject();
    SAFE_RELEASE(pWdfIoRequest);
}
```

上記のコード例は、次のこと。

1.  `pWdfDevice`変数がへのポインター、 [ **IWDFDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice) SPB に接続されている周辺機器を表す framework デバイス オブジェクトのインターフェイス。 [ **IWDFDevice::CreateRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createrequest)メソッドは、I/O 要求を作成しでこの要求をカプセル化、 [ **IWDFIoRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイスのインスタンスを指している`pWdfIoRequest`変数。
2.  `pWdfDriver`変数がへのポインター、 [ **IWDFDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdriver) SPB の周辺機器のドライバーを表すフレームワーク ドライバー オブジェクトのインターフェイス。 `pInBuffer`と`inBufferSize`変数は、アドレスと、書き込み要求のデータを格納している入力バッファーのサイズを指定します。 [ **IWDFDriver::CreatePreallocatedWdfMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)メソッドは、入力バッファーの framework メモリ オブジェクトを作成し、指定、 **IWDFIoRequest**ポイントされるオブジェクト`pWdfIoRequest`メモリ オブジェクトの親オブジェクトを (その親がリリースされたときにメモリ オブジェクトが自動的に解放されます)。 ドライバーの呼び出し後、**リリース**をメモリにローカル参照を解放するメソッドのオブジェクトを親はこのオブジェクトへの唯一の参照を保持します。
3.  `pWdfRemoteTarget`変数は、リモート ターゲット ポインターから取得された、 **OpenFileByName**前のコード例で呼び出します。 [ **IWDFRemoteTarget::FormatRequestForWrite** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)メソッドは、書き込み操作の I/O 要求を書式設定します。
4.  `fSynchronous`変数**TRUE**書き込み要求が同期的に送信して、かどうか**FALSE**非同期的に送信する場合。 `pCallback`変数が以前に作成したへのポインター [ **IRequestCallbackRequestCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)インターフェイス。 かどうか、要求は、非同期的に呼び出しを送信する、 [ **IWDFIoRequest::SetCompletionCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)メソッドは、このインターフェイスを登録します。 後で、 [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)メソッドが呼び出され、要求が非同期的に完了したときに、ドライバーに通知します。
5.  **送信**メソッドは、sp B に接続されている周辺機器に書式設定された書き込み要求を送信します。 `Flags`変数は、書き込み要求が同期的または非同期的に送信するかどうかを示します。
6.  要求が同期的に送信される場合、 [ **IWDFIoRequest::DeleteWdfObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)メソッドによって示される、両方の I/O 要求オブジェクトを削除`pWdfIoRequest`によって示される子オブジェクトと`pInputMemory`. **IWDFIoRequest**インターフェイスからこのメソッドを継承する、 [ **IWDFObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfobject)インターフェイス。 呼び出し、要求は、非同期的に送信されてかどうか、 **DeleteWdfObject**メソッドは、ドライバーので、後で発生する必要があります**OnCompletion**メソッド。

上記のコード例の代替実装を作成**IWDFIoRequest**と**IWDFMemory**ドライバーの初期化中に、および繰り返しオブジェクトの代わりにこれらの同じオブジェクトを使用作成して、毎回新しいオブジェクトを削除するには、I/O 要求が送信されます。 詳細については、次を参照してください。 [ **IWDFIoRequest2::Reuse** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)と[ **IWDFMemory::SetBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfmemory-setbuffer)します。

さらに、代替実装が I/O 要求からの I/O のステータス コード存在検査、**送信**呼び出しが成功します。 詳細については、次を参照してください。 [ **IWDFIoRequest::GetCompletionParams**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams)します。

 

 




