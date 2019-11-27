---
Description: このトピックでは、usb パイプの概要について説明し、usb ドライバースタックからパイプハンドルを取得するために USB クライアントドライバーが必要とする手順について説明します。
title: USB パイプの列挙方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d574a4ac44297d62edf158c0915b4644768a38c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844371"
---
# <a name="how-to-enumerate-usb-pipes"></a>USB パイプの列挙方法


このトピックでは、usb パイプの概要について説明し、usb ドライバースタックからパイプハンドルを取得するために USB クライアントドライバーが必要とする手順について説明します。

*USB エンドポイント*は、デバイス内のバッファーで、クライアントドライバーがデータを送信するか、データを受信します。 データを送受信するために、クライアントドライバーは、データをホストコントローラーに提示する、USB ドライバースタックに i/o 転送要求を送信します。 ホストコントローラーは、デバイスとの間でデータを転送する要求を構築するために、特定のプロトコル (エンドポイントの種類 (一括、割り込み、またはアイソクロナス) によって異なります) に従います。 データ転送の詳細はすべて、クライアントドライバーから抽象化されています。 クライアントドライバーが適切な形式の要求を送信する限り、USB ドライバースタックは要求を処理し、データをデバイスに転送します。

デバイスの構成中に、usb ドライバースタックは、usb インターフェイスに定義されているデバイスの各エンドポイントとそのアクティブな代替設定に対して、usb*パイプ*(ホスト側) を作成します。 USB パイプは、ホストコントローラーとエンドポイント間の通信チャネルです。 クライアントドライバーの場合、パイプはエンドポイントを論理的に抽象化したものです。 データ転送を送信するために、ドライバーは、転送先のエンドポイントに関連付けられているパイプハンドルを取得する必要があります。 パイプハンドルは、エラーが発生した場合に、ドライバーによって転送が中止されたり、パイプがリセットされたりする場合にも必要です。

パイプのすべての属性は、関連付けられているエンドポイント記述子から派生します。 たとえば、エンドポイントの種類によっては、USB ドライバースタックによってパイプの種類が割り当てられます。 一括エンドポイントの場合、USB ドライバースタックによって一括パイプが作成されます。アイソクロナスエンドポイントの場合は、アイソクロナスパイプが作成されます。 もう1つの重要な属性は、ホストコントローラーが要求のエンドポイントに送信できるデータの量です。 クライアントドライバーは、その値に応じて、転送バッファーのレイアウトを決定する必要があります。

Windows Driver Foundation (WDF) は、[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)と[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)に特化した i/o ターゲットオブジェクトを提供します。これにより、クライアントドライバーの多くの構成タスクを簡単に行うことができます。 これらのオブジェクトを使用することにより、クライアントドライバーは、インターフェイスの数、各インターフェイス内の別の設定、エンドポイントなど、現在の構成に関する情報を取得できます。 これらのオブジェクトのいずれか (*ターゲットパイプオブジェクト*と呼ばれます) によって、エンドポイント関連のタスクが実行されます。 このトピックでは、ターゲットパイプオブジェクトを使用してパイプ情報を取得する方法について説明します。

