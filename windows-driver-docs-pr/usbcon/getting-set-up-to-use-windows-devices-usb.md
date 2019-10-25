---
Description: Windows 8.1 以降、WinUSB 関数のセットには、デスクトップアプリケーションが USB デバイスのアイソクロナスエンドポイントとの間でデータを転送できるようにする Api が用意されています。 このようなアプリケーションの場合、Microsoft 提供の Winusb .sys はデバイスドライバーである必要があります。
title: WinUSB デスクトップ アプリから USB 等時性転送を送信する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab9a9edc25f53d571db05280476e3888ab56f026
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845008"
---
# <a name="send-usb-isochronous-transfers-from-a-winusb-desktop-app"></a>WinUSB デスクトップ アプリから USB 等時性転送を送信する


**要約**

-   アイソクロナス転送の概要を簡単に説明します。
-   エンドポイントの間隔の値に基づいてバッファーの計算を転送します。
-   [Winusb 関数](using-winusb-api-to-communicate-with-a-usb-device.md)を使用して、アイソクロナスデータの読み取りと書き込みを行う転送を送信します。

**重要な API**

-   [**WinUsb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)
-   [**WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)

Windows 8.1 以降、 [Winusb 関数](using-winusb-api-to-communicate-with-a-usb-device.md)のセットには、デスクトップアプリケーションが USB デバイスのアイソクロナスエンドポイントとの間でデータを転送できるようにする api が用意されています。 このようなアプリケーションの場合、Microsoft 提供の Winusb .sys はデバイスドライバーである必要があります。

USB デバイスでは、オーディオ/ビデオストリーミングなど、時間に依存するデータを安定した速度で転送するために、アイソクロナスエンドポイントをサポートできます。 保証された配信はありません。 適切な接続では、パケットを削除しないでください。また、パケットが失われる可能性はありませんが、アイソクロナスプロトコルではこのような損失が許容されます。

ホストコントローラーは、バス上の予約期間中にデータを送受信します。*バス間隔*と呼ばれます。 バス間隔の単位はバス速度によって異なります。 全速度の場合は1ミリ秒のフレームで、高速で SuperSpeed の場合は250マイクロ秒のマイクロフレームです。

ホストコントローラーは定期的にデバイスをポーリングします。 読み取り操作の場合、エンドポイントがデータを送信する準備が整うと、デバイスはバス間隔でデータを送信することによって応答します。 デバイスに書き込むには、ホストコントローラーがデータを送信します。

**アプリが1つのサービス間隔で送信できるデータの量**

このトピックの「*アイソクロナスパケット*とは」という用語は、1つのサービス間隔で転送されるデータの量を指します。 この値は USB ドライバースタックによって計算され、アプリはパイプ属性のクエリ中に値を取得できます。

アイソクロナスパケットのサイズによって、アプリが割り当てる転送バッファーのサイズが決まります。 バッファーはフレームの境界で終了する必要があります。 転送の合計サイズは、アプリが送信または受信するデータの量によって異なります。 転送がアプリによって開始されると、ホストは、各間隔で、ホストが1間隔で許可される最大バイト数を送受信できるように転送バッファーを packetizes します。

データ転送の場合、すべてのバス間隔が使用されるわけではありません。 このトピックでは、使用されるバス間隔を*サービス間隔*と呼びます。

**データが送信されるフレームを計算する方法**

アプリでは、次の2つの方法のいずれかでフレームを指定できます。

-   自動的に。 このモードでは、アプリは、次の適切なフレームで転送を送信するように USB ドライバースタックに指示します。 アプリでは、ドライバースタックが開始フレームを計算できるように、バッファーが連続ストリームであるかどうかも指定する必要があります。
-   現在のフレームよりも後の開始フレームを指定します。 アプリは、アプリが転送を開始してから、USB ドライバースタックで処理されるまでの待機時間を考慮する必要があります。

**コード例の説明**

