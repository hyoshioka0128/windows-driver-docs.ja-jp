---
Description: このトピックでは、USB パイプの概要を説明し、USB クライアント ドライバーで USB ドライバー スタックからパイプ ハンドルを取得するために必要な手順について説明します。
title: USB パイプの列挙方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 789c7f5416592b7a5af94e2b5b98e29eaf95ff5e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386263"
---
# <a name="how-to-enumerate-usb-pipes"></a>USB パイプの列挙方法


このトピックでは、USB パイプの概要を説明し、USB クライアント ドライバーで USB ドライバー スタックからパイプ ハンドルを取得するために必要な手順について説明します。

A *USB エンドポイント*クライアント ドライバーは、データを送信またはからのデータを受信するデバイスでのバッファーします。 データを送受信するには、クライアント ドライバーは、ホスト コント ローラーにデータを表示します。 USB ドライバー スタックへの I/O 転送要求を送信します。 ホスト コント ローラーの後に続く特定のプロトコル (エンドポイントの種類に応じて: 一括、割り込み、アイソクロナスまたは)、デバイス間でデータを転送する要求を構築します。 データ転送のすべての詳細は、クライアント ドライバーから抽象化されます。 クライアント ドライバーでは、適切な形式で要求を送信する限り、USB ドライバー スタックは要求を処理し、デバイスにデータを転送します。

USB ドライバー スタックの作成、デバイスの構成時に、 *USB パイプ*(ホスト側) に、USB インターフェイスとそのアクティブな代替設定で定義されているデバイスのエンドポイントごと。 USB パイプは、ホスト コント ローラーとエンドポイント間の通信チャネルです。 クライアント ドライバーの場合は、パイプは、エンドポイントの論理の抽象化です。 データ転送を送信するには、ドライバーは、転送対象となっているエンドポイントに関連付けられたパイプ ハンドルを取得する必要があります。 パイプ ハンドルは、ドライバーが転送を中止するか、エラー条件が発生した場合、パイプをリセットする場合にも必要です。

パイプのすべての属性は、関連付けられたエンドポイント記述子から派生します。 たとえば、USB ドライバー スタック、エンドポイントの種類に応じて、パイプの型が割り当てられます。 一括エンドポイントの場合は、USB ドライバー スタックは一括パイプ; を作成しますアイソクロナス エンドポイントの場合、アイソクロナス パイプが作成されなど。 もう 1 つの重要な属性は、ホスト コント ローラーは、要求で、エンドポイントのポイントに送信できるデータの量です。 クライアント ドライバーは、その値に応じて、転送バッファーのレイアウトを決定する必要があります。

Windows Driver Foundation (WDF) での特殊な I/O ターゲット オブジェクトを提供する[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)と[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)さまざまな構成タスクを簡略化クライアントドライバー。 これらのオブジェクトを使用すると、クライアント ドライバーはインターフェイスの数など、現在の構成に関する情報を取得、別の各インターフェイスとそのエンドポイント内で設定できます。 呼ばれるこれらのオブジェクトの 1 つ、*ターゲット パイプ オブジェクト*エンドポイントに関連するタスクを実行します。 このトピックでは、ターゲットのパイプ オブジェクトを使用してパイプ情報を取得する方法について説明します。

Windows Driver Model (WDM) クライアント ドライバーでは、USB ドライバー スタックの配列を返します[ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)構造体。 配列内の要素の数は、選択した構成でインターフェイスのアクティブな代替設定に定義されたエンドポイントの数によって異なります。 各要素には、特定のエンドポイント用に作成されたパイプに関する情報が含まれています。 構成を選択して、パイプ情報の配列を取得する方法については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

クライアント ドライバーでは、パイプを列挙できます、前に、これらの要件を満たしていることを確認してください。

-   クライアント ドライバー フレームワーク USB ターゲット デバイス オブジェクトを作成する必要があります。

    Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合、テンプレート コードは、これらのタスクを実行します。 テンプレート コードでは、ターゲット デバイス オブジェクトを識別するハンドルを取得し、デバイス コンテキストに格納します。

    \* * クライアント ドライバーの KMDF: * *

    KMDF クライアント ドライバーは、呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッド。 詳細については、「デバイスのソース コード」を参照してください[USB クライアント ドライバー コード構造 (KMDF) について](understanding-the-kmdf-template-code-for-usb.md)します。

    \* * クライアント ドライバーの UMDF: * *

    UMDF クライアント ドライバーを入手する必要があります、 [ **IWDFUsbTargetDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)フレームワーク ターゲットのデバイス オブジェクトのクエリを実行してポインター。 詳細については、次を参照してください。"[**IPnpCallbackHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)実装と USB の特定のタスク"で[USB クライアント ドライバー コード構造 (UMDF) について](understanding-the-umdf-template-code-for-usb.md)します。

