---
Description: USB デバイスは、一連の USB 構成と呼ばれるインターフェイスの形式でその機能を公開します。
title: USB 構成記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 056bc5f058b8da64fe43246f988a5d06489a0d1a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369514"
---
# <a name="usb-configuration-descriptors"></a>USB 構成記述子


USB デバイスは、一連の USB 構成と呼ばれるインターフェイスの形式でその機能を公開します。 各インターフェイスは 1 つまたは複数の代替設定と各代替の設定は、一連のエンドポイントの構成されます。 このトピックでは、USB 構成に関連付けられたさまざまな記述子について説明します。

USB の構成については、「構成記述子 (を参照してください[ **USB\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_configuration_descriptor)構造). 構成記述子には、構成し、そのインターフェイス、代替の設定とそのエンドポイントに関する情報が含まれています。 各インターフェイス記述子または代替の設定に記載されて、 [ **USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)構造体。 構成では、各インターフェイスの記述子の後にメモリ内ですべてのインターフェイスと設定の代替のエンドポイント記述子。 各エンドポイント記述子に格納されている、 [ **USB\_エンドポイント\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_endpoint_descriptor)構造体。

たとえばで説明されている USB web カメラ デバイス[USB デバイス レイアウト](usb-device-layout.md)します。 デバイスでサポートする 2 つのインターフェイスの構成 (インデックス 0) の最初のインターフェイスが 2 つの代替設定をサポートしています。

次の例は、USB web カメラ デバイスの構成記述子を示しています。

``` syntax
Configuration Descriptor:
wTotalLength:         0x02CA
bNumInterfaces:       0x02
bConfigurationValue:  0x01
iConfiguration:       0x00
bmAttributes:         0x80 (Bus Powered )
MaxPower:             0xFA (500 mA)
```

**BConfigurationValue**フィールドは、デバイスのファームウェアで定義されている構成の数を示します。 クライアント ドライバーでは、番号値を使用して、アクティブな構成を選択します。 詳細については[USB デバイスの構成](configuring-usb-devices.md)を参照してください[USB デバイスの構成の選択方法](how-to-select-a-configuration-for-a-usb-device.md)します。 USB の構成には、特定の電源の特性も示されます。 **BmAttributes**構成がリモートのウェイク アップ機能をサポートするかどうかと、デバイスは、バス供給または自己供給型かどうかを示すビットマスクが含まれています。 **MaxPower**フィールドをデバイスは、バス供給ときに、ホストからデバイスを描画できる最大電力 (milliamp 単位) を指定します。 構成記述子では、インターフェイスの合計数も示されます (**bNumInterfaces**) デバイスをサポートします。

次の例では、web カメラ デバイス用のインターフェイス 0 の代替設定 0 のインターフェイスの記述子を示しています。

``` syntax
Interface Descriptor:
bInterfaceNumber:     0x00
bAlternateSetting:    0x00
bNumEndpoints:        0x01
bInterfaceClass:      0x0E
bInterfaceSubClass:   0x02
bInterfaceProtocol:   0x00
iInterface:           0x02
0x0409: "Microsoft LifeCam VX-5000"
0x0409: "Microsoft LifeCam VX-5000"
```

前の例では、次に注意してください。 **bInterfaceNumber**と**bAlternateSetting**フィールドの値。 これらのフィールドには、クライアント ドライバーは、インターフェイスとその代替の設定のいずれかのアクティブ化を使用してインデックスの値が含まれます。 アクティブにするため、ドライバーは USB ドライバー スタックに選択インターフェイス要求を送信します。 ドライバー スタックは、標準のコントロール要求 (インターフェイスの設定) を作成し、デバイスに送信します。 注、 **bInterfaceClass**フィールド。 インターフェイスの記述子または代替の設定のいずれかの記述子は、クラスのコード、サブクラスでは、およびプロトコルを指定します。 0x0E の値は、ビデオ デバイス クラスのインターフェイスであることを示します。 また、 **iInterface**フィールド。 その値は、インターフェイスの記述子に追加する 2 つの文字列記述子があることを示します。 文字列記述子には、デバイスの列挙中に、機能を識別するために使用される Unicode の説明が含まれています。 文字列記述子の詳細については、次を参照してください。 [USB 文字列記述子](usb-string-descriptors.md)します。

インターフェイスで各エンドポイントには、入力またはデバイスの出力の 1 つのストリームがについて説明します。 関数のさまざまな種類のストリームをサポートするデバイスには、複数のインターフェイスがあります。 関数に関連する複数のストリームをサポートするデバイスは、1 つのインターフェイスで、複数のエンドポイントをサポートできます。

