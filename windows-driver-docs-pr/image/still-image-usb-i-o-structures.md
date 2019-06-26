---
title: 静止画像 USB I/O 構造体
description: 静止画像 USB I/O 構造体
ms.assetid: d70c5c11-c8f2-4196-a7f5-d97ceef10ca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66d2e3706a2e6058c36dbfb5d57af521d3a8b19f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358243"
---
# <a name="still-image-usb-io-structures"></a>静止画像 USB I/O 構造体





次の表では、一覧し、すべての SCSI バスの静止画像カーネル モード ドライバーによって認識される I/O 制御コードに関連付けられている構造について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>構造体</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_channel_info" data-raw-source="[&lt;strong&gt;CHANNEL_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_channel_info)"><strong>CHANNEL_INFO</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst)"> <strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_device_descriptor" data-raw-source="[&lt;strong&gt;DEVICE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_device_descriptor)"><strong>DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_device_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_device_descriptor)"> <strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_drv_version" data-raw-source="[&lt;strong&gt;DRV_VERSION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_drv_version)"><strong>DRV_VERSION</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_version" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_version)"> <strong>IOCTL_GET_VERSION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_io_block" data-raw-source="[&lt;strong&gt;IO_BLOCK&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_io_block)"><strong>IO_BLOCK</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_read_registers" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_read_registers)"> <strong>IOCTL_READ_REGISTERS</strong> </a>または<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_write_registers" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_write_registers)"> <strong>IOCTL_WRITE_REGISTERS</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_io_block_ex" data-raw-source="[&lt;strong&gt;IO_BLOCK_EX&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_io_block_ex)"><strong>IO_BLOCK_EX</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_send_usb_request" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_send_usb_request)"> <strong>IOCTL_SEND_USB_REQUEST</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_get_descriptor" data-raw-source="[&lt;strong&gt;USBSCAN_GET_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_get_descriptor)"><strong>USBSCAN_GET_DESCRIPTOR</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_usb_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_usb_descriptor)"> <strong>IOCTL_GET_USB_DESCRIPTOR</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_pipe_configuration" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_pipe_configuration)"><strong>USBSCAN_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration)"> <strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_pipe_information" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_INFORMATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_pipe_information)"><strong>USBSCAN_PIPE_INFORMATION</strong></a></p></td>
<td><p>静止画像デバイス用の USB 転送パイプの記述に使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_timeout" data-raw-source="[&lt;strong&gt;USBSCAN_TIMEOUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ns-usbscan-_usbscan_timeout)"><strong>USBSCAN_TIMEOUT</strong></a></p></td>
<td><p>USB 一括と一括操作では、タイムアウト値を格納し、中断します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造が定義されている*usbscan.h*します。 詳細についてはこれらの構造体を参照してください。

[USB 静止画像構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)

 

 




