---
Description: このトピックでは、選択インターフェイス USB インターフェイスでの代替設定をアクティブ化要求を発行する手順について説明します。
title: USB インターフェイスにおける代替設定の選択方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa8746c5b091a12aa15bd2a24855d529a60e34ef
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379515"
---
# <a name="how-to-select-an-alternate-setting-in-a-usb-interface"></a>USB インターフェイスにおける代替設定の選択方法


このトピックでは、選択インターフェイス USB インターフェイスでの代替設定をアクティブ化要求を発行する手順について説明します。 クライアント ドライバーでは、USB の設定を選択した後、この要求を発行する必要があります。 その構成内の各インターフェイスでの最初の代替設定をアクティブにも既定では、構成を選択します。

各 USB 構成では、1 つまたは複数の複数の USB インターフェイスをサポートする必要があります。 各インターフェイスには、デバイスとデータの転送に使用される 1 つまたは複数のエンドポイントが公開されます。 USB インターフェイスが必要、デバイス定義、*インターフェイス インデックス*インターフェイスを識別するために使用されます。 1 つまたは複数のインターフェイス必要がありますも*代替設定*インターフェイスのエンドポイントをグループ化します。 デバイスの構成の一環として、クライアント ドライバーする必要があります、代替の設定のいずれかのインターフェイスで選択します。 エンドポイントは、代替設定間で共有できる、ため、1 つだけ設定を有効にする特定の時点。 別の設定がアクティブに、そのエンドポイントはデータ転送を有効になります。

複数のインターフェイス デバイスでは、2 つのインターフェイスは、特定の時点でアクティブできます。 クライアント ドライバーでは、各インターフェイスでの代替の設定をアクティブ化する必要があります。 エンドポイントは、インターフェイスと、そのため、各インターフェイスでの転送を実行できる各同時データの間で共有されません。

代替の設定はデバイス定義されと呼ばれる番号で識別、*インデックス設定*します。 インデックス 0 位置にある別の設定が呼び出されます、*既定の代替設定*このドキュメントで設定します。 代替の設定が記載されて、 [ **USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065)構造体。 構造体には、設定が関連付けられているインターフェイスのインデックスと、設定で定義されたエンドポイントの数が含まれています。 インターフェイスの機能が準拠するクラスの指定に関する情報も含まれています。 、エンドポイントがグループ化、方法は、デバイスの機能によって異なります。

たとえば、インターフェイスは、アイソクロナス 2 と 3 つの代替設定 (インデックス 0、1、2) を使用して 2 つの一括エンドポイントを公開します。 別の設定 0 で任意のエンドポイントが定義されていません代替 Setting 1; 一括のエンドポイントを定義します代替設定 2 は、アイソクロナス エンドポイントを定義します。 代替の設定を 0 にエンドポイントがあるないために、クライアント ドライバーは、帯域幅を節約するためにデータ転送を無効にするには、この設定を選択できます。 その他の設定のいずれかが、アクティブな場合、デバイスがデータ転送の準備ができてです。 代替 Setting 1 は、一括データ転送に使用できます。 デバイスがストリーミング モードの場合、代替設定 2 を選択できます。 そのため、代替の設定の柔軟性のクライアント ドライバー、必要に応じて、デバイスの構成を変更します。 この例では、クライアント ドライバーは、代替の設定を選択するだけで、ストリーミングを一括転送からデバイスの機能を切り替えることができます。

代替設定が帯域幅の要件を設定することもできます。 例については、次を参照してください。、 [USB デバイス レイアウト](usb-device-layout.md)します。

Windows Driver Foundation (WDF) は、メソッドを提供します。[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)と[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)クライアント ドライバーが別の代替設定を選択して呼び出すことができます。 KMDF クライアント ドライバーは、インデックス設定、設定のインターフェイスの記述子を指定するか、要求を含む、URB を送信することで、設定を選択できます。 UMDF クライアント ドライバーでは、そのインデックスの設定を指定することによってのみ、代替の設定を選択できます。