-   デバイスをアクティブな構成が必要です。

    USB テンプレートを使用している場合に、コードは、各インターフェイスの最初の構成と既定の代替設定を選択します。 その既定の設定を変更する方法については、次を参照してください。 [USB インターフェイスで代替の設定を選択する方法](select-a-usb-alternate-setting.md)します。

    \* * クライアント ドライバーの KMDF: * *

    KMDF クライアント ドライバーを呼び出す必要があります、 [ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)メソッド。

    \* * クライアント ドライバーの UMDF: * *

    UMDF のクライアント ドライバーの場合は、フレームワークは、その構成の最初の構成と各インターフェイスの既定の代替設定を選択します。

<a name="instructions"></a>手順
------------

### <a name="getting-usb-pipe-handles---kmdf-client-driver"></a>USB パイプ ハンドルの取得 KMDF クライアント ドライバー

フレームワークは、USB ターゲット パイプ オブジェクトとして、USB ドライバー スタックによって開かれている、それぞれのパイプを表します。 KMDF クライアント ドライバーは、パイプに関する情報を取得する対象のパイプ オブジェクトのメソッドにアクセスできます。 データ転送を実行するには、クライアント ドライバーは、WDFUSBPIPE パイプ処理する必要があります。 パイプ ハンドルを取得するには、ドライバーがアクティブな構成のインターフェイスと代替の設定を列挙し、各設定で定義されているエンドポイントが列挙する必要があります。 各データ転送の列挙操作を実行すると、高価なことができます。 したがって、1 つの方法は、デバイスを構成した後は、パイプ ハンドルを取得し、ドライバーの定義済みのデバイス コンテキスト内に格納します。 ドライバーは、データ転送の要求を受信すると、ドライバーは、デバイス コンテキストから必要なパイプ ハンドルを取得し、それらを使用して要求を送信します。 クライアント ドライバーでは、デバイスの構成を変更する場合は、代替などが選択を設定するドライバーも更新する必要あります新しいパイプ ハンドルを使用して、デバイス コンテキスト。 それ以外の場合、ドライバーは古いパイプ ハンドルの転送要求を送信することが誤って。

**注**パイプ ハンドルはコントロールの転送に必要ありません。
WDF のクライアント ドライバーを呼び出してコントロールの転送要求を送信する**WdfUsbDevicexxxx** framework デバイス オブジェクトによって公開されるメソッド。 これらのメソッドには、コントロールの転送を開始する WDFUSBDEVICE ハンドルを対象とする既定のエンドポイントが必要があります。 要求の I/O ターゲット、このような転送に既定のエンドポイントし、WDFIOTARGET で表されるハンドルは抽象化を WDFUSBPIPE ハンドルでします。 デバイス レベルでは、WDFUSBDEVICE ハンドルは、既定のエンドポイントへの WDFUSBPIPE ハンドルの抽象化が。

コントロールの転送と KMDF メソッドに送信する方法の詳細については、次を参照してください。 [USB 制御転送を送信する方法](usb-control-transfer.md)します。



1.  パイプ ハンドルを格納するため、デバイス コンテキストの構造を拡張します。

    デバイスで、エンドポイントをわかっている場合は、関連付けられている USB パイプ ハンドルを格納する WDFUSBPIPE メンバーを追加することでデバイス コンテキストの構造体を拡張します。 たとえば、次に示すようにデバイス コンテキストの構造を拡張できます。

    ```cpp
    typedef struct _DEVICE_CONTEXT {  
        WDFUSBDEVICE    UsbDevice;  
        WDFUSBINTERFACE UsbInterface;  
        WDFUSBPIPE      BulkReadPipe;   // Pipe opened for the bulk IN endpoint.
        WDFUSBPIPE      BulkWritePipe;  // Pipe opened for the bulk IN endpoint.
        WDFUSBPIPE      InterruptPipe;  // Pipe opened for the interrupt IN endpoint.
        WDFUSBPIPE      StreamInPipe;   // Pipe opened for stream IN endpoint.
        WDFUSBPIPE      StreamOutPipe;  // Pipe opened for stream OUT endpoint.
        UCHAR           NumberConfiguredPipes;  // Number of pipes opened.
        ...
        ...                                     // Other members. Not shown.

    } DEVICE_CONTEXT, *PDEVICE_CONTEXT;  
    ```