このトピックの例では、これらの[Winusb 関数](using-winusb-api-to-communicate-with-a-usb-device.md)の使用方法を示します。

-   [**WinUsb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)
-   [**WinUsb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)
-   [**WinUsb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)
-   [**WinUsb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)
-   [**WinUsb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)
-   [**WinUsb\_WriteIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)
-   [**WinUsb\_ReadIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)
-   [**WinUsb\_GetCurrentFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)
-   [**WinUsb\_GetAdjustedFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)

このトピックでは、高速デバイスへの3つの転送で30ミリ秒のデータの読み取りと書き込みを行います。 パイプは、各サービス間隔で1024バイトを転送できます。 ポーリング間隔は1であるため、データはフレームのすべてのマイクロフレームで転送されます。 合計30フレームの\*8\*1024 バイトになります。

読み取りと書き込みの転送を送信するための関数呼び出しは似ています。 このアプリは、3つの転送すべてを保持するのに十分な大きさの転送バッファーを割り当てます。 アプリは、 [**Winusb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)を呼び出すことによって、特定のパイプのバッファーを登録します。 この呼び出しは、転送の送信に使用される登録ハンドルを返します。 バッファーは、後続の転送に再利用されます。バッファー内のオフセットは、次のデータセットを送受信するように調整されます。

この例の転送はすべて非同期に送信されます。 この場合、アプリは、転送ごとに1つずつ、3つの要素を持つ[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/shobjidl/ns-shobjidl-_overlapped)構造の配列を割り当てます。 アプリは、転送が完了したときに通知を受け取り、操作の結果を取得できるように、イベントを提供します。 この場合、配列内の各**オーバーラップ**構造では、アプリがイベントを割り当て、 **hevent**メンバーのハンドルを設定します。

このイメージは、 [**Winusb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)関数を使用した3つの読み取り転送を示しています。 この呼び出しは、各転送のオフセットと長さを指定します。 新しいストリームを示すには、*続行*するためのパラメーター値が FALSE です。 その後、アプリは、データの継続的ストリーミングを可能にするために、前の要求の最後のフレームの直後に後続の転送をスケジュールするように要求します。 アイソクロナスパケットの数はフレームごとにパケットとして計算されます \* フレーム数。8\*10。 この呼び出しでは、アプリは開始フレーム番号の計算を気にする必要がありません。

![アイソクロナス読み取り転送用 winusb 関数](images/isoch-app-read.png)

このイメージは、 [**Winusb\_WriteIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)関数を使用した3つの書き込み転送を示しています。 この呼び出しは、各転送のオフセットと長さを指定します。 この場合、アプリは、ホストコントローラーがデータの送信を開始できるフレーム番号を計算する必要があります。 出力時に、関数は、前の転送で使用された最後のフレームの次のフレーム番号を受け取ります。 現在のフレームを取得するために、アプリは[**Winusb\_GetCurrentFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)を呼び出します。 この時点で、アプリは、次の転送の開始フレームが現在のフレームよりも後であることを確認する必要があります。これにより、USB ドライバースタックは遅延パケットを破棄しません。 これを行うには、アプリは[**Winusb\_GetAdjustedFrameNumber**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)を呼び出して、実際の現在のフレーム番号を取得します (これは受信した現在のフレーム番号よりも後になります)。 安全性を高めるために、アプリはさらに5つのフレームを追加し、転送を送信します。

![アイソクロナス書き込み転送用 winusb 関数](images/isoch-app-write.png)

各転送が完了すると、 [**Winusb\_GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getoverlappedresult)を呼び出すことによって、転送の結果が得られます。 *Bwait*パラメーターは TRUE に設定されているため、操作が完了するまで呼び出しは返されません。 読み取りおよび書き込み転送の場合、 *lpNumberOfBytesTransferred*パラメーターは常に0です。 書き込み転送の場合、アプリは、操作が正常に完了した場合、すべてのバイトが転送されたと想定しています。 読み取り転送の場合、各アイソクロナスパケットの**長さ**のメンバー ([**USBD\_ISO\_パケット\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_iso_packet_descriptor)) には、そのパケットで転送されたバイト数が間隔ごとに含まれます。 合計の長さを取得するために、アプリはすべての**長さ**の値を追加します。

