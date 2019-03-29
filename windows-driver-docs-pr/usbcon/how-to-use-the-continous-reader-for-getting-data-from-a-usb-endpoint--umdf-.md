---
Description: This topic describes the WDF-provided continuous reader object. The procedures in this topic provide step-by-step instructions about how to configure the object and use it to read data from a USB pipe.
title: 継続的リーダーを使用して USB パイプからデータを読み取る方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1189bc0a691e605083181a55538c1d76a2970d6f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581313"
---
# <a name="how-to-use-the-continuous-reader-for-reading-data-from-a-usb-pipe"></a>継続的リーダーを使用して USB パイプからデータを読み取る方法


このトピックでは、WDF の継続的なリーダー オブジェクトについて説明します。 このトピックの手順では、オブジェクトを構成し、USB パイプからデータの読み取りに使用する方法についての詳細な手順を説明します。

Windows Driver Framework (WDF) と呼ばれる特殊なオブジェクトを提供する、*継続的なリーダー*します。 このオブジェクトは、データがある使用可能な限り、継続的に、一括および割り込みのエンドポイントからデータを読み取る USB クライアント ドライバーを使用できます。 リーダーを使用するには、クライアント ドライバーにドライバーがデータを読み取るエンドポイントに関連付けられている USB ターゲット パイプ オブジェクトを識別するハンドルが必要です。 エンドポイントは、アクティブな構成である必要があります。 構成をアクティブにできます 2 つの方法のいずれかで: USB 構成を選択するか、現在の構成で別の設定を変更することで。 これらの操作の詳細については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)と[USB インターフェイスで代替の設定を選択する方法](select-a-usb-alternate-setting.md)します。

継続的なリーダーを作成した後は、クライアント ドライバーは開始および必要な場合に、リーダーを停止できます。 読み取り要求が常にターゲット パイプ オブジェクトと、クライアント ドライバーで使用できるようにする継続的なリーダーでは、エンドポイントからデータを受信する準備が常にします。

継続的なリーダーは、自動的に電源管理の対象フレームワークによってではありません。 つまり、クライアント ドライバーが、デバイスが低電力状態に入ったときに、リーダーを停止し、デバイスが稼働状態に入ったときに、リーダーを再起動する必要があります。

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

クライアント ドライバーでは、継続的なリーダーを使用できます、前に、これらの要件を満たしていることを確認します。

-   USB デバイスのエンドポイントが必要です。 デバイスの構成をチェックイン[USBView](https://msdn.microsoft.com/library/ff560019(VS.85).aspx)します。 Usbview.exe は、すべての USB コント ローラーとそれらに接続されている USB デバイスを参照することができるアプリケーションです。 通常に USBView がインストール、**デバッガー** Windows Driver Kit (WDK) でのフォルダー。
-   クライアント ドライバー フレームワーク USB ターゲット デバイス オブジェクトを作成する必要があります。

    Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合、テンプレート コードは、これらのタスクを実行します。 テンプレート コードでは、ターゲット デバイス オブジェクトを識別するハンドルを取得し、デバイス コンテキストに格納します。

    **KMDF クライアント ドライバー:**

    KMDF クライアント ドライバーは、呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)メソッド。 詳細については、「デバイスのソース コード」を参照してください[USB クライアント ドライバー コード構造 (KMDF) について](understanding-the-kmdf-template-code-for-usb.md)します。

    **クライアント ドライバーの UMDF:**

    UMDF クライアント ドライバーを入手する必要があります、 [ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)フレームワーク ターゲットのデバイス オブジェクトのクエリを実行してポインター。 詳細については、次を参照してください。"[**IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)実装と USB の特定のタスク"で[USB クライアント ドライバー コード構造 (UMDF) について](understanding-the-umdf-template-code-for-usb.md)します。

-   デバイスをアクティブな構成が必要です。

    USB テンプレートを使用している場合に、コードは、各インターフェイスの最初の構成と既定の代替設定を選択します。 別の設定を変更する方法については、次を参照してください。 [USB インターフェイスで代替の設定を選択する方法](select-a-usb-alternate-setting.md)します。

    **KMDF クライアント ドライバー:**

    KMDF クライアント ドライバーを呼び出す必要があります、 [ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101)メソッド。

    **クライアント ドライバーの UMDF:**

    UMDF のクライアント ドライバーの場合は、フレームワークは、その構成の最初の構成と各インターフェイスの既定の代替設定を選択します。

-   クライアント ドライバーのエンドポイントのフレームワーク ターゲット パイプ オブジェクトを識別するハンドルが必要です。 詳細については、次を参照してください。 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

<a name="instructions"></a>手順
------------

### <a name="using-the-continuous-reader---kmdf-client-driver"></a>継続的なリーダー - KMDF クライアント ドライバーを使用します。

