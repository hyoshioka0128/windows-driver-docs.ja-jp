---
Description: A Universal Serial Bus (USB) device defines its capabilities and features through configurations, interfaces, alternate settings, and endpoints.
title: すべての USB 開発者の概念
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f8a91ceaf9fb8602e0c507f1541ebce1ef7e0624
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557665"
---
#  <a name="concepts-for-all-usb-developers"></a>すべての USB 開発者の概念


ユニバーサル シリアル バス (USB) デバイスでは、その機能と機能の構成、インターフェイス、代替の設定、およびエンドポイントを定義します。 このトピックでは、それらの概念の概要を説明します。 詳細についてでの USB 仕様を参照してください。[ユニバーサル シリアル バス ドキュメント]( https://go.microsoft.com/fwlink/p/?linkid=224892)します。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB デバイスのレイアウト</a></p></td>
<td><p>USB デバイスは、その機能と機能の構成、インターフェイス、代替の設定、およびエンドポイントを定義します。 このトピックでは、それらの概念の概要を説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="standard-usb-descriptors.md" data-raw-source="[Standard USB descriptors](standard-usb-descriptors.md)">標準の USB ディスクリプター</a></p></td>
<td><p>USB デバイスと呼ばれるデータ構造自体に関する情報を提供する<em>の USB ディスクリプター</em>します。 このセクションでは、デバイス、構成、インターフェイス、およびエンドポイント記述子および USB デバイスから取得する方法についての情報を提供します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-endpoints-and-their-pipes.md" data-raw-source="[USB endpoints and their pipes](usb-endpoints-and-their-pipes.md)">USB の端点と、パイプ</a></p></td>
<td><p>USB デバイスには、データ転送に使用されるエンドポイントがあります。 ホスト側のエンドポイントは、パイプで表されます。 このトピックでは、これら 2 つの用語によって区別されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-faq--introductory-level.md" data-raw-source="[USB in Windows - FAQ](usb-faq--introductory-level.md)">Windows - よく寄せられる質問で USB</a></p></td>
<td><p>このトピックでは、初心者の開発と Windows オペレーティング システムとの USB デバイスとドライバーの統合にはドライバー開発者向けのよく寄せられる質問を表示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="common-usb-scenarios"></a>**USB の一般的なシナリオ**


**1: デバイス ハンドルを取得**通信および処理またはデータを送信する転送オブジェクトを取得して、使用します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong>:<a href="https://msdn.microsoft.com/library/windows/hardware/hh439428" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439428)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></p>
<p><strong>UMDF</strong>:<a href="https://msdn.microsoft.com/library/windows/hardware/ff560362" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560362)"><strong>IWDFUsbTargetDevice</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn263883" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263883)"><strong>UsbDevice</strong></a></p>
<p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">USB デバイス (UWP アプリ) に接続する方法</a>します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540277" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540277)"><strong>WinUsb_Initialize</strong></a></p>
<p>参照してください<a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB テンプレートに基づく Windows デスクトップ アプリを記述</a>します。</p></td>
</tr>
</tbody>
</table>

 

**USB 記述子の取得**インターフェイス、デバイスの構成、設定、およびそのエンドポイントに関する情報を取得します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong>:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550090" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550090)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550098" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550098)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></p>
<p><strong>UMDF</strong>:</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560374" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560374)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></p>
<p>参照してください<a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">の USB ディスクリプター</a>します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264002" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264002)"><strong>UsbDevice.DeviceDescriptor</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn263802" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn263802)"><strong>UsbConfiguration.Descriptors</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264289" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264289)"><strong>UsbInterface.Descriptors</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264281" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264281)"><strong>UsbInterfaceSetting.Descriptors</strong></a></p>
<p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">USB ディスクリプター (UWP アプリ) を取得する方法</a>します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540257" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540257)"><strong>WinUsb_GetDescriptor</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540292" data-raw-source="[&lt;strong&gt;WinUsb_QueryInterfaceSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540292)"><strong>WinUsb_QueryInterfaceSettings</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540293" data-raw-source="[&lt;strong&gt;WinUsb_QueryPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540293)"><strong>WinUsb_QueryPipe</strong></a></p>
<p>参照してください<a href="using-winusb-api-to-communicate-with-a-usb-device.md#query" data-raw-source="[Query the Device for USB Descriptors](using-winusb-api-to-communicate-with-a-usb-device.md#query)">記述子の USB デバイスを照会</a>します。</p></td>
</tr>
</tbody>
</table>

 

