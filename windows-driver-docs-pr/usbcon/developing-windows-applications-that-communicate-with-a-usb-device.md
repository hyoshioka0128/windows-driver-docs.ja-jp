---
Description: このトピックでは、USB デバイスとの通信に UWP アプリまたは Windows デスクトップ アプリのどちらを作成する必要があるかどうかを判断するためのガイドラインを示します。
title: USB デバイス用 Windows アプリケーション開発の概要
ms.date: 04/20/2017
ms.localizationpriority: High
ms.openlocfilehash: 88e3dcae013cfc9d644ee8507ed77149c6b80e28
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "72007545"
---
# <a name="overview-of-developing-windows-applications-for-usb-devices"></a>USB デバイス用 Windows アプリケーション開発の概要


**要約**

-   適切なプログラミング モデルを選択するためのガイドライン
-   UWP アプリとデスクトップ アプリの開発者エクスペリエンス

**重要な API**

-   [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)
-   [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)

このトピックでは、USB デバイスとの通信に UWP アプリまたは Windows デスクトップ アプリのどちらを作成する必要があるかどうかを判断するためのガイドラインを示します。

Windows では、カスタム USB デバイスと通信するアプリの作成に使用できる API セットを提供しています。 この API は、デバイスの検索、データ転送など、一般的な USB 関連タスクを実行します。

このコンテキストにおける "カスタム デバイス" とは、Microsoft がインボックス クラスのドライバーを提供していないデバイスを意味します。 代わりに、デバイス ドライバーとして WinUSB (Winusb.sys) をインストールできます。

## <a name="choosing-a-programming-model"></a>プログラミング モデルの選択


[Winusb.sys](winusb-installation.md) をインストールする場合、プログラミング モデルのオプションは次のとおりです。