選択構成要求が正常に完了した後、以前にアクティブな別の設定が非アクティブ化します。

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

クライアント ドライバーでは、代替の設定を選択できます、前に、これらの要件を満たしていることを確認してください。

-   クライアント ドライバー フレームワーク USB ターゲット デバイス オブジェクトを作成する必要があります。

    -   KMDF クライアント ドライバーは、呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります、 [ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428)メソッド。 詳細については、「デバイスのソース コード」を参照してください[USB クライアント ドライバー コード構造 (KMDF) について](understanding-the-kmdf-template-code-for-usb.md)します。
    -   UMDF クライアント ドライバーを入手する必要があります、 [ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)フレームワーク ターゲットのデバイス オブジェクトのクエリを実行してポインター。 詳細については、次を参照してください"[**IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)実装と USB の特定のタスク"で[USB クライアント ドライバー コード構造 (UMDF) を理解する。](understanding-the-umdf-template-code-for-usb.md)

    Microsoft Visual Studio Professional 2012 と共に用意されている USB テンプレートを使用する場合、テンプレート コードは、これらのタスクを実行します。 テンプレート コードでは、ターゲット デバイス オブジェクトを識別するハンドルを取得し、デバイス コンテキストに格納します。

-   デバイスをアクティブな構成が必要です。
    -   KMDF クライアント ドライバーを呼び出す必要があります、 [ **WdfUsbTargetDeviceSelectConfig** ](https://msdn.microsoft.com/library/windows/hardware/ff550101)メソッド。
    -   UMDF のクライアント ドライバーの場合は、フレームワークは、その構成の最初の構成と各インターフェイスの既定の代替設定を選択します。

    USB テンプレートを使用している場合に、コードは、各インターフェイスの最初の構成と既定の代替設定を選択します。

<a name="instructions"></a>手順
------------

### <a name="select-an-alternate-setting---kmdf-client-driver"></a>代替の設定 - KMDF クライアント ドライバーを選択します。

1.  別の設定を持つインターフェイス WDFUSBINTERFACE ハンドルを取得します。

    ハンドルを取得するには、最初に呼び出すことで、選択した構成のインターフェイスの数を取得[ **WdfUsbTargetDeviceGetNumInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff550094)し、ループ内でインターフェイスが列挙されます。 各イテレーションの呼び出しで、 [ **WdfUsbTargetDeviceGetInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff550092)メソッドと増分値 (0 から始まる) インデックス。

    **注**  デバイスの列挙中に USB ドライバー スタックは、代替の設定に番号を割り当てます。 インターフェイスの番号は 0 から始まる連続しました。 これらの数値は、デバイス定義の設定のインデックスに異なる可能性があります。 デバイス定義の設定のインデックスを取得するには、呼び出し、 [ **WdfUsbInterfaceGetInterfaceNumber** ](https://msdn.microsoft.com/library/windows/hardware/ff550065)メソッド。

     

2.  呼び出して選択インターフェイス要求を開始、 [ **WdfUsbInterfaceSelectSetting** ](https://msdn.microsoft.com/library/windows/hardware/ff550073)メソッド。 *Params*呼び出しのパラメーターは、これらのオプションのいずれかを選択します。

    -   USB ドライバー スタックによって割り当てられた代替設定を指定します。 同じインデックスを渡すを一般に、手順 1. で設定を列挙するために使用します。
    -   別の設定を記述するインターフェイスの記述子のポインターを指定します。 ドライバー インターフェイスでの代替設定を呼び出すことによって列挙中にインターフェイスの記述子を取得できますし、 [ **WdfUsbInterfaceGetDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550060)メソッド。 ドライバーの列挙が完了したら、すべての列挙の代替設定に関する情報を取得します、 [ **USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065)構造体。
    -   選択インターフェイス要求に必要なすべての情報を含む、URB へのポインターを指定します。

        1.  配列を割り当てる[ **USBD\_インターフェイス\_一覧\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/ff539076)構造体。 この配列の要素の数は、選択した構成でインターフェイスの数によって異なります。 この配列の初期化については、次を参照してください。 [USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。
        2.  割り当て、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)呼び出すことによって選択インターフェイス要求に対して、 [ **USBD\_SelectInterfaceUrbAllocateAndBuild** ](https://msdn.microsoft.com/library/windows/hardware/hh406245)ルーチン。 この呼び出しでは、インターフェイスのリストの配列と構成の選択後に取得した構成のハンドルを指定します。 そのハンドルを呼び出して取得することができます、 [ **WdfUsbTargetDeviceWdmGetConfigurationHandle** ](https://msdn.microsoft.com/library/windows/hardware/ff551127)メソッド。
        3.  呼び出す[ **WdfUsbInterfaceSelectSetting** ](https://msdn.microsoft.com/library/windows/hardware/ff550073) URB を指定します。

        **WDM ドライバー:  **URB を送信する、IRP URB を関連付けるし、USB ドライバー スタックに IRP を送信します。 詳細については、次を参照してください。 [、URB を送信する方法](send-requests-to-the-usb-driver-stack.md)します。

    リストのオプションは、選択条件を指定するための柔軟性をクライアント ドライバーを提供します。 別の設定のエンドポイントの機能に注意してください。 既に場合は、一覧に (別の設定の番号) を含む最初のオプションを選択します。 それ以外の場合、インターフェイスの記述子を指定する 2 番目のオプションを選択します。 検査[ **USB\_インターフェイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff540065)構造体がすべての代替設定します。 設定ごとに、そのエンドポイントとエンドポイントの種類、最大パケット サイズなどの特性を列挙しなど。 データ転送に必要なエンドポイントのセットを検索するときに呼び出す[ **WdfUsbInterfaceSelectSetting** ](https://msdn.microsoft.com/library/windows/hardware/ff550073)そのインターフェイス記述子へのポインターを指定しています。 通常、USB ドライバー スタックに翻訳を送信して要求を送信できるだけ WDM ベースのクライアント ドライバーでない限り、3 番目のオプションを必要ありませんが。

    クライアント ドライバーによって提供される情報に基づき、USB ドライバー スタック標準のコントロール要求 (インターフェイスの設定) を作成し、デバイスに送信します。 要求が正常に完了すると、USB ドライバー スタックは、別の設定のエンドポイントへのパイプ ハンドルを取得します。

    代替の設定を選択した後、クライアント ドライバーは、新しい設定でエンドポイントのパイプ ハンドルを常に取得する必要があります。 これに失敗、ドライバーが古いパイプ ハンドルを使用してデータ転送の要求を送信することがあります。 パイプ ハンドルを取得する方法の詳細については、次を参照してください。 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

```cpp
NTSTATUS  FX3SelectInterfaceSetting(  
    _In_ WDFDEVICE Device,
    _In_ UCHAR SettingIndex)

{
    NTSTATUS                 status;  
    PDEVICE_CONTEXT          pDeviceContext;  
    WDF_OBJECT_ATTRIBUTES               pipeAttributes;

    WDF_USB_INTERFACE_SELECT_SETTING_PARAMS settingParams;

    PAGED_CODE();  

    pDeviceContext = GetDeviceContext(Device);

    if (pDeviceContext->UsbInterface == NULL)
    {
        status = USBD_STATUS_BAD_NUMBER_OF_INTERFACES;
        goto Exit;
    }

    WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE(&pipeAttributes, PIPE_CONTEXT);  

    pipeAttributes.EvtCleanupCallback = FX3EvtPipeContextCleanup;

    WDF_USB_INTERFACE_SELECT_SETTING_PARAMS_INIT_SETTING (&settingParams, SettingIndex);

    status = WdfUsbInterfaceSelectSetting (
        pDeviceContext->UsbInterface,
        &pipeAttributes,
        &settingParams);

    if (status != STATUS_SUCCESS)
    {
        goto Exit;
    }

    if (WdfUsbInterfaceGetNumConfiguredPipes (pDeviceContext->UsbInterface) > 0)
    {
        status = FX3EnumeratePipes (Device);

        if (status != STATUS_SUCCESS)
        {
            goto Exit;
        }
    }

Exit:
    return status;
}
```

### <a name="select-an-alternate-setting---umdf-client-driver"></a>代替の設定 - UMDF クライアント ドライバーを選択します。

1.  呼び出すことによって、アクティブな構成をサポートする USB インターフェイスの数を取得、 [ **IWDFUsbTargetDevice::GetNumInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff560366)メソッド。
2.  取得、 [ **IWDFUsbInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff560312)構成内の各インターフェイスへのポインター。

    すべてのインターフェイスを呼び出すことで列挙、 [ **IWDFUsbTargetDevice::RetrieveUsbInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff560381)関数は NULL を返すまで、ループ内のメソッド。 反復処理ごとに (0 から始まる) のメンバーのインデックスをインクリメントします。 ループの取得[ **IWDFUsbInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff560312)列挙されたすべてのインターフェイスへのポインター。

3.  各インターフェイスで呼び出すことによって WinUSB ハンドルを取得[ **IWDFUsbInterface::GetWinUsbHandle**](https://msdn.microsoft.com/library/windows/hardware/ff560337)します。 このハンドルは、次の手順で必要です。
4.  呼び出す[ **WinUsb\_GetAssociatedInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff540245)インターフェイスへのハンドルを取得します。 *AssociatedInterfaceIndex*パラメーター、手順 2. でインデックスを指定します。
5.  インターフェイスで代替の設定の数を決定します。

    呼び出す、 [ **WinUsb\_QueryInterfaceSettings** ](https://msdn.microsoft.com/library/windows/hardware/ff540292)ループ内で機能し、各イテレーションで (0 ベース) のインデックスをインクリメントします。 すべての設定が列挙されると、関数はエラーを返します\_いいえ\_詳細\_項目。 関数は、各設定のインターフェイスの記述子を返します。

6.  受信した値を使用して、 **bNumEndpoints**の各メンバーがインターフェイス記述子、およびそのエンドポイントを列挙します。 エンドポイント記述子を検査し、必要のある設定が要件を決定します。
7.  呼び出して選択インターフェイス要求を開始、 [ **WinUsb\_SetCurrentAlternateSetting** ](https://msdn.microsoft.com/library/windows/hardware/ff540302)関数。 呼び出しでは、手順 4. でインデックスに関連付けられている代替の設定の数を指定します。
8.  インターフェイスのハンドルが手順 4. で呼び出すことによって取得リリース、 [ **WinUsb\_Free** ](https://msdn.microsoft.com/library/windows/hardware/ff540233)関数。
9.  手順 3 で呼び出すことによって取得した WinUSB ハンドルを解放、 [ **WinUsb\_Free** ](https://msdn.microsoft.com/library/windows/hardware/ff540233)関数。
10. 完了した場合を使用して[ **IWDFUsbInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff560312)メソッド、手順 2 で取得したすべてのインターフェイス ポインターを解放します。

<a name="remarks"></a>コメント
-------

KMDF クライアント ドライバーでその[ **WdfUsbInterfaceSelectSetting** ](https://msdn.microsoft.com/library/windows/hardware/ff550073)を呼び出すには、ドライバーがドライバーの定義済みのパイプ コンテキストへのポインターを指定できます。 クライアント ドライバーは、パイプのコンテキストでパイプに関する情報を格納することができます。 パイプ情報の詳細については、次を参照してください。 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの構成](configuring-usb-devices.md)  