2.  パイプの context 構造体を宣言します。

    各パイプと呼ばれる別の構造でエンドポイントに関連する特性を格納できる、*パイプ コンテキスト*します。 デバイス コンテキストと同様に、パイプ コンテキストは、(クライアント ドライバーで定義された) データ構造のエンドポイントに関連付けられているパイプに関する情報を格納するため。 デバイスの構成時に、クライアント ドライバーは、フレームワークには、そのパイプ コンテキストへのポインターを渡します。 フレームワークは、構造体のサイズに基づいて、メモリのブロックを割り当てし、framework USB ターゲット パイプ オブジェクトには、そのメモリ位置へのポインターを格納します。 クライアント ドライバーは、ポインターを使用してアクセスし、パイプのコンテキストのメンバーでパイプ情報を格納します。

    ```cpp
    typedef struct _PIPE_CONTEXT {  

        ULONG MaxPacketSize;
        ULONG MaxStreamsSupported;
        PUSBD_STREAM_INFORMATION StreamInfo;
    } PIPE_CONTEXT, *PPIPE_CONTEXT;  

    WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(PIPE_CONTEXT, GetPipeContext)  

    ```

    この例では、パイプ コンテキストは、1 つの転送に送信できるバイトの最大数を格納します。 クライアント ドライバーでは、転送バッファーのサイズを決定する値を使用できます。 宣言にも含まれています、 [ **WDF\_DECLARE\_コンテキスト\_型\_WITH\_名前**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type-with-name)マクロで、インラインを生成します。関数、GetPipeContext です。 クライアント ドライバーでは、パイプのコンテキストを格納するメモリ ブロックへのポインターを取得するには、その関数を呼び出すことができます。

    コンテキストの詳細については、次を参照してください。[フレームワーク オブジェクト コンテキストの空間](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-context-space)します。

    フレームワークには、ポインターを渡す、クライアント ドライバー最初のパイプライン コンテキスト呼び出しを初期化します[ **WDF\_オブジェクト\_属性\_INIT\_コンテキスト\_型**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-object-attributes-init-context-type). 次に、呼び出し中にパイプ コンテキストへのポインターを渡します[ **WdfUsbTargetDeviceSelectConfig** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) (の構成を選択する) または[ **WdfUsbInterfaceSelectSetting** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting) (の代替設定を選択します)。

3.  デバイスの構成要求が完了した後は、インターフェイスを列挙し、構成されているパイプのパイプ ハンドルを取得します。 この一連の情報を必要となります。

    -   現在の設定を格納しているインターフェイスの WDFUSBINTERFACE ハンドル。 アクティブな構成でインターフェイスを列挙することによって、そのハンドルを取得できます。 またはへのポインターを指定した場合、 [ **WDF\_USB\_デバイス\_選択\_CONFIG\_PARAMS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_device_select_config_params) で構造体[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)からハンドルを取得する**Type.SingleInterface.ConfiguredUsbInterface** (1 つのインターフェイス デバイス) のメンバーまたは**Type.MultiInterface.Pairs.UsbInterface** (マルチ インターフェイス デバイス) のメンバー。
    -   現在の設定内のエンドポイント用に開くパイプの数。 特定のインターフェイスで呼び出してその数を取得することができます、 [ **WdfUsbInterfaceGetNumConfiguredPipes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes)メソッド。
    -   WDFUSBPIPE が構成されているすべてのパイプ処理します。 呼び出すことによって、ハンドルを取得することができます、 [ **WdfUsbInterfaceGetConfiguredPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)メソッド。

    パイプ ハンドルを取得した後、クライアント ドライバーは、型およびパイプの方向を判断するメソッドを呼び出すことができます。 ドライバーはで、エンドポイントに関する情報を取得することができます、 [ **WDF\_USB\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)構造体。 ドライバーは呼び出すことによって設定された構造体を取得することができます、 [ **WdfUsbTargetPipeGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)メソッド。 または、ドライバーに構造体へのポインターを指定できます、 [ **WdfUsbInterfaceGetConfiguredPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)呼び出します。

次のコード例では、現在の設定でパイプを列挙します。 デバイスの一括と割り込みエンドポイント用のパイプ ハンドルを取得し、ドライバーのデバイス コンテキストの構造体に格納します。 関連するパイプのコンテキストで各エンドポイントの最大パケット サイズを格納します。 エンドポイントは、ストリームをサポートする場合は、OpenStreams ルーチンを呼び出すことによって静的なストリームを開きます。 OpenStreams の実装を示した[を開いて、USB 一括エンドポイントで静的なストリームを閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)します。

