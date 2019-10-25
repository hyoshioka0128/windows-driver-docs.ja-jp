---
Description: ユニバーサルシリアルバス (USB) デバイスは、構成、インターフェイス、代替設定、およびエンドポイントを使用して、その機能と機能を定義します。
title: USB 開発の概要
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b2356e973c1b8d3236ef29a06544080e22cb42fa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823706"
---
# <a name="getting-started-with-usb-development"></a>USB 開発の概要

ユニバーサルシリアルバス (USB) デバイスは、構成、インターフェイス、代替設定、およびエンドポイントを使用して、その機能と機能を定義します。 このトピックでは、これらの概念の概要について説明します。 詳細については、[ユニバーサルシリアルバスのドキュメント]( https://go.microsoft.com/fwlink/p/?linkid=224892)で USB 仕様を参照してください。

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
<td><p><a href="usb-device-layout.md" data-raw-source="[USB device layout](usb-device-layout.md)">USB デバイスレイアウト</a></p></td>
<td><p>USB デバイスは、構成、インターフェイス、代替設定、およびエンドポイントを使用して、機能と機能を定義します。 このトピックでは、これらの概念の概要について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="standard-usb-descriptors.md" data-raw-source="[Standard USB descriptors](standard-usb-descriptors.md)">標準の USB 記述子</a></p></td>
<td><p>USB デバイスは、それ自体に関する情報を<em>usb 記述子</em>と呼ばれるデータ構造に提供します。 このセクションでは、デバイス、構成、インターフェイス、エンドポイント記述子、およびそれらを USB デバイスから取得する方法について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-endpoints-and-their-pipes.md" data-raw-source="[USB endpoints and their pipes](usb-endpoints-and-their-pipes.md)">USB エンドポイントとそのパイプ</a></p></td>
<td><p>USB デバイスには、データ転送のために使用されるエンドポイントがあります。 ホスト側では、エンドポイントはパイプで表されます。 このトピックでは、これら2つの用語を区別します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-faq--introductory-level.md" data-raw-source="[USB in Windows - FAQ](usb-faq--introductory-level.md)">Windows での USB-FAQ</a></p></td>
<td><p>このトピックでは、Windows オペレーティングシステムで USB デバイスとドライバーを開発して統合することを初めて行うドライバー開発者に関してよく寄せられる質問を示します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="common-usb-scenarios"></a>一般的な USB シナリオ


**1 —** 通信用のデバイスハンドルを取得し、取得したハンドルまたはオブジェクトを使用してデータ転送を送信します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Kmdf</strong>: <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"> <strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></p>
<p><strong>UMDF</strong>: <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)"> <strong>IWDFUsbTargetDevice</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice" data-raw-source="[&lt;strong&gt;UsbDevice&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice)"><strong>UsbDevice</strong></a></p>
<p><a href="how-to-connect-to-a-usb-device--uwp-app-.md" data-raw-source="[How to connect to a USB device (UWP app)](how-to-connect-to-a-usb-device--uwp-app-.md)">USB デバイスに接続する方法 (UWP アプリ)</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize" data-raw-source="[&lt;strong&gt;WinUsb_Initialize&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)"><strong>WinUsb_Initialize</strong></a></p>
<p>「 <a href="how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md" data-raw-source="[Write a Windows desktop app based on the WinUSB template](how-to-write-a-windows-desktop-app-that-communicates-with-a-usb-device.md)">WinUSB テンプレートに基づく Windows デスクトップアプリの作成</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

