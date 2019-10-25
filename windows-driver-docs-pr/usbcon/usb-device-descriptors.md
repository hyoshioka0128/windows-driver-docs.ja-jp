---
Description: デバイス記述子には、USB デバイス全体に関する情報が含まれています。 このトピックでは、USB_DEVICE_DESCRIPTOR 構造体について説明します。また、クライアントドライバーが get 記述子要求を送信してデバイス記述子を取得する方法についても説明します。
title: USB デバイス記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f6a01644f1b7890d3956d1623a6d70a320131b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844827"
---
# <a name="usb-device-descriptors"></a>USB デバイス記述子


デバイス記述子には、USB デバイス全体に関する情報が含まれています。 このトピックでは、 [**USB\_デバイスの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)構造について説明し、クライアントドライバーがデバイス記述子を取得するために get 記述子要求を送信する方法について説明します。

各 Universal Serial Bus (USB) デバイスは、デバイスに関する関連情報を含む単一のデバイス記述子を提供できる必要があります。 [**USB\_デバイスの\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)構造体は、デバイス記述子を記述します。 Windows では、その情報を使用して、さまざまな情報のセットを取得します。 たとえば、 **idvendor**フィールドと**idvendor**フィールドでは、それぞれベンダー id と製品識別子が指定されています。 Windows では、これらのフィールド値を使用して、デバイスの*ハードウェア ID*を作成します。 特定のデバイスのハードウェア ID を表示するには、**デバイスマネージャー**を開き、デバイスのプロパティを表示します。 **[詳細]** タブの **[ハードウェア id]** プロパティ値は、Windows によって生成されるハードウェア id ("USB\\*XXX*") を示します。 **Bcdusb**フィールドは、デバイスが準拠している USB 仕様のバージョンを示します。 たとえば、0x0200 は、デバイスが USB 2.0 仕様に従って設計されていることを示します。 **Bcddevice**値は、デバイス定義のリビジョン番号を示します。 USB ドライバースタックでは、デバイスのハードウェア Id と互換性 Id を生成するために、 **Idvendor**および**idvendor**と共に**bcddevice**が使用されます。 これらの識別子は**デバイスマネージャー**で確認できます。 デバイス記述子は、デバイスがサポートしている構成の合計数も示しています。

デバイスが高速容量で接続されている場合よりも高速な容量でホストコンピューターに接続されている場合、デバイスはデバイス記述子に異なる情報を報告することがあります。 デバイスでは、接続の有効期間中にデバイス記述子に含まれる情報を変更することはできません (電源状態の変更時を含む)。

ホストは制御転送を介してデバイス記述子を取得します。 転送では、要求の種類は GET 記述子で、受信者はデバイスです。 クライアントドライバーは、フレームワークの USB ターゲットデバイスオブジェクトを使用するか、要求情報との URB を送信することによって、この転送を開始できます。

-   [デバイス記述子の取得](#getting-the-device-descriptor)
-   [サンプルデバイス記述子](#sample-device-descriptor)

## <a name="getting-the-device-descriptor"></a>デバイス記述子の取得


Windows Driver framework (WDF) クライアントドライバーは、フレームワークの USB ターゲットデバイスオブジェクトが作成された後にのみ、デバイス記述子を取得できます。

KMDF ドライバーは、 [**WdfUsbTargetDeviceCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreate)を呼び出して、USB ターゲットデバイスオブジェクトへの WDFUSBDEVICE ハンドルを取得する必要があります。 通常、クライアントドライバーは、ドライバーの[*EvtdeviceWdfUsbTargetDeviceCreate ハードウェア*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック実装でを呼び出します。 その後、クライアントドライバーは[**WdfUsbTargetDeviceGetDeviceDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)メソッドを呼び出す必要があります。 呼び出しが完了すると、呼び出し元によって割り当てられた[**USB\_デバイス\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)構造でデバイス記述子が受信されます。

UMDF ドライバーは、 [**IWDFUsbTargetDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)ポインターのフレームワークデバイスオブジェクトに対してクエリを実行し、 [**IWDFUsbTargetDevice:: RetrieveDescriptor**](https://msdn.microsoft.com/library/windows/hardware/ff560362_retrievedescriptor)メソッドを呼び出して、次のように\_型の USB\_デバイス\_記述子を指定する必要があります。記述子の型。

ホストは、URB を送信することによってデバイス記述子を取得することもできます。 このメソッドは、カーネルモードドライバーにのみ適用されます。 ただし、ドライバーが Windows Driver Model (WDM) に基づいている場合を除き、クライアントドライバーはこの種類の要求に対して URB を送信する必要はありません。 このようなドライバーでは、 [**urb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb)構造を割り当ててから、 [**Usbbuildget記述子要求**](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))マクロを呼び出して、要求の urb の形式を指定する必要があります。 ドライバーは、USB ドライバースタックに URB を送信することによって、要求を送信できます。 詳細については、「 [URB を送信する方法](send-requests-to-the-usb-driver-stack.md)」を参照してください。

このコード例では、次のように、適切な URB を使用して、が指すバッファーをフォーマットする Usbbuildget記述子要求呼び出しを示します。

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

## <a name="sample-device-descriptor"></a>サンプルデバイス記述子


次の例では、USBView アプリケーションを使用して取得した USB web カメラデバイスのデバイス記述子 (「 [Usb デバイスレイアウト](usb-device-layout.md)」を参照) を示します。

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

前の例では、デバイスが USB 仕様バージョン2.0 に従って開発されていることがわかります。 **Bdeviceclass**、 **BDeviceSubClass**、および**bdeviceclass**の値に注意してください。 これらの値は、関数ごとに複数のインターフェイスをグループ化するために使用できる1つ以上の USB インターフェイスの関連付け記述子がデバイスに含まれていることを示します。 詳細については、「 [USB インターフェイスの関連付け記述子](usb-interface-association-descriptor.md)」を参照してください。

次に、 **bMaxPacketSize0**の値を確認します。 この値は、既定のエンドポイントの最大パケットサイズを示します。 このサンプルデバイスは、既定のエンドポイントを使用して最大64バイトのデータを転送できます。

通常、デバイスを構成するために、クライアントドライバーはデバイス記述子を取得した後に、デバイスでサポートされている構成に関する情報を取得します。 デバイスでサポートされる構成の数を確認するには、返された構造体の**Bnumconfigurations**メンバーを調べます。 このデバイスは、1つの構成をサポートします。 USB 構成に関する情報を取得するには、ドライバーが[Usb 構成記述子](usb-configuration-descriptors.md)を取得する必要があります。

## <a name="related-topics"></a>関連トピック
[USB 記述子](usb-descriptors.md)  
[USB 構成記述子](usb-configuration-descriptors.md)  