特定の一括エンドポイントは静的なストリームをサポートするかどうかを確認するのには、クライアント ドライバーは、エンドポイント記述子を調べます。 そのコードは、という名前の次のコード ブロックに示された RetrieveStreamInfoFromEndpointDesc ヘルパー ルーチンに実装されます。

```cpp
NTSTATUS  
    FX3EnumeratePipes(  
    _In_ WDFDEVICE Device)

{  

    NTSTATUS                    status;  
    PDEVICE_CONTEXT             pDeviceContext;  

    UCHAR                       i; 

    PPIPE_CONTEXT               pipeContext;

    WDFUSBPIPE                  pipe; 

    WDF_USB_PIPE_INFORMATION    pipeInfo;  

    PAGED_CODE();  

    pDeviceContext = GetDeviceContext(Device);

    // Get the number of pipes in the current altenrate setting.
    pDeviceContext->NumberConfiguredPipes = WdfUsbInterfaceGetNumConfiguredPipes(
        pDeviceContext->UsbInterface);

    if (pDeviceContext->NumberConfiguredPipes == 0)
    {
        status = USBD_STATUS_BAD_NUMBER_OF_ENDPOINTS;
        goto Exit;
    }
    else
    {
        status = STATUS_SUCCESS;
    }

    // Enumerate the pipes and get pipe information for each pipe.
    for (i = 0; i < pDeviceContext->NumberConfiguredPipes; i++) 
    {
        WDF_USB_PIPE_INFORMATION_INIT(&pipeInfo); 

        pipe =  WdfUsbInterfaceGetConfiguredPipe(
            pDeviceContext->UsbInterface,  
            i, 
            &pipeInfo); 

        if (pipe == NULL)
        {
            continue;
        }

        pipeContext = GetPipeContext (pipe);

        // If the pipe is a bulk endpoint that supports streams, 
        // If the host controller supports streams, open streams.
        // Use the endpoint as an IN bulk endpoint.
        // Store the maximum packet size.

        if ((WdfUsbPipeTypeBulk == pipeInfo.PipeType) &&
            WdfUsbTargetPipeIsInEndpoint (pipe))
        {

            // Check if this is a streams IN endpoint. If it is,
            // Get the maximum number of streams and store
            // the value in the pipe context.
            RetrieveStreamInfoFromEndpointDesc (
                Device,
                pipe);

            if ((pipeContext->IsStreamsCapable) &&
                (pipeContext->MaxStreamsSupported > 0))
            {           
                status = OpenStreams (
                    Device,
                    pipe);

                if (status != STATUS_SUCCESS)
                {
                    TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                        "%!FUNC! Could not open streams.");

                    pDeviceContext->StreamInPipe = NULL;
                }
                else
                {
                    pDeviceContext->StreamInPipe = pipe;

                    pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

                }
            }
            else
            {
                pDeviceContext->BulkReadPipe = pipe;

                pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

            }

            continue;
        }

        if ((WdfUsbPipeTypeBulk == pipeInfo.PipeType) &&
            WdfUsbTargetPipeIsOutEndpoint (pipe))
        {
            // Check if this is a streams IN endpoint. If it is,
            // Get the maximum number of streams and store
            // the value in the pipe context.
            RetrieveStreamInfoFromEndpointDesc (
                Device,
                pipe);

            if ((pipeContext->IsStreamsCapable) &&
                (pipeContext->MaxStreamsSupported > 0))
            {           
                status = OpenStreams (
                    Device,
                    pipe);

                if (status != STATUS_SUCCESS)
                {
                    TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
                        "%!FUNC! Could not open streams.");

                    pDeviceContext->StreamOutPipe = NULL;
                }
                else
                {
                    pDeviceContext->StreamOutPipe = pipe;

                    pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

                }
            }
            else
            {
                pDeviceContext->BulkWritePipe = pipe;

                pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

            }

            continue;
        }

        if ((WdfUsbPipeTypeInterrupt == pipeInfo.PipeType) &&
            WdfUsbTargetPipeIsInEndpoint (pipe))
        {
            pDeviceContext->InterruptPipe = pipe;

            pipeContext->MaxPacketSize = pipeInfo.MaximumPacketSize;

            continue;
        }

    }  


Exit:
    return status;

}
```

次のコード例では、パイプを列挙中に、クライアント ドライバーを呼び出す RetrieveStreamInfoFromEndpointDesc、という名前のヘルパー ルーチンを示します。

