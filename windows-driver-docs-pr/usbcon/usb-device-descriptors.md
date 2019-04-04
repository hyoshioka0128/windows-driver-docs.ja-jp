---
Description: The device descriptor contains information about a USB device as a whole. This topic describes the USB_DEVICE_DESCRIPTOR structure and includes information about how a client driver can send a get-descriptor request to obtain the device descriptor.
title: USB デバイス記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cc586d3575f648784d45b99544e029d0d3af7c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579194"
---
# <a name="usb-device-descriptors"></a>USB デバイス記述子


デバイス記述子には、全体として、USB デバイスに関する情報が含まれています。 このトピックで説明します、 [ **USB\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539280)構造体であり、クライアント ドライバーがデバイスを取得する get 記述子の要求を送信する方法に関する情報が含まれています記述子。

すべてのユニバーサル シリアル バス (USB) デバイスは、デバイスに関連する情報を含む 1 つのデバイス記述子を提供できる必要があります。 [ **USB\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539280)構造体には、デバイスの記述子がについて説明します。 Windows では、その情報を使用して、情報のさまざまなセットを派生させます。 たとえば、 **idVendor**と**idProduct**フィールドはベンダーと製品の id をそれぞれ指定します。 Windows では、これらのフィールド値を使用して、作成、*ハードウェア ID*デバイス。 特定のデバイスのハードウェア ID を表示するには、開く**デバイス マネージャー**とデバイスのプロパティを表示します。 **詳細** タブで、**ハードウェア Id**プロパティの値をハードウェア ID を示します ("USB\\*XXX*") Windows によって生成されます。 **BcdUSB**フィールドは、デバイスが準拠する USB 仕様のバージョンを示します。 たとえば、0x0200 では、デバイスが USB 2.0 仕様どおりに設計されていることを示します。 **BcdDevice**値がデバイス定義のリビジョン番号を示します。 USB ドライバー スタックを使用して**bcdDevice**、と共に**idVendor**と**idProduct**ハードウェアとデバイスの互換性 Id を生成します。 これらを表示することで識別子**デバイス マネージャー**。 デバイス記述子では、デバイスがサポートする構成の総数も示します。

容量は最高速度で接続したときよりも高速容量でホスト コンピューターに、デバイスが接続されているときに、デバイスはそのデバイス記述子でさまざまな情報をレポート可能性があります。 デバイスでは、電源の状態の変更時など、接続の有効期間中にデバイス記述子に含まれる情報は変更しないでください。

ホストは、コントロール転送を介してデバイス記述子を取得します。 転送の要求の種類は記述子を取得、宛先は、デバイスです。 クライアント ドライバーは、2 つの方法のいずれかでその転送を開始できます: framework USB ターゲット デバイス オブジェクトを使用して、または、URB 要求情報を送信することです。