完了すると、アプリは[**Winusb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)を呼び出すことによって、アイソクロナスバッファーハンドルを解放します。

## <a name="before-you-start"></a>はじめに...


このことを確認してください。

-   デバイスドライバーは、Microsoft 提供のドライバーである WinUSB (Winusb .sys) です。 このドライバは \\Windows\\System32\\ フォルダに含まれています。 詳細については、 [winusb (winusb .sys) のインストール](winusb-installation.md)に関する説明を参照してください。

-   [**Winusb\_Initialize**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)を呼び出して、デバイスへの winusb インターフェイスハンドルを取得しました。 すべての操作は、そのハンドルを使用して実行されます。 「 [Winusb 機能を使用して Usb デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)」を参照してください。

-   アクティブインターフェイスの設定には、アイソクロナスエンドポイントがあります。 それ以外の場合、ターゲットエンドポイントのパイプにアクセスすることはできません。

## <a name="step-1-find-the-isochronous-pipe-in-the-active-setting"></a>手順 1: アクティブな設定でアイソクロナスパイプを検索する


1.  [**Winusb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)を呼び出して、アイソクロナスエンドポイントを持つ USB インターフェイスを取得します。
2.  エンドポイントを定義するインターフェイス設定のパイプを列挙します。
3.  各エンドポイントについて、winusb [ **\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)を呼び出すことによって、 [**winusb\_パイプ\_情報\_EX**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)構造体に関連付けられているパイプのプロパティを取得します。 取得した**Winusb\_パイプの\_情報\_EX**構造体には、アイソクロナスパイプに関する情報が含まれています。 構造体には、パイプ、その型、id などに関する情報が含まれています。
4.  構造体のメンバーを調べて、転送に使用する必要があるパイプであるかどうかを判断します。 存在する場合は、 **PipeId**値を格納します。 テンプレートコードで、デバイスにメンバーを追加します。この\_データ構造は、デバイス .h に定義されています。

この例では、アクティブな設定にアイソクロナスエンドポイントがあるかどうかを確認し、それに関する情報を取得する方法を示します。 この例では、デバイスはスーパー Mutt デバイスです。 デバイスには、既定のインターフェイスに2つのアイソクロナスエンドポイント (代替設定 1) があります。

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

SuperMUTT デバイスは、設定1で、既定のインターフェイス内のアイソクロナスエンドポイントを定義します。 上記のコードでは、 **PipeId**値を取得し、デバイス\_データ構造体に格納します。

## <a name="step-2-get-interval-information-about-the-isochronous-pipe"></a>手順 2: アイソクロナスパイプに関する間隔情報を取得する


次に、 [**Winusb\_QueryPipeEx**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipeex)の呼び出しで取得したパイプに関する詳細情報を取得します。

-   **転送サイズ**

    1.  取得した[**Winusb\_パイプ\_情報\_EX**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)構造体から、 **maximumbytesperinterval**と**interval**の値を取得します。
    2.  送信または受信するアイソクロナスデータの量に応じて、転送サイズを計算します。 たとえば、次の計算を考えてみます。

        ` TransferSize = ISOCH_DATA_SIZE_MS * pipeInfoEx.MaximumBytesPerInterval * (8 / pipeInfoEx.Interval);             `

        この例では、転送サイズは10ミリ秒のアイソクロナスデータに対して計算されます。

-   **アイソクロナスパケットの数**たとえば、次の計算を考えてみます。

    転送全体を保持するために必要なアイソクロナスパケットの合計数を計算します。 この情報は、読み取り転送に必要であり、`>IsochInTransferSize / pipe.MaximumBytesPerInterval;             `として計算されます。

