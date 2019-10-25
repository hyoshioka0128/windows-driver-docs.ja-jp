---
Description: このトピックでは、USB インターフェイスで別の設定を有効にするために、選択インターフェイスの要求を発行する手順について説明します。
title: USB インターフェイスにおける代替設定の選択方法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d82ce7f0d7c988fc84c9e1f82f72005d82c4e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824186"
---
# <a name="how-to-select-an-alternate-setting-in-a-usb-interface"></a>USB インターフェイスにおける代替設定の選択方法


このトピックでは、USB インターフェイスで別の設定を有効にするために、選択インターフェイスの要求を発行する手順について説明します。 クライアントドライバーは、USB 構成を選択した後に、この要求を発行する必要があります。 既定では、構成を選択すると、その構成の各インターフェイスの最初の代替設定もアクティブになります。

各 USB 構成では、1つまたは複数の USB インターフェイスをサポートする必要があります。 各インターフェイスは、デバイスとの間でデータを転送するために使用される1つ以上のエンドポイントを公開します。 USB インターフェイスには、インターフェイスを識別するために使用されるデバイス定義の*インターフェイスインデックス*が必要です。 インターフェイスには、インターフェイスのエンドポイントをグループ化する1つ以上の*代替設定*も必要です。 デバイス構成の一部として、クライアントドライバーはインターフェイスの代替設定の1つを選択する必要があります。 エンドポイントは別の設定間で共有できるため、特定の時点でアクティブにできる設定は1つだけです。 代替設定がアクティブになると、そのエンドポイントはデータ転送に使用できるようになります。

複数のインターフェイスデバイスでは、特定の時点で2つのインターフェイスをアクティブにすることができます。 クライアントドライバーは、各インターフェイスで別の設定を有効にする必要があります。 エンドポイントはインターフェイス間で共有されないため、各インターフェイスで各同時データ転送を実行できます。

代替設定はデバイスで定義され、*設定インデックス*と呼ばれる番号で識別されます。 インデックス0の代替設定は、このドキュメントセットの*既定の代替設定*と呼ばれます。 代替の設定については、「 [**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)の構造」を参照してください。 構造体には、設定が関連付けられているインターフェイスインデックス、および設定で定義されているエンドポイントの数が含まれます。 また、インターフェイスの機能が準拠するクラス仕様に関する情報も含まれています。 エンドポイントがグループ化される方法は、デバイスの機能によって異なります。

たとえば、インターフェイスでは、3つの代替設定 (インデックス0、1、2) を介して2つのアイソクロナスエンドポイントと2つの一括エンドポイントが公開されます。 別の設定0では、エンドポイントは定義されません。別の設定1では、一括エンドポイントを定義します。代替設定2では、アイソクロナスエンドポイントを定義します。 代替設定0にはエンドポイントがないため、クライアントドライバーはこの設定を選択して、帯域幅を節約するためにデータ転送を無効にすることができます。 他の設定のいずれかがアクティブになっている場合、デバイスはデータ転送の準備ができています。 別の設定1を使用すると、一括データを転送できます。 デバイスがストリーミングモードの場合は、代替設定2を選択できます。 そのため、代替の設定により、クライアントドライバーは、必要に応じて、デバイス構成を柔軟に変更できます。 この例では、クライアントドライバーは、別の設定を選択するだけで、デバイスの機能を一括転送からストリーミングに切り替えることができます。

代替設定を使用して、帯域幅の要件を設定することもできます。 例については、「 [USB デバイスのレイアウト](usb-device-layout.md)」を参照してください。

Windows Driver Foundation (WDF) には、クライアントドライバーが別の代替設定を選択するために呼び出すことができる[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)と[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)のメソッドが用意されています。 KMDF クライアントドライバーは、設定インデックス、設定のインターフェイス記述子、または要求を含む URB を送信することによって、設定を選択できます。 UMDF client ドライバーは、設定インデックスを指定することによってのみ、代替設定を選択できます。

選択構成要求が正常に完了すると、以前にアクティブになっていた代替設定が非アクティブになります。

## <a name="what-you-need-to-know"></a>理解しておく必要があること


### <a name="technologies"></a>テクノロジ

-   [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)

### <a name="prerequisites"></a>前提条件

クライアントドライバーで別の設定を選択する前に、次の要件が満たされていることを確認してください。

