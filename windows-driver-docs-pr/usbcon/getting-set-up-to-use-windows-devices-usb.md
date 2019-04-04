---
Description: Starting in Windows 8.1, the set of WinUSB Functions have APIs that allow a desktop application to transfer data to and from isochronous endpoints of a USB device. For such an application, the Microsoft-provided Winusb.sys must be the device driver.
title: WinUSB デスクトップ アプリから USB 等時性転送を送信する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e006c8cce52229f75dcfbe0771fb8ea4cf7d607b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580916"
---
# <a name="send-usb-isochronous-transfers-from-a-winusb-desktop-app"></a>WinUSB デスクトップ アプリから USB 等時性転送を送信する


**概要**

-   アイソクロナス転送の概要。
-   エンドポイントの間隔の値に基づく計算をバッファーに転送します。
-   送信転送を使用してアイソクロナス データを読み書きする[WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)します。

**重要な API**

-   [**WinUsb\_QueryPipeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265563)
-   [**WinUsb\_WriteIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265569)
-   [**WinUsb\_ReadIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265565)

以降では、Windows 8.1、一連の[WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)と USB デバイスのアイソクロナス エンドポイントからデータを転送するデスクトップ アプリケーションを許可する Api があります。 このようなアプリケーションには、Microsoft から提供された Winusb.sys はデバイス ドライバーである必要があります。

USB デバイスは、オーディオ/ビデオ ストリーミングなど、一定の速度で時間に依存するデータを転送するアイソクロナス エンドポイントをサポートできます。 配信の保証はありません。 正常な接続がすべてのパケットを削除しないでください、通常のいずれかにすると、パケットが失われる予測ではありませんが、アイソクロナス プロトコルは、このような損失を許容します。

ホスト コント ローラーを送信または受信データ バス上の時間帯の予約と呼ばれる*間隔のバス*。 バスの間隔の単位は、バス速度に依存します。 フル_スピード、高速および SuperSpeed、1 ミリ秒のフレームは、250 マイクロ秒 microframes は。

ホスト コント ローラーは、一定の間隔でデバイスをポーリングします。 読み取り操作は、エンドポイントが、データを送信する準備ができたときにデバイスを bus 間隔でデータを送信して応答します。 デバイスへの書き込みには、ホスト コント ローラーは、データを送信します。

**アプリは 1 つのサービスの間隔で送信データの量**

用語*アイソクロナス パケット*このトピックでは 1 つのサービスの間隔で転送されるデータの量を示します。 USB ドライバー スタックでその値が計算され、アプリは、パイプの属性を照会中に値を取得できます。

アイソクロナスのパケットのサイズは、アプリによって割り当てられる転送バッファーのサイズを決定します。 バッファーは、フレームの境界線に終了する必要があります。 転送の合計サイズは、データ、アプリが送信または受信する必要がある量に依存します。 アプリによって、転送が開始されると後、は、各間隔で、ホストは送信または、間隔ごとに許可される最大バイト数を受信するため、転送バッファーが packetizes ホスト。

データ転送では、すべてのバスの間隔が使用されます。 このトピックで使用するバスの間隔と呼ばれる*サービス間隔*します。

**データが転送されるフレームを計算する方法**

アプリは、2 つの方法のいずれかでフレームを指定できます。

-   自動的に。 このモードでは、アプリは、次の適切なフレームで、転送を送信する USB ドライバー スタックを指示します。 アプリは、バッファーがドライバー スタックが開始フレームを計算するために、継続的なストリームがかどうかを指定する必要がありますもできます。
-   現在のフレームよりも後の開始フレームを指定します。 アプリでは、転送し、USB ドライバー スタックがそれを処理するときに、アプリを起動するまでの待ち時間を考慮します。

**コード例の説明**

このトピックの例では、これらの使用法を示します[WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md):