次のコード例では、クライアント ドライバーは、パイプを列挙中に前のヘルパー ルーチンの RetrieveStreamInfoFromEndpointDesc を呼び出します。 ルーチンでは、最初の取得の構成記述子を調査し、エンドポイント記述子の取得を解析します。 パイプのエンドポイント記述子が USB を含むかどうか\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子\_型記述子では、ドライバーでサポートされているストリームの最大数を取得します、エンドポイント。

```cpp
/*++

Routine Description:

This routine parses the configuration descriptor and finds the endpoint
with which the specified pipe is associated.
It then retrieves the maximum number of streams supported by the endpoint.
It stores maximum number of streams in the pipe context.

Arguments:

Device - WDFUSBDEVICE handle to the target device object. 
The driver obtained that handle in a previous call to
WdfUsbTargetDeviceCreateWithParameters.

Pipe - WDFUSBPIPE handle to the target pipe object.

Return Value:

NTSTATUS
++*/

VOID RetrieveStreamInfoFromEndpointDesc (
    WDFDEVICE Device,
    WDFUSBPIPE Pipe)
{
    PDEVICE_CONTEXT                                 deviceContext                = NULL;
    PUSB_CONFIGURATION_DESCRIPTOR                   configDescriptor             = NULL;
    WDF_USB_PIPE_INFORMATION                        pipeInfo;
    PUSB_COMMON_DESCRIPTOR                          pCommonDescriptorHeader      = NULL;
    PUSB_INTERFACE_DESCRIPTOR                       pInterfaceDescriptor         = NULL;
    PUSB_ENDPOINT_DESCRIPTOR                        pEndpointDescriptor          = NULL;
    PUSB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR   pEndpointCompanionDescriptor = NULL;
    ULONG                                           maxStreams;
    ULONG                                           index;
    BOOLEAN                                         found                        = FALSE;
    UCHAR                                           interfaceNumber = 0;
    UCHAR                                           alternateSetting = 1;
    PPIPE_CONTEXT                                   pipeContext = NULL;
    NTSTATUS                                        status;

    PAGED_CODE();

    deviceContext = GetDeviceContext (Device);

    pipeContext = GetPipeContext (Pipe);


    // Get the configuration descriptor of the currently selected configuration
    status = FX3RetrieveConfigurationDescriptor (
        deviceContext->UsbDevice,
        &deviceContext->ConfigurationNumber,
        &configDescriptor);

    if (!NT_SUCCESS (status))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor.");

        status = USBD_STATUS_INAVLID_CONFIGURATION_DESCRIPTOR;

        goto Exit;
    }

    if (deviceContext->ConfigurationNumber == 1)
    {
        alternateSetting = 1;
    }
    else
    {
        alternateSetting = 0;
    }

    // Get the Endpoint Address of the pipe
    WDF_USB_PIPE_INFORMATION_INIT(&pipeInfo);  
    WdfUsbTargetPipeGetInformation (Pipe, &pipeInfo);


    // Parse the ConfigurationDescriptor (including all Interface and
    // Endpoint Descriptors) and locate a Interface Descriptor which
    // matches the InterfaceNumber, AlternateSetting, InterfaceClass,
    // InterfaceSubClass, and InterfaceProtocol parameters.  

    pInterfaceDescriptor = USBD_ParseConfigurationDescriptorEx(
        configDescriptor,
        configDescriptor,
        interfaceNumber,  //Interface number is 0.
        alternateSetting,  // Alternate Setting is 1
        -1, // InterfaceClass, ignore
        -1, // InterfaceSubClass, ignore
        -1  // InterfaceProtocol, ignore
        );

    if (pInterfaceDescriptor == NULL ) 
    {
        // USBD_ParseConfigurationDescriptorEx failed to retrieve Interface Descriptor.
        goto Exit;
    }

    pCommonDescriptorHeader = (PUSB_COMMON_DESCRIPTOR) pInterfaceDescriptor;

    for(index = 0; index < pInterfaceDescriptor->bNumEndpoints; index++) 
    {

        pCommonDescriptorHeader = USBD_ParseDescriptors(
            configDescriptor,
            configDescriptor->wTotalLength,
            pCommonDescriptorHeader,
            USB_ENDPOINT_DESCRIPTOR_TYPE);

        if (pCommonDescriptorHeader == NULL) 
        {
            // USBD_ParseDescriptors failed to retrieve Endpoint Descriptor unexpectedly.
            goto Exit;

        }

        pEndpointDescriptor = (PUSB_ENDPOINT_DESCRIPTOR) pCommonDescriptorHeader;

        // Search an Endpoint Descriptor that matches the EndpointAddress
        if (pEndpointDescriptor->bEndpointAddress == pipeInfo.EndpointAddress)
        {

            found = TRUE;

            break;

        }

        // Skip the current Endpoint Descriptor and search for the next.
        pCommonDescriptorHeader = (PUSB_COMMON_DESCRIPTOR)(((PUCHAR)pCommonDescriptorHeader) 
            + pCommonDescriptorHeader->bLength);

    }

    if (found) 
    {
        // Locate the SuperSpeed Endpoint Companion Descriptor 
        // associated with the endpoint descriptor
        pCommonDescriptorHeader = USBD_ParseDescriptors (
            configDescriptor,
            configDescriptor->wTotalLength,
            pEndpointDescriptor,
            USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR_TYPE);

        if (pCommonDescriptorHeader != NULL) 
        {
            pEndpointCompanionDescriptor = 
                (PUSB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR) pCommonDescriptorHeader;

            maxStreams = pEndpointCompanionDescriptor->bmAttributes.Bulk.MaxStreams;

            if (maxStreams == 0) 
            {

                pipeContext->MaxStreamsSupported = 0;

                pipeContext->IsStreamsCapable = FALSE;
            } 
            else 
            {
                pipeContext->IsStreamsCapable = TRUE;

                pipeContext->MaxStreamsSupported = 1 << maxStreams;

            }

        } 
        else 
        {
            KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, 
                "USBD_ParseDescriptors failed to retrieve SuperSpeed Endpoint Companion Descriptor unexpectedly.\n" ));        
        }

    }
    else
    {
        pipeContext->MaxStreamsSupported = 0;

        pipeContext->IsStreamsCapable = FALSE;
    }

Exit:
    if (configDescriptor)
    {
        ExFreePoolWithTag (configDescriptor, USBCLIENT_TAG);
    }

    return;
}
```

