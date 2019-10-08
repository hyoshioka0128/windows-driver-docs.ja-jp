---
Description: このトピックでは、USB デバイスと通信するために UWP アプリまたは Windows デスクトップアプリを作成する必要があるかどうかを判断するためのガイドラインを示します。
title: USB デバイス用 Windows アプリケーション開発の概要
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 88e3dcae013cfc9d644ee8507ed77149c6b80e28
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007545"
---
# <a name="overview-of-developing-windows-applications-for-usb-devices"></a>USB デバイス用 Windows アプリケーション開発の概要


**概要**

-   適切なプログラミングモデルを選択するためのガイドライン
-   UWP アプリとデスクトップアプリの開発者エクスペリエンス

**重要な API**

-   [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)
-   [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)

このトピックでは、USB デバイスと通信するために UWP アプリまたは Windows デスクトップアプリを作成する必要があるかどうかを判断するためのガイドラインを示します。

Windows には、カスタム USB デバイスと通信するアプリの作成に使用できる API セットが用意されています。 この API は、デバイスの検索、データ転送など、一般的な USB 関連タスクを実行します。

このコンテキストの "カスタムデバイス" とは、Microsoft がインボックスクラスのドライバーを提供していないデバイスを意味します。 代わりに、デバイスドライバーとして WinUSB (Winusb .sys) をインストールできます。

## <a name="choosing-a-programming-model"></a>プログラミングモデルの選択


[Winusb .sys](winusb-installation.md)をインストールする場合、プログラミングモデルのオプションは次のとおりです。