**2-デバイスを構成する**アクティブな USB 構成およびインターフェイスごとの設定を選択します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550101" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550101)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439423" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateUrb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439423)"><strong>WdfUsbTargetDeviceCreateUrb</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550073" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550073)"><strong>WdfUsbInterfaceSelectSetting</strong></a></p>
<p>参照してください<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>します。</p>
<p>参照してください<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで代替の設定を選択する方法</a>します。</p>
<p><strong>UMDF:</strong></p>
<p>選択した構成はサポートされていません。</p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560343" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560343)"><strong>IWDFUsbInterface::SelectSetting</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264286" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264286)"><strong>UsbInterfaceSetting.SelectSettingAsync</strong></a></p>
<p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">USB インターフェイスの設定 (UWP アプリ) を選択する方法</a>します。</p></td>
<td><a href="https://msdn.microsoft.com/library/windows/hardware/ff540302" data-raw-source="[&lt;strong&gt;WinUsb_SetCurrentAlternateSetting&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540302)"><strong>WinUsb_SetCurrentAlternateSetting</strong></a></td>
</tr>
</tbody>
</table>

 

**3-送信制御転送**デバイスを構成し、特定のデバイスに固有の仕入先のコマンドを実行するためです。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550104" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550104)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550082" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550082)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406243" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406243)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><strong>UMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560363" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560363)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a></p>
<p>参照してください<a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">USB 制御転送を送信する方法</a>します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn264037" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264037)"><strong>SendControlInTransferAsync</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn264047" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn264047)"><strong>SendControlOutTransferAsync</strong></a></p>
<p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">USB 制御転送 (UWP アプリ) を送信する方法</a>します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540219" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540219)"><strong>WinUsb_ControlTransfer</strong></a></p>
<p>参照してください<a href="using-winusb-api-to-communicate-with-a-usb-device.md#control" data-raw-source="[Send Control Transfer to the Default Endpoint](using-winusb-api-to-communicate-with-a-usb-device.md#control)">制御転送を既定のエンドポイントに送信</a>します。</p></td>
</tr>
</tbody>
</table>

 

**4-一括転送を送信**大量のデータを転送する大容量記憶装置デバイスで一般的に使用されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551155" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeReadSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551155)"><strong>WdfUsbTargetPipeReadSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551163" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeWriteSynchronously&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551163)"><strong>WdfUsbTargetPipeWriteSynchronously</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551136" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForRead&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551136)"><strong>WdfUsbTargetPipeFormatRequestForRead</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551141" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForWrite&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551141)"><strong>WdfUsbTargetPipeFormatRequestForWrite</strong></a></p>
<p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">USB 一括転送要求を送信する方法</a></p>
<p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">継続的なリーダーを使用して、USB パイプからデータを読み取る方法</a>します。</p>
<p><strong>UMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556908" data-raw-source="[&lt;strong&gt;IUsbTargetPipeContinuousReaderCallbackReadComplete&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556908)"><strong>IUsbTargetPipeContinuousReaderCallbackReadComplete</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560391" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560391)"><strong>IWDFUsbTargetPipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560394" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560394)"><strong>IWDFUsbTargetPipe2</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn297601" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.InputStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297601)"><strong>UsbBulkInPipe.InputStream</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn297669" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe.OutputStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn297669)"><strong>UsbBulkOutPipe.OutputStream</strong></a></p>
<p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">USB 一括転送要求 (UWP アプリ) を送信する方法</a>します。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540322" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540322)"><strong>WinUsb_WritePipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540297" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540297)"><strong>WinUsb_ReadPipe</strong></a></p>
<p>参照してください<a href="using-winusb-api-to-communicate-with-a-usb-device.md#io" data-raw-source="[Issue I/O Requests](using-winusb-api-to-communicate-with-a-usb-device.md#io)">I/O 要求を発行</a>します。</p></td>
</tr>
</tbody>
</table>

 