### <a name="getting-pipe-handles---umdf-client-driver"></a>パイプ ハンドルの取得 - UMDF クライアント ドライバー

UMDF クライアント ドライバーでは、COM インフラストラクチャを使用し、framework デバイス オブジェクトと組み合わせて使用する COM コールバック クラスを実装します。 KMDF ドライバーと同様に、クライアント UMDF ドライバーのみを取得できますパイプ情報、デバイスを構成した後。 ドライバー情報を取得するパイプ クライアントへのポインターを取得する必要があります、 [ **IWDFUsbTargetPipe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)アクティブな設定を含むフレームワーク インターフェイス オブジェクトのインターフェイス。 インターフェイス ポインターを使用すると、ドライバーはパイプを取得するには、その設定の列挙できる**IWDFUsbTargetPipe**インターフェイス フレームワーク ターゲットのパイプ オブジェクトによって公開されるポインター。

ドライバーは、パイプを列挙するを起動する前に、デバイスの構成とサポートされているエンドポイントについて、ドライバーが必要です。 その情報に基づいて、ドライバーはクラスのメンバー変数としてパイプ オブジェクトを格納できます。

次のコード例では、Visual Studio Professional 2012 に付属している USB UMDF テンプレートを拡張します。 スタート コードの詳細については、次を参照してください"[**IPnpCallbackHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackhardware)実装と USB の特定のタスク"で[USB クライアント ドライバー コード構造 (UMDF)について](understanding-the-umdf-template-code-for-usb.md).

CDevice クラスの宣言は、次に示すように拡張します。 このコード例では、デバイスが OSR FX2 ボードであると仮定します。 記述子のレイアウトについては、次を参照してください。 [USB デバイス レイアウト](usb-device-layout.md)します。

```cpp
class CMyDevice :
    public CComObjectRootEx<CComMultiThreadModel>,
    public IPnpCallbackHardware
{

public:

    DECLARE_NOT_AGGREGATABLE(CMyDevice)

    BEGIN_COM_MAP(CMyDevice)
        COM_INTERFACE_ENTRY(IPnpCallbackHardware)
    END_COM_MAP()

    CMyDevice() :
        m_FxDevice(NULL),
        m_IoQueue(NULL),
        m_FxUsbDevice(NULL)
    {
    }

    ~CMyDevice()
    {
    }

private:

    IWDFDevice *            m_FxDevice;

    CMyIoQueue *            m_IoQueue;

    IWDFUsbTargetDevice *   m_FxUsbDevice;

    IWDFUsbInterface *      m_pIUsbInterface;  //Pointer to the target interface object.

    IWDFUsbTargetPipe *     m_pIUsbInputPipe;  // Pointer to the target pipe object for the bulk IN endpoint.

    IWDFUsbTargetPipe *     m_pIUsbOutputPipe; // Pointer to the target pipe object for the bulk OUT endpoint.

    IWDFUsbTargetPipe *     m_pIUsbInterruptPipe; // Pointer to the target pipe object for the interrupt endpoint.

private:

    HRESULT
    Initialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit
        );

public:

    static
    HRESULT
    CreateInstanceAndInitialize(
        __in IWDFDriver *FxDriver,
        __in IWDFDeviceInitialize *FxDeviceInit,
        __out CMyDevice **Device
        );

    HRESULT
    Configure(
        VOID
        );

    HRESULT                     // Declare a helper function to enumerate pipes.
    ConfigureUsbPipes(  
        );
public:

    // IPnpCallbackHardware methods

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnPrepareHardware(
            __in IWDFDevice *FxDevice
            );

    virtual
    HRESULT
    STDMETHODCALLTYPE
    OnReleaseHardware(
        __in IWDFDevice *FxDevice
        );

};
```