-   [**WinUsb\_QueryPipeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265563)
-   [**WinUsb\_RegisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265566)
-   [**WinUsb\_UnregisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265567)
-   [**WinUsb\_WriteIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265569)
-   [**WinUsb\_ReadIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265565)
-   [**WinUsb\_WriteIsochPipe**](https://msdn.microsoft.com/library/windows/hardware/dn265568)
-   [**WinUsb\_ReadIsochPipe**](https://msdn.microsoft.com/library/windows/hardware/dn265564)
-   [**WinUsb\_GetCurrentFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265549)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265548)

このトピックでは読み取りがお高速デバイスに 3 つの転送に 30 ミリ秒のデータを書き込みます。 パイプは、各サービスの間隔で 1024 バイトを転送することができます。 ポーリング間隔が 1 であるために、フレームのすべての microframe でデータが転送されます。 30 フレームの合計は 30 に実行\*8\*1024 バイト。

読み取りを送信するため、関数を呼び出すし、書き込みの転送は似ています。 アプリでは、次の 3 つのすべての転送を保持するために十分な大きさ転送バッファーを割り当てます。 アプリが呼び出すことによって特定パイプのバッファーを登録します[ **WinUsb\_RegisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265566)します。 呼び出しは、送信、転送に使用される登録ハンドルを返します。 転送のバッファーを再利用し、バッファーのオフセットは次の一連のデータの送受信を調整します。

すべての転送の例では、非同期的に送信されます。 これは、アプリがの配列を割り当てます[ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/bb773368)の各転送には、1 つずつ、3 つの要素を含む構造体。 アプリは、転送が完了し、操作の結果を取得するときに通知を取得できるように、イベントを提供します。 これは、各**OVERLAPPED** 、配列は、アプリ内の構造がイベントの割り当てし、ハンドルを設定、 **hEvent**メンバー。

この図を使用して読み取り転送の 3 つ、 [ **WinUsb\_ReadIsochPipeAsap** ](https://msdn.microsoft.com/library/windows/hardware/dn265565)関数。 呼び出しでは、各転送のオフセットと長さを指定します。 *ContinueStream*パラメーター値が false に設定すると、新しいストリームを示します。 その後、アプリは、データのストリーミングを継続的なために、前回の要求の最後のフレームの直後に続く後続の転送をスケジュールすることを要求します。 アイソクロナス パケットの数はフレームあたりのパケット数として計算されます\*フレームの数は 8\*10。 この呼び出しで、アプリは開始フレームの数を計算するについて心配しない必要があります。

![アイソクロナス読み取り転送 winusb 関数](images/isoch-app-read.png)

この図は、転送を使用して書き込む 3 つ、 [ **WinUsb\_WriteIsochPipe** ](https://msdn.microsoft.com/library/windows/hardware/dn265568)関数。 呼び出しでは、各転送のオフセットと長さを指定します。 この場合、アプリでは、ホスト コント ローラーでデータの送信を開始できますフレーム数を計算する必要があります。 出力では、関数は、前の転送に使用される最後のフレームを次のフレームのフレーム数を受け取ります。 現在のフレームでは、アプリの呼び出しを取得する[ **WinUsb\_GetCurrentFrameNumber**](https://msdn.microsoft.com/library/windows/hardware/dn265549)します。 この時点で、アプリは、USB ドライバー スタックは遅延のパケットを削除しないように、[次へ] の転送の開始フレームが現在のフレームよりも後であることを確認して行う必要があります。 そのためをアプリの呼び出しを[ **WinUsb\_GetAdjustedFrameNumber** ](https://msdn.microsoft.com/library/windows/hardware/dn265548)現実的な現在のフレーム数を取得する (これは、受信した現在のフレーム数よりも後です)。 安全策としては、アプリは、5 つ以上のフレームを追加し、転送を送信します。

![アイソクロナス書き込み転送 winusb 関数](images/isoch-app-write.png)

アプリが呼び出すことによって、転送の結果を取得する各転送が完了すると、 [ **WinUsb\_GetOverlappedResult**](https://msdn.microsoft.com/library/windows/hardware/ff540263)します。 *して*できるように、操作が完了するまで、呼び出しが返されませんが、パラメーターを TRUE に設定します。 読み取りし、書き込みの転送の場合、 *lpNumberOfBytesTransferred*パラメーターは常に 0 です。 書き込み転送では、アプリでは、操作を正常に完了する場合すべてのバイトに転送された想定しています。 読み取りの転送、**長さ**アイソクロナス各パケットのメンバー ([**USBD\_ISO\_パケット\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539084))、間隔ごと、そのパケットの転送バイト数が含まれています。 合計の長さを取得するには、アプリを追加すべて**長さ**値。

呼び出すことによって、アプリのアイソクロナス バッファー ハンドルがリリースし終わったら、 [ **WinUsb\_UnregisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265567)します。

## <a name="before-you-start"></a>はじめに...


いることを確認してください、

-   デバイス ドライバーは、Microsoft 提供のドライバーを示します。WinUSB (Winusb.sys)。 そのドライバーが含まれて、 \\Windows\\System32\\フォルダー。 詳細については、[WinUSB (Winusb.sys) インストール](winusb-installation.md)を参照してください。

-   呼び出すことによってデバイスに WinUSB インターフェイスのハンドルを取得する以前[ **WinUsb\_初期化**](https://msdn.microsoft.com/library/windows/hardware/ff540277)します。 すべての操作は、そのハンドルを使用して実行されます。 読み取り[WinUSB 関数を使用して、USB デバイスへのアクセス方法](using-winusb-api-to-communicate-with-a-usb-device.md)します。

-   アクティブなインターフェイスの設定が、アイソクロナス エンドポイント。 それ以外の場合、ターゲット エンドポイントのパイプにアクセスすることはできません。

## <a name="step-1-find-the-isochronous-pipe-in-the-active-setting"></a>手順 1:アクティブな設定でアイソクロナス パイプを検索します。


1.  呼び出すことによって、アイソクロナス エンドポイントを持つ USB インターフェイスを取得[ **WinUsb\_QueryInterfaceSettings**](https://msdn.microsoft.com/library/windows/hardware/ff540292)します。
2.  エンドポイントを定義するインターフェイスの設定のパイプを列挙します。
3.  エンドポイントごと関連するパイプのプロパティを取得、 [ **WINUSB\_パイプ\_情報\_EX** ](https://msdn.microsoft.com/library/windows/hardware/dn265570)呼び出して構造[ **WinUsb\_QueryPipeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265563)します。 取得して、 **WINUSB\_パイプ\_情報\_EX**アイソクロナス パイプに関する情報を含む構造体。 構造体には、パイプ、その種類、id、およびなどに関する情報が含まれています。
4.  パイプの転送に使用する必要がありますがあるかどうかを判断する構造体のメンバーを確認します。 場合は、格納、 **PipeId**値。 テンプレート コードでは、デバイスにメンバーを追加\_Device.h で定義されているデータ構造体。

この例では、アクティブな設定がアイソクロナス エンドポイントを持つかどうかを決定し、それらについての情報を取得する方法を示します。 この例では、デバイスは SuperMUTT デバイスです。 デバイスでは、1 を設定する代替既定インターフェイスで 2 つのアイソクロナス エンドポイントがあります。

```ManagedCPlusPlus

typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];
    UCHAR                   IsochOutPipe;
    UCHAR                   IsochInPipe;

} DEVICE_DATA, *PDEVICE_DATA;

HRESULT
       GetIsochPipes(
       _Inout_ PDEVICE_DATA DeviceData
       )
{
       BOOL result;
       USB_INTERFACE_DESCRIPTOR usbInterface;
       WINUSB_PIPE_INFORMATION_EX pipe;
       HRESULT hr = S_OK;
       UCHAR i;

       result = WinUsb_QueryInterfaceSettings(DeviceData->WinusbHandle,
              0,
              &usbInterface);

       if (result == FALSE)
       {
              hr = HRESULT_FROM_WIN32(GetLastError());
              printf(_T("WinUsb_QueryInterfaceSettings failed to get USB interface.\n"));
              CloseHandle(DeviceData->DeviceHandle);
              return hr;
       }

       for (i = 0; i < usbInterface.bNumEndpoints; i++)
       {
              result = WinUsb_QueryPipeEx(
                     DeviceData->WinusbHandle,
                     1,
                     (UCHAR) i,
                     &pipe);

              if (result == FALSE)
              {
                     hr = HRESULT_FROM_WIN32(GetLastError());
                     printf(_T("WinUsb_QueryPipeEx failed to get USB pipe.\n"));
                     CloseHandle(DeviceData->DeviceHandle);
                     return hr;
              }

              if ((pipe.PipeType == UsbdPipeTypeIsochronous) && (!(pipe.PipeId == 0x80)))
              {
                     DeviceData->IsochOutPipe = pipe.PipeId;
              }
              else if (pipe.PipeType == UsbdPipeTypeIsochronous)
              {
                     DeviceData->IsochInPipe = pipe.PipeId;
              }
       }

       return hr;
}
```

SuperMUTT デバイスで、既定のインターフェイスでそのアイソクロナス エンドポイントが定義されて 1 を設定します。 上記のコードを取得、 **PipeId**値し、デバイスに格納\_データ構造体。

## <a name="step-2-get-interval-information-about-the-isochronous-pipe"></a>手順 2:アイソクロナス パイプに関する間隔情報を取得します。


次に、パイプへの呼び出しで取得したに関する情報を入手[ **WinUsb\_QueryPipeEx**](https://msdn.microsoft.com/library/windows/hardware/dn265563)します。

-   **転送サイズ**

    1.  取得して、 [ **WINUSB\_パイプ\_情報\_EX** ](https://msdn.microsoft.com/library/windows/hardware/dn265570)構造体を取得、 **MaximumBytesPerInterval**と**間隔**値。
    2.  アイソクロナス データの量によってを送信または受信は、転送のサイズを計算します。 たとえば、この計算を考慮してください。

        ` TransferSize = ISOCH_DATA_SIZE_MS * pipeInfoEx.MaximumBytesPerInterval * (8 / pipeInfoEx.Interval);             `

        例では、10 ミリ秒アイソクロナス データの転送サイズを計算します。

-   **Isochronous パケット数**たとえば、この計算。

    全体の転送を保持するために必要な isochronous パケットの合計数を計算します。 この情報は、読み取り転送と、計算に必要な`>IsochInTransferSize / pipe.MaximumBytesPerInterval;             `します。

この例示しますは手順 1 の例にコードを追加し、アイソクロナス パイプの間隔の値を取得します。

```ManagedCPlusPlus

#define ISOCH_DATA_SIZE_MS   10

typedef struct _DEVICE_DATA {

    BOOL                    HandlesOpen;
    WINUSB_INTERFACE_HANDLE WinusbHandle;
    HANDLE                  DeviceHandle;
    TCHAR                   DevicePath[MAX_PATH];
                UCHAR                   IsochOutPipe;
                UCHAR                   IsochInPipe;
                ULONG                   IsochInTransferSize;
                ULONG                   IsochOutTransferSize;
                ULONG                   IsochInPacketCount;

} DEVICE_DATA, *PDEVICE_DATA;


...

if ((pipe.PipeType == UsbdPipeTypeIsochronous) && (!(pipe.PipeId == 0x80)))
{
       DeviceData->IsochOutPipe = pipe.PipeId;

       if ((pipe.MaximumBytesPerInterval == 0) || (pipe.Interval == 0))
       {
         hr = E_INVALIDARG;             
             printf("Isoch Out: MaximumBytesPerInterval or Interval value is 0.\n");
             CloseHandle(DeviceData->DeviceHandle);
             return hr;
       }
       else
       {
             DeviceData->IsochOutTransferSize = 
                 ISOCH_DATA_SIZE_MS * 
                 pipe.MaximumBytesPerInterval *
                 (8 / pipe.Interval);
       }
}
else if (pipe.PipeType == UsbdPipeTypeIsochronous)
{
       DeviceData->IsochInPipe = pipe.PipeId;

       if (pipe.MaximumBytesPerInterval == 0 || (pipe.Interval == 0))
       {
         hr = E_INVALIDARG;    
             printf("Isoch Out: MaximumBytesPerInterval or Interval value is 0.\n");
             CloseHandle(DeviceData->DeviceHandle);
             return hr;
       }
       else
       {
             DeviceData->IsochInTransferSize = 
                 ISOCH_DATA_SIZE_MS * 
                 pipe.MaximumBytesPerInterval * 
                 (8 / pipe.Interval);

             DeviceData->IsochInPacketCount = 
                  DeviceData->IsochInTransferSize / pipe.MaximumBytesPerInterval;
       }
}

...
```

上記のコードでは、アプリを取得**間隔**と**MaximumBytesPerInterval**から[ **WINUSB\_パイプ\_情報\_EX** ](https://msdn.microsoft.com/library/windows/hardware/dn265570)転送サイズと読み取りの転送に必要な isochronous パケットの数を計算します。 両方のアイソクロナス エンドポイント、**間隔**は 1 です。 その値は、フレームのすべての microframes がデータを伝達することを示します。 10 フレームを作成する必要があります、転送の合計サイズは 10 に基づいて、データの 10 ミリ秒を送信する\*1024\*8 バイトと 80 アイソクロナス パケット、各 1024 バイト長。

## <a name="step-3-send-a-write-transfer-to-send-data-to-an-isochronous-out-endpoint"></a>手順 3:データをアイソクロナス エンドポイントに送信する書き込み転送を送信します。


この手順では、アイソクロナス エンドポイントにデータを書き込むための手順をまとめたものです。

1.  送信するデータを格納しているバッファーを割り当てます。
2.  データを非同期的に送信する場合は、割り当てし、初期化、 [ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/bb773368)イベントの呼び出し元が割り当てたオブジェクトへのハンドルを含む構造体。 構造体をゼロに初期化する必要があります、それ以外の場合、呼び出しは失敗します。
3.  バッファーを呼び出すことによって登録[ **WinUsb\_RegisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265566)します。
4.  転送を呼び出すことによって開始[ **WinUsb\_WriteIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265569)します。 データが転送は、呼び出しフレームを手動で指定する場合[ **WinUsb\_WriteIsochPipe** ](https://msdn.microsoft.com/library/windows/hardware/dn265568)代わりにします。
5.  呼び出すことによって、転送の結果を得る[ **WinUsb\_GetOverlappedResult**](https://msdn.microsoft.com/library/windows/hardware/ff540263)します。
6.  完了したら、呼び出すことによってバッファー ハンドルを解放[ **WinUsb\_UnregisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265567)、重複イベント ハンドル、および転送バッファー。

書き込み転送を送信する方法を示す例を次に示します。

```ManagedCPlusPlus
#define ISOCH_TRANSFER_COUNT   3

VOID
    SendIsochOutTransfer(
    _Inout_ PDEVICE_DATA DeviceData,
    _In_ BOOL AsapTransfer
    )
{
    PUCHAR writeBuffer;
    LPOVERLAPPED overlapped;
    ULONG numBytes;
    BOOL result;
    DWORD lastError;
    WINUSB_ISOCH_BUFFER_HANDLE isochWriteBufferHandle;
    ULONG frameNumber;
    ULONG startFrame;
    LARGE_INTEGER timeStamp;
    ULONG i;
    ULONG totalTransferSize;

    isochWriteBufferHandle = INVALID_HANDLE_VALUE;
    writeBuffer = NULL;
    overlapped = NULL;

    printf(_T("\n\nWrite transfer.\n"));

    totalTransferSize = DeviceData->IsochOutTransferSize * ISOCH_TRANSFER_COUNT;

    if (totalTransferSize % DeviceData->IsochOutBytesPerFrame != 0)
    {
        printf(_T("Transfer size must end at a frame boundary.\n"));
        goto Error;
    }

    writeBuffer = new UCHAR[totalTransferSize];

    if (writeBuffer == NULL)
    {
        printf(_T("Unable to allocate memory.\n"));
        goto Error;
    }

    ZeroMemory(writeBuffer, totalTransferSize);

    overlapped = new OVERLAPPED[ISOCH_TRANSFER_COUNT];
    if (overlapped == NULL)
    {
        printf("Unable to allocate memory.\n");
        goto Error;

    }

    ZeroMemory(overlapped, (sizeof(OVERLAPPED) * ISOCH_TRANSFER_COUNT));

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        overlapped[i].hEvent = CreateEvent(NULL, TRUE, FALSE, NULL);

        if (overlapped[i].hEvent == NULL)
        {
            printf("Unable to set event for overlapped operation.\n");
            goto Error;

        }
    }

    result = WinUsb_RegisterIsochBuffer(
        DeviceData->WinusbHandle,
        DeviceData->IsochOutPipe,
        writeBuffer,
        totalTransferSize,
        &isochWriteBufferHandle);

    if (!result)
    {
        printf(_T("Isoch buffer registration failed.\n"));
        goto Error;
    }

    result = WinUsb_GetCurrentFrameNumber(
                DeviceData->WinusbHandle,
                &frameNumber,
                &timeStamp);

    if (!result)
    {
        printf(_T("WinUsb_GetCurrentFrameNumber failed.\n"));
        goto Error;
    }

    startFrame = frameNumber + 5;

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {

        if (AsapTransfer)
        {
            result = WinUsb_WriteIsochPipeAsap(
                isochWriteBufferHandle,
                DeviceData->IsochOutTransferSize * i,
                DeviceData->IsochOutTransferSize,
                (i == 0) ? FALSE : TRUE,
                &overlapped[i]);

            printf(_T("Write transfer sent by using ASAP flag.\n"));
        }
        else
        {

            printf("Transfer starting at frame %d.\n", startFrame);

            result = WinUsb_WriteIsochPipe(
                isochWriteBufferHandle,
                i * DeviceData->IsochOutTransferSize,
                DeviceData->IsochOutTransferSize,
                &startFrame,
                &overlapped[i]);

            printf("Next transfer frame %d.\n", startFrame);

        }

        if (!result)
        {
            lastError = GetLastError();

            if (lastError != ERROR_IO_PENDING)
            {
                printf("Failed to send write transfer with error %x\n", lastError);
            }
        }
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        result = WinUsb_GetOverlappedResult(
            DeviceData->WinusbHandle,
            &overlapped[i],
            &numBytes,
            TRUE);

        if (!result)
        {
            lastError = GetLastError();

            printf("Write transfer %d with error %x\n", i, lastError);
        }
        else
        {
            printf("Write transfer %d completed. \n", i);

        }
    }




Error:
    if (isochWriteBufferHandle != INVALID_HANDLE_VALUE)
    {
        result = WinUsb_UnregisterIsochBuffer(isochWriteBufferHandle);
        if (!result)
        {
            printf(_T("Failed to unregister isoch write buffer. \n"));
        }
    }

    if (writeBuffer != NULL)
    {
        delete [] writeBuffer;
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        if (overlapped[i].hEvent != NULL)
        {
            CloseHandle(overlapped[i].hEvent);
        }

    }

    if (overlapped != NULL)
    {
        delete [] overlapped;
    }


    return;
}
```

## <a name="step-4-send-a-read-transfer-to-receive-data-from-an-isochronous-in-endpoint"></a>手順 4:アイソクロナス エンドポイントからデータを受け取る読み取り転送を送信します。


この手順では、アイソクロナス エンドポイントからデータを読み取るための手順をまとめたものです。

1.  転送の最後にデータを受け取る転送バッファーを割り当てます。 バッファーのサイズに基づく必要がある手順 2. で、転送のサイズを計算します。 転送バッファーは、フレームの境界線に終了する必要があります。
2.  データを非同期的に送信する場合は、割り当て、 [ **OVERLAPPED** ](https://msdn.microsoft.com/library/windows/desktop/bb773368)イベントの呼び出し元が割り当てたオブジェクトへのハンドルを含む構造体。 構造体をゼロに初期化する必要があります、それ以外の場合、呼び出しは失敗します。
3.  バッファーを呼び出すことによって登録[ **WinUsb\_RegisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265566)します。
4.  アイソクロナス数に基づいて、手順 2. で計算されたパケットがアイソクロナス パケットの配列を割り当てます ([**USBD\_ISO\_パケット\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539084))。
5.  転送を呼び出すことによって開始[ **WinUsb\_ReadIsochPipeAsap**](https://msdn.microsoft.com/library/windows/hardware/dn265565)します。 データが転送は、呼び出しの開始フレームを手動で指定する場合[ **WinUsb\_ReadIsochPipe** ](https://msdn.microsoft.com/library/windows/hardware/dn265564)代わりにします。
6.  呼び出すことによって、転送の結果を得る[ **WinUsb\_GetOverlappedResult**](https://msdn.microsoft.com/library/windows/hardware/ff540263)します。
7.  完了したら、呼び出すことによってバッファー ハンドルを解放[ **WinUsb\_UnregisterIsochBuffer**](https://msdn.microsoft.com/library/windows/hardware/dn265567)、重複イベント ハンドル、アイソクロナスのパケットの配列、および転送バッファー。

WinUsb を呼び出すことによって、読み取りの転送を送信する方法を示す例を次に示します\_ReadIsochPipeAsap と WinUsb\_ReadIsochPipe します。

```ManagedCPlusPlus
#define ISOCH_TRANSFER_COUNT   3

VOID
    SendIsochInTransfer(
    _Inout_ PDEVICE_DATA DeviceData,
    _In_ BOOL AsapTransfer
    )
{
    PUCHAR readBuffer;
    LPOVERLAPPED overlapped;
    ULONG numBytes;
    BOOL result;
    DWORD lastError;
    WINUSB_ISOCH_BUFFER_HANDLE isochReadBufferHandle;
    PUSBD_ISO_PACKET_DESCRIPTOR isochPackets;
    ULONG i;
    ULONG j;

    ULONG frameNumber;
    ULONG startFrame;
    LARGE_INTEGER timeStamp;

    ULONG totalTransferSize;

    readBuffer = NULL;
    isochPackets = NULL;
    overlapped = NULL;
    isochReadBufferHandle = INVALID_HANDLE_VALUE;

    printf(_T("\n\nRead transfer.\n"));

    totalTransferSize = DeviceData->IsochOutTransferSize * ISOCH_TRANSFER_COUNT;

    if (totalTransferSize % DeviceData->IsochOutBytesPerFrame != 0)
    {
        printf(_T("Transfer size must end at a frame boundary.\n"));
        goto Error;
    }

    readBuffer = new UCHAR[totalTransferSize];

    if (readBuffer == NULL)
    {
        printf(_T("Unable to allocate memory.\n"));
        goto Error;
    }

    ZeroMemory(readBuffer, totalTransferSize);

    overlapped = new OVERLAPPED[ISOCH_TRANSFER_COUNT];
    ZeroMemory(overlapped, (sizeof(OVERLAPPED) * ISOCH_TRANSFER_COUNT));

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        overlapped[i].hEvent = CreateEvent(NULL, TRUE, FALSE, NULL);

        if (overlapped[i].hEvent == NULL)
        {
            printf("Unable to set event for overlapped operation.\n");
            goto Error;
        }
    }

    isochPackets = new USBD_ISO_PACKET_DESCRIPTOR[DeviceData->IsochInPacketCount * ISOCH_TRANSFER_COUNT];
    ZeroMemory(isochPackets, DeviceData->IsochInPacketCount * ISOCH_TRANSFER_COUNT);

    result = WinUsb_RegisterIsochBuffer(
        DeviceData->WinusbHandle,
        DeviceData->IsochInPipe,
        readBuffer,
        DeviceData->IsochInTransferSize * ISOCH_TRANSFER_COUNT,
        &isochReadBufferHandle);

    if (!result)
    {
        printf(_T("Isoch buffer registration failed.\n"));
        goto Error;
    }

    result = WinUsb_GetCurrentFrameNumber(
                DeviceData->WinusbHandle,
                &frameNumber,
                &timeStamp);

    if (!result)
    {
        printf(_T("WinUsb_GetCurrentFrameNumber failed.\n"));
        goto Error;
    }

    startFrame = frameNumber + 5;

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        if (AsapTransfer)
        {
            result = WinUsb_ReadIsochPipeAsap(
                isochReadBufferHandle,
                DeviceData->IsochInTransferSize * i,
                DeviceData->IsochInTransferSize,
                (i == 0) ? FALSE : TRUE,
                DeviceData->IsochInPacketCount,
                &isochPackets[i * DeviceData->IsochInPacketCount],
                &overlapped[i]);

            printf(_T("Read transfer sent by using ASAP flag.\n"));

        }
        else
        {

            printf("Transfer starting at frame %d.\n", startFrame);

            result = WinUsb_ReadIsochPipe(
                isochReadBufferHandle,
                DeviceData->IsochInTransferSize * i,
                DeviceData->IsochInTransferSize,
                &startFrame,
                DeviceData->IsochInPacketCount,
                &isochPackets[i * DeviceData->IsochInPacketCount],
                &overlapped[i]);

            printf("Next transfer frame %d.\n", startFrame);

        }

        if (!result)
        {
            lastError = GetLastError();

            if (lastError != ERROR_IO_PENDING)
            {
                printf("Failed to start a read operation with error %x\n", lastError);
            }
        }
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)
    {
        result = WinUsb_GetOverlappedResult(
            DeviceData->WinusbHandle,
            &overlapped[i],
            &numBytes,
            TRUE);

        if (!result)
        {
            lastError = GetLastError();

            printf("Failed to read with error %x\n", lastError);
        }
        else
        {
            numBytes = 0;
            for (j = 0; j < DeviceData->IsochInPacketCount; j++)
            {
                numBytes += isochPackets[j].Length;
            }

            printf("Requested %d bytes in %d packets per transfer.\n", DeviceData->IsochInTransferSize, DeviceData->IsochInPacketCount);
        }

        printf("Transfer %d completed. Read %d bytes. \n\n", i+1, numBytes);
    }



Error:
    if (isochReadBufferHandle != INVALID_HANDLE_VALUE)
    {
        result = WinUsb_UnregisterIsochBuffer(isochReadBufferHandle);
        if (!result)
        {
            printf(_T("Failed to unregister isoch read buffer. \n"));
        }
    }    

    if (readBuffer != NULL)
    {
        delete [] readBuffer;
    }

    if (isochPackets != NULL)
    {
        delete [] isochPackets;
    }

    for (i = 0; i < ISOCH_TRANSFER_COUNT; i++)

    {
        if (overlapped[i].hEvent != NULL)
        {
            CloseHandle(overlapped[i].hEvent);
        }

    }

    if (overlapped != NULL)
    {
        delete [] overlapped;
    }
    return;
}
```

## <a name="related-topics"></a>関連トピック
[WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)  