-   クライアントドライバーによって、フレームワークの USB ターゲットデバイスオブジェクトが作成されている必要があります。

    -   KMDF クライアントドライバーは、 [**WdfUsbTargetDeviceCreateWithParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)メソッドを呼び出すことによって WDFUSBDEVICE ハンドルを取得する必要があります。 詳細については、「 [USB クライアントドライバーのコード構造 (KMDF)](understanding-the-kmdf-template-code-for-usb.md)について」の「デバイスのソースコード」を参照してください。
    -   UMDF クライアントドライバーは、フレームワークのターゲットデバイスオブジェクトを照会することによって、 [**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)ポインターを取得する必要があります。 詳細については、「 [usb クライアントドライバーコード構造 (UMDF)](understanding-the-umdf-template-code-for-usb.md)について」の「[**IPnpCallbackHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackhardware)の実装と usb 固有のタスク」を参照してください。

    Microsoft Visual Studio Professional 2012 で提供されている USB テンプレートを使用している場合は、テンプレートコードによってそれらのタスクが実行されます。 テンプレートコードは、ターゲットデバイスオブジェクトへのハンドルを取得し、デバイスコンテキストに格納します。

-   デバイスにはアクティブな構成が必要です。
    -   KMDF クライアントドライバーは、 [**WdfUsbTargetDeviceSelectConfig**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)メソッドを呼び出す必要があります。
    -   UMDF クライアントドライバーでは、フレームワークによって、最初の構成と、その構成内の各インターフェイスの既定の代替設定が選択されます。

    USB テンプレートを使用している場合、コードは各インターフェイスの最初の構成と既定の代替設定を選択します。

<a name="instructions"></a>手順
------------

### <a name="select-an-alternate-setting---kmdf-client-driver"></a>別の設定を選択する-KMDF クライアントドライバー

1.  代替設定を持つインターフェイスへの WDFUSBINTERFACE ハンドルを取得します。

    ハンドルを取得するには、まず、 [**WdfUsbTargetDeviceGetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetnuminterfaces)を呼び出し、ループ内のインターフェイスを列挙することによって、選択した構成のインターフェイスの数を取得します。 各イテレーションで、 [**WdfUsbTargetDeviceGetInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetinterface)メソッドを呼び出し、インデックスを (0 から開始して) インクリメントします。

    **注**  デバイスの列挙中に、USB ドライバースタックによって代替設定に数値が割り当てられます。 インターフェイス番号は、0から始まり、順次です。 これらの数値は、デバイス定義の設定インデックスとは異なる場合があります。 デバイス定義の設定インデックスを取得するには、 [**WdfUsbInterfaceGetInterfaceNumber**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetinterfacenumber)メソッドを呼び出します。

     

2.  [**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)メソッドを呼び出して、選択インターフェイスの要求を開始します。 呼び出しの*Params*パラメーターで、次のいずれかのオプションを選択します。

    -   USB ドライバースタックによって割り当てられた別の設定番号を指定します。 通常、設定を列挙するには、手順 1. で使用したのと同じインデックスを渡します。
    -   代替設定を記述するインターフェイス記述子を指すポインターを指定します。 ドライバーは、 [**WdfUsbInterfaceGetDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)メソッドを呼び出すことによってインターフェイスの代替設定を列挙しながら、インターフェイス記述子を取得できます。 列挙が完了すると、ドライバーは、 [**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)構造のすべての列挙された代替設定に関する情報を取得します。
    -   選択インターフェイスの要求に必要なすべての情報が含まれている URB へのポインターを指定します。

        1.  [**USBD\_INTERFACE\_LIST\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/ns-usbdlib-_usbd_interface_list_entry)構造体の配列を割り当てます。 この配列内の要素の数は、選択した構成のインターフェイスの数によって異なります。 この配列の初期化の詳細については、「 [USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。
        2.  [**USBD\_SelectInterfaceUrbAllocateAndBuild**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectinterfaceurballocateandbuild)ルーチンを呼び出して、選択インターフェイス要求の[**URB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)を割り当てます。 この呼び出しでは、インターフェイスリストの配列と、構成を選択した後に取得された構成ハンドルを指定します。 このハンドルは、 [**WdfUsbTargetDeviceWdmGetConfigurationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicewdmgetconfigurationhandle)メソッドを呼び出すことによって取得できます。
        3.  [**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)を呼び出し、URB を指定します。

        **WDM ドライバー:  **URB を送信するには、URB を IRP に関連付け、IRP を USB ドライバースタックに送信します。 詳細については、「 [URB を送信する方法](send-requests-to-the-usb-driver-stack.md)」を参照してください。

    一覧のオプションを使用すると、クライアントドライバーは選択条件を柔軟に指定できます。 別の設定のエンドポイント機能を既に認識している場合は、一覧の最初のオプション (別の設定番号を使用) を選択します。 それ以外の場合は、インターフェイス記述子を指定する2番目のオプションを選択します。 すべての代替設定の[**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)構造を検査します。 各設定について、エンドポイントとその特性 (エンドポイントの種類、最大パケットサイズなど) を列挙します。 データ転送に必要な一連のエンドポイントが見つかったら、そのインターフェイス記述子へのポインターを指定して[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)を呼び出します。 通常、URBs を送信して USB ドライバースタックに要求を送信できるのは、WDM ベースのクライアントドライバーでない限り、3番目のオプションは必要ありません。

    クライアントドライバーによって指定された情報に基づいて、USB ドライバースタックは標準の制御要求 (インターフェイスの設定) を作成し、デバイスに送信します。 要求が正常に完了した場合、USB ドライバースタックは、代替設定のエンドポイントにパイプハンドルを取得します。

    別の設定を選択すると、クライアントドライバーは常に新しい設定のエンドポイントのパイプハンドルを取得する必要があります。 そうしないと、ドライバーが古いパイプハンドルを使用してデータ転送要求を送信する可能性があります。 パイプハンドルの取得の詳細については、「 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)」を参照してください。

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