Windows Driver Model (WDM) クライアントドライバーの場合、USB ドライバースタックは、 [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体の配列を返します。 配列内の要素の数は、選択した構成のインターフェイスのアクティブな代替設定に定義されているエンドポイントの数によって異なります。 各要素には、特定のエンドポイント用に作成されたパイプに関する情報が含まれます。 構成を選択し、パイプ情報の配列を取得する方法の詳細については、「 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

クライアントドライバーがパイプを列挙できるようにするには、次の要件が満たされていることを確認します。

-   クライアント ドライバーによって、フレームワーク USB ターゲット デバイス オブジェクトが作成されている必要があります。

    Microsoft Visual Studio Professional 2012 に付属する USB テンプレートを使用している場合、テンプレート コードでこれらのタスクが実行されます。 テンプレート コードによりターゲット デバイス オブジェクトのハンドルが取得され、デバイス コンテキストに格納されます。

    **KMDF クライアント ドライバー: **

    KMDF クライアント ドライバーでは、[**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters) メソッドを呼び出すことで WDFUSBDEVICE ハンドルを取得する必要があります。 詳細については、「[USB クライアント ドライバー コード構造について (KMDF)](understanding-the-kmdf-template-code-for-usb.md)」の「デバイスのソース コード」を参照してください。

    **UMDF クライアント ドライバー: **

    UMDF クライアント ドライバーは、フレームワーク ターゲット デバイス オブジェクトを問い合わせることで、[**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice) ポインターを取得する必要があります。 詳細については、「[USB クライアント ドライバー コード構造について (UMDF) **」の「** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)IPnpCallbackHardware[](understanding-the-umdf-template-code-for-usb.md) 実装と USB 固有のタスク」を参照してください。

-   デバイスにはアクティブな構成が必要です。

    USB テンプレートを使用している場合、コードは各インターフェイスの最初の構成と既定の代替設定を選択します。 この既定の設定を変更する方法の詳細については、「 [USB インターフェイスで別の設定を選択する方法](select-a-usb-alternate-setting.md)」を参照してください。

    **KMDF クライアント ドライバー: **

    KMDF クライアントドライバーは、 [**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)メソッドを呼び出す必要があります。

    **UMDF クライアント ドライバー: **

    UMDF クライアントドライバーでは、フレームワークによって、最初の構成と、その構成内の各インターフェイスの既定の代替設定が選択されます。

<a name="instructions"></a>手順
------------

### <a name="getting-usb-pipe-handles---kmdf-client-driver"></a>USB パイプハンドルの取得-KMDF クライアントドライバー

このフレームワークは、usb ドライバースタックによって開かれる各パイプを、USB ターゲットパイプオブジェクトとして表します。 KMDF クライアントドライバーは、パイプに関する情報を取得するために、ターゲットパイプオブジェクトのメソッドにアクセスできます。 データ転送を実行するには、クライアントドライバーが WDFUSBPIPE パイプハンドルを持っている必要があります。 パイプハンドルを取得するには、ドライバーは、アクティブな構成のインターフェイスと代替設定を列挙し、各設定で定義されているエンドポイントを列挙する必要があります。 データ転送ごとに列挙操作を実行すると、コストが高くなる可能性があります。 そのため、デバイスの構成後にパイプハンドルを取得し、ドライバー定義のデバイスコンテキストに格納する方法があります。 ドライバーは、データ転送要求を受信すると、デバイスコンテキストから必要なパイプハンドルを取得し、それを使用して要求を送信できます。 クライアントドライバによってデバイスの構成が変更された場合 (たとえば、が代替設定を選択した場合)、ドライバは新しいパイプハンドルを使用してデバイスコンテキストを更新する必要があります。 それ以外の場合、ドライバーは古いパイプハンドルに対して誤って転送要求を送信できます。

**メモ** パイプハンドルは、制御転送には必要ありません。
制御転送要求を送信するために、WDF クライアントドライバーは、フレームワークデバイスオブジェクトによって公開されている**WdfUsbDevicexxxx**メソッドを呼び出します。 これらのメソッドでは、既定のエンドポイントを対象とする制御転送を開始するために、WDFUSBDEVICE ハンドルが必要です。 このような転送では、要求の i/o ターゲットは既定のエンドポイントであり、WDFUSBPIPE ハンドルによって抽象化される WDFIOTARGET ハンドルによって表されます。 デバイスレベルでは、WDFUSBDEVICE ハンドルは、既定のエンドポイントへの WDFUSBPIPE ハンドルを抽象化したものです。

制御転送と KMDF メソッドの送信の詳細については、「 [USB 制御転送を送信する方法](usb-control-transfer.md)」を参照してください。



1.  パイプハンドルを格納するようにデバイスコンテキスト構造を拡張します。

    デバイスのエンドポイントがわかっている場合は、関連付けられている USB パイプハンドルを格納する WDFUSBPIPE メンバーを追加することによって、デバイスコンテキスト構造を拡張します。 たとえば、次に示すように、デバイスコンテキスト構造を拡張できます。

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

2.  パイプコンテキスト構造体を宣言します。

    各パイプは、*パイプコンテキスト*と呼ばれる別の構造にエンドポイント関連の特性を格納できます。 デバイスコンテキストと同様に、パイプコンテキストは、エンドポイントに関連付けられているパイプに関する情報を格納するためのデータ構造 (クライアントドライバーによって定義される) です。 デバイスの構成中に、クライアントドライバーはパイプコンテキストへのポインターをフレームワークに渡します。 フレームワークは、構造体のサイズに基づいてメモリのブロックを割り当て、フレームワークの USB ターゲットパイプオブジェクトを使用して、そのメモリ位置へのポインターを格納します。 クライアントドライバーは、ポインターを使用してパイプの情報にアクセスし、パイプのコンテキストのメンバーに格納することができます。

    ```cpp
    typedef struct _PIPE_CONTEXT {  

        ULONG MaxPacketSize;
        ULONG MaxStreamsSupported;
        PUSBD_STREAM_INFORMATION StreamInfo;
    } PIPE_CONTEXT, *PPIPE_CONTEXT;  

    WDF_DECLARE_CONTEXT_TYPE_WITH_NAME(PIPE_CONTEXT, GetPipeContext)  

    ```

    この例では、パイプコンテキストは、1回の転送で送信できる最大バイト数を格納します。 クライアントドライバーは、その値を使用して転送バッファーのサイズを決定できます。 宣言には、インライン関数 GetPipeContext を生成する\_NAME マクロを使用して[ **\_コンテキスト\_型\_を宣言する WDF\_** ](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-declare-context-type-with-name)も含まれています。 クライアントドライバーは、その関数を呼び出して、パイプコンテキストを格納するメモリブロックへのポインターを取得できます。

    コンテキストの詳細については、「[フレームワークオブジェクトコンテキスト空間](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-object-context-space)」を参照してください。

    クライアントドライバーは、ポインターをフレームワークに渡すために、まず[**WDF\_OBJECT\_属性\_初期化\_コンテキスト\_型**](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdf-object-attributes-init-context-type)を呼び出して、そのパイプコンテキストを初期化します。 次に、は、 [**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig) (構成を選択する場合) または[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting) (別の設定を選択する場合) を呼び出すときに、パイプコンテキストへのポインターを渡します。

3.  デバイス構成要求が完了したら、インターフェイスを列挙し、構成されているパイプのパイプハンドルを取得します。 この情報のセットが必要になります。

    -   WDFUSBINTERFACE は、現在の設定を含むインターフェイスをハンドルします。 アクティブ構成のインターフェイスを列挙することで、そのハンドルを取得できます。 または、 [**WDF\_USB\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_device_select_config_params)へのポインターを指定し\_\_CONFIG\_PARAMS 構造体を選択した場合は、 **ConfiguredUsbInterface**メンバー (単一インターフェイスデバイスの場合) または[**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)**インターフェイス**メンバー (マルチインターフェイスデバイスの場合) からハンドルを取得することもできます。
    -   現在の設定のエンドポイントで開かれているパイプの数。 [**WdfUsbInterfaceGetNumConfiguredPipes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetnumconfiguredpipes)メソッドを呼び出すことによって、特定のインターフェイスでその番号を取得できます。
    -   構成されているすべてのパイプの WDFUSBPIPE ハンドル。 ハンドルを取得するには、 [**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)メソッドを呼び出します。

    パイプハンドルを取得した後、クライアントドライバーはメソッドを呼び出して、パイプの型と方向を決定できます。 ドライバーは、エンドポイントに関する情報を、 [**WDF\_USB\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/ns-wdfusb-_wdf_usb_pipe_information)構造で取得できます。 ドライバーは、 [**WdfUsbTargetPipeGetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)メソッドを呼び出すことによって、設定された構造体を取得できます。 また、ドライバーは、 [**WdfUsbInterfaceGetConfiguredPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetconfiguredpipe)呼び出しの構造体へのポインターを提供することもできます。

次のコード例では、現在の設定のパイプを列挙します。 デバイスの bulk および interrupt エンドポイントのパイプハンドルを取得し、ドライバーのデバイスコンテキスト構造に格納します。 各エンドポイントの最大パケットサイズは、関連付けられているパイプコンテキストに格納されます。 エンドポイントでストリームがサポートされている場合は、OpenStreams ルーチンを呼び出すことによって、静的ストリームが開かれます。 OpenStreams の実装については、「 [USB 一括エンドポイントで静的ストリームを開いて閉じる方法](how-to-open-streams-in-a-usb-endpoint.md)」を参照してください。

特定の一括エンドポイントで静的ストリームがサポートされているかどうかを判断するために、クライアントドライバーはエンドポイント記述子を調べます。 このコードは、次のコードブロックに示すように、RetrieveStreamInfoFromEndpointDesc という名前のヘルパールーチンに実装されています。

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

次のコード例は、パイプの列挙中にクライアントドライバーが呼び出す、RetrieveStreamInfoFromEndpointDesc という名前のヘルパールーチンを示しています。

次のコード例では、クライアントドライバーは、パイプの列挙中に、前のヘルパールーチン RetrieveStreamInfoFromEndpointDesc を呼び出します。 ルーチンは最初に構成記述子を取得し、それを解析してエンドポイント記述子を取得します。 パイプのエンドポイント記述子に、USB\_SUPERSPEED\_エンドポイント\_コンパニオン\_記述子\_型記述子が含まれている場合、ドライバーはエンドポイントでサポートされているストリームの最大数を取得します。

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

### <a name="getting-pipe-handles---umdf-client-driver"></a>パイプハンドルの取得-UMDF クライアントドライバー

UMDF クライアントドライバーは、COM インフラストラクチャを使用し、フレームワークデバイスオブジェクトとペアになる COM コールバッククラスを実装します。 KMDF ドライバーと同様に、UMDF クライアントドライバーは、デバイスが構成された後でのみ、パイプ情報を取得できます。 パイプ情報を取得するには、クライアントドライバーは、アクティブな設定を含むフレームワークインターフェイスオブジェクトの[**IWDFUsbTargetPipe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)インターフェイスへのポインターを取得する必要があります。 インターフェイスポインターを使用すると、ドライバーはその設定のパイプを列挙して、フレームワークのターゲットパイプオブジェクトによって公開されている**IWDFUsbTargetPipe**インターフェイスポインターを取得できます。

ドライバーがパイプの列挙を開始する前に、ドライバーはデバイスの構成とサポートされているエンドポイントを認識している必要があります。 ドライバーは、その情報に基づいて、パイプオブジェクトをクラスメンバー変数として格納できます。

次のコード例では、Visual Studio Professional 2012 で提供される USB UMDF テンプレートを拡張します。 スターターコードの説明については、「 [usb クライアントドライバーコード構造 (UMDF) につい](understanding-the-umdf-template-code-for-usb.md)て」の「[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)の実装と usb 固有のタスク」を参照してください。

次に示すように CDevice クラスの宣言を拡張します。 このコード例では、デバイスが OSR FX2 board であることを前提としています。 記述子のレイアウトの詳細については、「 [USB デバイスのレイアウト](usb-device-layout.md)」を参照してください。

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

CDevice クラスの定義で、CreateUsbIoTargets というヘルパーメソッドを実装します。 このメソッドは、ドライバーがターゲットデバイスオブジェクトへのポインターを取得した後に、IPnpCallbackHardware:: On ハードウェアの実装から呼び出されます。

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

UMDF では、クライアントドライバーはパイプインデックスを使用してデータ転送要求を送信します。 パイプインデックスは、設定内のエンドポイントに対してパイプを開くときに、USB ドライバースタックによって割り当てられる番号です。 パイプインデックスを取得するには、[**IWDFUsbTargetPipe:: GetInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)メソッドを呼び出します。 メソッドは、 [**Winusb\_パイプ\_情報**](https://docs.microsoft.com/windows/desktop/api/winusbio/ns-winusbio-_winusb_pipe_information)構造体を設定します。 **PipeId**値は、パイプのインデックスを示します。

ターゲットパイプで読み取りおよび書き込み操作を実行する方法の1つとして、 [**IWDFUsbInterface:: GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)を呼び出して winusb ハンドルを取得し、 [winusb 関数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)を呼び出すことができます。 たとえば、ドライバーは[**winusb\_ReadPipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)または[**Winusb\_writepipe**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)関数を呼び出すことができます。 これらの関数呼び出しでは、ドライバーはパイプインデックスを指定する必要があります。 詳細については、「 [Winusb 機能を使用して Usb デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md)」を参照してください。

<a name="remarks"></a>注釈
-------

### <a name="pipe-handles-for-wdm-based-client-drivers"></a>WDM ベースのクライアントドライバーのパイプハンドル

構成を選択すると、USB ドライバースタックは、各デバイスのエンドポイントにパイプを設定します。 USB ドライバースタックは、 [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)構造体の配列を返します。 配列内の要素の数は、選択した構成のインターフェイスのアクティブな代替設定に定義されているエンドポイントの数によって異なります。 各要素には、特定のエンドポイント用に作成されたパイプに関する情報が含まれます。 パイプハンドルの取得の詳細については、「 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。

I/o 転送要求を作成するには、クライアントドライバーが、そのエンドポイントに関連付けられているパイプへのハンドルを持っている必要があります。 クライアントドライバーは、配列の[**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)の**PipeHandle**メンバーからパイプハンドルを取得できます。

パイプハンドルに加えて、クライアントドライバーもパイプの種類を必要とします。 クライアントドライバーは、 **PipeType**メンバーを調べることによって、パイプの種類を決定できます。

USB ドライバースタックでは、エンドポイントの種類に基づいて、さまざまな種類のパイプがサポートされています。 クライアントドライバーは、パイプの種類を特定できます。そのためには、 [**USBD\_パイプ\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_usbd_pipe_information)の**PipeType**メンバーを調べます。 さまざまなパイプの種類で i/o トランザクションを実行するには、さまざまな種類の USB 要求ブロック (URBs) が必要です。

その後、クライアントドライバーは、USB ドライバースタックに URB を送信します。 USB ドライバースタックは要求を処理し、指定されたデータを要求されたターゲットパイプに送信します。

URB には、ターゲットパイプハンドル、転送バッファー、その長さなど、要求に関する情報が含まれています。 [**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)共用体内の各構造体は、特定のメンバー ( **transferflags**、 **transferflags**、 **Transferbufferlength**、および**transferbuffermdl**) を共有します。 各 URB の種類に対応する**transferflags**メンバーには、型固有のフラグがあります。 すべてのデータ転送 URBs について、 **Transferflags**のフラグ内の USBD\_TRANSFER\_direction\_は転送の方向を指定します。 クライアントドライバーは、デバイスからデータを読み取るフラグで、USBD\_転送\_の方向\_設定します。 ドライバーは、デバイスにデータを送信するために、このフラグをクリアします。 データは、メモリまたは MDL に常駐しているバッファーに対して読み取りまたは書き込みを行うことができます。 どちらの場合も、ドライバーは**Transferbufferlength**メンバー内のバッファーのサイズを指定します。 このドライバーは、 **transferbuffer**メンバーの常駐バッファーと**TRANSFERBUFFERMDL**メンバーの MDL を提供します。 ドライバーが提供するいずれかの方法で、もう1つは NULL である必要があります。

## <a name="related-topics"></a>関連トピック
[USB i/o 転送](usb-device-i-o.md)  
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB インターフェイスで別の設定を選択する方法](select-a-usb-alternate-setting.md)  
[USB クライアントドライバーの一般的なタスク](wdk-resources-for-usb-driver-development.md)  



