---
Description: USB デバイスは、USB 構成と呼ばれる一連のインターフェイスの形式で機能を公開します。
title: USB 構成記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da2735614412e3d10e90db80afdaf986f26792c0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844831"
---
# <a name="usb-configuration-descriptors"></a>USB 構成記述子


USB デバイスは、USB 構成と呼ばれる一連のインターフェイスの形式で機能を公開します。 各インターフェイスは、1つまたは複数の代替設定で構成され、各代替設定は一連のエンドポイントで構成されます。 このトピックでは、USB 構成に関連付けられているさまざまな記述子について説明します。

USB 構成は、構成記述子に記述されています (「 [**usb\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)の構造」を参照してください)。 構成記述子には、構成とそのインターフェイス、代替設定、およびエンドポイントに関する情報が含まれています。 各インターフェイス記述子または代替設定は、 [**USB\_インターフェイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)構造体で記述されています。 構成では、インターフェイスと代替設定のすべてのエンドポイント記述子によって、各インターフェイス記述子がメモリ内に続きます。 各エンドポイント記述子は、 [**USB\_エンドポイント\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_endpoint_descriptor)構造体に格納されます。

たとえば、「 [Usb デバイスレイアウト](usb-device-layout.md)」で説明されている usb webcam デバイスを考えてみます。 デバイスは2つのインターフェイスを持つ構成をサポートし、1つ目のインターフェイス (インデックス 0) は2つの代替設定をサポートします。

次の例は、USB web カメラデバイスの構成記述子を示しています。

``` syntax
Configuration Descriptor:
wTotalLength:         0x02CA
bNumInterfaces:       0x02
bConfigurationValue:  0x01
iConfiguration:       0x00
bmAttributes:         0x80 (Bus Powered )
MaxPower:             0xFA (500 mA)
```

**Bconfigurationvalue**フィールドは、デバイスのファームウェアで定義されている構成の番号を示します。 クライアントドライバーは、その数値を使用してアクティブな構成を選択します。 [Usb デバイスの構成](configuring-usb-devices.md)の詳細については、「 [Usb デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)」を参照してください。 USB 構成では、特定の電源特性も示されます。 **Bmattributes**には、構成でリモートウェイクアップ機能がサポートされているかどうか、およびデバイスの電源が入っているかどうかを示すビットマスクが含まれています。 **Maxpower**フィールドは、デバイスのバス電源がオンになっている場合に、デバイスがホストから描画できる最大電力 (milliamp ユニット単位) を指定します。 構成記述子は、デバイスがサポートするインターフェイスの合計数 (**Bnuminterfaces**) も示します。

次の例は、web カメラデバイスのインターフェイス0の代替設定0のインターフェイス記述子を示しています。

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

前の例では、 **bInterfaceNumber**と**balternatesetting**のフィールド値に注意してください。 これらのフィールドには、クライアントドライバーがインターフェイスおよびその代替設定の1つをアクティブ化するために使用するインデックス値が含まれています。 アクティベーションの場合、ドライバーは、USB ドライバースタックに選択インターフェイス要求を送信します。 次に、ドライバースタックは標準の制御要求 (インターフェイスの設定) を作成し、デバイスに送信します。 **BInterfaceClass**フィールドに注意してください。 インターフェイス記述子、またはその代替設定の記述子は、クラスコード、サブクラス、およびプロトコルを指定します。 0x0E の値は、インターフェイスが video device クラス用であることを示します。 また、 **Iinterface**フィールドにも注目してください。 この値は、インターフェイス記述子に2つの文字列記述子が追加されていることを示します。 文字列記述子には、機能を識別するためにデバイスの列挙時に使用される Unicode の説明が含まれています。 文字列記述子の詳細については、「 [USB 文字列記述子](usb-string-descriptors.md)」を参照してください。

インターフェイス内の各エンドポイントは、デバイスの入力または出力の1つのストリームを記述します。 さまざまな種類の関数のストリームをサポートするデバイスには、複数のインターフェイスがあります。 1つの関数に関連する複数のストリームをサポートするデバイスでは、単一のインターフェイスで複数のエンドポイントをサポートできます。

