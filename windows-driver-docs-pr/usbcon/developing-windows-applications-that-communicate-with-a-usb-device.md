---
Description: このトピックでは、UWP アプリまたは USB デバイスと通信する Windows デスクトップ アプリを作成する必要があるかどうかを決定するためのガイドラインを提供します。
title: USB デバイス用の Windows アプリケーションの開発の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ef1af894c3e0a7ff8bc3118ffb51c4117497c65
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67717000"
---
# <a name="overview-of-developing-windows-applications-for-usb-devices"></a>USB デバイス用の Windows アプリケーションの開発の概要


**概要**

-   適切なプログラミング モデルの選択に関するガイドライン
-   UWP アプリとデスクトップ アプリの開発者エクスペリエンス

**重要な API**

-   [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)
-   [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)

このトピックでは、UWP アプリまたは USB デバイスと通信する Windows デスクトップ アプリを作成する必要があるかどうかを決定するためのガイドラインを提供します。

Windows には、カスタムの USB デバイスと通信するアプリの記述に使用できる API のセットが用意されています。 API は、デバイス、データ転送の検索などの一般的な USB 関連タスクを実行します。

このコンテキストで「カスタム デバイス」は、デバイスを Microsoft が、インボックス クラス ドライバーを行いません。 代わりに、デバイス ドライバーとして WinUSB (Winusb.sys) をインストールすることができます。

## <a name="choosing-a-programming-model"></a>プログラミング モデルを選択します。


インストールする場合[Winusb.sys](winusb-installation.md)、プログラミング モデルのオプションを次に示します。