**5-送信割り込み転送**します。 データは、ハードウェア割り込みのデータを取得する読み取り専用です。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>一括転送と同じです。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/apps/dn278418" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe.DataReceived&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278418)"><strong>UsbInterruptInPipe.DataReceived</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/apps/dn278428" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe.OutputStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/apps/dn278428)"><strong>UsbInterruptOutPipe.OutputStream</strong></a></p>
<p><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">USB 割り込み転送要求 (UWP アプリ) を送信する方法</a>します。</p></td>
<td><p>一括転送と同じです。</p></td>
</tr>
</tbody>
</table>

 

**6-送信アイソクロナス転送**メディア ストリーミングのデバイスのほとんどの場合に使用されます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439420" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateIsochUrb&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439420)"><strong>WdfUsbTargetDeviceCreateIsochUrb</strong></a></p>
<p>参照してください<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">USB アイソクロナス エンドポイントにデータを転送する方法</a>します。</p>
<p><strong>UMDF:</strong>サポートされません。</p></td>
<td><p>サポートされません。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265566" data-raw-source="[&lt;strong&gt;WinUsb_RegisterIsochBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265566)"><strong>WinUsb_RegisterIsochBuffer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265567" data-raw-source="[&lt;strong&gt;WinUsb_UnregisterIsochBuffer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265567)"><strong>WinUsb_UnregisterIsochBuffer</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265569" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265569)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265565" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265565)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265568" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265568)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265564" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265564)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265549" data-raw-source="[&lt;strong&gt;WinUsb_GetCurrentFrameNumber&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265549)"><strong>WinUsb_GetCurrentFrameNumber</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/dn265548" data-raw-source="[&lt;strong&gt;WinUsb_GetAdjustedFrameNumber&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn265548)"><strong>WinUsb_GetAdjustedFrameNumber</strong></a></p>
<p>参照してください<a href="getting-set-up-to-use-windows-devices-usb.md" data-raw-source="[Sending USB isochronous transfers from a WinUSB desktop app](getting-set-up-to-use-windows-devices-usb.md)">WinUSB デスクトップ アプリから送信する USB アイソクロナス転送</a>します。</p></td>
</tr>
</tbody>
</table>

 

**7-USB のセレクティブ サスペンド**を稼働状態に戻す低電力状態を入力し、デバイスのデバイスを許可します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアント ドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップ アプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551270" data-raw-source="[&lt;strong&gt;WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551270)"><strong>WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff545903" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff545903)"><strong>WdfDeviceAssignS0IdleSettings</strong></a></p>
<p><strong>UMDF:</strong></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff560385" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::SetPowerPolicy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff560385)"><strong>IWDFUsbTargetDevice::SetPowerPolicy</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556920" data-raw-source="[&lt;strong&gt;IWDFDevice2::AssignS0IdleSettings&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556920)"><strong>IWDFDevice2::AssignS0IdleSettings</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/hh451202" data-raw-source="[&lt;strong&gt;IWDFDevice3::AssignS0IdleSettingsEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh451202)"><strong>IWDFDevice3::AssignS0IdleSettingsEx</strong></a></p>
<p>参照してください<a href="https://msdn.microsoft.com/windows/hardware/gg463309" data-raw-source="[How to send a device to selective suspend](https://msdn.microsoft.com/windows/hardware/gg463309)">デバイスをセレクティブ サスペンドを送信する方法</a>します。</p></td>
<td><p>サポートされません。</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540309" data-raw-source="[&lt;strong&gt;WinUsb_SetPowerPolicy&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540309)"><strong>WinUsb_SetPowerPolicy</strong></a></p>
<p>参照してください<a href="winusb-power-management.md" data-raw-source="[WinUSB Power Management](winusb-power-management.md)">WinUSB 電源管理</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://msdn.microsoft.com/library/windows/hardware/ff538930)  