デバイスの構成、インターフェイス、設定、およびそれらのエンドポイントに関する情報を取得するための、 **USB 記述子の取得**。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Kmdf</strong>:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceGetDeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicegetdevicedescriptor)"><strong>WdfUsbTargetDeviceGetDeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceRetrieveConfigDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceretrieveconfigdescriptor)"><strong>WdfUsbTargetDeviceRetrieveConfigDescriptor</strong></a></p>
<p><strong>UMDF</strong>:</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::RetrieveDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-retrievedescriptor)"><strong>IWDFUsbTargetDevice::RetrieveDescriptor</strong></a></p>
<p>「 <a href="usb-descriptors.md" data-raw-source="[USB descriptors](usb-descriptors.md)">USB 記述子</a>」を参照してください。</p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor" data-raw-source="[&lt;strong&gt;UsbDevice.DeviceDescriptor&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_DeviceDescriptor)"><strong>UsbDevice. DeviceDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors" data-raw-source="[&lt;strong&gt;UsbConfiguration.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbConfiguration#Windows_Devices_Usb_UsbConfiguration_Descriptors)"><strong>UsbConfiguration. 記述子</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterface.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterface#Windows_Devices_Usb_UsbInterface_Descriptors)"><strong>UsbInterface. 記述子</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.Descriptors&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_Descriptors)"><strong>UsbInterfaceSetting. 記述子</strong></a></p>
<p><a href="how-to-get-usb-descriptors--uwp-app-.md" data-raw-source="[How to get USB descriptors (UWP app)](how-to-get-usb-descriptors--uwp-app-.md)">USB 記述子を取得する方法 (UWP アプリ)</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor" data-raw-source="[&lt;strong&gt;WinUsb_GetDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getdescriptor)"><strong>WinUsb_GetDescriptor</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings" data-raw-source="[&lt;strong&gt;WinUsb_QueryInterfaceSettings&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_queryinterfacesettings)"><strong>WinUsb_QueryInterfaceSettings</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe" data-raw-source="[&lt;strong&gt;WinUsb_QueryPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_querypipe)"><strong>WinUsb_QueryPipe</strong></a></p>
<p>「<a href="using-winusb-api-to-communicate-with-a-usb-device.md#query" data-raw-source="[Query the Device for USB Descriptors](using-winusb-api-to-communicate-with-a-usb-device.md#query)">デバイスで USB 記述子を照会する」を</a>参照してください。</p></td>
</tr>
</tbody>
</table>

 

**2:** アクティブな USB 構成とインターフェイスごとの設定を選択するようにデバイスを構成します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSelectConfig&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceselectconfig)"><strong>WdfUsbTargetDeviceSelectConfig</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)"><strong>WdfUsbTargetDeviceCreateUrb</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting" data-raw-source="[&lt;strong&gt;WdfUsbInterfaceSelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbinterfaceselectsetting)"><strong>WdfUsbInterfaceSelectSetting</strong></a></p>
<p>「 <a href="how-to-select-a-configuration-for-a-usb-device.md" data-raw-source="[How to select a configuration for a USB device](how-to-select-a-configuration-for-a-usb-device.md)">USB デバイスの構成を選択する方法</a>」を参照してください。</p>
<p>「 <a href="select-a-usb-alternate-setting.md" data-raw-source="[How to select an alternate setting in a USB interface](select-a-usb-alternate-setting.md)">USB インターフェイスで別の設定を選択する方法</a>」を参照してください。</p>
<p><strong>UMDF</strong></p>
<p>構成の選択はサポートされていません。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting" data-raw-source="[&lt;strong&gt;IWDFUsbInterface::SelectSetting&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbinterface-selectsetting)"><strong>IWDFUsbInterface:: SelectSetting</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync" data-raw-source="[&lt;strong&gt;UsbInterfaceSetting.SelectSettingAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterfaceSetting#Windows_Devices_Usb_UsbInterfaceSetting_SelectSettingAsync)"><strong>UsbInterfaceSetting. SelectSettingAsync</strong></a></p>
<p><a href="how-to-select-a-usb-interface-setting--uwp-app-.md" data-raw-source="[How to select a USB interface setting (UWP app)](how-to-select-a-usb-interface-setting--uwp-app-.md)">USB インターフェイス設定を選択する方法 (UWP アプリ)</a></p></td>
<td><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting" data-raw-source="[&lt;strong&gt;WinUsb_SetCurrentAlternateSetting&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setcurrentalternatesetting)"><strong>WinUsb_SetCurrentAlternateSetting</strong></a></td>
</tr>
</tbody>
</table>

 

