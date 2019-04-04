---
Description: A USB device provides information about itself in data structures called USB descriptors. This section provides information about device, configuration, interface, and endpoint descriptors and ways to retrieve them from a USB device.
title: 標準の USB ディスクリプター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d72b445cd88a078b261dfcdee731338b8e332bcc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548670"
---
# <a name="standard-usb-descriptors"></a>標準の USB ディスクリプター


**要約**

-   USB の記述子の種類
-   記述子を取得する USB の Microsoft が提供するプログラミング インターフェイス

**重要な API**

-   このトピックに含まれる参照テーブルを参照してください。

USB デバイスと呼ばれるデータ構造自体に関する情報を提供する*の USB ディスクリプター*します。 このセクションでは、デバイス、構成、インターフェイス、およびエンドポイント記述子および USB デバイスから取得する方法についての情報を提供します。

## <a name="usb-descriptors-mapped-to-device-layout"></a>デバイスのレイアウトにマップされている USB ディスクリプター


ホスト ソフトウェアは、既定のエンドポイント (記述子の Get 要求を参照してください USB 仕様のセクション 9.4.3) にさまざまな標準のコントロール要求を送信することによって接続されたデバイスからの記述子を取得します。 これらの要求を取得する記述子の種類を指定します。 このような要求に応答して、デバイスは、デバイス、その構成、インターフェイスと、関連するエンドポイントについての情報を含む記述子を送信します。 *デバイス記述子*全体のデバイスに関する情報が含まれます。 *構成記述子*各デバイスの構成に関する情報が含まれます。 *記述子文字列*Unicode テキスト文字列が含まれます。

すべての USB デバイスは、クラスについては、デバイスのベンダーと製品の id、および構成の数を示すデバイス記述子を公開します。 各構成は、it の構成記述子インターフェイスと電源の特徴の数を示すを公開します。 各インターフェイスでは、各クラスとエンドポイントの数に関する情報を含む別の設定、インターフェイスの記述子を公開します。 各インターフェイス内の各エンドポイントは、エンドポイントの種類とパケットの最大サイズを示すエンドポイント記述子を公開します。

たとえば、OSR FX2 ボード デバイスのレイアウトを考えてみましょう (USB デバイスのレイアウトを参照してください)。 デバイス レベルでは、デバイスはデバイス記述子と既定のエンドポイントのエンドポイント記述子を公開します。 構成レベルでは、デバイスは、0 の構成の構成記述子を公開します。 インターフェイス レベルでの代替設定 0 インターフェイスの 1 つの記述子を公開します。 エンドポイント レベルでは、次の 3 つのエンドポイント記述子が公開されます。

![usb デバイス記述子のレイアウト](images/device-descriptors.png)

## <a name="usb-device-descriptor"></a>USB デバイス記述子


すべてのユニバーサル シリアル バス (USB) デバイスは、デバイスに関連する情報を含む 1 つのデバイス記述子を提供できる必要があります。 Windows では、その情報を使用して、情報のさまざまなセットを派生させます。 たとえば、 **idVendor**と**idProduct**フィールドはベンダーと製品の id をそれぞれ指定します。 Windows では、これらのフィールド値を使用して、デバイスのハードウェア ID を作成します。 特定のデバイスのハードウェア ID を表示するには、デバイス マネージャー デバイスのプロパティを開きます。 **詳細** タブで、**ハードウェア Id**プロパティの値をハードウェア ID を示します ("USB\\XXX") Windows によって生成されます。 **BcdUSB**フィールドは、デバイスが準拠する USB 仕様のバージョンを示します。 たとえば、0x0200 では、デバイスが USB 2.0 仕様どおりに設計されていることを示します。 **BcdDevice**値がデバイス定義のリビジョン番号を示します。 USB ドライバー スタックを使用して**bcdDevice**、と共に**idVendor**と**idProduct**ハードウェアとデバイスの互換性 Id を生成します。 これらを表示するデバイス マネージャーでの識別子。 デバイス記述子では、デバイスがサポートする構成の総数も示します。

ホストは、コントロール転送を介してデバイス記述子を取得します。 Microsoft では、記述子を取得するプログラミング インターフェイスを提供します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成する場合、.</th>
<th>呼び出す.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用する UWP アプリ<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><a href="https://msdn.microsoft.com/library/windows/apps/dn264002" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264002)"><strong>UsbDevice.DeviceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>Win32 デスクトップ アプリを使用する<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 関数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550090" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550090)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540357" data-raw-source="[&lt;strong&gt;_URB_CONTROL_DESCRIPTOR_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540357)"><strong>_URB_CONTROL_DESCRIPTOR_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-configuration-descriptor"></a>USB 構成記述子


USB の構成には、一連インターフェイスにはが含まれています。 各インターフェイスは 1 つまたは複数の代替設定と、各代替の設定で構成された一連のエンドポイント (USB デバイスのレイアウトを参照してください)。 構成記述子は、構成全体を説明します。 そのインターフェイス、代替の設定とそのエンドポイントが含まれます。 各エンティティは、記述子の形式でも説明します。 構成記述子では、デバイスの製造元によって定義されているカスタムの記述子を含めることもできます。