ホストは、エンドポイントに関する情報を取得できるように、エンドポイント (既定のエンドポイント) を除くのすべての種類はエンドポイント記述子を提供する必要があります。 エンドポイント記述子には、そのアドレスの種類、方向などの情報が含まれています。、エンドポイントのデータの量を処理できます。 エンドポイントへのデータ転送は、その情報に基づいています。

次の例は、web カメラ デバイスのエンドポイント記述子を示しています。

``` syntax
Endpoint Descriptor:
bEndpointAddress:   0x82  IN
bmAttributes:       0x01
wMaxPacketSize:     0x0080 (128)
bInterval:          0x01
```

**BEndpointAddress**フィールドがエンドポイントの数 (Bits 3..0) と、エンドポイント (ビット 7) の方向を含む一意のエンドポイント アドレスを指定します。 上記の例ではこれらの値を読み取ることによって、記述子がエンドポイントの数は 2 のエンドポイントを記述することを判断できます。 **BmAttributes**属性は、エンドポイントの種類がアイソクロナスであることを示します。 **WMaxPacketSizefield**エンドポイントが送信または単一のトランザクションで受信するバイトの最大数を示します。 Bits 12..11 microframe ごとに送信できるトランザクションの合計数を示します。 **BInterval**エンドポイントを送信またはデータの受信頻度を示します。

## <a name="how-to-get-the-configuration-descriptor"></a>構成記述子を取得する方法


構成記述子は、標準のデバイス要求を使用してデバイスから取得されます (入手\_記述子)、USB ドライバー スタックによってコントロール転送として送信します。 USB クライアント ドライバーでは、次の方法のいずれかで、要求を開始できます。

