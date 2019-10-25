---
Description: USB デバイスは、それ自体に関する情報を USB 記述子と呼ばれるデータ構造に提供します。 このセクションでは、デバイス、構成、インターフェイス、エンドポイント記述子、およびそれらを USB デバイスから取得する方法について説明します。
title: 標準の USB 記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b951b8f4ad092e35627b6bb983a47b3f72e6ccd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824168"
---
# <a name="standard-usb-descriptors"></a>標準の USB 記述子


**要約**

-   USB 記述子の種類
-   USB 取得記述子用の Microsoft 提供のプログラミングインターフェイス

**重要な API**

-   このトピックに記載されている参照テーブルを参照してください。

USB デバイスは、それ自体に関する情報を*usb 記述子*と呼ばれるデータ構造に提供します。 このセクションでは、デバイス、構成、インターフェイス、エンドポイント記述子、およびそれらを USB デバイスから取得する方法について説明します。

## <a name="usb-descriptors-mapped-to-device-layout"></a>デバイスレイアウトにマップされた USB 記述子


ホストソフトウェアは、さまざまな標準コントロール要求を既定のエンドポイントに送信することによって、接続されているデバイスから記述子を取得します (Get Descriptor requests、「USB specification」セクション9.4.3 を参照してください)。 これらの要求は、取得する記述子の種類を指定します。 デバイスは、このような要求に応答して、デバイス、その構成、インターフェイス、および関連するエンドポイントに関する情報を含む記述子を送信します。 デバイス*記述子*には、デバイス全体に関する情報が含まれています。 *構成記述子*には、各デバイスの構成に関する情報が含まれています。 *文字列記述子*には Unicode テキスト文字列が含まれます。

すべての USB デバイスは、デバイスのクラス情報、ベンダーと製品の識別子、および構成の数を示すデバイス記述子を公開します。 各構成は、インターフェイスの数と電源特性を示す構成記述子を公開します。 各インターフェイスは、クラスとエンドポイントの数に関する情報を含むそれぞれの代替設定のインターフェイス記述子を公開します。 各インターフェイス内の各エンドポイントは、エンドポイントの種類と最大パケットサイズを示すエンドポイント記述子を公開します。

たとえば、OSR FX2 ボードデバイスのレイアウトについて考えてみましょう (「USB デバイスのレイアウト」を参照してください)。 デバイスレベルでは、デバイスは既定のエンドポイントのデバイス記述子とエンドポイント記述子を公開します。 構成レベルでは、デバイスは構成0の構成記述子を公開します。 インターフェイスレベルでは、別の設定0に対して1つのインターフェイス記述子を公開します。 エンドポイントレベルでは、3つのエンドポイント記述子が公開されます。

![usb デバイス記述子のレイアウト](images/device-descriptors.png)

## <a name="usb-device-descriptor"></a>USB デバイス記述子


各 Universal Serial Bus (USB) デバイスは、デバイスに関する関連情報を含む単一のデバイス記述子を提供できる必要があります。 Windows では、その情報を使用して、さまざまな情報のセットを取得します。 たとえば、 **idvendor**フィールドと**idvendor**フィールドでは、それぞれベンダー id と製品識別子が指定されています。 Windows では、これらのフィールド値を使用して、デバイスのハードウェア ID を作成します。 特定のデバイスのハードウェア ID を表示するには、デバイスマネージャーを開き、デバイスのプロパティを表示します。 **[詳細]** タブの **[ハードウェア id]** プロパティ値は、Windows によって生成されるハードウェア id ("USB\\XXX") を示します。 **Bcdusb**フィールドは、デバイスが準拠している USB 仕様のバージョンを示します。 たとえば、0x0200 は、デバイスが USB 2.0 仕様に従って設計されていることを示します。 **Bcddevice**値は、デバイス定義のリビジョン番号を示します。 USB ドライバースタックでは、デバイスのハードウェア Id と互換性 Id を生成するために、 **Idvendor**および**idvendor**と共に**bcddevice**が使用されます。 これらの識別子はデバイスマネージャーで確認できます。 デバイス記述子は、デバイスがサポートしている構成の合計数も示しています。

ホストは制御転送を介してデバイス記述子を取得します。 Microsoft では、記述子を取得するためのプログラミングインターフェイスを提供しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成している...</th>
<th>呼び出し...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows. Devices. Usb</strong>を使用する UWP アプリ</a></td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice. DeviceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">Winusb 機能</a>を使用する Win32 デスクトップアプリ</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>Usbbuildget記述子要求</strong></a>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_descriptor_request)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-configuration-descriptor"></a>USB 構成記述子