1.  継続的なリーダーを構成します。

    1.  初期化を[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552561)構造を呼び出すことによって、 [ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552561_init)マクロ。
    2.  その構成オプションを指定、 [ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552561)構造体。
    3.  呼び出す、 [ **WdfUsbTargetPipeConfigContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff551130)メソッド。

    次のコード例では、指定されたターゲット パイプ オブジェクトの継続的なリーダーを構成します。

    ```cpp
    NTSTATUS FX3ConfigureContinuousReader(
        _In_ WDFDEVICE Device,
        _In_ WDFUSBPIPE Pipe)
    {
        NTSTATUS status;

        PDEVICE_CONTEXT                     pDeviceContext;       

        WDF_USB_CONTINUOUS_READER_CONFIG    readerConfig;

        PPIPE_CONTEXT                       pipeContext;  

        PAGED_CODE();

        pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);

        pipeContext = GetPipeContext (Pipe);

        WDF_USB_CONTINUOUS_READER_CONFIG_INIT(  
            &readerConfig,  
            FX3EvtReadComplete,  
            pDeviceContext,  
            pipeContext->MaxPacketSize);  

        readerConfig.EvtUsbTargetPipeReadersFailed=FX3EvtReadFailed;  

        status = WdfUsbTargetPipeConfigContinuousReader(  
            Pipe,  
            &readerConfig);  

        if (!NT_SUCCESS (status))
        {
            TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                "%!FUNC! WdfUsbTargetPipeConfigContinuousReader failed 0x%x", status);

            goto Exit;
        }


    Exit:
        return status;
    }
    ```

通常、クライアント ドライバーが連続でリーダーを構成、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)アクティブな設定で、対象のパイプ オブジェクトを列挙した後、コールバック関数。

前の例では、クライアント ドライバーは、2 つの方法では、その構成オプションを指定します。 呼び出して最初[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552566)を設定してから[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552561)メンバー。 パラメーターに注意してください**WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG\_INIT**します。 これらの値が必須です。 この例では、クライアント ドライバーを指定します。