-   [USB デバイス用の UWP アプリ](writing-usb-device-companion-apps-for-microsoft-store.md)

    Windows 8.1 には、新しい名前空間が用意されています。[**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)します。 名前空間は、Windows の以前のバージョンでは使用できません。 その他の Microsoft Store のリソースは、ここでは。[UWP アプリ](https://msdn.microsoft.com/windows/apps)します。

-   [USB デバイスの Windows デスクトップ アプリ](windows-desktop-app-for-a-usb-device.md)

    Windows 8.1、経由の通信がアプリの前に[Winusb.sys](winusb-installation.md)を使用して記述されたデスクトップ アプリ、 [WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)します。 Windows 8.1 では、API のセットが拡張されました。 その他の Windows デスクトップ アプリのリソースは、ここでは。[Windows デスクトップ アプリ](https://developer.microsoft.com/windows/desktop)します。

最適なプログラミング モデルを選択するための戦略は、さまざまな要因によって異なります。

-   **アプリが内部の USB デバイスと通信するのでしょうか。**

    Api は主に、周辺機器にアクセスするために設計されています。 API は、内部の USB デバイスを PC にもアクセスできます。 ただし、UWP アプリから PC 内部の USB デバイスへのアクセスは明示的にで宣言されているデバイスのメタデータ、OEM によってその PC の特権を持つアプリに制限されます。

-   **アプリが USB アイソクロナス エンドポイントと通信するのでしょうか。**

    アプリでは、デバイスのアイソクロナス エンドポイント間でデータを送信、Windows デスクトップ アプリを記述する必要があります。 Windows 8.1、新しいで[WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)が追加されていますアイソクロナス エンドポイントからデータを送受信するデスクトップ アプリを許可する API のセットにします。

-   **[コントロール パネル] の種類のアプリ、アプリとは?**

    UWP アプリはユーザーごとのアプリと、アプリごとのスコープ外で変更することはありません。 この種のアプリでは、Windows デスクトップ アプリを記述する必要があります。

-   **UWP アプリでサポートされているクラスのクラスは、USB デバイスですか。**

    いずれかに属している、デバイスが、これらのデバイス クラスを使用するかどうか、UWP アプリを記述します。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **注**場合は、デバイスは、DeviceFirmwareUpdate クラスに属している、アプリが特権を持つアプリをする必要があります。




デバイスが属していない場合に、1 つ前のデバイス クラスは、Windows のデスクトップ アプリを作成します。


## <a name="driver-requirement"></a>ドライバーの要件


| ドライバーの要件 | UWP アプリ                                                                                                                          | Windows デスクトップ アプリ                                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 関数のドライバー    | Microsoft から提供された[Winusb.sys](winusb-installation.md) (カーネル モード ドライバー)。                                                             | Microsoft から提供された[Winusb.sys](winusb-installation.md) (カーネル モード ドライバー)。                                                            |
| フィルター ドライバー      | フィルター ドライバーが存在する場合は、アクセスは特権のあるアプリに制限されます。 アプリは、OEM によってデバイスのメタデータでの特権を持つアプリとして宣言されます。 | アクセスをブロックしない限り、フィルター ドライバーはカーネル モード デバイス スタック内に存在できる[Winusb.sys](winusb-installation.md)します。 |



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
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>これらのサンプルを概要します。</td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">カスタム USB デバイスへのアクセスのサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC コントロールのサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">ファームウェアの更新プログラムの USB デバイスのサンプル</a></li>
</ul></td>
<td><ul>
<li>始まり、 <strong>WinUsb アプリケーション</strong>(Ultimate または Professional) は、Microsoft Visual Studio に含まれているテンプレート</li>
<li>コードの例に示すようを使用して、テンプレートを拡張<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">WinUSB 関数を使用して、USB デバイスへのアクセス方法</a>します。</li>
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
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>開発環境</td>
<td><p>Microsoft Visual Studio 2013</p>
<p>Windows 8.1 用 Microsoft Windows ソフトウェア開発キット (SDK)</p></td>
<td><p>使用<strong>WinUSB アプリケーション</strong>(Ultimate または Professional)、Visual Studio と Windows Driver Kit (WDK) 8 に含まれるテンプレート</p>
<div class="alert">
<strong>注</strong>isochronous 転送、Visual Studio 2013 では、Windows Driver Kit (WDK) 8.1
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>プログラミング言語</td>
<td>C#、VB.NET、C++、JavaScript</td>
<td>C と C++</td>
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
<th>重要なシナリオ</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>デバイスの検出</td>
<td>使用<a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration" data-raw-source="[&lt;strong&gt;Windows.Devices.Enumeration&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)"> <strong>Windows.Devices.Enumeration</strong> </a>名前空間を取得する、 <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"> <strong>UsbDevice</strong></a>します。</td>
<td>使用<a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)">SetupAPI</a>関数と<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"> <strong>WinUsb_Initialize</strong> </a> WINUSB_INTERFACE_HANDLE を取得します。</td>
</tr>
<tr class="even">
<td>USB 制御転送</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket)"><strong>UsbSetupPacket</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType" data-raw-source="[&lt;strong&gt;UsbControlRequestType&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType)"><strong>UsbControlRequestType</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)"><strong>UsbDevice.SendControlInTransferAsync</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>UsbDevice.SendControlOutTransferAsync</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet" data-raw-source="[&lt;strong&gt;WINUSB_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)"><strong>WINUSB_SETUP_PACKET</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)"><strong>WinUsb_ControlTransfer</strong></a></p></td>
</tr>
<tr class="odd">
<td>USB の記述子を取得します。</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice.DeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor" data-raw-source="[&lt;strong&gt;UsbEndpointDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbEndpointDescriptor)"><strong>UsbEndpointDescriptor</strong></a></p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></td>
</tr>
<tr class="even">
<td>USB 一括転送を送信します。</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe" data-raw-source="[&lt;strong&gt;UsbBulkInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe)"><strong>UsbBulkInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe)"><strong>UsbBulkOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="odd">
<td>USB の割り込みの転送を送信します。</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe)"><strong>UsbInterruptInPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe)"><strong>UsbInterruptOutPipe</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p></td>
</tr>
<tr class="even">
<td>USB isochronous 転送を送信します。</td>
<td>サポートされません。</td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p></td>
</tr>
<tr class="odd">
<td>デバイスを閉じる</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close" data-raw-source="[&lt;strong&gt;UsbDevice.Close&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_Close)"><strong>UsbDevice.Close</strong></a></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free" data-raw-source="[&lt;strong&gt;WinUsb_Free&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_free)"><strong>WinUsb_Free</strong></a></td>
</tr>
</tbody>
</table>



## <a name="documentation"></a>ドキュメント


| ドキュメント     | UWP アプリ                                                                     | Windows デスクトップ アプリ                                                                                           |
|-------------------|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|
| プログラミング ガイド | [USB デバイスとの対話、開始から終了まで](talking-to-usb-devices-start-to-finish.md) | [WinUSB 関数を使用して、USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md) |
| API リファレンス     | [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)                              | [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)                                     |



## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