### <a name="select-an-alternate-setting---umdf-client-driver"></a>別の設定を選択する-UMDF client driver

1.  [**IWDFUsbTargetDevice:: GetNumInterfaces**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-getnuminterfaces)メソッドを呼び出すことによって、アクティブ構成がサポートする USB インターフェイスの数を取得します。
2.  構成内の各インターフェイスの[**IWDFUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)ポインターを取得します。

    関数が NULL を返すまで、ループで[**IWDFUsbTargetDevice:: RetrieveUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrieveusbinterface)メソッドを呼び出すことにより、すべてのインターフェイスを列挙します。 各反復処理で、メンバーインデックス (0 から始まる) をインクリメントします。 ループは、列挙されたすべてのインターフェイスへの[**IWDFUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)ポインターを取得します。

3.  インターフェイスごとに、 [**IWDFUsbInterface:: GetWinUsbHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getwinusbhandle)を呼び出して winusb ハンドルを取得します。 このハンドルは、次の手順で必要になります。
4.  [**Winusb\_GetAssociatedInterface**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getassociatedinterface)を呼び出して、インターフェイスへのハンドルを取得します。 *AssociatedInterfaceIndex*パラメーターで、手順 2. でインデックスを指定します。
5.  インターフェイスの代替設定の数を決定します。

    ループで[**Winusb\_QueryInterfaceSettings**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)関数を呼び出し、各反復処理でインデックス (0 から始まる) をインクリメントします。 すべての設定が列挙されると、この関数はエラーを返します。\_\_の項目はこれ以上\_ません。 関数は、各設定のインターフェイス記述子も返します。

6.  各インターフェイス記述子の**Bnumendpoints**メンバーで受け取った値を使用して、そのエンドポイントを列挙します。 エンドポイント記述子を調べ、どの設定が要件を満たしているかを判断します。
7.  [**Winusb\_SetCurrentAlternateSetting**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting)関数を呼び出して、選択インターフェイス要求を開始します。 呼び出しで、手順 4. でインデックスに関連付けられている別の設定番号を指定します。
8.  [**Winusb\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)関数を呼び出して、手順4で取得したインターフェイスハンドルを解放します。
9.  [**Winusb\_Free**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)関数を呼び出して、手順3で取得した winusb ハンドルを解放します。
10. [**IWDFUsbInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)メソッドの使用が終了したら、手順 2. で取得したすべてのインターフェイスポインターを解放します。

<a name="remarks"></a>注釈
-------

KMDF クライアントドライバーの[**WdfUsbInterfaceSelectSetting**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)呼び出しでは、ドライバーによって定義されたパイプコンテキストへのポインターをドライバーが提供できます。 クライアントドライバーはパイプに関する情報をパイプコンテキストに格納できます。 パイプ情報の詳細については、「 [USB パイプを列挙する方法](how-to-get-usb-pipe-handles.md)」を参照してください。

## <a name="related-topics"></a>関連トピック
[USB デバイスの構成](configuring-usb-devices.md)  



