---
title: ユーザーモード SPB 周辺機器ドライバーのハードウェア リソース
description: SPB の周辺機器用の UMDF ドライバーのコード例を示し、ハードウェアリソースを取得します。
ms.assetid: 4D240011-1F4E-4C1E-8258-A2CF44BD3F06
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48c0e0dbbe16b774cad1beb96885bbe29cde3136
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844783"
---
# <a name="hardware-resources-for-user-mode-spb-peripheral-drivers"></a>ユーザーモード SPB 周辺機器ドライバーのハードウェア リソース


このトピックのコード例では、[シンプルな周辺機器バス](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(SPB) 上の周辺機器の[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) ドライバーが、デバイスを操作するために必要なハードウェアリソースを取得する方法を示します。 これらのリソースには、デバイスへの論理接続を確立するためにドライバーが使用する情報が含まれています。 その他のリソースには、割り込み、1つ以上の GPIO 入力ピンまたは出力ピンが含まれる場合があります。 (GPIO pin は、入力または出力として構成されている汎用 i/o コントローラーデバイスの pin です。詳細については、「 [Gpio Controller ドライバー](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview)」を参照してください)。メモリマップトデバイスの場合とは異なり、SPB に接続されている周辺機器は、レジスタをにマップするためにシステムメモリアドレスのブロックを必要としません。

このドライバーは、 [**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware2)インターフェイスを実装し、ドライバーの[**Idriverentry:: ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドの呼び出し中にこのインターフェイスを UMDF に登録します。 フレームワークは、 **IPnpCallbackHardware2**インターフェイスのメソッドを呼び出して、デバイスの電源状態の変更をドライバーに通知します。

電源が SPB に接続されている周辺機器に復元されると、ドライバーフレームワークは[**IPnpCallbackHardware2:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)メソッドを呼び出して、このデバイスが使用できるように準備する必要があることをドライバーに通知します。 この呼び出し中に、ドライバーは入力パラメーターとして2つのハードウェアリソースリストを受け取ります。 *Pwdfresourcesraw*パラメーターは生のリソースの一覧を指し、 *pWdfResourcesTranslated*パラメーターは翻訳されたリソースの一覧を指します。 どちらのパラメーターも、 [**Iwdfcmresourcelist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)オブジェクトへのポインターです。 変換されたリソースには、spb 周辺機器への論理接続を確立するのに必要な*接続 ID*が含まれています。 詳細については、「 [SPB 周辺機器の接続 id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)」を参照してください。

UMDF 周辺機器ドライバーがリソースリスト内の接続 Id を受信できるようにするには、ドライバーをインストールする INF ファイルで、WDF 固有の**Ddinstall**セクションに次のディレクティブを含める必要があります。

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**このディレクティブの詳細については、「 [INF ファイルでの WDF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)」を参照してください。

次のコード例では、ドライバーの**OnpWdfResourcesTranslated hardware**メソッドが、パラメーターから接続 ID を取得する方法を示します。

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

上記のコード例では、SPB に接続されている周辺機器の接続 ID を `connectionId`という名前の変数にコピーします。 次のコード例では、周辺機器を識別するために使用できるデバイスパス名に接続 ID を組み込む方法を示します。

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

前のコード例では、SPB に接続されている周辺機器のパス名を `szTargetPath` 配列に書き込みます。 次のコード例では、このデバイスパス名を使用して、SPB に接続されている周辺機器へのファイルハンドルを開きます。

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

前のコード例では、`pRemoteTarget` 変数は[**Iwdfremotetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)オブジェクトへのポインターです。 [**Iwdfremotetarget:: OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)メソッドへの呼び出しが成功した場合、SPB に接続されている周辺機器のドライバーは、 **iwdfremotetarget**オブジェクトを使用して、周辺機器に i/o 要求を送信できます。 ドライバーは、読み取り、書き込み、または IOCTL 要求を周辺機器に送信する前に、 [**Iwdfremotetarget:: FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)、 [**Iwdfremotetarget:: Formatrequestforread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)、または[**iwdfremotetarget:: を呼び出します。FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)メソッドを指定して、i/o 要求をフォーマットします。 **Iwdfremotetarget**インターフェイスは、 [**Iwdfremotetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイスからこれら3つのメソッドを継承します。 次に、ドライバーは[**IWDFIoRequest:: Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)メソッドを呼び出して、SPB に接続されている周辺機器に i/o 要求を送信します。

次のコード例では、SPB 周辺機器ドライバーが**send**メソッドを呼び出して、 [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求を spb に接続されている周辺機器に送信します。

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

上記のコード例では、次のことを行います。

1.  `pWdfDevice` 変数は、SPB に接続されている周辺機器を表すフレームワークデバイスオブジェクトの[**Iwdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスへのポインターです。 [**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)メソッドは、i/o 要求を作成し、この要求を、`pWdfIoRequest` 変数が指す[**IWDFIoRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイスインスタンスにカプセル化します。
2.  `pWdfDriver` 変数は、SPB 周辺ドライバーを表す framework driver オブジェクトの[**Iwdfdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)インターフェイスへのポインターです。 `pInBuffer` 変数と `inBufferSize` 変数は、書き込み要求のデータを格納する入力バッファーのアドレスとサイズを指定します。 [**Iwdfdriver:: CreatePreallocatedWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)メソッドは、入力バッファー用のフレームワークメモリオブジェクトを作成し、メモリオブジェクトの親オブジェクトとして `pWdfIoRequest` が指す**IWDFIoRequest**オブジェクトを指定します。これにより、memory オブジェクトは次のようになります。親がリリースされるときに自動的に解放されます)。 ドライバーが**release**メソッドを呼び出してメモリオブジェクトへのローカル参照を解放した後、親はこのオブジェクトへの唯一の参照を保持します。
3.  `pWdfRemoteTarget` 変数は、前のコード例で**OpenFileByName**呼び出しから取得したリモートターゲットポインターです。 [**Iwdfremotetarget:: FormatRequestForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)メソッドは、書き込み操作の i/o 要求を書式設定します。
4.  `fSynchronous` 変数は、書き込み要求が同期的に送信される場合は**TRUE** 、非同期的に送信される場合は**FALSE**です。 `pCallback` 変数は、以前に作成された[**Irequestによる要求完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)インターフェイスへのポインターです。 要求が非同期に送信される場合、 [**IWDFIoRequest:: Set callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)メソッドを呼び出すと、このインターフェイスが登録されます。 後で、要求が非同期に完了したことをドライバーに通知するために、 [**Irequestて Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)メソッドが呼び出されます。
5.  **Send**メソッドは、フォーマットされた書き込み要求を SPB 接続周辺機器に送信します。 `Flags` 変数は、書き込み要求が同期または非同期のどちらで送信されるかを示します。
6.  要求が同期的に送信された場合、 [**IWDFIoRequest::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)メソッドは、`pWdfIoRequest` が指す i/o 要求オブジェクトと `pInputMemory`が指す子オブジェクトの両方を削除します。 **IWDFIoRequest**インターフェイスは、このメソッドを[**Iwdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)インターフェイスから継承します。 要求が非同期に送信される場合は、ドライバーの**Oncompletion**メソッドで**Deletewdfobject**メソッドの呼び出しを後で実行する必要があります。

前のコード例の別の実装では、ドライバーの初期化中に**IWDFIoRequest**オブジェクトと**Iwdfmemory**オブジェクトを作成し、i/o が発生するたびに新しいオブジェクトを作成および削除するのではなく、同じオブジェクトを繰り返し使用します。要求が送信されました。 詳細については、「 [**IWDFIoRequest2:: 再利用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-reuse)と[**Iwdfmemory:: setbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfmemory-setbuffer)」を参照してください。

また、別の実装では、**送信**呼び出しが成功した場合に i/o 要求から i/o 状態コードを検査できます。 詳細については、「 [**IWDFIoRequest:: Get params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcompletionparams)」を参照してください。

 

 