USB 構成には、一連のインターフェイスが含まれています。 各インターフェイスは、1つまたは複数の代替設定で構成され、各代替設定は一連のエンドポイントで構成されます (「USB デバイスレイアウト」を参照してください)。 構成記述子は、そのインターフェイス、代替設定、およびエンドポイントを含む構成全体を示します。 これらの各エンティティは、記述子の形式でも記述されています。 構成記述子には、デバイスの製造元によって定義されたカスタム記述子を含めることもできます。

そのため、構成記述子の最初の部分のみが固定されています (9 バイト)。 残りの部分は、インターフェイスの数とその代替設定、およびデバイスでサポートされているエンドポイントによって異なります。 このドキュメントセットでは、最初の9バイトを構成記述子と呼びます。 記述子の最初の2バイトは、合計の長さを示します。

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

**Bconfigurationvalue**フィールドは、デバイスのファームウェアで定義されている構成の番号を示します。 USB 構成では、特定の電源特性も示されます。 **Bmattributes**には、構成でリモートウェイクアップ機能がサポートされているかどうか、およびデバイスの電源が入っているかどうかを示すビットマスクが含まれています。 **Maxpower**フィールドは、デバイスのバス電源がオンになっている場合に、デバイスがホストから描画できる最大電力 (milliamp ユニット単位) を指定します。 構成記述子は、デバイスがサポートするインターフェイスの合計数 (**Bnuminterfaces**) も示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成している...</th>
<th>呼び出し...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows. Devices. Usb</strong>を使用する UWP アプリ</a></td>
<td><p>固定長の部分を取得するには、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.ConfigurationDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfigurationDescriptor)"><strong>Usbdevice. ConfigurationDescriptor</strong></a> 。</p>
<p>構成セット全体を取得するための、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>Usbconfiguration。</strong></a></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">Winusb 機能</a>を使用する Win32 デスクトップアプリ</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアントドライバー</td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>Usbbuildget記述子要求</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-interface-descriptor"></a>USB インターフェイス記述子


インターフェイス記述子には、USB インターフェイスの別の設定に関する情報が含まれています。

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

前の例では、 **bInterfaceNumber**と**balternatesetting**のフィールド値に注意してください。 これらのフィールドには、ホストがインターフェイスをアクティブ化するために使用するインデックス値と、その代替設定の1つが含まれます。 アクティベーションでは、アプリケーションまたはドライバーによって関数呼び出しのインデックス値が指定されます。 その情報に基づいて、USB ドライバースタックは標準の制御要求 (インターフェイスの設定) を作成し、デバイスに送信します。 **BInterfaceClass**フィールドに注意してください。 インターフェイス記述子、またはその代替設定の記述子は、クラスコード、サブクラス、およびプロトコルを指定します。 0x0E の値は、インターフェイスが video device クラス用であることを示します。 また、 **Iinterface**フィールドにも注目してください。 この値は、インターフェイス記述子に2つの文字列記述子が追加されていることを示します。 文字列記述子には、機能を識別するためにデバイスの列挙時に使用される Unicode の説明が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成している...</th>
<th>呼び出し...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows. Devices. Usb</strong>を使用する UWP アプリ</a></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)"><strong>Usbinterfacesetting。</strong></a>特定の代替設定の記述子を取得するための記述子です。</p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)"><strong>Usbinterface 記述子</strong></a>は、インターフェイスのすべての設定の記述子を取得します。</p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">Winusb 機能</a>を使用する Win32 デスクトップアプリ</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-getinterfacedescriptor)"><strong>IWDFUsbInterface:: GetInterfaceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfacegetdescriptor)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアントドライバー</td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>Usbbuildget記述子要求</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a>してから、インターフェイス記述子ごとに解析します。 詳細については、「 <a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-endpoint-descriptor"></a>USB エンドポイント記述子


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

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成している...</th>
<th>呼び出し...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)"> <strong>Windows. Devices. Usb</strong>を使用する UWP アプリ</a></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)"><strong>UsbEndpointDescriptor</strong></a></p></td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb" data-raw-source="[WinUSB Functions](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)">Winusb 機能</a>を使用する Win32 デスクトップアプリ</td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation" data-raw-source="[&lt;strong&gt;WDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetpipe-getinformation)"><strong>WDFUsbTargetPipe:: GetInformation</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアントドライバー</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipegetinformation)"><strong>WdfUsbTargetPipeGetInformation</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアントドライバー</td>
<td><p><a href="https://docs.microsoft.com/previous-versions/ff538943(v=vs.85)" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff538943(v=vs.85))"><strong>Usbbuildget記述子要求</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usb/ns-usb-_urb_control_get_configuration_request)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a>を使用して、エンドポイント記述子ごとに解析します。 詳細については、「 <a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[すべての USB 開発者向けの概念](usb-concepts-for-all-developers.md)  



