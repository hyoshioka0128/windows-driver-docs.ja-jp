---
Description: このトピックでは、WDF に用意されている連続リーダーオブジェクトについて説明します。 このトピックの手順では、オブジェクトを構成し、それを使用して USB パイプからデータを読み取る方法について、手順を追って説明します。
title: 継続的リーダーを使用して USB パイプからデータを読み取る方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b00563d9357dc9791250f91362eaece03f87748c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837544"
---
# <a name="how-to-use-the-continuous-reader-for-reading-data-from-a-usb-pipe"></a>継続的リーダーを使用して USB パイプからデータを読み取る方法


このトピックでは、WDF に用意されている連続リーダーオブジェクトについて説明します。 このトピックの手順では、オブジェクトを構成し、それを使用して USB パイプからデータを読み取る方法について、手順を追って説明します。

Windows Driver Framework (WDF) には、*継続的リーダー*と呼ばれる特殊なオブジェクトが用意されています。 このオブジェクトを使用すると、使用可能なデータがある限り、USB クライアントドライバーが一括および中断エンドポイントからデータを継続的に読み取ることができます。 リーダーを使用するには、クライアントドライバーが、ドライバーがデータを読み取るエンドポイントに関連付けられている、USB ターゲットパイプオブジェクトのハンドルを持っている必要があります。 エンドポイントはアクティブ構成である必要があります。 構成をアクティブにするには、USB 構成を選択するか、現在の構成の別の設定を変更します。 これらの操作の詳細については、「 [Usb デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」および「 [usb インターフェイスで別の設定を選択する方法](select-a-usb-alternate-setting.md)」を参照してください。

継続的リーダーを作成した後、クライアントドライバーは必要に応じて、リーダーを開始および停止できます。 読み取り要求が常にターゲットパイプオブジェクトで使用可能であり、クライアントドライバーは常にエンドポイントからデータを受信する準備ができていることを確認する継続的リーダー。

継続的リーダーは、フレームワークによって自動的に電源管理されることはありません。 これは、デバイスが電力状態を低くしたときに、クライアントドライバーがリーダーを停止し、デバイスが動作状態になったときにリーダーを再起動する必要があることを意味します。

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

クライアントドライバーが連続リーダーを使用できるようにするには、次の要件が満たされていることを確認します。

-   USB デバイスには、エンドポイントが必要です。 [Usbview](https://docs.microsoft.com/windows-hardware/drivers/debugger/usbview)でデバイスの構成を確認します。 Usbview .exe は、すべての USB コントローラーとそれらに接続されている USB デバイスを参照できるアプリケーションです。 通常、USBView は、Windows Driver Kit (WDK) の **[デバッガー]** フォルダーにインストールされます。
-   クライアント ドライバーによって、フレームワーク USB ターゲット デバイス オブジェクトが作成されている必要があります。

    Microsoft Visual Studio Professional 2012 に付属する USB テンプレートを使用している場合、テンプレート コードでこれらのタスクが実行されます。 テンプレート コードによりターゲット デバイス オブジェクトのハンドルが取得され、デバイス コンテキストに格納されます。

    **KMDF クライアントドライバー:**

    KMDF クライアント ドライバーでは、[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) メソッドを呼び出すことで WDFUSBDEVICE ハンドルを取得する必要があります。 詳細については、「[USB クライアント ドライバー コード構造について (KMDF)](understanding-the-kmdf-template-code-for-usb.md)」の「デバイスのソース コード」を参照してください。

    **UMDF クライアントドライバー:**

    UMDF クライアント ドライバーは、フレームワーク ターゲット デバイス オブジェクトを問い合わせることで、[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) ポインターを取得する必要があります。 詳細については、「[USB クライアント ドライバー コード構造について (UMDF) **」の「** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)IPnpCallbackHardware[](understanding-the-umdf-template-code-for-usb.md) 実装と USB 固有のタスク」を参照してください。

-   デバイスにはアクティブな構成が必要です。

    USB テンプレートを使用している場合、コードは各インターフェイスの最初の構成と既定の代替設定を選択します。 代替設定を変更する方法の詳細については、「 [USB インターフェイスで別の設定を選択する方法](select-a-usb-alternate-setting.md)」を参照してください。

    **KMDF クライアントドライバー:**

    KMDF クライアントドライバーは、 [**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)メソッドを呼び出す必要があります。

    **UMDF クライアントドライバー:**

    UMDF クライアントドライバーでは、フレームワークによって、最初の構成と、その構成内の各インターフェイスの既定の代替設定が選択されます。

-   クライアントドライバーには、のエンドポイント用のフレームワークのターゲットパイプオブジェクトへのハンドルが必要です。 詳細については、「 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)」を参照してください。

<a name="instructions"></a>手順
------------

### <a name="using-the-continuous-reader---kmdf-client-driver"></a>継続的リーダーの使用-KMDF クライアントドライバー

1.  継続的リーダーを構成します。

    1.  [**WDF\_usb\_continuous\_reader\_config\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552561_init)マクロを呼び出して、[**継続的\_リーダー\_CONFIG 構造体を WDF\_usb\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)初期化します。
    2.  [**WDF\_USB\_継続的\_リーダー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)構造体で構成オプションを指定します。
    3.  [**WdfUsbTargetPipeConfigContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeconfigcontinuousreader)メソッドを呼び出します。

    次のコード例では、指定されたターゲットパイプオブジェクトの連続リーダーを構成します。

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

通常、クライアントドライバーは、アクティブな設定でターゲットパイプオブジェクトを列挙した後、 [*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック関数で継続的リーダーを構成します。

前の例では、クライアントドライバーは2つの方法で構成オプションを指定しています。 最初に、 [**WDF\_usb\_連続\_リーダー\_config\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_continuous_reader_config_init)を呼び出し、次に[**WDF\_usb\_継続的\_リーダー\_config**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)メンバーを設定します。 **WDF\_USB\_継続的\_リーダー\_CONFIG\_INIT**のパラメーターに注意してください。 これらの値は必須です。 この例では、クライアントドライバーは次のように指定します。

-   ドライバーが実装する完了ルーチンへのポインター。 フレームワークは、読み取り要求の完了時にこのルーチンを呼び出します。 完了ルーチンでは、ドライバーは読み取られたデータを格納しているメモリ位置にアクセスできます。 完了ルーチンの実装については、手順 2. で説明します。
-   ドライバーで定義されたコンテキストへのポインター。
-   1回の転送でデバイスから読み取ることができるバイト数。 クライアントドライバーは、 [**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)または[**WdfUsbTargetPipeGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)メソッドを呼び出すことによって、 [**WDF\_USB\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)構造でその情報を取得できます。 詳細については、「 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)」を参照してください。

[**WDF\_USB\_継続的\_リーダー\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_continuous_reader_config_init)は、 *numpendingreads*の既定値を使用するように連続リーダーを構成します。 この値によって、フレームワークが保留キューに追加する読み取り要求の数が決まります。 既定値は、多くのプロセッサ構成の多くのデバイスで適度に良好なパフォーマンスを提供するように決定されています。

[**WDF\_usb\_継続的\_リーダー\_CONFIG\_INIT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdf_usb_continuous_reader_config_init)で指定された構成パラメーターに加えて、この例では、 [**WDF\_usb\_連続したエラールーチンも設定\_リーダー\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)。 このエラールーチンは省略可能です。

エラールーチンに加えて、 [**WDF\_USB\_継続的\_リーダー\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_continuous_reader_config)には、クライアントドライバーが転送バッファーのレイアウトを指定するために使用できる他のメンバーもあります。 たとえば、連続したリーダーを使用してネットワークパケットを受信するネットワークドライバーがあるとします。 各パケットには、ヘッダー、ペイロード、およびフッターのデータが含まれています。 パケットを記述するには、ドライバーはまず、 [**WDF\_USB\_継続的\_リーダー\_CONFIG\_INIT**](https://msdn.microsoft.com/library/windows/hardware/ff552561_init)の呼び出しでパケットのサイズを指定する必要があります。 次に、ドライバーは、 **WDF\_USB\_連続\_リーダー\_CONFIG**の**Headerlength**と**TrailerLength**メンバーを設定して、ヘッダーとフッターの長さを指定する必要があります。 フレームワークは、これらの値を使用して、ペイロードの両側のバイトオフセットを計算します。 ペイロードデータがエンドポイントから読み取られると、フレームワークは、オフセット間のバッファーの部分にそのデータを格納します。

2.  完了ルーチンを実装します。

    フレームワークは、要求が完了するたびに、クライアントドライバーで実装された完了ルーチンを呼び出します。 このフレームワークは、読み取ったバイト数と、パイプから読み取られたデータをバッファーに格納する WDFMEMORY オブジェクトを渡します。

    次のコード例は、完了ルーチンの実装を示しています。

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

フレームワークは、要求が完了するたびに、クライアントドライバーで実装された完了ルーチンを呼び出します。 フレームワークは、読み取り操作ごとにメモリオブジェクトを割り当てます。 完了ルーチンでは、フレームワークは読み取ったバイト数と WDFMEMORY ハンドルをメモリオブジェクトに渡します。 メモリオブジェクトバッファーには、パイプから読み取られたデータが含まれています。 クライアントドライバーは、メモリオブジェクトを解放しないでください。 各完了ルーチンからが返された後に、フレームワークによってオブジェクトが解放されます。 クライアントドライバーが受信したデータを格納する場合、ドライバーは、完了ルーチンでバッファーの内容をコピーする必要があります。

3.  エラールーチンを実装します。

    フレームワークは、クライアントドライバーで実装されたエラールーチンを呼び出して、読み取り要求の処理中に継続的なリーダーがエラーを報告したことをドライバーに通知します。 フレームワークは、要求が失敗したターゲットパイプオブジェクトおよびエラーコード値へのポインターを渡します。 これらのエラーコード値に基づいて、ドライバーはエラー回復メカニズムを実装できます。 また、ドライバーは、フレームワークが継続的リーダーを再起動する必要があるかどうかをフレームワークに示す適切な値も返す必要があります。

    次のコード例は、エラールーチンの実装を示しています。

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

前の例では、ドライバーは TRUE を返します。 この値は、パイプをリセットした後、連続リーダーを再起動する必要があることをフレームワークに示します。

または、クライアントドライバーが FALSE を返し、パイプでストール条件が発生した場合にエラー復旧メカニズムを提供することもできます。 たとえば、ドライバーは USBD の状態を確認し、リセットパイプ要求を発行して、失速条件をクリアできます。

パイプでのエラー回復の詳細については、「 [USB パイプエラーから回復する方法](how-to-recover-from-usb-pipe-errors.md)」を参照してください。

4.  デバイスが動作状態になったときに、継続的リーダーを起動するようにフレームワークに指示します。デバイスが動作状態のままになったときに、リーダーを停止します。 これらのメソッドを呼び出し、ターゲットパイプオブジェクトを i/o ターゲットオブジェクトとして指定します。

    -   [**WdfIoTargetStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)
    -   [**WdfIoTargetStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)

    継続的リーダーは、フレームワークによって自動的に電源管理されることはありません。 したがって、クライアントドライバーは、デバイスの電源状態が変化したときに、ターゲットパイプオブジェクトを明示的に開始または停止する必要があります。 ドライバーは、ドライバーの[*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)実装で[**Wdfiotargetstart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstart)を呼び出します。 この呼び出しにより、デバイスが動作状態のときにのみ、キューが要求を配信するようになります。 逆に、ドライバーは[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)の実装で[**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)を呼び出し、デバイスがより低い電力状態になると、キューが要求の配信を停止するようにします。

次のコード例では、指定されたターゲットパイプオブジェクトの連続リーダーを構成します。

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

前の例は、 [*EvtDeviceD0Entry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry)と[*EvtDeviceD0Exit*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_exit)のコールバックルーチンの実装を示しています。 [**Wdfiotargetstop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetstop)の action パラメーターを使用すると、クライアントドライバーは、デバイスが動作状態のままになったときに、キュー内の保留中の要求に対するアクションを決定できます。 この例では、ドライバーは**WdfIoTargetCancelSentIo**を指定しています。 このオプションは、キュー内のすべての保留中の要求をキャンセルするようにフレームワークに指示します。 または、ドライバーは、保留中の要求が完了するのを待ってから i/o ターゲットを停止するか、保留中の要求を保持し、i/o ターゲットの再起動時に再開するようにフレームワークに指示できます。

### <a name="using-the-continuous-reader---umdf-client-driver"></a>継続的リーダーの使用-UMDF クライアントドライバー

継続的リーダーの使用を開始する前に、 [**IPnpCallbackHardware:: On hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)メソッドの実装でリーダーを構成する必要があります。 [**IWDFUSBTARGETPIPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe) IN エンドポイントに関連付けられているターゲットパイプオブジェクトのインターフェイスへのポインターを取得した後、次の手順を実行します。

**継続的リーダーの構成**

1.  ターゲットパイプオブジェクト ([**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)) で**QueryInterface**を呼び出し、 [**IWDFUsbTargetPipe2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)インターフェイスのクエリを実行します。
2.  デバイスコールバックオブジェクトで**QueryInterface**を呼び出し、 [**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)インターフェイスのクエリを実行します。 連続リーダーを使用するには、IUsbTargetPipeContinuousReaderCallbackReadComplete を実装する必要があります。 実装については、このトピックの後半で説明します。
3.  エラーコールバックを実装している場合は、デバイスコールバックオブジェクトで**QueryInterface**を呼び出し、 [IUsbTargetPipeContinuousReaderCallbackReadersFailed](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)インターフェイスのクエリを実行します。 実装については、このトピックの後半で説明します。
4.  [**IWDFUsbTargetPipe2:: ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)メソッドを呼び出し、ヘッダー、トレーラー、保留中の要求の数、完了と失敗のコールバックメソッドへの参照などの構成パラメーターを指定します。

    メソッドは、ターゲットパイプオブジェクトの連続リーダーを構成します。 連続リーダーは、ターゲットパイプオブジェクトとの間で送受信される一連の読み取り要求を管理するキューを作成します。

次のコード例では、指定されたターゲットパイプオブジェクトの連続リーダーを構成します。 この例では、呼び出し元によって指定されたターゲットパイプオブジェクトがエンドポイントのに関連付けられていることを前提としています。 継続的リーダーは、USBD を読み取るように構成されています。\_既定\_最大\_転送\_サイズバイトです。フレームワークでを使用して、既定の数の保留中の要求を使用するには、クライアントドライバーが提供した完了および失敗のコールバックメソッドを呼び出す場合は。 受信したバッファーには、ヘッダーまたはトレーラーデータは含まれません。

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

次に、デバイスが動作状態 (**D0**) に入って終了するときに、ターゲットパイプオブジェクトの状態を指定します。

クライアントドライバーが電源管理キューを使用してパイプに要求を送信する場合、キューはデバイスが**D0**状態のときにのみ要求を配信します。 デバイスの電源状態が**d0**から低電力状態に変わると ( **d0**終了時)、ターゲットパイプオブジェクトは保留中の要求を完了し、キューはターゲットパイプオブジェクトへの要求の送信を停止します。 したがって、クライアントドライバーは、ターゲットパイプオブジェクトを開始および停止する必要はありません。

継続的リーダーは、要求を送信するために、電源管理キューを使用しません。 そのため、デバイスの電源状態が変化したときに、ターゲットパイプオブジェクトを明示的に開始または停止する必要があります。 ターゲットパイプオブジェクトの状態を変更するには、フレームワークによって実装されている[**IWDFIoTargetStateManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイスを使用できます。 [**IWDFUSBTARGETPIPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe) IN エンドポイントに関連付けられているターゲットパイプオブジェクトのインターフェイスへのポインターを取得した後、次の手順を実行します。

**状態管理の実装**

1.  [**IPnpCallbackHardware:: 代わっ hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)の実装で、ターゲットパイプオブジェクト ([**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)) に対して **[QueryInterface]** を呼び出し、 [**IWDFIoTargetStateManagement**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイスに対してクエリを実行します。 デバイスコールバッククラスのメンバー変数に参照を格納します。
2.  デバイスコールバックオブジェクトに[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)インターフェイスを実装します。
3.  [**IPnpCallback:: OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)メソッドの実装では、 [**IWDFIoTargetStateManagement:: start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)を呼び出して、連続リーダーを開始します。
4.  [**IPnpCallback:: OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)メソッドの実装では、 [**IWDFIoTargetStateManagement:: stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)を呼び出して、連続リーダーを停止します。

デバイスが動作状態 (**d0**) になると、フレームワークは、ターゲットパイプオブジェクトを開始する、クライアントドライバーが提供する D0-entry コールバックメソッドを呼び出します。 デバイスが**d0**状態のままになると、フレームワークは d0-exit コールバックメソッドを呼び出します。 ターゲットパイプオブジェクトは、クライアントドライバーによって構成された保留中の読み取り要求の数を完了し、新しい要求の受け入れを停止します。
次のコード例では、デバイスコールバックオブジェクトに[IPnpCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)インターフェイスを実装しています。

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

次のコード例は、IPnpCallback:: OnIWDFIoTargetStateManagement Hardware メソッドでターゲットパイプオブジェクトのインターフェイスへのポインターを取得する方法を示しています。

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

次のコード例は、 [**IPnpCallbackHardware:: OnIWDFIoTargetStateManagement hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)メソッドでターゲットパイプオブジェクトの[](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotargetstatemanagement)インターフェイスへのポインターを取得する方法を示しています。

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

継続的リーダーが読み取り要求を完了すると、クライアントドライバーは、要求が読み取り要求を正常に完了したときに通知を受け取る方法を提供する必要があります。 クライアントドライバーは、デバイスコールバックオブジェクトにこのコードを追加する必要があります。

**IUsbTargetPipeContinuousReaderCallbackReadComplete を実装して完了コールバックを提供する**

1.  デバイスコールバックオブジェクトに[**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)インターフェイスを実装します。
2.  デバイスコールバックオブジェクトの**QueryInterface**実装がコールバックオブジェクトの参照カウントをインクリメントし、 [**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)インターフェイスポインターを返すことを確認します。
3.  [**IUsbTargetPipeContinuousReaderCallbackReadComplete:: OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion)メソッドの実装では、パイプから読み取られたデータにアクセスします。 *Pmemory*パラメーターは、データを格納するフレームワークによって割り当てられたメモリを指します。 [**Iwdfmemory:: GetDataBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisgetdatabuffer)を呼び出して、データを含むバッファーを取得できます。 バッファーにはヘッダーが含まれていますが、 **Onreadercompletion**の*NumBytesTransferred*パラメーターによって示されるデータの長さには、ヘッダーの長さが含まれていません。 ヘッダーの長さはクライアントドライバーによって指定され、ドライバーの[**IWDFUsbTargetPipe2:: ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)への呼び出しで継続的リーダーを構成します。
4.  [**IWDFUsbTargetPipe2:: ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)メソッドの*pOnCompletion*パラメーターで、完了コールバックへのポインターを指定します。

デバイス上のエンドポイントでデータが使用可能になるたびに、ターゲットパイプオブジェクトは読み取り要求を完了します。 読み取り要求が正常に完了した場合、フレームワークは[**IUsbTargetPipeContinuousReaderCallbackReadComplete:: OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion)を呼び出すことによってクライアントドライバーに通知します。 そうしないと、ターゲットパイプオブジェクトが読み取り要求でエラーを報告したときに、フレームワークがクライアントドライバーから提供されたエラーコールバックを呼び出します。

次のコード例では、デバイスコールバックオブジェクトに[**IUsbTargetPipeContinuousReaderCallbackReadComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)インターフェイスを実装しています。

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

次のコード例は、デバイスコールバックオブジェクトの QueryInterface 実装を示しています。

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

次のコード例は、 [**IUsbTargetPipeContinuousReaderCallbackReadComplete:: OnReaderCompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete-onreadercompletion)によって返されるバッファーからデータを取得する方法を示しています。 ターゲットパイプオブジェクトが読み取り要求を正常に完了するたびに、フレームワークは**Onreadercompletion**を呼び出します。 この例では、データを containsng するバッファーを取得し、その内容をデバッガーの出力に出力します。

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

クライアントドライバーは、読み取り要求の完了中にターゲットパイプオブジェクトでエラーが発生したときに、フレームワークから通知を受け取ることができます。 クライアントドライバーは、通知を取得するために、エラーコールバックを実装し、連続リーダーの構成中にコールバックへのポインターを提供する必要があります。 次の手順では、エラーコールバックを実装する方法について説明します。

**IUsbTargetPipeContinuousReaderCallbackReadersFailed を実装してエラーコールバックを提供する**

1.  デバイスコールバックオブジェクトに[**IUsbTargetPipeContinuousReaderCallbackReadersFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)インターフェイスを実装します。
2.  デバイスコールバックオブジェクトの**QueryInterface**実装がコールバックオブジェクトの参照カウントをインクリメントし、 [**IUsbTargetPipeContinuousReaderCallbackReadersFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)インターフェイスポインターを返すことを確認します。
3.  [**IUsbTargetPipeContinuousReaderCallbackReadersFailed:: OnReaderFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)メソッドの実装では、失敗した読み取り要求のエラー処理を提供します。

    連続リーダーが読み取り要求を完了できず、クライアントドライバーがエラーコールバックを提供する場合、フレームワークは[**IUsbTargetPipeContinuousReaderCallbackReadersFailed:: OnReaderFailure**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed-onreaderfailure)メソッドを呼び出します。 このフレームワークでは、ターゲットパイプオブジェクトで発生したエラーコードを示す HRESULT 値が*Hrstatus*パラメーターに指定されています。 このエラーコードに基づいて、特定のエラー処理を提供する場合があります。 たとえば、フレームワークでパイプをリセットし、継続的リーダーを再起動する必要がある場合は、コールバックによって TRUE が返されることを確認します。

    **メモ** 失敗コールバック内で[**IWDFIoTargetStateManagement:: Start**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-start)と[**IWDFIoTargetStateManagement:: Stop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotargetstatemanagement-stop)を呼び出さないでください。



4.  [**IWDFUsbTargetPipe2:: ConfigureContinuousReader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe2-configurecontinuousreader)メソッドの*pOnFailure*パラメーターに、エラーコールバックへのポインターを指定します。

次のコード例では、デバイスコールバックオブジェクトに[**IUsbTargetPipeContinuousReaderCallbackReadersFailed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadersfailed)インターフェイスを実装しています。

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

次のコード例は、デバイスコールバックオブジェクトの QueryInterface 実装を示しています。

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

次のコード例は、エラーコールバックの実装を示しています。 読み取り要求が失敗した場合、メソッドはフレームワークによって報告されたエラーコードをデバッガーに出力し、パイプをリセットして継続的リーダーを再起動するようにフレームワークに指示します。

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

クライアントドライバーでエラーコールバックが提供されず、エラーが発生した場合、フレームワークは USB パイプをリセットし、連続リーダーを再起動します。

## <a name="related-topics"></a>関連トピック
[USB i/o 転送](usb-device-i-o.md)  
[USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)  
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB インターフェイスで別の設定を選択する方法](select-a-usb-alternate-setting.md)  
[USB クライアントドライバーの一般的なタスク](wdk-resources-for-usb-driver-development.md)  