-   [USB デバイス用の UWP アプリ](writing-usb-device-companion-apps-for-microsoft-store.md)

    Windows 8.1 は、新しい名前空間を提供します。[**Windows. デバイス. Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)。 名前空間は、以前のバージョンの Windows では使用できません。 その他の Microsoft Store リソースは次のとおりです。[UWP アプリ](https://msdn.microsoft.com/windows/apps)。

-   [USB デバイス用の Windows デスクトップアプリ](windows-desktop-app-for-a-usb-device.md)

    Windows 8.1 する前に、 [Winusb](winusb-installation.md)を介して通信していたアプリは、 [winusb 機能](using-winusb-api-to-communicate-with-a-usb-device.md)を使用して作成されたデスクトップアプリでした。 Windows 8.1 では、API セットが拡張されています。 その他の Windows デスクトップアプリリソースは次のとおりです。[Windows デスクトップアプリ](https://developer.microsoft.com/windows/desktop)。

最適なプログラミングモデルを選択するための戦略は、さまざまな要因によって異なります。

-   **アプリは内部 USB デバイスと通信しますか。**

    これらの Api は、主に周辺機器にアクセスするように設計されています。 この API は、PC 内部 USB デバイスにアクセスすることもできます。 ただし、UWP アプリからの PC 内部 USB デバイスへのアクセスは、その PC の OEM によってデバイスメタデータで明示的に宣言されている特権アプリに限定されます。

-   **アプリは USB アイソクロナスエンドポイントと通信しますか。**

    アプリがデバイスのアイソクロナスエンドポイントとの間でデータを送信する場合は、Windows デスクトップアプリを作成する必要があります。 Windows 8.1 では、デスクトップアプリがアイソクロナスエンドポイントとの間でデータを送受信できるようにする新しい[Winusb 関数](using-winusb-api-to-communicate-with-a-usb-device.md)が API セットに追加されました。

-   **アプリはアプリの "コントロールパネル" の種類ですか。**

    UWP アプリはユーザーごとのアプリであり、各アプリのスコープ外で変更を行うことはできません。 これらの種類のアプリでは、Windows デスクトップアプリを作成する必要があります。

-   **USB デバイスクラスは、UWP アプリでサポートされているクラスですか。**

    デバイスが1つのデバイスクラスに属している場合は、UWP アプリを作成します。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **メモ** デバイスが DeviceFirmwareUpdate クラスに属している場合、アプリは特権アプリである必要があります。




デバイスが、上記のいずれかのデバイスクラスに属していない場合は、Windows デスクトップアプリを作成します。


## <a name="driver-requirement"></a>ドライバーの要件


| ドライバーの要件 | UWP アプリ                                                                                                                          | Windows デスクトップアプリ                                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 関数ドライバー    | Microsoft 提供の[Winusb .sys](winusb-installation.md) (カーネルモードドライバー)。                                                             | Microsoft 提供の[Winusb .sys](winusb-installation.md) (カーネルモードドライバー)。                                                            |
| フィルタードライバー      | フィルタードライバーが存在する場合、アクセスは特権アプリに限定されます。 アプリは、OEM によってデバイスメタデータ内の特権アプリとして宣言されます。 | フィルタードライバーは、 [Winusb .sys](winusb-installation.md)へのアクセスがブロックされていない限り、カーネルモードのデバイススタックに存在することができます。 |



## <a name="code-samples"></a>コード サンプル


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>サンプル</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>これらのサンプルを使ってみる</td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">カスタム USB デバイスアクセスのサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 制御のサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">ファームウェア更新の USB デバイスのサンプル</a></li>
</ul></td>
<td><ul>
<li>Microsoft Visual Studio (Ultimate または Professional) に含まれる<strong>Winusb アプリケーション</strong>テンプレートを使用して開始する</li>
<li>「 <a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">Winusb 機能を使用して Usb デバイスにアクセスする方法</a>」に示されているコード例を使用して、テンプレートを拡張します。</li>
</ul></td>
</tr>
</tbody>
</table>



## <a name="development-tools"></a>開発ツール


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>開発ツール</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>開発者環境</td>
<td><p>Microsoft Visual Studio 2013</p>
<p>Windows 8.1 用 Microsoft Windows ソフトウェア開発キット (SDK)</p></td>
<td><p>Visual Studio (Ultimate または Professional) および Windows Driver Kit (WDK) 8 に含まれる<strong>Winusb アプリケーション</strong>テンプレートを使用する</p>
<div class="alert"></strong> アイソクロナス転送の場合は @ no__t-1、Windows ドライバーキット (WDK) 8.1 では Visual Studio 2013
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>プログラミング言語</td>
<td>C#、VB.NET、 C++、JavaScript</td>
<td>40U-CC++</td>
</tr>
</tbody>
</table>



## <a name="feature-implementation"></a>機能の実装


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>主要シナリオ</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>デバイスの検出</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"><strong>Usb デバイス</strong></a>を取得するには、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration" data-raw-source="[&lt;strong&gt;Windows.Devices.Enumeration&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)"><strong>Windows の Enumeration</strong></a>名前空間を使用します。</td>
<td>WINUSB_INTERFACE_HANDLE を取得するには、 <a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)">setupapi.log</a>関数と<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"><strong>WinUsb_Initialize</strong></a>を使用します。</td>
</tr>
<tr class="even">
<td>USB 制御の転送</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket)"><strong>UsbSetupPacket</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType" data-raw-source="[&lt;strong&gt;UsbControlRequestType&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType)"><strong>UsbControlRequestType</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)"><strong>UsbDevice. Send制御 Lintransferasync</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>UsbDevice. SendControlOutTransferAsync</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet" data-raw-source="[&lt;strong&gt;WINUSB_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)"><strong>WINUSB_SETUP_PACKET</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)"><strong>WinUsb_ControlTransfer</strong></a></p></td>
</tr>
<tr class="odd">
<td>USB 記述子の取得</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice. DeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration. 記述子</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface. 記述子</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)"><strong>UsbEndpointDescriptor</strong></a></p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>USB 一括転送の送信</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)"><strong>UsbBulkInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)"><strong>UsbBulkOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="odd">
<td>USB 割り込み転送の送信</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)"><strong>UsbInterruptInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)"><strong>UsbInterruptOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="even">
<td>USB アイソクロナス転送の送信</td>
<td>サポートされていません。</td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p></td>
</tr>
<tr class="odd">
<td>デバイスを閉じる</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)"><strong>UsbDevice. Close</strong></a></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free" data-raw-source="[&lt;strong&gt;WinUsb_Free&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)"><strong>WinUsb_Free</strong></a></td>
</tr>
</tbody>
</table>



## <a name="documentation"></a>ドキュメント


| ドキュメント     | UWP アプリ                                                                     | Windows デスクトップアプリ                                                                                           |
|-------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| プログラミングガイド | [USB デバイスとの対話の開始](talking-to-usb-devices-start-to-finish.md) | [WinUSB 機能を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md) |
| API リファレンス     | [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)                              | [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)                                     |



## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