CDevice クラスの定義では、CreateUsbIoTargets というヘルパー メソッドを実装します。 このメソッドは、ドライバーは、ターゲット デバイスのオブジェクトへのポインターを取得した後、IPnpCallbackHardware::OnPrepareHardware 実装から呼び出されます。

```cpp

HRESULT  CMyDevice::CreateUsbIoTargets()  

    HRESULT                 hr;  
    UCHAR                   NumEndPoints = 0;  

    IWDFUsbInterface *      pIUsbInterface = NULL;  
    IWDFUsbTargetPipe *     pIUsbPipe = NULL;  


    if (SUCCEEDED(hr))   
    {  
        UCHAR NumInterfaces = pIUsbTargetDevice->GetNumInterfaces();  

        WUDF_TEST_DRIVER_ASSERT(1 == NumInterfaces);  

        hr = pIUsbTargetDevice->RetrieveUsbInterface(0, &pIUsbInterface);  
        if (FAILED(hr))  
        {  
            TraceEvents(TRACE_LEVEL_ERROR,   
                        TEST_TRACE_DEVICE,   
                        "%!FUNC! Unable to retrieve USB interface from USB Device I/O Target %!HRESULT!",  
                        hr  
                        );          
        }  
        else  
        {  
            m_pIUsbInterface = pIUsbInterface;  

            DriverSafeRelease (pIUsbInterface); //release creation reference                                
        }
     }  

    if (SUCCEEDED(hr))   
    {  
        NumEndPoints = pIUsbInterface->GetNumEndPoints();  

        if (NumEndPoints != NUM_OSRUSB_ENDPOINTS) 
        {  
            hr = E_UNEXPECTED;  
            TraceEvents(TRACE_LEVEL_ERROR,   
                        TEST_TRACE_DEVICE,   
                        "%!FUNC! Has %d endpoints, expected %d, returning %!HRESULT! ",   
                        NumEndPoints,  
                        NUM_OSRUSB_ENDPOINTS,  
                        hr  
                        );  
        }  
    }  

    if (SUCCEEDED(hr))   
    {  
        for (UCHAR PipeIndex = 0; PipeIndex < NumEndPoints; PipeIndex++)  
        {  
            hr = pIUsbInterface->RetrieveUsbPipeObject(PipeIndex,   
                                                  &pIUsbPipe);  

            if (FAILED(hr))  
            {  
                TraceEvents(TRACE_LEVEL_ERROR,   
                            TEST_TRACE_DEVICE,   
                            "%!FUNC! Unable to retrieve USB Pipe for PipeIndex %d, %!HRESULT!",  
                            PipeIndex,  
                            hr  
                            );          
            }  
            else  
            {  
                if ( pIUsbPipe->IsInEndPoint() )  
                {  
                    if ( UsbdPipeTypeInterrupt == pIUsbPipe->GetType() )  
                    {  
                        m_pIUsbInterruptPipe = pIUsbPipe;  
                    }  
                    else if ( UsbdPipeTypeBulk == pIUsbPipe->GetType() )  
                    {  
                        m_pIUsbInputPipe = pIUsbPipe;  
                    }  
                    else  
                    {  
                        pIUsbPipe->DeleteWdfObject();  
                    }                        
                }  
                else if ( pIUsbPipe->IsOutEndPoint() && (UsbdPipeTypeBulk == pIUsbPipe->GetType()) )  
                {  
                    m_pIUsbOutputPipe = pIUsbPipe;  
                }  
                else  
                {  
                    pIUsbPipe->DeleteWdfObject();  
                }  

                DriverSafeRelease(pIUsbPipe);  //release creation reference
            }  
        }  

        if (NULL == m_pIUsbInputPipe || NULL == m_pIUsbOutputPipe)  
        {  
            hr = E_UNEXPECTED;  
            TraceEvents(TRACE_LEVEL_ERROR,   
                        TEST_TRACE_DEVICE,   
                        "%!FUNC! Input or output pipe not found, returning %!HRESULT!",  
                        hr  
                        );          
        }  
    }  

    return hr;  
}  
```