**3:** デバイスを構成し、特定のデバイスに固有のベンダーコマンドを実行するための制御転送を送信します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceSendControlTransferSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicesendcontroltransfersynchronously)"><strong>WdfUsbTargetDeviceSendControlTransferSynchronously</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceFormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdeviceformatrequestforcontroltransfer)"><strong>WdfUsbTargetDeviceFormatRequestForControlTransfer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild" data-raw-source="[&lt;strong&gt;USBD_SelectConfigUrbAllocateAndBuild&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_selectconfigurballocateandbuild)"><strong>USBD_SelectConfigUrbAllocateAndBuild</strong></a></p>
<p><strong>UMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::FormatRequestForControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-formatrequestforcontroltransfer)"><strong>IWDFUsbTargetDevice:: FormatRequestForControlTransfer</strong></a></p>
<p>「 <a href="usb-control-transfer.md" data-raw-source="[How to send a USB control transfer](usb-control-transfer.md)">USB 制御転送を送信する方法」を</a>参照してください。</p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;SendControlInTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlInTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>Send制御 Lintransferasync</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_" data-raw-source="[&lt;strong&gt;SendControlOutTransferAsync&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbDevice#Windows_Devices_Usb_UsbDevice_SendControlOutTransferAsync_Windows_Devices_Usb_UsbSetupPacket_)"><strong>SendControlOutTransferAsync</strong></a></p>
<p><a href="how-to-send-a-usb-control-transfer--uwp-app-.md" data-raw-source="[How to send a USB control transfer (UWP app)](how-to-send-a-usb-control-transfer--uwp-app-.md)">USB 制御転送を送信する方法 (UWP アプリ)</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer" data-raw-source="[&lt;strong&gt;WinUsb_ControlTransfer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_controltransfer)"><strong>WinUsb_ControlTransfer</strong></a></p>
<p>「<a href="using-winusb-api-to-communicate-with-a-usb-device.md#control" data-raw-source="[Send Control Transfer to the Default Endpoint](using-winusb-api-to-communicate-with-a-usb-device.md#control)">既定のエンドポイントへの送信制御転送」を</a>参照してください。</p></td>
</tr>
</tbody>
</table>

 

**4 —** 大量のデータを転送する大容量記憶装置で通常使用される一括転送を送信します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeReadSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipereadsynchronously)"><strong>WdfUsbTargetPipeReadSynchronously</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeWriteSynchronously&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipewritesynchronously)"><strong>WdfUsbTargetPipeWriteSynchronously</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForRead&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforread)"><strong>WdfUsbTargetPipeFormatRequestForRead</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite" data-raw-source="[&lt;strong&gt;WdfUsbTargetPipeFormatRequestForWrite&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetpipeformatrequestforwrite)"><strong>WdfUsbTargetPipeFormatRequestForWrite</strong></a></p>
<p><a href="usb-bulk-and-interrupt-transfer.md" data-raw-source="[How to send USB bulk transfer requests](usb-bulk-and-interrupt-transfer.md)">USB 一括転送要求を送信する方法</a></p>
<p><a href="how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md" data-raw-source="[How to use the continuous reader for reading data from a USB pipe](how-to-use-the-continous-reader-for-getting-data-from-a-usb-endpoint--umdf-.md)">連続リーダーを使用して、USB パイプからデータを読み取る方法</a>。</p>
<p><strong>UMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete" data-raw-source="[&lt;strong&gt;IUsbTargetPipeContinuousReaderCallbackReadComplete&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iusbtargetpipecontinuousreadercallbackreadcomplete)"><strong>IUsbTargetPipeContinuousReaderCallbackReadComplete</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)"><strong>IWDFUsbTargetPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe2" data-raw-source="[&lt;strong&gt;IWDFUsbTargetPipe2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe2)"><strong>IWDFUsbTargetPipe2</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_InputStream" data-raw-source="[&lt;strong&gt;UsbBulkInPipe.InputStream&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkInPipe#Windows_Devices_Usb_UsbBulkInPipe_InputStream)"><strong>UsbBulkInPipe InputStream</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_OutputStream" data-raw-source="[&lt;strong&gt;UsbBulkOutPipe.OutputStream&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbBulkOutPipe#Windows_Devices_Usb_UsbBulkOutPipe_OutputStream)"><strong>UsbBulkOutPipe. OutputStream</strong></a></p>
<p><a href="how-to-send-a-usb-bulk-transfer--uwp-app-.md" data-raw-source="[How to send a USB bulk transfer request (UWP app)](how-to-send-a-usb-bulk-transfer--uwp-app-.md)">USB 一括転送要求を送信する方法 (UWP アプリ)</a></p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a></p>
<p>「 <a href="using-winusb-api-to-communicate-with-a-usb-device.md#io" data-raw-source="[Issue I/O Requests](using-winusb-api-to-communicate-with-a-usb-device.md#io)">I/o 要求</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

**5: 割り込み転送を送信**します。 データは、ハードウェアの割り込みデータを取得するために読み取られます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>一括転送と同じです。</p></td>
<td><p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived" data-raw-source="[&lt;strong&gt;UsbInterruptInPipe.DataReceived&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptInPipe#Windows_Devices_Usb_UsbInterruptInPipe_DataReceived)"><strong>UsbInterruptInPipe を受信しました</strong></a></p>
<p><a href="https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe#Windows_Devices_Usb_UsbInterruptOutPipe_OutputStream" data-raw-source="[&lt;strong&gt;UsbInterruptOutPipe.OutputStream&lt;/strong&gt;](https://docs.microsoft.com/uwp/api/Windows.Devices.Usb.UsbInterruptOutPipe#Windows_Devices_Usb_UsbInterruptOutPipe_OutputStream)"><strong>UsbInterruptOutPipe</strong></a></p>
<p><a href="how-to-send-a-usb-interrupt-transfer--uwp-app-.md" data-raw-source="[How to send a USB interrupt transfer request (UWP app)](how-to-send-a-usb-interrupt-transfer--uwp-app-.md)">USB 割り込み転送要求を送信する方法 (UWP アプリ)</a>。</p></td>
<td><p>一括転送と同じです。</p></td>
</tr>
</tbody>
</table>

 

**6 —** ほとんどの場合、メディアストリーミングデバイスで使用される、アイソクロナス転送を送信します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateIsochUrb&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateisochurb)"><strong>WdfUsbTargetDeviceCreateIsochUrb</strong></a></p>
<p>「<a href="transfer-data-to-isochronous-endpoints.md" data-raw-source="[How to transfer data to USB isochronous endpoints](transfer-data-to-isochronous-endpoints.md)">データを USB アイソクロナスエンドポイントに転送する方法</a>」を参照してください。</p>
<p><strong>UMDF:</strong>サポートされていません。</p></td>
<td><p>サポートされません。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer" data-raw-source="[&lt;strong&gt;WinUsb_RegisterIsochBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_registerisochbuffer)"><strong>WinUsb_RegisterIsochBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer" data-raw-source="[&lt;strong&gt;WinUsb_UnregisterIsochBuffer&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_unregisterisochbuffer)"><strong>WinUsb_UnregisterIsochBuffer</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipeasap)"><strong>WinUsb_WriteIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipeAsap&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipeasap)"><strong>WinUsb_ReadIsochPipeAsap</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_WriteIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writeisochpipe)"><strong>WinUsb_WriteIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadIsochPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readisochpipe)"><strong>WinUsb_ReadIsochPipe</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber" data-raw-source="[&lt;strong&gt;WinUsb_GetCurrentFrameNumber&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getcurrentframenumber)"><strong>WinUsb_GetCurrentFrameNumber</strong></a></p>
<p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber" data-raw-source="[&lt;strong&gt;WinUsb_GetAdjustedFrameNumber&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getadjustedframenumber)"><strong>WinUsb_GetAdjustedFrameNumber</strong></a></p>
<p>「 <a href="getting-set-up-to-use-windows-devices-usb.md" data-raw-source="[Sending USB isochronous transfers from a WinUSB desktop app](getting-set-up-to-use-windows-devices-usb.md)">Winusb デスクトップアプリからの usb アイソクロナス転送の送信</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