-   [USB デバイス用の UWP アプリ](writing-usb-device-companion-apps-for-microsoft-store.md)

    Windows 8.1 では、次の新しい名前空間が提供されています。[**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)。 名前空間は、以前のバージョンの Windows では使用できません。 その他の Microsoft Store リソースは次のとおりです。[UWP アプリ](https://msdn.microsoft.com/windows/apps)。

-   [USB デバイス用の Windows デスクトップ アプリ](windows-desktop-app-for-a-usb-device.md)

    Windows 8.1 以前では、[Winusb.sys](winusb-installation.md) を介して通信していたアプリは、[WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)を使用して作成されたデスクトップ アプリでした。 Windows 8.1 では、API セットが拡張されました。 その他の Windows デスクトップ アプリ リソースは次のとおりです。[Windows デスクトップ アプリ](https://developer.microsoft.com/windows/desktop)。

最適なプログラミング モデルを選択する方法は、さまざまな要因によって左右されます。

-   **アプリで内部 USB デバイスと通信するかどうか。**

    API は、主に周辺機器にアクセスするように設計されています。 この API は、PC の内部 USB デバイスにアクセスすることもできます。 ただし、UWP アプリから PC の内部 USB デバイスへのアクセスは、その PC の OEM によってデバイス メタデータで明示的に宣言されている特権アプリに限定されます。

-   **アプリで USB 等時性エンドポイントと通信するかどうか。**

    アプリと、デバイスの等時性エンドポイントとの間でデータのやりとりを行う場合は、Windows デスクトップ アプリを作成する必要があります。 Windows 8.1 では、デスクトップ アプリと等時性エンドポイントとの間でデータの送受信を行うことができる、新しい [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)が API セットに追加されました。

-   **アプリが "コントロール パネル" タイプのアプリであるかどうか。**

    UWP アプリはユーザー単位のアプリであり、各アプリのスコープ外で変更を行うことはできません。 これらの種類のアプリの場合、Windows デスクトップ アプリを作成する必要があります。

-   **USB デバイス クラスが、UWP アプリでサポートされているクラスであるかどうか。**

    デバイスがいずれかのデバイス クラスに属している場合は、UWP アプリを作成します。

    -   `name:cdcControl,           classId:02 * *`
    -   `name:physical, classId:05 * *`
    -   `name:personalHealthcare,   classId:0f 00 00`
    -   `name:activeSync,           classId:ef 01 01`
    -   `name:palmSync,             classId:ef 01 02`
    -   `name:deviceFirmwareUpdate, classId:fe 01 01`
    -   `name:irda,                 classId:fe 02 00     `
    -   `name:measurement,          classId:fe 03 *`
    -   `name:vendorSpecific,       classId:ff * *`

    **注** デバイスが DeviceFirmwareUpdate クラスに属している場合、アプリは特権アプリである必要があります。




デバイスが、上記のどのデバイス クラスにも属していない場合は、Windows デスクトップ アプリを作成します。


## <a name="driver-requirement"></a>ドライバーの要件


| ドライバーの要件 | UWP アプリ                                                                                                                          | Windows デスクトップ アプリ                                                                                                                       |
|--------------------|--------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| 関数ドライバー    | Microsoft が提供する [Winusb.sys](winusb-installation.md) (カーネル モード ドライバー)。                                                             | Microsoft が提供する [Winusb.sys](winusb-installation.md) (カーネル モード ドライバー)。                                                            |
| フィルター ドライバー      | フィルター ドライバーが存在する場合、アクセスは特権アプリに限定されます。 アプリは、OEM によってデバイス メタデータ内で特権アプリとして宣言されます。 | フィルター ドライバーは、[Winusb.sys](winusb-installation.md) へのアクセスをブロックしない限り、カーネル モードのデバイス スタックに存在することができます。 |



## <a name="code-samples"></a>コード サンプル


<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>［サンプル］</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>これらのサンプルを試してみる</td>
<td><ul>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Custom USB device access sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">カスタム USB デバイス アクセスのサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[USB CDC Control sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">USB CDC 制御のサンプル</a></li>
<li><a href="https://go.microsoft.com/fwlink/p/?linkid=309716" data-raw-source="[Firmware Update USB Device sample](https://go.microsoft.com/fwlink/p/?linkid=309716)">ファームウェア更新の USB デバイスのサンプル</a></li>
</ul></td>
<td><ul>
<li>Microsoft Visual Studio (Ultimate または Professional) に含まれている <strong>WinUsb アプリケーション</strong> テンプレートを使用して開始する</li>
<li>「<a href="using-winusb-api-to-communicate-with-a-usb-device.md" data-raw-source="[How to Access a USB Device by Using WinUSB Functions](using-winusb-api-to-communicate-with-a-usb-device.md)">WinUSB 関数を使用して USB デバイスにアクセスする方法</a>」に示されているコード例を使用して、テンプレートを拡張します。</li>
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
<td>開発者環境</td>
<td><p>Microsoft Visual Studio 2013</p>
<p>Windows 8.1 用 Microsoft Windows ソフトウェア開発キット (SDK)</p></td>
<td><p>Visual Studio (Ultimate または Professional) および Windows Driver Kit (WDK) 8 に含まれている <strong>WinUSB アプリケーション</strong> テンプレートを使用する</p>
<div class="alert">
<strong>注</strong> 等時性転送の場合は Visual Studio 2013 with Windows Driver Kit (WDK) 8.1
</div>
<div>

</div></td>
</tr>
<tr class="even">
<td>プログラミング言語</td>
<td>C#、VB.NET、C++、JavaScript</td>
<td>C/C++</td>
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
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>デバイスの検出</td>
<td><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration" data-raw-source="[&lt;strong&gt;Windows.Devices.Enumeration&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Enumeration)"><strong>Windows.Devices.Enumeration</strong></a> 名前空間を使用して <a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"><strong>UsbDevice</strong></a> を取得します。</td>
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/install/setupapi" data-raw-source="[SetupAPI](https://docs.microsoft.com/windows-hardware/drivers/install/setupapi)">SetupAPI</a> 関数および <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"><strong>WinUsb_Initialize</strong></a> を使用して、WINUSB_INTERFACE_HANDLE を取得します。</td>
</tr>
<tr class="even">
<td>USB コントロール転送</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket" data-raw-source="[&lt;strong&gt;UsbSetupPacket&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbSetupPacket)"><strong>UsbSetupPacket</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType" data-raw-source="[&lt;strong&gt;UsbControlRequestType&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbControlRequestType)"><strong>UsbControlRequestType</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_Windows_Storage_Streams_IBuffer_)"><strong>UsbDevice.SendControlInTransferAsync</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;UsbDevice.SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>UsbDevice.SendControlOutTransferAsync</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet" data-raw-source="[&lt;strong&gt;WINUSB_SETUP_PACKET&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/ns-winusb-_winusb_setup_packet)"><strong>WINUSB_SETUP_PACKET</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)"><strong>WinUsb_ControlTransfer</strong></a></p></td>
</tr>
<tr class="odd">
<td>USB 記述子の取得</td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice.DeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface.Descriptors</strong></a></p>
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
<td>USB 等時性転送の送信</td>
<td>サポートされていません。</td>
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
| プログラミング ガイド | [USB デバイスとの対話、開始から終了まで](talking-to-usb-devices-start-to-finish.md) | [WinUSB 関数を使用して USB デバイスにアクセスする方法](using-winusb-api-to-communicate-with-a-usb-device.md) |
| API リファレンス     | [**Windows.Devices.Usb**](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb)                              | [WinUSB 関数](using-winusb-api-to-communicate-with-a-usb-device.md)                                     |



## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