すべての種類のエンドポイント (既定のエンドポイントを除く) は、エンドポイント記述子を提供する必要があります。これにより、ホストはエンドポイントに関する情報を取得できます。 エンドポイント記述子には、アドレス、型、方向、エンドポイントが処理できるデータの量などの情報が含まれます。 エンドポイントへのデータ転送は、その情報に基づいています。

次の例は、web カメラデバイスのエンドポイント記述子を示しています。

``` syntax
Endpoint Descriptor:
bEndpointAddress:   0x82  IN
bmAttributes:       0x01
wMaxPacketSize:     0x0080 (128)
bInterval:          0x01
```

**Bendpointaddress**フィールドは、エンドポイント番号 (ビット 3.. 0) とエンドポイントの方向 (ビット 7) を含む一意のエンドポイントアドレスを指定します。 前の例でこれらの値を読み取ることで、エンドポイント番号が2のエンドポイントが記述子によって記述されていることを確認できます。 **Bmattributes**属性は、エンドポイントの種類がアイソクロナスであることを示します。 **Wmaxpacketsizefield**は、エンドポイントが1つのトランザクションで送信または受信できる最大バイト数を示します。 ビット 12.. 11 は、マイクロフレームごとに送信できるトランザクションの合計数を示します。 **Binterval**は、エンドポイントがデータを送受信できる頻度を示します。

## <a name="how-to-get-the-configuration-descriptor"></a>構成記述子を取得する方法


構成記述子は、デバイスから標準のデバイス要求 (GET\_DESCRIPTOR) を介して取得されます。この要求は、USB ドライバースタックによる制御転送として送信されます。 USB クライアントドライバーは、次のいずれかの方法で要求を開始できます。

- デバイスが1つの構成のみをサポートしている場合、最も簡単な方法は、フレームワークに用意されている[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)メソッドを呼び出すことです。
- 複数の構成をサポートするデバイスでは、クライアントドライバーが1つ目以外の構成の記述子を取得する場合、ドライバーは URB を送信する必要があります。 URB を送信するには、ドライバーは、USB ドライバースタックに割り当て、フォーマットし、URB を送信する必要があります。

  URB を割り当てるには、クライアントドライバーで[**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッドを呼び出す必要があります。 メソッドは、USB ドライバースタックによって割り当てられた URB へのポインターを受け取ります。

  URB をフォーマットするために、クライアントドライバーは[**Usbbuildget記述子要求**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))マクロを使用できます。 マクロは、記述子を取得するデバイス定義の構成番号など、URB に必要なすべての情報を設定します。 URB 関数は、\_デバイスから\_記述子\_を取得する\_\_関数に設定されています (「 [ **\_URB\_CONTROL\_DESCRIPTOR\_REQUEST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)」を参照してください)。記述子の種類は USB に設定されてい\_構成\_記述子\_型。 URB に含まれている情報を使用して、USB ドライバースタックは標準の制御要求を作成し、デバイスに送信します。

  URB を送信するには、クライアントドライバーで WDF request オブジェクトを使用する必要があります。 要求オブジェクトを USB ドライバースタックに非同期的に送信するには、ドライバーが[**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)メソッドを呼び出す必要があります。 同期的に送信するには、 [**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)メソッドを呼び出します。

  <strong>Wdm ドライバー: * * Windows Driver Model (wdm) クライアントドライバーは、URB を送信することによってのみ構成記述子を取得できます。URB を割り当てるには、ドライバーは[ </strong>USBD\_Urを検索<strong>](<https://msdn.microsoft.com/library/windows/hardware/hh406250>)するルーチンを呼び出す必要があります。URB をフォーマットする[</strong>には、ドライバーが usbbuildget記述子 request * * マクロを呼び出す必要があり](<https://msdn.microsoft.com/library/windows/hardware/ff538943>)ます。 URB を送信するには、ドライバーが URB を IRP に関連付け、IRP を USB ドライバースタックに送信する必要があります。 詳細については、「 [URB を送信する方法](send-requests-to-the-usb-driver-stack.md)」を参照してください。

USB 構成では、インターフェイスの数とその代替設定は変数です。 そのため、構成記述子を保持するために必要なバッファーのサイズを予測することは困難です。 クライアントドライバーは、次の2つの手順ですべての情報を収集する必要があります。 最初に、すべての構成記述子を保持するために必要なサイズバッファーを決定し、記述子全体を取得する要求を発行します。 クライアントドライバーは、次のいずれかの方法でサイズを取得できます。

**WdfUsbTargetDeviceRetrieveConfigDescriptor を呼び出して構成記述子を取得するには、次の手順を実行します。**

1.  [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)を呼び出すことによって、すべての構成情報を保持するために必要なバッファーのサイズを取得します。 ドライバーは、バッファーに NULL を渡す必要があり、バッファーのサイズを保持する変数が必要です。
2.  前の[**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)呼び出しで受信したサイズに基づいて、より大きなバッファーを割り当てます。
3.  [**WdfUsbTargetDeviceRetrieveConfigDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)をもう一度呼び出し、手順 2. で割り当てた新しいバッファーへのポインターを指定します。

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

**URB を送信することによって構成記述子を取得するには、次の手順を実行します。**

1.  [**WdfUsbTargetDeviceCreateUrb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)メソッドを呼び出して、URB を割り当てます。
2.  [**Usbbuildget記述子 request**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))マクロを呼び出して、URB をフォーマットします。 URB の転送バッファーは、 [**USB\_構成\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)構造を保持するのに十分な大きさのバッファーを指している必要があります。
3.  [**Wdfrequestsend**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestsend)または[**WdfUsbTargetDeviceSendUrbSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendurbsynchronously)を呼び出して、WDF request オブジェクトとして URB を送信します。
4.  要求が完了したら、 [**USB\_CONFIGURATION\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor)の**wTotalLength**メンバーを確認します。 この値は、完全な構成記述子を格納するために必要なバッファーのサイズを示します。
5.  **WTotalLength**で取得したサイズに基づいて、より大きなバッファーを割り当てます。
6.  大きなバッファーで同じ要求を発行します。

