---
title: UMDF 周辺機器ドライバーをシリアル ポートに接続する
description: SerCx2 で管理されているシリアルポートの周辺機器用の UMDF ドライバーでは、デバイスを操作するために特定のハードウェアリソースが必要です。 これらのリソースには、ドライバーがシリアルポートへの論理接続を開くために必要な情報が含まれています。
ms.assetid: 75FC5E79-59E9-4C07-9119-A4FE81CC318E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f5ec0d6bf4f286c41e3fcdd5d3e1d50c6088a04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845291"
---
# <a name="connecting-a-umdf-peripheral-driver-to-a-serial-port"></a>UMDF 周辺機器ドライバーをシリアル ポートに接続する

SerCx2 で管理されているシリアルポートの周辺機器用の UMDF ドライバーでは、デバイスを操作するために特定のハードウェアリソースが必要です。 これらのリソースには、ドライバーがシリアルポートへの論理接続を開くために必要な情報が含まれています。 その他のリソースには、割り込み、1つ以上の GPIO 入力ピンまたは出力ピンが含まれる場合があります。

このドライバーは、 [**IPnpCallbackHardware2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware2)インターフェイスを実装し、ドライバーの[**Idriverentry:: ondeviceadd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-idriverentry-ondeviceadd)メソッドの呼び出し中に、このインターフェイスを Windows ドライバーフレームワークに登録します。 フレームワークは、 **IPnpCallbackHardware2**インターフェイスのメソッドを呼び出して、デバイスの電源状態の変更をドライバーに通知します。

シリアル接続された周辺機器が初期化されていない D0 デバイスの電源状態になると、ドライバーフレームワークはドライバーの[**IPnpCallbackHardware2:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware2-onpreparehardware)メソッドを呼び出して、このデバイスの使用を準備するようにドライバーに指示します。 この呼び出し中に、ドライバーは入力パラメーターとして2つのハードウェアリソースリストを受け取ります。 *Pwdfresourcesraw*パラメーターは生のリソースの一覧を指し、 *pWdfResourcesTranslated*パラメーターは翻訳されたリソースの一覧を指します。 どちらのパラメーターも、 [**Iwdfcmresourcelist**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfcmresourcelist)オブジェクトへのポインターです。 変換されたリソースには、周辺ドライバーがシリアル接続された周辺機器への論理接続を確立するために必要な接続 ID が含まれます。