-   [デバイス記述子を取得します。](#getting--the-device-descriptor)
-   [サンプル デバイス記述子](#sample-device-descriptor)

## <a name="getting-the-device-descriptor"></a>デバイス記述子を取得します。


Windows Driver Frameworks (WDF) のクライアント ドライバーは、framework USB ターゲット デバイス オブジェクトが作成された後にのみデバイス記述子を取得できます。

KMDF ドライバーは、呼び出すことで、USB ターゲット デバイス オブジェクト WDFUSBDEVICE ハンドルを取得する必要があります[ **WdfUsbTargetDeviceCreate**](https://msdn.microsoft.com/library/windows/hardware/ff550077)します。 通常、クライアント ドライバーを呼び出す**WdfUsbTargetDeviceCreate**ドライバーの[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック実装します。 その後、クライアント ドライバーを呼び出す必要があります、 [ **WdfUsbTargetDeviceGetDeviceDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/ff550090)メソッド。 デバイス記述子が呼び出し元が割り当てたで受信した後、呼び出しが完了したら、 [ **USB\_デバイス\_記述子**](https://msdn.microsoft.com/library/windows/hardware/ff539280)構造体。

UMDF ドライバーの framework デバイス オブジェクトをクエリする必要があります、 [ **IWDFUsbTargetDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff560362)ポインターと、呼び出し、 [ **IWDFUsbTargetDevice::RetrieveDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff560362_retrievedescriptor)メソッド USB を指定して\_デバイス\_記述子\_記述子の型と型。

ホストは、URB を送信することによってもデバイス記述子を取得できます。 このメソッドは、カーネル モード ドライバーにのみ適用されます。 ただし、クライアント ドライバーはドライバーが Windows Driver Model (WDM) に基づいていない限り、URB この種類の要求を送信することが必要です。 このようなドライバーを割り当てる必要があります、 [ **URB** ](https://msdn.microsoft.com/library/windows/hardware/ff538923)構造体を呼び出して、 [ **UsbBuildGetDescriptorRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff538943)マクロの形式を指定します要求の URB します。 ドライバーは、USB ドライバー スタックに URB を送信することで、要求を送信できます。 詳細については、[、URB を送信する方法](send-requests-to-the-usb-driver-stack.md)を参照してください。

このコード例では、適切な URB で pURB によって指し示されるバッファーの形式を UsbBuildGetDescriptorRequest 呼び出しを示します。

```cpp
UsbBuildGetDescriptorRequest(
    pURB,                                                 // Points to the URB to be formatted
    sizeof(struct _URB_CONTROL_DESCRIPTOR_REQUEST),
    USB_DEVICE_DESCRIPTOR_TYPE,
    0,                                                    // Not used for device descriptors
    0,                                                    // Not used for device descriptors
    pDescriptor,                                          // Points to a USB_DEVICE_DESCRIPTOR structure
    NULL,
    sizeof(USB_DEVICE_DESCRIPTOR),
    NULL
);
```

## <a name="sample-device-descriptor"></a>サンプル デバイス記述子


この例は、USB web カメラ デバイスのデバイス記述子 (を参照してください[USB デバイス レイアウト](usb-device-layout.md)) USBView アプリケーションを使用して取得される。

``` syntax
Device Descriptor:
bcdUSB:             0x0200
bDeviceClass:         0xEF
bDeviceSubClass:      0x02
bDeviceProtocol:      0x01
bMaxPacketSize0:      0x40 (64)
idVendor:           0x045E (Microsoft Corporation)
idProduct:          0x0728
bcdDevice:          0x0100
iManufacturer:        0x01
0x0409: "Microsoft"
iProduct:             0x02
0x0409: "Microsoft LifeCam VX-5000"
0x0409: "Microsoft LifeCam VX-5000"
iSerialNumber:        0x00
bNumConfigurations:   0x01
```

前の例では、デバイスは、USB 仕様、バージョン 2.0 に従って開発されて表示されます。 注、 **bDeviceClass**、 **bDeviceSubClass**、および**bDeviceProtocol**値。 これらの値は、1 つまたは複数の USB インターフェイスの関連付け記述子関数ごとの複数のインターフェイスをグループ化に使用できますが、デバイスに含まれているを示します。 詳細については、[USB インターフェイスの関連付けの記述子](usb-interface-association-descriptor.md)を参照してください。

値を次に、確認**bMaxPacketSize0**します。 この値は、既定のエンドポイントの最大パケット サイズを示します。 このサンプルのデバイスは、その既定のエンドポイントを使用してデータを 64 バイトまでに転送できます。

通常でデバイスを構成するクライアント ドライバーに関する情報を取得でサポートされる構成、デバイスでデバイス記述子を取得した後にします。 デバイスでサポートされる構成の数を確認するのには、検査、 **bNumConfigurations**返される構造体のメンバー。 このデバイスは、1 つの構成をサポートします。 USB の構成に関する情報を取得するには、ドライバーを取得する必要があります[USB 構成記述子](usb-configuration-descriptors.md)します。

## <a name="related-topics"></a>関連トピック
[USB ディスクリプター](usb-descriptors.md)  
[USB 構成記述子](usb-configuration-descriptors.md)  