次のコード例は、i 番目の構成の構成情報を取得する要求に対する[**Usbbuildget記述子要求**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))呼び出しを示しています。

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

デバイスが構成記述子を返すと、要求バッファーには、すべての代替設定のインターフェイス記述子と、特定の代替設定内のすべてのエンドポイントのエンドポイント記述子が格納されます。 「 [USB デバイスレイアウト](usb-device-layout.md)」で説明されているデバイスの場合、次の図は、構成情報をメモリにレイアウトする方法を示しています。

![構成記述子のレイアウトを示す図](images/usbconfig.png)

[**USB\_INTERFACE\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_interface_descriptor)の0から始まる**bInterfaceNumber**メンバーは、構成内のインターフェイスを区別します。 特定のインターフェイスについて、0から始まる**Balternatesetting**メンバーは、インターフェイスの代替設定を区別します。 デバイスは、 **bInterfaceNumber**値の順にインターフェイス記述子を返し、 **balternatesetting**値の順序で返します。

構成内で特定のインターフェイス記述子を検索するために、クライアントドライバーは[**USBD\_ParseConfigurationDescriptorEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parseconfigurationdescriptorex)を呼び出すことができます。 この呼び出しでは、クライアントドライバーは構成内の開始位置を提供します。 必要に応じて、ドライバーはインターフェイス番号、代替設定、クラス、サブクラス、またはプロトコルを指定できます。 ルーチンは、次に一致するインターフェイス記述子へのポインターを返します。

エンドポイントまたは文字列記述子の構成記述子を調べるには、 [**USBD\_parsedescriptors**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_parsedescriptors)ルーチンを使用します。 呼び出し元は、構成内の開始位置と記述子の種類を提供します。たとえば、USB\_文字列\_記述子\_TYPE または USB\_エンドポイント\_記述子\_型です。 ルーチンは、次に一致する記述子へのポインターを返します。

## <a name="related-topics"></a>関連トピック
[USB デバイスの構成を選択する方法](how-to-select-a-configuration-for-a-usb-device.md)  
[USB 記述子](usb-descriptors.md)  