**7 — USB の選択的な中断**により、デバイスは電力の状態を低くし、デバイスを動作状態に戻すことができます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>クライアントドライバー</th>
<th>UWP アプリ</th>
<th>Windows デスクトップアプリ</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings" data-raw-source="[&lt;strong&gt;WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/ns-wdfdevice-_wdf_device_power_policy_idle_settings)"><strong>WDF_DEVICE_POWER_POLICY_IDLE_SETTINGS</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings" data-raw-source="[&lt;strong&gt;WdfDeviceAssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings)"><strong>WdfDeviceAssignS0IdleSettings</strong></a></p>
<p><strong>UMDF</strong></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy" data-raw-source="[&lt;strong&gt;IWDFUsbTargetDevice::SetPowerPolicy&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfusb/nf-wudfusb-iwdfusbtargetdevice-setpowerpolicy)"><strong>IWDFUsbTargetDevice:: SetPowerPolicy</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings" data-raw-source="[&lt;strong&gt;IWDFDevice2::AssignS0IdleSettings&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-assigns0idlesettings)"><strong>IWDFDevice2::AssignS0IdleSettings</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex" data-raw-source="[&lt;strong&gt;IWDFDevice3::AssignS0IdleSettingsEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-assigns0idlesettingsex)"><strong>IWDFDevice3::AssignS0IdleSettingsEx</strong></a></p>
<p>「<a href="https://msdn.microsoft.com/windows/hardware/gg463309" data-raw-source="[How to send a device to selective suspend](https://msdn.microsoft.com/windows/hardware/gg463309)">選択的中断にデバイスを送信する方法</a>」を参照してください。</p></td>
<td><p>サポートされません。</p></td>
<td><p><a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy" data-raw-source="[&lt;strong&gt;WinUsb_SetPowerPolicy&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpowerpolicy)"><strong>WinUsb_SetPowerPolicy</strong></a></p>
<p>「 <a href="winusb-power-management.md" data-raw-source="[WinUSB Power Management](winusb-power-management.md)">Winusb 電源管理</a>」を参照してください。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