そのため、構成記述子の最初の部分のみが固定されて 9 バイト。 残りの部分は、インターフェイスと、代替の設定と、デバイスでサポートされているエンドポイントの数に応じて変数です。 このドキュメント セットでは、最初の 9 バイトを構成記述子と呼びます。 記述子の最初の 2 バイトでは、長さの合計を示します。

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

**BConfigurationValue**フィールドは、デバイスのファームウェアで定義されている構成の数を示します。 USB の構成には、特定の電源の特性も示されます。 **BmAttributes**構成がリモートのウェイク アップ機能をサポートするかどうかと、デバイスは、バス供給または自己供給型かどうかを示すビットマスクが含まれています。 **MaxPower**フィールドをデバイスは、バス供給ときに、ホストからデバイスを描画できる最大電力 (milliamp 単位) を指定します。 構成記述子では、インターフェイスの合計数も示されます (**bNumInterfaces**) デバイスをサポートします。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成する場合、.</th>
<th>呼び出す.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用する UWP アプリ<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn297689" data-raw-source="[&lt;strong&gt;UsbDevice.ConfigurationDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297689)"><strong>UsbDevice.ConfigurationDescriptor</strong> </a>を固定長の部分を取得します。</p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn263802" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263802)"><strong>UsbConfiguration.Descriptors</strong> </a>全体の構成セットを取得します。</p></td>
</tr>
<tr class="even">
<td>Win32 デスクトップ アプリを使用する<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 関数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550098" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550098)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアント ドライバー</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong></a></p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-interface-descriptor"></a>USB インターフェイス記述子


インターフェイスを記述子には、USB インターフェイスの別の設定に関する情報が含まれています。

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

前の例では、次に注意してください。 **bInterfaceNumber**と**bAlternateSetting**フィールドの値。 これらのフィールドには、ホストは、インターフェイスとその代替の設定のいずれかのアクティブ化を使用してインデックスの値が含まれます。 アクティブにするため、アプリケーションやドライバーは、関数呼び出しでインデックス値を指定します。 その情報に基づいて、USB ドライバー スタック標準のコントロール要求 (インターフェイスの設定) を作成し、デバイスに送信します。 注、 **bInterfaceClass**フィールド。 インターフェイスの記述子または代替の設定のいずれかの記述子は、クラスのコード、サブクラスでは、およびプロトコルを指定します。 0x0E の値は、ビデオ デバイス クラスのインターフェイスであることを示します。 また、 **iInterface**フィールド。 その値は、インターフェイスの記述子に追加する 2 つの文字列記述子があることを示します。 文字列記述子には、デバイスの列挙中に、機能を識別するために使用される Unicode の説明が含まれています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成する場合、.</th>
<th>呼び出す.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用する UWP アプリ<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264281" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264281)"><strong>UsbInterfaceSetting.Descriptors</strong> </a>特定の代替設定の特定の記述子を取得します。</p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264281" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264281)"><strong>UsbInterface.Descriptors</strong> </a>インターフェイスのすべての設定の記述子を取得します。</p></td>
</tr>
<tr class="even">
<td>Win32 デスクトップ アプリを使用する<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 関数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560320" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::GetInterfaceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560320)"><strong>IWDFUsbInterface::GetInterfaceDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff550060" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceGetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550060)"><strong>WdfUsbInterfaceGetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアント ドライバー</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong> </a>各インターフェイスの記述子を解析します。 詳細については、<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="usb-endpoint-descriptor"></a>USB エンドポイント記述子


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

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>作成する場合、.</th>
<th>呼び出す.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>使用する UWP アプリ<a href="https://msdn.microsoft.com/library/windows/apps/dn278466" data-raw-source="[&lt;strong&gt;Windows.Devices.Usb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278466)"> <strong>Windows.Devices.Usb</strong></a></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264052" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264052)"><strong>UsbEndpointDescriptor</strong></a></p></td>
</tr>
<tr class="even">
<td>Win32 デスクトップ アプリを使用する<a href="https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb" data-raw-source="[WinUSB Functions](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)">WinUSB 関数</a></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="odd">
<td>UMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff560403" data-raw-source="[&lt;strong&gt;WDFUsbTargetPipe::GetInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560403)"><strong>WDFUsbTargetPipe::GetInformation</strong></a></td>
</tr>
<tr class="even">
<td>KMDF ベースのクライアント ドライバー</td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff551142" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeGetInformation&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551142)"><strong>WdfUsbTargetPipeGetInformation</strong></a></td>
</tr>
<tr class="odd">
<td>WDM ベースのクライアント ドライバー</td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538943" data-raw-source="[&lt;strong&gt;UsbBuildGetDescriptorRequest&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538943)"><strong>UsbBuildGetDescriptorRequest</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540365" data-raw-source="[&lt;strong&gt;_URB_CONTROL_GET_CONFIGURATION_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540365)"><strong>_URB_CONTROL_GET_CONFIGURATION_REQUEST</strong> </a>の各エンドポイント記述子解析します。 詳細については、<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[すべての USB 開発者の概念](usb-concepts-for-all-developers.md)  