-   ドライバーを実装する完了ルーチンへのポインター。 フレームワークは、読み取り要求を完了すると、このルーチンを呼び出します。 入力候補のルーチンで、ドライバーは読み取られたデータが含まれるメモリ位置にアクセスできます。 完了ルーチンの実装は、手順 2. で説明します。
-   ドライバー定義のコンテキストへのポインター。
-   1 つの転送にデバイスから読み取ることができるバイト数。 クライアント ドライバーは、その情報を取得できます、 [ **WDF\_USB\_パイプ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff553037)呼び出して構造[ **WdfUsbInterfaceGetConfiguredPipe**](https://msdn.microsoft.com/library/windows/hardware/ff550057)または[ **WdfUsbTargetPipeGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff551142)メソッド。 詳細については、次を参照してください。 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

[**WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG\_INIT** ](https://msdn.microsoft.com/library/windows/hardware/ff552566)構成の既定値を使用する継続的なリーダー *NumPendingReads*. その値は、フレームワークが保留中のキューに追加の読み取り要求の数を決定します。 多くのプロセッサ構成の多くのデバイスのそれなりのパフォーマンスを提供する既定値と判断されました。

指定された構成パラメーターだけでなく[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552566)、例でも設定して失敗ルーチン[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff552561)します。 このエラーのルーチンでは、省略可能です。

他のメンバーがあるだけでなく、エラー ルーチン[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG** ](https://msdn.microsoft.com/library/windows/hardware/ff552561)クライアント ドライバーができます。転送バッファーのレイアウトを指定する場合に使用します。 たとえば、ネットワーク パケットの受信を継続的なリーダーを使用するネットワーク ドライバーを検討してください。 各パケットには、ヘッダー、ペイロード、およびフッターのデータが含まれています。 パケットを記述するドライバーする必要がありますまずサイズを指定、パケットの呼び出しで[ **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552561_init). ドライバーが設定して、ヘッダーとフッターの長さを指定する必要がありますし、 **HeaderLength**と**TrailerLength**のメンバー **WDF\_USB\_CONTINUOUS\_リーダー\_CONFIG**します。 フレームワークでは、これらの値を使って、ペイロードのいずれかの側のバイト オフセットを計算します。 エンドポイントのペイロード データが読み取られると、フレームワークは、バッファー、オフセットの間の部分でそのデータを格納します。

2.  完了ルーチンを実装します。

    フレームワークは、要求が完了するたびにクライアント ドライバーの実装の完了ルーチンを呼び出します。 フレームワークは、読み取られたバイトとパイプから読み取られるデータを格納するバッファーが WDFMEMORY オブジェクトの数を渡します。

    次のコード例では、完了の日常的な実装を示します。

    ```cpp
    EVT_WDF_USB_READER_COMPLETION_ROUTINE FX3EvtReadComplete;

    VOID FX3EvtReadComplete(
        __in  WDFUSBPIPE Pipe,
        __in  WDFMEMORY Buffer,
        __in  size_t NumBytesTransferred,
        __in  WDFCONTEXT Context
        )
    {

        PDEVICE_CONTEXT  pDeviceContext;  
        PVOID  requestBuffer;    

        pDeviceContext = (PDEVICE_CONTEXT)Context;

        if (NumBytesTransferred == 0)
        {
            return;
        }

        requestBuffer = WdfMemoryGetBuffer(Buffer, NULL);

        if (Pipe == pDeviceContext->InterruptPipe)
        {
            KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL,
                                    "Interrupt endpoint: %s.\n", 
                                    requestBuffer )); 
        }


        return;
    }

    ```

フレームワークは、要求が完了するたびにクライアント ドライバーの実装の完了ルーチンを呼び出します。 フレームワークは、各読み取り操作にメモリ オブジェクトを割り当てます。 入力候補のルーチンでは、フレームワークは、メモリ オブジェクトに読み取られたバイトと WDFMEMORY ハンドルの数を渡します。 オブジェクトのメモリ バッファーには、パイプから読み取られるデータが含まれています。 クライアント ドライバーでは、メモリ オブジェクトを解放する必要があります。 各完了ルーチンの返された後に、フレームワークは、オブジェクトを解放します。 クライアント ドライバーは、受信データを格納する必要がある場合、ドライバーは、完了のルーチンで、バッファーの内容をコピーする必要があります。

3.  失敗ルーチンを実装します。

    フレームワークは、継続的なリーダーが読み取り要求の処理中にエラーを報告しているドライバーを通知するためにクライアント ドライバーが実装されている失敗ルーチンを呼び出します。 要求が失敗したフレームワーク パス ターゲット パイプへのポインターがオブジェクト、およびエラー コードの値。 これらのエラー コード値に基づいて、ドライバーは、エラー回復メカニズムを実装できます。 ドライバーは、フレームワークに、フレームワーク、継続的なリーダーを再起動する必要があるかどうかを示す適切な値を返すも必要があります。

    次のコード例では、障害の日常的な実装を示します。

    ```cpp
    EVT_WDF_USB_READERS_FAILED FX3EvtReadFailed;  

    BOOLEAN  
    FX3EvtReadFailed(  
        WDFUSBPIPE      Pipe,  
        NTSTATUS        Status,  
        USBD_STATUS     UsbdStatus  
        )  
    {      
        UNREFERENCED_PARAMETER(Status);  

        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                "%!FUNC! ReadersFailedCallback failed NTSTATUS 0x%x, UsbdStatus 0x%x\n", 
                     status,
                     UsbdStatus);

        return TRUE;  
    }  
    ```

前の例では、ドライバーは、TRUE を返します。 この値は、ことは、パイプをリセットし、継続的なリーダーを再起動が必要があります、フレームワークに示します。

または、クライアント ドライバーは、FALSE を返すし、パイプで停止条件が発生した場合、エラー回復メカニズムを提供します。 たとえば、ドライバーは USBD 状態を確認し、停止状態をクリアするパイプのリセット要求を発行できます。

エラー回復パイプの詳細については、次を参照してください。 [USB パイプ エラーから回復する方法](how-to-recover-from-usb-pipe-errors.md)します。

4.  デバイスが稼働状態に入ったときに、継続的なリーダーを開始するためにフレームワークを指示します。デバイスが稼働状態になったときに、リーダーを停止します。 これらのメソッドを呼び出すし、I/O の対象オブジェクトとしてターゲット パイプ オブジェクトを指定します。

    -   [**WdfIoTargetStart**](https://msdn.microsoft.com/library/windows/hardware/ff548677)
    -   [**WdfIoTargetStop**](https://msdn.microsoft.com/library/windows/hardware/ff548680)

    継続的なリーダーは、自動的に電源管理の対象フレームワークによってではありません。 そのため、クライアント ドライバーが開始に明示的に、またはデバイスの電源の状態が変更されたときにターゲット パイプ オブジェクトを停止する必要があります。 ドライバー呼び出し[ **WdfIoTargetStart** ](https://msdn.microsoft.com/library/windows/hardware/ff548677)ドライバーの[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)実装します。 この呼び出しにより、デバイスが稼働状態の場合にのみ、キューが要求を配信するようになります。 逆に、ドライバーを呼び出す[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)ドライバーで[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)実装、キューを停止するようにデバイスが低電力状態に入ったときに、要求を提供します。

次のコード例では、指定されたターゲット パイプ オブジェクトの継続的なリーダーを構成します。

```cpp

EVT_WDF_DEVICE_D0_ENTRY FX3EvtDeviceD0Entry;

NTSTATUS FX3EvtDeviceD0Entry(
    __in  WDFDEVICE Device,
    __in  WDF_POWER_DEVICE_STATE PreviousState
    )
{
    PDEVICE_CONTEXT  pDeviceContext;

    NTSTATUS status;

    PAGED_CODE();

    pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);


    status = WdfIoTargetStart (WdfUsbTargetPipeGetIoTarget (pDeviceContext->InterruptPipe));

    if (!NT_SUCCESS (status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not start interrupt pipe failed 0x%x", status);
    }

}

EVT_WDF_DEVICE_D0_EXIT FX3EvtDeviceD0Exit;

NTSTATUS FX3EvtDeviceD0Exit(
    __in  WDFDEVICE Device,
    __in  WDF_POWER_DEVICE_STATE TargetState
    )
{
    PDEVICE_CONTEXT  pDeviceContext;      

    NTSTATUS status;

    PAGED_CODE();

    pDeviceContext = WdfObjectGet_DEVICE_CONTEXT(Device);


    WdfIoTargetStop (WdfUsbTargetPipeGetIoTarget (pDeviceContext->InterruptPipe), WdfIoTargetCancelSentIo));

}
```

前の例では、実装[ *EvtDeviceD0Entry* ](https://msdn.microsoft.com/library/windows/hardware/ff540848)と[ *EvtDeviceD0Exit* ](https://msdn.microsoft.com/library/windows/hardware/ff540855)コールバック ルーチン。 Action パラメーターの[ **WdfIoTargetStop** ](https://msdn.microsoft.com/library/windows/hardware/ff548680)デバイスが稼働状態になったときに、キューで保留中の要求のアクションを決定する、クライアント ドライバーを使用します。 例では、ドライバーを指定します**WdfIoTargetCancelSentIo**します。 そのオプションは、キュー内のすべての保留中の要求をキャンセルするためにフレームワークを指示します。 または、ドライバーは保留中の I/O ターゲットを停止する前に完了または保留中の要求を保持し、I/O ターゲットを再起動すると再開要求を待機するフレームワークに指示できます。

### <a name="using-the-continuous-reader---umdf-client-driver"></a>継続的なリーダー - UMDF クライアント ドライバーを使用します。

継続的なリーダーを使用して、開始する前に、リーダーの実装でを構成する必要があります[ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)メソッド。 ポインターを取得したら[ **IWDFUsbTargetPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff560391)のエンドポイントに関連付けられているターゲット パイプ オブジェクトのインターフェイスでこれらの手順を実行します。

**継続的なリーダーを構成します。**

1.  呼び出す**QueryInterface**ターゲット パイプ オブジェクトの ([**IWDFUsbTargetPipe**](https://msdn.microsoft.com/library/windows/hardware/ff560391)) に対してクエリを実行し、 [ **IWDFUsbTargetPipe2**](https://msdn.microsoft.com/library/windows/hardware/ff560394)インターフェイス。
2.  呼び出す**QueryInterface**デバイス コールバック オブジェクトとのクエリで、 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)インターフェイス。 継続的なリーダーを使用するには、IUsbTargetPipeContinuousReaderCallbackReadComplete を実装する必要があります。 実装は、このトピックの後半で説明します。
3.  呼び出す**QueryInterface**デバイス コールバック オブジェクトとのクエリで、 [IUsbTargetPipeContinuousReaderCallbackReadersFailed](https://msdn.microsoft.com/library/windows/hardware/ff556914)インターフェイスのエラーのコールバックを実装している場合。 実装は、このトピックの後半で説明します。
4.  呼び出す、 [ **IWDFUsbTargetPipe2::ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)メソッド ヘッダー、トレーラー、保留中の要求、および完了への参照の数など、構成パラメーターを指定しますエラー コールバック メソッドです。

    メソッドは、ターゲットのパイプ オブジェクトの継続的なリーダーを構成します。 継続的なリーダーは、送信はそのターゲット パイプ オブジェクトから受信した読み取り要求のセットを管理するキューを作成します。

次のコード例では、指定されたターゲット パイプ オブジェクトの継続的なリーダーを構成します。 例では、呼び出し元によって指定されたターゲット パイプ オブジェクトがのエンドポイントに関連付けられていることを前提としています。 継続的なリーダーが読み取るように構成 USBD\_既定\_最大\_転送\_サイズ バイトを表します保留中の要求が、framework で使用して、ドライバーによって提供される、クライアントを呼び出す既定の数を使用するには。入力候補およびエラーのコールバック メソッド。 受信バッファーでは、任意のヘッダーまたはトレーラーのデータは含まれません。

```cpp
HRESULT CDeviceCallback::ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe)
{
    if (!pFxPipe)
    {
        return E_INVALIDARG;
    }

    IUsbTargetPipeContinuousReaderCallbackReadComplete *pOnCompletionCallback = NULL;
    IUsbTargetPipeContinuousReaderCallbackReadersFailed *pOnFailureCallback = NULL;
    IWDFUsbTargetPipe2* pFxUsbPipe2 = NULL;

    HRESULT hr = S_OK;

    // Set up the continuous reader to read from the target pipe object.

    //Get a pointer to the target pipe2 object.
    hr = pFxPipe->QueryInterface(IID_PPV_ARGS(&pFxUsbPipe2));
    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

    //Get a pointer to the completion callback.
    hr = QueryInterface(IID_PPV_ARGS(&pOnCompletionCallback));
    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

    //Get a pointer to the failure callback.
    hr = QueryInterface(IID_PPV_ARGS(&pOnFailureCallback));
    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

    //Get a pointer to the target pipe2 object.
    hr = pFxUsbPipe2->ConfigureContinuousReader (    
        USBD_DEFAULT_MAXIMUM_TRANSFER_SIZE, //size of data to be read
        0, //Header
        0, //Trailer
        0, // Number of pending requests queued by WDF
        NULL, // Cleanup callback. Not provided.
        pOnCompletionCallback, //Completion routine.
        NULL, //Completion routine context. Not provided.
        pOnFailureCallback); //Failure routine. Not provided

    if (FAILED(hr))
    {   
        goto ConfigureContinuousReaderExit;
    }

ConfigureContinuousReaderExit:

    if (pOnFailureCallback)
    {
        pOnFailureCallback->Release();
        pOnFailureCallback = NULL;
    }

    if (pOnCompletionCallback)
    {
        pOnCompletionCallback->Release();
        pOnCompletionCallback = NULL;
    }

    if (pFxUsbPipe2)
    {
        pFxUsbPipe2->Release();
        pFxUsbPipe2 = NULL;
    }

    return hr;
}
```

デバイスに入って動作状態を終了するときに、ターゲットのパイプ オブジェクトの状態を次に、指定 (**D0**)。

デバイスがである場合にのみ、キューが要求を配信クライアント ドライバーでは、パイプに要求を送信する電源管理対象のキューを使用している場合、 **D0**状態。 デバイスの電源状態が変更された場合**D0**低電力状態に (で**D0**終了)、ターゲットのパイプ オブジェクトが保留中の要求を完了すると、およびターゲット パイプ オブジェクトに要求を送信、キューを停止します. そのため、クライアント ドライバーでは、開始およびターゲットのパイプ オブジェクトを停止する必要はありません。

継続的なリーダーは、要求を送信するのに電源管理対象のキューを使用しません。 そのため、開始または、デバイスの電源の状態が変更されたときにターゲット パイプ オブジェクトを停止する必要があります明示的にします。 ターゲットのパイプ オブジェクトの状態を変更するには、使用することができます、 [ **IWDFIoTargetStateManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff559198) framework によって実装されるインターフェイス。 ポインターを取得したら[ **IWDFUsbTargetPipe** ](https://msdn.microsoft.com/library/windows/hardware/ff560391)のエンドポイントに関連付けられているターゲット パイプ オブジェクトのインターフェイスで、次の手順を実行します。

**状態管理を実装します。**

1.  実装で[ **IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)、呼び出す [**QueryInterface**ターゲット パイプ オブジェクトの ([ **IWDFUsbTargetPipe**](https://msdn.microsoft.com/library/windows/hardware/ff560391)) に対してクエリを実行し、 [ **IWDFIoTargetStateManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff559198)インターフェイス。 デバイス コールバック クラスのメンバー変数に参照を格納します。
2.  実装、 [ **IPnpCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff556762)デバイス コールバック オブジェクトのインターフェイス。
3.  実装では、 [ **IPnpCallback::OnD0Entry** ](https://msdn.microsoft.com/library/windows/hardware/ff556799)メソッドを呼び出します[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)を開始します継続的なリーダー。
4.  実装では、 [ **IPnpCallback::OnD0Exit** ](https://msdn.microsoft.com/library/windows/hardware/ff556803)メソッドを呼び出します[ **IWDFIoTargetStateManagement::Stop** ](https://msdn.microsoft.com/library/windows/hardware/ff559217)を停止します継続的なリーダー。

動作状態を入力すると、デバイス (**D0**)、指定されたターゲットを起動するコールバック メソッドを D0 エントリのクライアント ドライバー、フレームワークによってオブジェクトをパイプ処理します。 デバイスから離したときに、 **D0**状態では、フレームワーク、D0 終了のコールバック メソッドを呼び出します。 ターゲットのパイプ オブジェクトでは、保留中のクライアント ドライバーで構成されている、読み取り要求の数が完了して、新しい要求の受け入れを停止します。
次のコード例の実装、 [IPnpCallback](https://msdn.microsoft.com/library/windows/hardware/ff556762)デバイス コールバック オブジェクトのインターフェイス。

```cpp
class CDeviceCallback : 
    public IPnpCallbackHardware, 
    public IPnpCallback,
{
public:
    CDeviceCallback();
    ~CDeviceCallback();
    virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, VOID** ppvObject);
    virtual ULONG STDMETHODCALLTYPE AddRef();
    virtual ULONG STDMETHODCALLTYPE Release();

    virtual HRESULT STDMETHODCALLTYPE OnPrepareHardware(IWDFDevice* pDevice);
    virtual HRESULT STDMETHODCALLTYPE OnReleaseHardware(IWDFDevice* pDevice); 

    virtual HRESULT STDMETHODCALLTYPE OnD0Entry(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual HRESULT STDMETHODCALLTYPE OnD0Exit(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual void STDMETHODCALLTYPE OnSurpriseRemoval(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryRemove(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryStop(IWDFDevice*  pWdfDevice);    

private:
    LONG m_cRefs;
    IWDFUsbTargetPipe* m_pFxUsbPipe;
    IWDFIoTargetStateManagement* m_pFxIoTargetInterruptPipeStateMgmt;

    HRESULT CreateUSBTargetDeviceObject (IWDFDevice* pFxDevice, IWDFUsbTargetDevice** ppUSBTargetDevice);
    HRESULT ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe);
};
```

次のコード例は、IPnpCallback::OnPrepareHardware メソッドでターゲット パイプ オブジェクトの IWDFIoTargetStateManagement インターフェイスへのポインターを取得する方法を示しています。

```cpp
   //Enumerate the endpoints and get the interrupt pipe.

    for (UCHAR index = 0; index < NumEndpoints; index++)
    {
        hr = pFxInterface->RetrieveUsbPipeObject(index, &pFxPipe);

        if (SUCCEEDED (hr) && pFxPipe)
        {
            if ((pFxPipe->IsInEndPoint()) && (pFxPipe->GetType()==UsbdPipeTypeInterrupt))
            {
                //Pipe is for an interrupt IN endpoint.

                hr = pFxPipe->QueryInterface(IID_PPV_ARGS(&m_pFxIoTargetInterruptPipeStateMgmt));

                if (m_pFxIoTargetInterruptPipeStateMgmt)
                {               
                    m_pFxUsbPipe = pFxPipe;

                    break;
                }

            }
            else
            {
                //Pipe is NOT for an interrupt IN endpoint.

                pFxPipe->Release();
                pFxPipe = NULL;
            }
        }
        else
        {
             //Pipe not found.
        }
    }
```

次のコード例へのポインターを取得する方法を示しています、 [ **IWDFIoTargetStateManagement** ](https://msdn.microsoft.com/library/windows/hardware/ff559198)でターゲット パイプ オブジェクトのインターフェイス、 [ **IPnpCallbackHardware::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556766)メソッド。

```cpp
 HRESULT CDeviceCallback::OnD0Entry(
    IWDFDevice*  pWdfDevice,
    WDF_POWER_DEVICE_STATE  previousState
    )
{

    if (!m_pFxIoTargetInterruptPipeStateMgmt)
    {
        return E_FAIL;
    }

    HRESULT hr = m_pFxIoTargetInterruptPipeStateMgmt->Start();

    if (FAILED (hr))
    {
        goto OnD0EntryExit;
    }

OnD0EntryExit:
    return hr;
}

HRESULT CDeviceCallback::OnD0Exit(
    IWDFDevice*  pWdfDevice,
    WDF_POWER_DEVICE_STATE  previousState
    )
{
    if (!m_pFxIoTargetInterruptPipeStateMgmt)
    {
        return E_FAIL;
    }

    // Stop the I/O target always succeeds.

    (void)m_pFxIoTargetInterruptPipeStateMgmt->Stop(WdfIoTargetCancelSentIo);

    return S_OK;
}
```

継続的なリーダーには、読み取り要求が完了すると、クライアント ドライバーは、要求が読み取り要求を正常に完了するときに通知を受け取るする方法を提供する必要があります。 クライアント ドライバーでは、デバイス コールバック オブジェクトに次のコードを追加する必要があります。

**IUsbTargetPipeContinuousReaderCallbackReadComplete を実装して完了コールバックを提供します。**

1.  実装、 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)デバイス コールバック オブジェクトのインターフェイス。
2.  必ず、 **QueryInterface**デバイス コールバック オブジェクトの実装は、コールバック オブジェクトの参照カウントをインクリメントしてから返します、 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)インターフェイス ポインター。
3.  実装では、 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556910)メソッド、データの読み取りアクセスは、パイプから読み取られました。 *PMemory*パラメーター データを含む、フレームワークによって割り当てられたメモリを指します。 呼び出すことができます[ **IWDFMemory::GetDataBuffer** ](https://msdn.microsoft.com/library/windows/hardware/ff562631)データを格納しているバッファーを取得します。 バッファーには、ヘッダーが含まれています。 ただしデータの長さが付いて、 *NumBytesTransferred*パラメーターの**OnReaderCompletion**ヘッダーの長さは含まれません。 ヘッダーの長さは、クライアント ドライバー、ドライバーの呼び出しで継続的なリーダーの構成時に指定した[ **IWDFUsbTargetPipe2::ConfigureContinuousReader**](https://msdn.microsoft.com/library/windows/hardware/ff560395)します。
4.  完了コールバックへのポインターを指定、 *pOnCompletion*のパラメーター、 [ **IWDFUsbTargetPipe2::ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)メソッド。

データは、デバイス上のエンドポイントで使用するたびにターゲット パイプ オブジェクトは、読み取り要求を完了します。 フレームワークが呼び出すことによって、クライアント ドライバーを通知する場合は、読み取り要求が正常に完了したら、 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff556910)します。 それ以外の場合、フレームワークは、ターゲットのパイプ オブジェクトが読み取り要求のエラーを報告したときに、クライアント ドライバーによって提供されるエラーのコールバックを呼び出します。

次のコード例の実装、 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff556908)デバイス コールバック オブジェクトのインターフェイス。

```cpp
class CDeviceCallback : 
    public IPnpCallbackHardware, 
    public IPnpCallback,   
    public IUsbTargetPipeContinuousReaderCallbackReadComplete

{
public:
    CDeviceCallback();
    ~CDeviceCallback();
    virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, VOID** ppvObject);
    virtual ULONG STDMETHODCALLTYPE AddRef();
    virtual ULONG STDMETHODCALLTYPE Release();

    virtual HRESULT STDMETHODCALLTYPE OnPrepareHardware(IWDFDevice* pDevice);
    virtual HRESULT STDMETHODCALLTYPE OnReleaseHardware(IWDFDevice* pDevice); 

    virtual HRESULT STDMETHODCALLTYPE OnD0Entry(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual HRESULT STDMETHODCALLTYPE OnD0Exit(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual void STDMETHODCALLTYPE OnSurpriseRemoval(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryRemove(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryStop(IWDFDevice*  pWdfDevice);    

    virtual VOID STDMETHODCALLTYPE OnReaderCompletion(IWDFUsbTargetPipe* pPipe, IWDFMemory* pMemory, SIZE_T NumBytesTransferred, PVOID Context);    


private:
    LONG m_cRefs;
    IWDFUsbTargetPipe* m_pFxUsbPipe;
    IWDFIoTargetStateManagement* m_pFxIoTargetInterruptPipeStateMgmt;

    HRESULT CreateUSBTargetDeviceObject (IWDFDevice* pFxDevice, IWDFUsbTargetDevice** ppUSBTargetDevice);
    HRESULT ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe);
};
```

次のコード例では、デバイス コールバック オブジェクトの QueryInterface の実装を示します。

```cpp
HRESULT CDeviceCallback::QueryInterface(REFIID riid, LPVOID* ppvObject)
{
    if (ppvObject == NULL)
    {
        return E_INVALIDARG;
    }

    *ppvObject = NULL;

    HRESULT hr = E_NOINTERFACE;

    if(  IsEqualIID(riid, __uuidof(IPnpCallbackHardware))   ||  IsEqualIID(riid, __uuidof(IUnknown))  )
    {  
        *ppvObject = static_cast<IPnpCallbackHardware*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IPnpCallback)))
    {  
        *ppvObject = static_cast<IPnpCallback*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IUsbTargetPipeContinuousReaderCallbackReadComplete)))
    {  
        *ppvObject = static_cast<IUsbTargetPipeContinuousReaderCallbackReadComplete*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    return hr;
}
```

次のコード例は、によって返されるバッファーからデータを取得する方法を示しています。 [ **IUsbTargetPipeContinuousReaderCallbackReadComplete::OnReaderCompletion**](https://msdn.microsoft.com/library/windows/hardware/ff556910)します。 ターゲット パイプ オブジェクトには、読み取りが完了するたびには、フレームワークによって要求が正常に**OnReaderCompletion**します。 この例では、containsng データ バッファーを取得し、デバッガーの出力の内容を出力します。

```cpp
 VOID CDeviceCallback::OnReaderCompletion(
    IWDFUsbTargetPipe* pPipe,
    IWDFMemory* pMemory,
    SIZE_T NumBytesTransferred,
    PVOID Context)
{        
    if (pPipe != m_pFxUsbInterruptPipe)
    {
        return;
    }

    if (NumBytesTransferred == 0) 
    {
        // NumBytesTransferred is zero.

        return;
    }

    PVOID pBuff = NULL;
    LONG CurrentData = 0;
    char data[20];

    pBuff = pMemory->GetDataBuffer(NULL);

    if (pBuff)
    {
        CopyMemory(&CurrentData, pBuff, sizeof(CurrentData));
        sprintf_s(data, 20, "%d\n", CurrentData);
        OutputDebugString(data);
        pBuff = NULL;
    }
    else
    {
        OutputDebugString(TEXT("Unable to get data buffer."));
    }
}
```

クライアント ドライバーは、読み取り要求の完了中にターゲット パイプ オブジェクトで障害が発生したときに、フレームワークから通知を受け取ることができます。 通知を取得するには、クライアント ドライバーはエラー コールバックを実装し、継続的なリーダーを構成するときに、コールバックへのポインターを指定する必要があります。 次の手順では、エラー コールバックを実装する方法について説明します。

**IUsbTargetPipeContinuousReaderCallbackReadersFailed を実装してエラーのコールバックを提供します。**

1.  実装、 [ **IUsbTargetPipeContinuousReaderCallbackReadersFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff556914)デバイス コールバック オブジェクトのインターフェイス。
2.  必ず、 **QueryInterface**デバイス コールバック オブジェクトの実装は、コールバック オブジェクトの参照カウントをインクリメントしてから返します、 [ **IUsbTargetPipeContinuousReaderCallbackReadersFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff556914)インターフェイス ポインター。
3.  実装では、 [ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** ](https://msdn.microsoft.com/library/windows/hardware/ff556915)メソッド、失敗した読み取り要求のエラー処理を提供します。

    読み取り要求と、クライアント ドライバーは、エラー コールバックを提供します完了する継続的なリーダーが失敗した場合は、フレームワーク、 [ **IUsbTargetPipeContinuousReaderCallbackReadersFailed::OnReaderFailure** 。](https://msdn.microsoft.com/library/windows/hardware/ff556915)メソッド。 フレームワークの HRESULT 値を提供する、 *hrStatus*ターゲット パイプ オブジェクトで発生したエラー コードを示すパラメーターです。 基づく特定のエラー処理を提供するエラー コード可能性があります。 たとえば、パイプをリセットし、継続的なリーダーを再起動するためにフレームワークを実行する場合に、確認、コールバックが TRUE を返します。

    **注**呼び出さない[ **IWDFIoTargetStateManagement::Start** ](https://msdn.microsoft.com/library/windows/hardware/ff559213)と[ **IWDFIoTargetStateManagement::Stop** ](https://msdn.microsoft.com/library/windows/hardware/ff559217)内でのエラーのコールバック。



4.  失敗コールバックへのポインターを指定、 *pOnFailure*のパラメーター、 [ **IWDFUsbTargetPipe2::ConfigureContinuousReader** ](https://msdn.microsoft.com/library/windows/hardware/ff560395)メソッド。

次のコード例の実装、 [ **IUsbTargetPipeContinuousReaderCallbackReadersFailed** ](https://msdn.microsoft.com/library/windows/hardware/ff556914)デバイス コールバック オブジェクトのインターフェイス。

```cpp
class CDeviceCallback : 
    public IPnpCallbackHardware, 
    public IPnpCallback,
    public IUsbTargetPipeContinuousReaderCallbackReadComplete,
    public IUsbTargetPipeContinuousReaderCallbackReadersFailed
{
public:
    CDeviceCallback();
    ~CDeviceCallback();
    virtual HRESULT STDMETHODCALLTYPE QueryInterface(REFIID riid, VOID** ppvObject);
    virtual ULONG STDMETHODCALLTYPE AddRef();
    virtual ULONG STDMETHODCALLTYPE Release();

    virtual HRESULT STDMETHODCALLTYPE OnPrepareHardware(IWDFDevice* pDevice);
    virtual HRESULT STDMETHODCALLTYPE OnReleaseHardware(IWDFDevice* pDevice); 

    virtual HRESULT STDMETHODCALLTYPE OnD0Entry(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual HRESULT STDMETHODCALLTYPE OnD0Exit(IWDFDevice*  pWdfDevice, WDF_POWER_DEVICE_STATE  previousState);
    virtual void STDMETHODCALLTYPE OnSurpriseRemoval(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryRemove(IWDFDevice*  pWdfDevice);
    virtual HRESULT STDMETHODCALLTYPE OnQueryStop(IWDFDevice*  pWdfDevice);    

    virtual VOID STDMETHODCALLTYPE OnReaderCompletion(IWDFUsbTargetPipe* pPipe, IWDFMemory* pMemory, SIZE_T NumBytesTransferred, PVOID Context);    
    virtual BOOL STDMETHODCALLTYPE OnReaderFailure(IWDFUsbTargetPipe * pPipe, HRESULT hrCompletion);

private:
    LONG m_cRefs;
    IWDFUsbTargetPipe* m_pFxUsbInterruptPipe;
    IWDFIoTargetStateManagement* m_pFxIoTargetInterruptPipeStateMgmt;

    HRESULT CreateUSBTargetDeviceObject (IWDFDevice* pFxDevice, IWDFUsbTargetDevice** ppUSBTargetDevice);
    HRESULT RetrieveUSBDeviceDescriptor (IWDFUsbTargetDevice* pUSBTargetDevice, PUSB_DEVICE_DESCRIPTOR DescriptorHeader, PULONG cbDescriptor);
    HRESULT ConfigureContinuousReader (IWDFUsbTargetPipe* pFxPipe);
};
```

次のコード例では、デバイス コールバック オブジェクトの QueryInterface の実装を示します。

```cpp
HRESULT CDeviceCallback::QueryInterface(REFIID riid, LPVOID* ppvObject)
{
    if (ppvObject == NULL)
    {
        return E_INVALIDARG;
    }

    *ppvObject = NULL;

    HRESULT hr = E_NOINTERFACE;

    if(  IsEqualIID(riid, __uuidof(IPnpCallbackHardware))   ||  IsEqualIID(riid, __uuidof(IUnknown))  )
    {  
        *ppvObject = static_cast<IPnpCallbackHardware*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IPnpCallback)))
    {  
        *ppvObject = static_cast<IPnpCallback*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;

    }

    if(  IsEqualIID(riid, __uuidof(IUsbTargetPipeContinuousReaderCallbackReadComplete)))
    {  
        *ppvObject = static_cast<IUsbTargetPipeContinuousReaderCallbackReadComplete*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;
    }

    if(  IsEqualIID(riid, __uuidof(IUsbTargetPipeContinuousReaderCallbackReadersFailed)))
    {  
        *ppvObject = static_cast<IUsbTargetPipeContinuousReaderCallbackReadersFailed*>(this);
        reinterpret_cast<IUnknown*>(*ppvObject)->AddRef();
        hr = S_OK;
    }

    return hr;
}
```

次のコード例では、エラー コールバックの実装を示します。 読み取り要求が失敗した場合、メソッドは、デバッガーで、フレームワークによって報告されたエラー コードを出力し、パイプをリセットし、継続的なリーダーを再起動するためにフレームワークを指示します。

```cpp
 BOOL CDeviceCallback::OnReaderFailure(
    IWDFUsbTargetPipe * pPipe,
    HRESULT hrCompletion
    )
{
    UNREFERENCED_PARAMETER(pPipe);  
    UNREFERENCED_PARAMETER(hrCompletion);     

    return TRUE;
}
```

クライアント ドライバーはエラー コールバックを提供していない、エラーが発生した場合は、フレームワークは、USB パイプをリセットし、継続的なリーダーを再起動します。

## <a name="related-topics"></a>関連トピック
[USB I/O の転送](usb-device-i-o.md)  
[USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)  
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB インターフェイスで代替の設定を選択する方法](select-a-usb-alternate-setting.md)  
[USB クライアント ドライバーに関する一般的なタスク](wdk-resources-for-usb-driver-development.md)  