UMDF 周辺機器ドライバーがリソースリスト内の接続 Id を受信できるようにするには、ドライバーをインストールする INF ファイルで、WDF 固有の**Ddinstall**セクションに次のディレクティブを含める必要があります。

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**このディレクティブの詳細については、「 [INF ファイルでの WDF ディレクティブの指定](https://docs.microsoft.com/windows-hardware/drivers/wdf/specifying-wdf-directives-in-inf-files)」を参照してください。 このディレクティブを使用する INX ファイル (対応する INF ファイルのビルドに使用) の例については、 [WDK ドライバーサンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)の SpbAccelerometer を参照してください。

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
                    if (Type == CM_RESOURCE_CONNECTION_TYPE_SERIAL_UART)
                    {
                        if (fConnIdFound == FALSE)
                        {
                            // Save the serial controller's connection ID.
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

上記のコード例では、シリアル接続された周辺機器の接続 ID を `connectionId`という名前の変数にコピーします。 次のコード例では、周辺機器が接続されているシリアルコントローラーを識別するために使用できるデバイスパス名に接続 ID を組み込む方法を示します。

```cpp
WCHAR szTargetPath[100];
HRESULT hres;

// Create the device path using the well-known resource hub
// path name and the connection ID.
//
hres = StringCbPrintfW(&szTargetPath[0],
                       sizeof(DevicePath),
                       L"\\\\.\\RESOURCE_HUB\\%0*I64x",
                       (size_t)(sizeof(LARGE_INTEGER) * 2),
                       connectionId.QuadPart);
if (FAILED(hres))
{
     // Error handling
     ...
}
```

前のコード例では、シリアルコントローラーのデバイスパス名を `szTargetPath` 配列に書き込みます。 次のコード例では、このパス名を使用して、シリアルコントローラーへのファイルハンドルを開きます。

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

前のコード例では、`pRemoteTarget` パラメーターは[**Iwdfremotetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfremotetarget)オブジェクトへのポインターです。 [**Iwdfremotetarget:: OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname)メソッドの呼び出しが成功した場合、接続されている周辺機器のドライバーは**iwdfremotetarget**オブジェクトを使用して、シリアルコントローラーに i/o 要求を送信できます。

読み取り要求または書き込み要求を周辺機器に送信するために、ドライバーはまず、このオブジェクトの[**Iwdfremotetarget:: FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)または[**iwdfremotetarget:: Formatrequestforread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforwrite)メソッドを呼び出して要求を書式設定します。 ( **Iwdfremotetarget**インターフェイスは、 [**Iwdfremotetarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイスからこれら2つのメソッドを継承します)。

I/o 制御要求をシリアルコントローラーに送信するために、ドライバーはまず[**Iwdfremotetarget:: FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)メソッドを呼び出して要求を書式設定します。 ( **Iwdfremotetarget**インターフェイスは、 **Iwdfremotetarget**インターフェイスからこのメソッドを継承します)。次に、ドライバーは**IWDFIoRequest:: Send**メソッドを呼び出して、シリアル接続されている周辺機器に i/o 制御要求を送信します。

次のコード例では、周辺ドライバーがシリアルコントローラーに i/o 制御要求を送信します。

```cpp
HRESULT hres;
IWDFMemory *pInputMemory = NULL;

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
}

// Format the request to be an I/O control request.
if (SUCCEEDED(hres))
{
    hres = pRemoteTarget->FormatRequestForIoctl(pWdfIoRequest,
                                                ioctlCode,
                                                NULL,
                                                pInputMemory, 
                                                NULL, 
                                                NULL,
                                                NULL);
    if (FAILED(hres))
    {
        // Error handling
        ...
    }
}

// Send the request to the serial controller.
if (SUCCEEDED(hres))
{
    ULONG Flags = fSynchronous ? WDF_REQUEST_SEND_OPTION_SYNCHRONOUS : 0;

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

1.  `pWdfDevice` 変数は、シリアル接続された周辺機器を表すフレームワークデバイスオブジェクトの[**Iwdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスへのポインターです。 [**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)メソッドは、i/o 要求を作成し、この要求を、`pWdfIoRequest` パラメーターによってポイントされる[**IWDFIoRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)インターフェイスインスタンスにカプセル化します。 I/o 要求は、後で削除されます (手順 6. を参照)。 この実装は、送信される各 i/o 要求に対して要求オブジェクトを作成し、削除するため、多少非効率的です。 より効率的な方法は、一連の i/o 要求に対して同じ要求オブジェクトを再利用することです。 詳細については、「[フレームワークの要求オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/wdf/reusing-framework-request-objects)の再利用」を参照してください。
2.  `pWdfDriver` 変数は、周辺機器ドライバーを表すフレームワークドライバーオブジェクトの[**Iwdfdriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)インターフェイスへのポインターです。 `pInBuffer` 変数と `inBufferSize` 変数は、i/o 制御要求の入力バッファーのアドレスとサイズを指定します。 [**Iwdfdriver:: CreatePreallocatedWdfMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createpreallocatedwdfmemory)メソッドは、入力バッファーのフレームワークメモリオブジェクトを作成し、メモリオブジェクトの親オブジェクトとして `pWdfIoRequest` が指す**IWDFIoRequest**オブジェクトを指定します。
3.  `pWdfRemoteTarget` 変数は、前のコード例で**OpenFileByName**呼び出しから取得したリモートターゲットポインターです。 [**Iwdfremotetarget:: FormatRequestForIoctl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforioctl)メソッドは、i/o 制御操作の要求を書式設定します。 `ioctlCode` 変数は、「[直列 I/o 要求インターフェイス](serial-i-o-request-interface.md)」の表に示されている i/o 制御コードのいずれかに設定されます。
4.  `fSynchronous` 変数は、i/o 制御要求が同期的に送信される場合は**TRUE** 、非同期的に送信される場合は**FALSE**です。 `pCallback` 変数は、以前に作成された[**Irequestによる要求完了**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)インターフェイスへのポインターです。 要求が非同期に送信される場合、 [**IWDFIoRequest:: Set callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)メソッドを呼び出すと、このインターフェイスが登録されます。 後で、要求が非同期に完了したことをドライバーに通知するために、 [**Irequestて Requestcompletion:: OnCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)メソッドが呼び出されます。
5.  **Send**メソッドは、フォーマットされた書き込み要求を、シリアル接続されている周辺機器に送信します。 `Flags` 変数は、書き込み要求が同期または非同期のどちらで送信されるかを示します。
6.  要求が同期的に送信された場合、 [**IWDFIoRequest::D eletewdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfobject-deletewdfobject)メソッドは、`pWdfIoRequest` が指す i/o 要求オブジェクトと `pInputMemory`が指す子オブジェクトの両方を削除します。 **IWDFIoRequest**インターフェイスは、このメソッドを[**Iwdfobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)インターフェイスから継承します。 要求が非同期に送信される場合は、ドライバーの**Oncompletion**メソッドで**Deletewdfobject**メソッドの呼び出しを後で実行する必要があります。