UMDF では、クライアント ドライバーは、データ転送の要求を送信するのにパイプ インデックスを使用します。 パイプのインデックスは、設定でエンドポイントの場合、パイプを開くときに、USB ドライバー スタックによって割り当てられた番号です。 パイプのインデックスを取得するには、呼び出し、[**IWDFUsbTargetPipe::GetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)メソッド。 メソッドの設定、 [ **WINUSB\_パイプ\_情報**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)構造体。 **PipeId**値がパイプ インデックスを示します。

実行する方法の 1 つの読み取りし、ターゲットのパイプで書き込み操作を呼び出すことです[ **IWDFUsbInterface::GetWinUsbHandle** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle) WinUSB ハンドルを取得し、呼び出す[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb). たとえば、ドライバーを呼び出すことができます、 [ **WinUsb\_ReadPipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)または[ **WinUsb\_WritePipe** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)関数。 これらの関数呼び出しで、ドライバーは、パイプ インデックスを指定する必要があります。 詳細については、次を参照してください。 [WinUSB 関数を使用して、USB デバイスへのアクセス方法](using-winusb-api-to-communicate-with-a-usb-device.md)します。

<a name="remarks"></a>注釈
-------

### <a name="pipe-handles-for-wdm-based-client-drivers"></a>WDM ベースのクライアント ドライバー用のパイプ ハンドル

構成を選択すると、USB ドライバー スタックは、各デバイスのエンドポイントへのパイプを設定します。 USB ドライバー スタックの配列を返します[ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)構造体。 配列内の要素の数は、選択した構成でインターフェイスのアクティブな代替設定に定義されたエンドポイントの数によって異なります。 各要素には、特定のエンドポイント用に作成されたパイプに関する情報が含まれています。 パイプ ハンドルを取得する方法の詳細については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。

I/O の転送要求をビルドするには、クライアント ドライバーは、そのエンドポイントに関連付けられているパイプへのハンドルをする必要があります。 クライアント ドライバーからパイプ ハンドルを取得できます、 **PipeHandle**のメンバー [ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)配列にします。

クライアント ドライバーには、パイプ ハンドルだけでなく、パイプ型も必要です。 クライアント ドライバーを調べることでパイプ タイプを決定できます、 **PipeType**メンバー。

エンドポイントの種類に基づいて、USB ドライバー スタックは、パイプのさまざまな種類をサポートします。 クライアント ドライバーを調べることでパイプ タイプを決定できます、 **PipeType**のメンバー [ **USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_usbd_pipe_information)します。 別のパイプ型では、さまざまな種類の USB 要求のブロック (翻訳) I/O トランザクションを実行する必要があります。

クライアント ドライバーでは、USB ドライバー スタックに URB、送信します。 USB ドライバー スタックは、要求を処理し、要求されたターゲットのパイプを指定したデータを送信します。

URB には、ターゲットのパイプ ハンドル、転送のバッファーの長さなどの要求に関する情報が含まれています。 内の各構造、 [ **URB** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb)共用体は、特定のメンバーを共有します。**TransferFlags**、 **TransferBuffer**、 **TransferBufferLength**、および**TransferBufferMDL**します。 型固有のフラグがあります、 **TransferFlags** URB の種類ごとに対応するメンバー。 すべてのデータ転送の翻訳、USBD\_転送\_方向\_IN フラグ**TransferFlags**転送の方向を指定します。 クライアント ドライバーの設定、USBD\_転送\_方向\_デバイスからデータを読み取るフラグ。 ドライバーは、デバイスにデータを送信するには、このフラグをクリアします。 データの読み取りし、メモリに常駐しているか、バッファーまたは MDL に書き込むことがあります。 どちらの場合、ドライバーは、バッファーのサイズを指定します、 **TransferBufferLength**メンバー。 ドライバーに常駐しているバッファーを提供する、 **TransferBuffer**メンバーとの MDL、 **TransferBufferMDL**メンバー。 いずれか 1 つ、ドライバーには、NULL にする他の必要があります。

## <a name="related-topics"></a>関連トピック
[USB I/O の転送](usb-device-i-o.md)  
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB インターフェイスで代替の設定を選択する方法](select-a-usb-alternate-setting.md)  
[USB クライアント ドライバーに関する一般的なタスク](wdk-resources-for-usb-driver-development.md)  