この例では、手順1の例にコードを追加し、アイソクロナスパイプの間隔の値を取得します。

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

前のコードでは、アプリは、 [**Winusb\_パイプ\_情報\_EX**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information_ex)から**Interval**と**maximumbytesperinterval**を取得して、読み取り転送に必要な転送サイズとアイソクロナスパケットの数を計算します. 両方のアイソクロナスエンドポイントでは、 **Interval**は1です。 この値は、フレームのすべてのマイクロフレームがデータを保持することを示します。 これに基づき、10ミリ秒のデータを送信するには、10個のフレームが必要です。合計転送サイズは 10\*1024\*8 バイトと80アイソクロナスパケットで、各1024バイトになります。

## <a name="step-3-send-a-write-transfer-to-send-data-to-an-isochronous-out-endpoint"></a>手順 3: データをアイソクロナス出力エンドポイントに送信するための書き込み転送を送信する


この手順では、アイソクロナスエンドポイントにデータを書き込む手順の概要を示します。

1.  送信するデータを格納するバッファーを割り当てます。
2.  データを非同期に送信する場合は、呼び出し元が割り当てたイベントオブジェクトへのハンドルを含む[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/shobjidl/ns-shobjidl-_overlapped)構造体を割り当て、初期化します。 構造体はゼロに初期化する必要があります。それ以外の場合、呼び出しは失敗します。
3.  [**Winusb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)を呼び出してバッファーを登録します。
4.  [**Winusb\_WriteIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)を呼び出して転送を開始します。 データを転送するフレームを手動で指定する場合は、代わりに[**Winusb\_WriteIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)を呼び出します。
5.  [**Winusb\_GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getoverlappedresult)を呼び出して、転送の結果を取得します。
6.  完了したら、 [**Winusb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)、重複イベントハンドル、および転送バッファーを呼び出して、バッファーハンドルを解放します。

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

## <a name="step-4-send-a-read-transfer-to-receive-data-from-an-isochronous-in-endpoint"></a>手順 4: エンドポイントのアイソクロナスからデータを受信するために読み取り転送を送信する


この手順は、アイソクロナスエンドポイントからデータを読み取る手順をまとめたものです。

1.  転送の最後にデータを受信する転送バッファーを割り当てます。 バッファーのサイズは、手順2での転送サイズの計算に基づいている必要があります。 転送バッファーはフレーム境界で終了する必要があります。
2.  データを非同期で送信する場合は、呼び出し元が割り当てたイベントオブジェクトへのハンドルを含む[**オーバーラップ**](https://docs.microsoft.com/windows/desktop/api/shobjidl/ns-shobjidl-_overlapped)構造体を割り当てます。 構造体はゼロに初期化する必要があります。それ以外の場合、呼び出しは失敗します。
3.  [**Winusb\_RegisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)を呼び出してバッファーを登録します。
4.  手順 2. で計算したアイソクロナスパケットの数に基づいて、アイソクロナスパケットの配列 ([**USBD\_ISO\_パケット\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_iso_packet_descriptor)) を割り当てます。
5.  [**Winusb\_ReadIsochPipeAsap**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)を呼び出して転送を開始します。 データを転送する開始フレームを手動で指定する場合は、代わりに[**Winusb\_ReadIsochPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)を呼び出します。
6.  [**Winusb\_GetOverlappedResult**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getoverlappedresult)を呼び出して、転送の結果を取得します。
7.  完了したら、 [**Winusb\_UnregisterIsochBuffer**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)、重複イベントハンドル、アイソクロナスパケットの配列、および転送バッファーを呼び出すことによって、バッファーハンドルを解放します。

WinUsb\_ReadIsochPipeAsap と WinUsb\_ReadIsochPipe を呼び出して、読み取り転送を送信する方法の例を次に示します。

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
[WinUSB 機能を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)  