- 呼び出して、フレームワークが提供最も簡単な方法は、デバイスは、1 つのみの構成をサポートする場合[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)メソッド。
- 複数の構成をサポートするデバイス、クライアント ドライバーでの記述子を取得する必要がある場合、1 つ目のドライバー以外の構成は、URB にする必要があります送信します。 ドライバーを割り当てる必要があります、URB を送信するには、書式設定、および、USB ドライバー スタックに URB を送信します。

  URB を割り当てるには、クライアント ドライバーを呼び出す必要があります、 [ **WdfUsbTargetDeviceCreateUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッド。 メソッドは、USB ドライバー スタックによって割り当てられた、URB へのポインターを受け取ります。

  URB、書式設定、クライアント ドライバーを使用して、 [ **UsbBuildGetDescriptorRequest** ](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))マクロ。 マクロは、記述子を取得する対象のデバイス定義の構成の数など、URB で必要なすべての情報を設定します。 URB に URB 関数が設定されている\_関数\_取得\_記述子\_FROM\_デバイス (を参照してください[  **\_URB\_コントロール\_記述子\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usb/ns-usb-_urb_control_descriptor_request))、記述子の型が usb\_構成\_記述子\_型。 URB に含まれる情報を使用すると、USB ドライバー スタックは標準のコントロール要求を作成し、デバイスに送信します。

  URB を送信するには、クライアント ドライバーは WDF 要求オブジェクトを使用する必要があります。 USB ドライバー スタックに要求オブジェクトを非同期的に送信するドライバーを呼び出す必要があります、 [ **WdfRequestSend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッド。 同期的に送信する呼び出し、 [ **WdfUsbTargetDeviceSendUrbSynchronously** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)メソッド。

  <strong>WDM ドライバー: * * A Windows Driver Model (WDM) クライアント ドライバーでは構成記述子を URB を送信することでのみ取得できます。URB を割り当てることで、ドライバーを呼び出す必要があります、 [ </strong>USBD\_UrbAllocate<strong> ](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)ルーチン。URB の書式を設定するドライバーを呼び出す必要があります、 [ </strong>UsbBuildGetDescriptorRequest * *](<https://msdn.microsoft.com/library/windows/hardware/ff538943>)マクロ。 URB を送信するには、ドライバーは IRP、URB を関連付けるし、USB ドライバー スタックに IRP を送信する必要があります。 詳細については、次を参照してください。 [、URB を送信する方法](send-requests-to-the-usb-driver-stack.md)します。

USB 構成では、変数はインターフェイスとその代替の設定の数です。 そのため、これは構成記述子を保持するために必要なバッファーのサイズを予測する困難です。 クライアント ドライバーでは、2 つの手順でそのすべての情報を収集する必要があります。 まず、どのようなサイズを決定バッファー構成記述子のすべてを保持し、全体の記述子を取得する要求を発行するために必要です。 クライアント ドライバーでは、次の方法のいずれかで、サイズを取得できます。

**を呼び出して WdfUsbTargetDeviceRetrieveConfigDescriptor 構成記述子を取得するには、次の手順を実行します。**

1.  呼び出すことによってすべての構成情報を保持するために必要なバッファーのサイズを取得[ **WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)します。 ドライバーは、バッファーおよびバッファーのサイズを保持する変数で NULL を渡す必要があります。
2.  以前から受信したサイズに基づくより大きなバッファーを割り当てる[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)呼び出します。
3.  呼び出す[ **WdfUsbTargetDeviceRetrieveConfigDescriptor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)もう一度手順 2 で割り当てられた新しいバッファーへのポインターを指定します。

```cpp
 NTSTATUS RetrieveDefaultConfigurationDescriptor (
    _In_  WDFUSBDEVICE  UsbDevice,
    _Out_ PUSB_CONFIGURATION_DESCRIPTOR *ConfigDescriptor 
    )
{
    NTSTATUS ntStatus = -1;

    USHORT sizeConfigDesc;

    PUSB_CONFIGURATION_DESCRIPTOR fullConfigDesc = NULL;

    PAGED_CODE();

    *ConfigDescriptor  = NULL;

    ntStatus = WdfUsbTargetDeviceRetrieveConfigDescriptor (
        UsbDevice, 
        NULL,
        &sizeConfigDesc);

    if (sizeConfigDesc == 0)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor size.");

        goto Exit;
    }
    else
    {
        fullConfigDesc = (PUSB_CONFIGURATION_DESCRIPTOR) ExAllocatePoolWithTag (
            NonPagedPool, 
            sizeConfigDesc,
            USBCLIENT_TAG);

        if (!fullConfigDesc)
        {
            ntStatus = STATUS_INSUFFICIENT_RESOURCES;
            goto Exit;
        }  
    }

    RtlZeroMemory (fullConfigDesc, sizeConfigDesc);

    ntStatus = WdfUsbTargetDeviceRetrieveConfigDescriptor (
        UsbDevice, 
        fullConfigDesc,
        &sizeConfigDesc);

    if (!NT_SUCCESS(ntStatus))
    {           
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor.");

        goto Exit;
    }

    *ConfigDescriptor = fullConfigDesc;

Exit:

    return ntStatus;   
}
```

**構成記述子を URB を送信することで取得するには、次の手順を実行します。**

1.  呼び出すことによって、URB を割り当て、 [ **WdfUsbTargetDeviceCreateUrb** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッド。
2.  呼び出すことによって、URB を書式設定、 [ **UsbBuildGetDescriptorRequest** ](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))マクロ。 URB の転送のバッファーが保持するために十分な大きさのバッファーを指す必要があります、 [ **USB\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_configuration_descriptor)構造体。
3.  WDF の要求オブジェクトとして呼び出すことによって、URB を送信[ **WdfRequestSend** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestsend)または[ **WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)します。
4.  要求が完了すると、確認、 **wTotalLength**のメンバー [ **USB\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_configuration_descriptor)します。 その値は、完全な構成記述子を格納するために必要なバッファーのサイズを示します。
5.  取得したサイズに基づいてより大きなバッファーを割り当てる**wTotalLength**します。
6.  大きなバッファーでは、同じ要求を発行します。

次の例のコードは、 [ **UsbBuildGetDescriptorRequest** ](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)) i 番目の構成の構成情報を取得する要求を呼び出します。

```cpp
NTSTATUS FX3_RetrieveConfigurationDescriptor (
    _In_ WDFUSBDEVICE  UsbDevice,
    _In_ PUCHAR ConfigurationIndex,
    _Out_ PUSB_CONFIGURATION_DESCRIPTOR *ConfigDescriptor 
    )
{
    NTSTATUS ntStatus = STATUS_SUCCESS;

    USB_CONFIGURATION_DESCRIPTOR configDesc;
    PUSB_CONFIGURATION_DESCRIPTOR fullConfigDesc = NULL;

    PURB urb = NULL;

    WDFMEMORY urbMemory = NULL;

    PAGED_CODE();

    RtlZeroMemory (&configDesc, sizeof(USB_CONFIGURATION_DESCRIPTOR));
    *ConfigDescriptor = NULL;

    // Allocate an URB for the get-descriptor request. 
    // WdfUsbTargetDeviceCreateUrb returns the address of the 
    // newly allocated URB and the WDFMemory object that 
    // contains the URB.

    ntStatus = WdfUsbTargetDeviceCreateUrb (
        UsbDevice,
        NULL,
        &urbMemory,
        &urb);

    if (!NT_SUCCESS (ntStatus))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not allocate URB for an open-streams request.");

        goto Exit;
    }

       // Format the URB.
    UsbBuildGetDescriptorRequest (
        urb,                                                        // Points to the URB to be formatted
        (USHORT) sizeof( struct _URB_CONTROL_DESCRIPTOR_REQUEST ),  // Size of the URB.
        USB_CONFIGURATION_DESCRIPTOR_TYPE,                          // Type of descriptor
        *ConfigurationIndex,                                        // Index of the configuration
        0,                                                          // Not used for configuration descriptors
        &configDesc,                                                // Points to a USB_CONFIGURATION_DESCRIPTOR structure
        NULL,                                                       // Not required because we are providing a buffer not MDL
        sizeof(USB_CONFIGURATION_DESCRIPTOR),                       // Size of the USB_CONFIGURATION_DESCRIPTOR structure.
        NULL                                                        // Reserved.
        );

       // Send the request synchronously.
    ntStatus = WdfUsbTargetDeviceSendUrbSynchronously (
        UsbDevice,
        NULL,
        NULL,
        urb);

    if (configDesc.wTotalLength == 0)
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor size.");

        ntStatus = USBD_STATUS_INAVLID_CONFIGURATION_DESCRIPTOR;

        goto Exit;
    }

    // Allocate memory based on the retrieved size. 
       // The allocated memory is released by the caller.
    fullConfigDesc = (PUSB_CONFIGURATION_DESCRIPTOR) ExAllocatePoolWithTag (
        NonPagedPool, 
        configDesc.wTotalLength,
        USBCLIENT_TAG);

    RtlZeroMemory (fullConfigDesc, configDesc.wTotalLength);

    if (!fullConfigDesc)
    {
        ntStatus = STATUS_INSUFFICIENT_RESOURCES;

        goto Exit;
    }

       // Format the URB.
    UsbBuildGetDescriptorRequest (
        urb,                                                        
        (USHORT) sizeof( struct _URB_CONTROL_DESCRIPTOR_REQUEST ),  
        USB_CONFIGURATION_DESCRIPTOR_TYPE,                          
        *ConfigurationIndex,                                         
        0,                                                          
        fullConfigDesc,                                                 
        NULL,                                                       
        configDesc.wTotalLength,                       
        NULL                                                        
        );

       // Send the request again.
    ntStatus = WdfUsbTargetDeviceSendUrbSynchronously (
        UsbDevice,
        NULL,
        NULL,
        urb);

    if ((fullConfigDesc->wTotalLength == 0) || !NT_SUCCESS (ntStatus))
    {
        TraceEvents(TRACE_LEVEL_ERROR, TRACE_DEVICE, 
            "%!FUNC! Could not retrieve the configuration descriptor.");

        ntStatus = USBD_STATUS_INAVLID_CONFIGURATION_DESCRIPTOR;

        goto Exit;
    }

       // Return to the caller.
    *ConfigDescriptor = fullConfigDesc;

Exit:

    if (urbMemory)
    {
        WdfObjectDelete (urbMemory);
    }

    return ntStatus;   
}
```

デバイスの構成記述子が戻るときは、インターフェイスの記述子のすべての代替設定と特定の代替設定内のすべてのエンドポイントのエンドポイント記述子要求バッファーが入力されます。 記載されているデバイスの[USB デバイス レイアウト](usb-device-layout.md)、次の図は、構成情報がメモリにレイアウトする方法を示します。

![構成記述子のレイアウトを示す図](images/usbconfig.png)

0 から始まる**bInterfaceNumber**のメンバー [ **USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbspec/ns-usbspec-_usb_interface_descriptor)インターフェイス、構成内で区別されます。 指定したインターフェイスでは、0 から始まる**bAlternateSetting**メンバーがインターフェイスの代替設定を区別します。 デバイスでは、インターフェイスの記述子を返しますの順序で**bInterfaceNumber**値と、次の順序で**bAlternateSetting**値。

クライアント ドライバーを呼び出すことができます、構成内で指定されたインターフェイスの記述子を検索する[ **USBD\_ParseConfigurationDescriptorEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)します。 呼び出しでは、クライアント ドライバーは、構成内の開始位置を提供します。 必要に応じて、ドライバーでは、インターフェイスの番号、代替の設定、クラス、サブクラスでは、またはプロトコルを指定できます。 ルーチンは、次の一致するインターフェイス記述子へのポインターを返します。

使用して、エンドポイント、または文字列記述子の構成記述子を確認する、 [ **USBD\_ParseDescriptors** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_parsedescriptors)ルーチン。 呼び出し元は、構成と USB など、記述子の種類内の開始位置\_文字列\_記述子\_型または USB\_エンドポイント\_記述子\_型。 ルーチンは、次の一致する記述子へのポインターを返します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB ディスクリプター](usb-descriptors.md)  



