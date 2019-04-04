---
title: UMDF 周辺機器ドライバーをシリアル ポートに接続する
description: SerCx2 で管理されたシリアル ポートに周辺機器のデバイスの UMDF ドライバーでは、デバイスを操作する特定のハードウェア リソースが必要です。 これらのリソースに含まれるは、ドライバーは、シリアル ポートへの論理接続を開く必要がある情報です。
ms.assetid: 75FC5E79-59E9-4C07-9119-A4FE81CC318E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87dec0cb81cf16e100621063c2eb6ad4738d2c8
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349637"
---
# <a name="connecting-a-umdf-peripheral-driver-to-a-serial-port"></a>UMDF 周辺機器ドライバーをシリアル ポートに接続する


SerCx2 で管理されたシリアル ポートに周辺機器のデバイスの UMDF ドライバーでは、デバイスを操作する特定のハードウェア リソースが必要です。 これらのリソースに含まれるは、ドライバーは、シリアル ポートへの論理接続を開く必要がある情報です。 その他のリソースは、割り込みを含めることができ、1 つまたは複数の GPIO 入力または出力ピンです。

このドライバーは、実装、 [ **IPnpCallbackHardware2** ](https://msdn.microsoft.com/library/windows/hardware/hh439727)インターフェイス、および Windows ドライバー フレームワークの呼び出し中に、ドライバーのこのインターフェイスに登録[ **IDriverEntry::OnDeviceAdd** ](https://msdn.microsoft.com/library/windows/hardware/ff554896)メソッド。 フレームワークでメソッドを呼び出します、 **IPnpCallbackHardware2**インターフェイス、デバイスの電源状態の変化のドライバーに通知します。

逐次的に接続されている周辺機器が初期化されていない D0 デバイスの電源状態を入力した後、ドライバーのフレームワークが、ドライバーの[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)メソッドへの通知使用するためには、このデバイスを準備するドライバー。 この呼び出し中には、ドライバーは、入力パラメーターとして 2 つのハードウェア リソースのリストを受け取ります。 *PWdfResourcesRaw*パラメーターが指す生のリソースの一覧と*pWdfResourcesTranslated*パラメーターは変換されたリソースの一覧を指します。 両方のパラメーターがへのポインター [ **IWDFCmResourceList** ](https://msdn.microsoft.com/library/windows/hardware/hh439762)オブジェクト。 翻訳済みのリソースには、周辺機器のドライバーが連続的に接続されている周辺機器への論理接続を確立する必要がある接続 ID が含まれます。

そのリソースの一覧で接続 Id を受信する周辺 UMDF ドライバーを有効にするドライバーをインストールする INF ファイルは、WDF 固有で、次のディレクティブを含める必要があります**DDInstall**セクション。

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess**このディレクティブの詳細については、[INF ファイルで WDF ディレクティブを指定する](https://msdn.microsoft.com/library/windows/hardware/ff560526)を参照してください。 このディレクティブを使用する (対応する INF ファイルをビルドするために使用) INX ファイルの例は、、 [SpbAccelerometer ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=618052)を参照してください。

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

上記のコード例では、逐次的に接続されている周辺機器の接続 ID をコピーという名前の変数に`connectionId`します。 次のコード例では、シリアル コント ローラーに接続している周辺機器のデバイスを識別するために使用できるデバイスのパス名に、接続 ID を組み込む方法を示します。

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

上記のコード例は、シリアル コント ローラーに、デバイス パス名を書き込みます、`szTargetPath`配列。 次のコード例では、このパス名を使用して、シリアル コント ローラーへのファイル ハンドルを開きます。

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

上記のコード例で、`pRemoteTarget`パラメーターへのポインター、 [ **IWDFRemoteTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff560247)オブジェクト。 場合に呼び出し、 [ **IWDFRemoteTarget::OpenFileByName** ](https://msdn.microsoft.com/library/windows/hardware/ff560273)メソッドが成功すると、ドライバー、逐次的に接続されている周辺機器を使用できます、 **IWDFRemoteTarget**シリアル コント ローラーに I/O 要求を送信するオブジェクト。

読み取りを送信または周辺機器への書き込み要求は、ドライバー最初に呼び出すこのオブジェクトの[ **IWDFRemoteTarget::FormatRequestForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559233)または[ **IWDFRemoteTarget:。FormatRequestForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559236)メソッド要求の書式を設定します。 (、 **IWDFRemoteTarget**インターフェイスからこれらの 2 つのメソッドを継承する、 [ **IWDFIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff559170)インターフェイスです)。

最初の呼び出しをシリアル コント ローラー、ドライバーに I/O 制御要求を送信する、 [ **IWDFRemoteTarget::FormatRequestForIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff559230)メソッド要求の書式を設定します。 (、 **IWDFRemoteTarget**インターフェイスからこのメソッドを継承する、 **IWDFIoTarget**インターフェイスです)。次に、ドライバーを呼び出し、 **IWDFIoRequest::Send** I/O 制御の要求を逐次的に接続されている周辺機器に送信するメソッド。

次のコード例では、周辺機器のドライバーは、シリアル コント ローラーに I/O 制御要求を送信します。

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

上記のコード例は、次のこと。

1.  `pWdfDevice`変数がへのポインター、 [ **IWDFDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff556917)逐次的に接続されている周辺機器を表す framework デバイス オブジェクトのインターフェイス。 [ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)メソッドは、I/O 要求を作成しでこの要求をカプセル化、 [ **IWDFIoRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558985)インターフェイスのインスタンスを指している`pWdfIoRequest`パラメーター。 I/O 要求は後で削除されます (手順 6 を参照してください)。 作成し、送信される各 I/O 要求の要求オブジェクトを削除するため、この実装はやや効率的ではありません。 効率的な方法では、一連の I/O 要求の同じ要求オブジェクトを再利用します。 詳細については、[Framework 要求オブジェクトを再利用](https://msdn.microsoft.com/library/windows/hardware/ff544600)を参照してください。
2.  `pWdfDriver`変数がへのポインター、 [ **IWDFDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff558893)周辺のドライバーを表すフレームワーク ドライバー オブジェクトのインターフェイス。 `pInBuffer`と`inBufferSize`変数は、アドレスと I/O 制御要求の入力バッファーのサイズを指定します。 [ **IWDFDriver::CreatePreallocatedWdfMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff558902)メソッドは、入力バッファーの framework メモリ オブジェクトを作成し、指定、 **IWDFIoRequest**ポイントされるオブジェクト`pWdfIoRequest`メモリ オブジェクトの親オブジェクトとして。
3.  `pWdfRemoteTarget`変数は、リモート ターゲット ポインターから取得された、 **OpenFileByName**前のコード例で呼び出します。 [ **IWDFRemoteTarget::FormatRequestForIoctl** ](https://msdn.microsoft.com/library/windows/hardware/ff559230)メソッドは、I/O 制御操作の要求を書式設定します。 `ioctlCode`変数がテーブルに表示されている I/O 制御コードのいずれかに設定されている[シリアル I/O 要求インターフェイス](serial-i-o-request-interface.md)します。
4.  `fSynchronous`変数**TRUE** I/O 制御の要求が同期的に送信してはかどうか**FALSE**非同期的に送信する場合。 `pCallback`変数が以前に作成したへのポインター [ **IRequestCallbackRequestCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556904)インターフェイス。 かどうか、要求は、非同期的に呼び出しを送信する、 [ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)メソッドは、このインターフェイスを登録します。 後で、 [ **IRequestCallbackRequestCompletion::OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905)メソッドが呼び出され、要求が非同期的に完了したときに、ドライバーに通知します。
5.  **送信**メソッドは、逐次的に接続されている周辺機器に書式設定された書き込み要求を送信します。 `Flags`変数は、書き込み要求が同期的または非同期的に送信するかどうかを示します。
6.  要求が同期的に送信される場合、 [ **IWDFIoRequest::DeleteWdfObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560210)メソッドによって示される、両方の I/O 要求オブジェクトを削除`pWdfIoRequest`によって示される子オブジェクトと`pInputMemory`. **IWDFIoRequest**インターフェイスからこのメソッドを継承する、 [ **IWDFObject** ](https://msdn.microsoft.com/library/windows/hardware/ff560200)インターフェイス。 呼び出し、要求は、非同期的に送信されてかどうか、 **DeleteWdfObject**メソッドは、ドライバーので、後で発生する必要があります**OnCompletion**メソッド。

 

 




