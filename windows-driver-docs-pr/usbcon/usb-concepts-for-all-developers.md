---
Description: ユニバーサル シリアル バス (USB) デバイスでは、その機能と機能の構成、インターフェイス、代替の設定、およびエンドポイントを定義します。
title: すべての USB 開発者のための概念
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9fa4669b9961feb10e3da824f5dd14155fdc503
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369523"
---
#  <a name="concepts-for-all-usb-developers"></a>すべての USB 開発者のための概念


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
<td><p><strong>KMDF</strong>:<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></p>
<p><strong>UMDF</strong>:<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetdevice)"><strong>IWDFUsbTargetDevice</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"><strong>UsbDevice</strong></a></p>
<p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">USB デバイス (UWP アプリ) に接続する方法</a>します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"><strong>WinUsb_Initialize</strong></a></p>
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
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></p>
<p><strong>UMDF</strong>:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></p>
<p>参照してください<a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">の USB ディスクリプター</a>します。</p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice.DeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface.Descriptors</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)"><strong>UsbInterfaceSetting.Descriptors</strong></a></p>
<p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">USB ディスクリプター (UWP アプリ) を取得する方法</a>します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings" data-raw-source="[&lt;strong&gt;WinUsb_QueryInterfaceSettings&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)"><strong>WinUsb_QueryInterfaceSettings</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe" data-raw-source="[&lt;strong&gt;WinUsb_QueryPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe)"><strong>WinUsb_QueryPipe</strong></a></p>
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
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)"><strong>WdfUsbTargetDeviceCreateUrb</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"><strong>WdfUsbInterfaceSelectSetting</strong></a></p>
<p>参照してください<a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>します。</p>
<p>参照してください<a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで代替の設定を選択する方法</a>します。</p>
<p><strong>UMDF:</strong></p>
<p>選択した構成はサポートされていません。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"><strong>IWDFUsbInterface::SelectSetting</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync)"><strong>UsbInterfaceSetting.SelectSettingAsync</strong></a></p>
<p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">USB インターフェイスの設定 (UWP アプリ) を選択する方法</a>します。</p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting" data-raw-source="[&lt;strong&gt;WinUsb_SetCurrentAlternateSetting&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting)"><strong>WinUsb_SetCurrentAlternateSetting</strong></a></td>
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
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><strong>UMDF:</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice::FormatRequestForControlTransfer</strong></a></p>
<p>参照してください<a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">USB 制御転送を送信する方法</a>します。</p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>SendControlInTransferAsync</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>SendControlOutTransferAsync</strong></a></p>
<p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">USB 制御転送 (UWP アプリ) を送信する方法</a>します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)"><strong>WinUsb_ControlTransfer</strong></a></p>
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
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeReadSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)"><strong>WdfUsbTargetPipeReadSynchronously</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeWriteSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)"><strong>WdfUsbTargetPipeWriteSynchronously</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)"><strong>WdfUsbTargetPipeFormatRequestForRead</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)"><strong>WdfUsbTargetPipeFormatRequestForWrite</strong></a></p>
<p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">USB 一括転送要求を送信する方法</a></p>
<p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">継続的なリーダーを使用して、USB パイプからデータを読み取る方法</a>します。</p>
<p><strong>UMDF:</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete" data-raw-source="[&lt;strong&gt;IUsbTargetPipeContinuousReaderCallbackReadComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)"><strong>IUsbTargetPipeContinuousReaderCallbackReadComplete</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe)"><strong>IWDFUsbTargetPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe2" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)"><strong>IWDFUsbTargetPipe2</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_InputStream" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.InputStream&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_InputStream)"><strong>UsbBulkInPipe.InputStream</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_OutputStream" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe.OutputStream&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_OutputStream)"><strong>UsbBulkOutPipe.OutputStream</strong></a></p>
<p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">USB 一括転送要求 (UWP アプリ) を送信する方法</a>します。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
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
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe.DataReceived&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)"><strong>UsbInterruptInPipe.DataReceived</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe#Windows_Devices_Usb_UsbInterruptOutPipe_OutputStream" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe.OutputStream&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe#Windows_Devices_Usb_UsbInterruptOutPipe_OutputStream)"><strong>UsbInterruptOutPipe.OutputStream</strong></a></p>
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
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateIsochUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)"><strong>WdfUsbTargetDeviceCreateIsochUrb</strong></a></p>
<p>参照してください<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">USB アイソクロナス エンドポイントにデータを転送する方法</a>します。</p>
<p><strong>UMDF:</strong>サポートされません。</p></td>
<td><p>サポートされません。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer" data-raw-source="[&lt;strong&gt;WinUsb_RegisterIsochBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)"><strong>WinUsb_RegisterIsochBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer" data-raw-source="[&lt;strong&gt;WinUsb_UnregisterIsochBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)"><strong>WinUsb_UnregisterIsochBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber" data-raw-source="[&lt;strong&gt;WinUsb_GetCurrentFrameNumber&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)"><strong>WinUsb_GetCurrentFrameNumber</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber" data-raw-source="[&lt;strong&gt;WinUsb_GetAdjustedFrameNumber&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)"><strong>WinUsb_GetAdjustedFrameNumber</strong></a></p>
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
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings" data-raw-source="[&lt;strong&gt;WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)"><strong>WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a></p>
<p><strong>UMDF:</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::SetPowerPolicy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)"><strong>IWDFUsbTargetDevice::SetPowerPolicy</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings" data-raw-source="[&lt;strong&gt;IWDFDevice2::AssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)"><strong>IWDFDevice2::AssignS0IdleSettings</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex" data-raw-source="[&lt;strong&gt;IWDFDevice3::AssignS0IdleSettingsEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex)"><strong>IWDFDevice3::AssignS0IdleSettingsEx</strong></a></p>
<p>参照してください<a href="https://msdn.microsoft.com/windows/hardware/gg463309" data-raw-source="[How to send a device to selective suspend](https://msdn.microsoft.com/windows/hardware/gg463309)">デバイスをセレクティブ サスペンドを送信する方法</a>します。</p></td>
<td><p>サポートされません。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy" data-raw-source="[&lt;strong&gt;WinUsb_SetPowerPolicy&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy)"><strong>WinUsb_SetPowerPolicy</strong></a></p>
<p>参照してください<a href="winusb-power-management.md" data-raw-source="[WinUSB Power Management](winusb-power-management.md)">WinUSB 電源管理</a>します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



