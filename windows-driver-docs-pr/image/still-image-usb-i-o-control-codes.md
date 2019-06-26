---
title: 静止画像 USB I/O 制御コード
description: 静止画像 USB I/O 制御コード
ms.assetid: 66a06a25-2fcb-4b14-85e2-485d2d4ac9d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84750fd52d2c4add057c392694c2b61106e8631b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377699"
---
# <a name="still-image-usb-io-control-codes"></a>静止画像 USB I/O 制御コード





次の表では、すべて USB バス静止画像カーネル モード ドライバーによって認識される I/O 制御コードの記述と。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>I/O 制御コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_cancel_io" data-raw-source="[&lt;strong&gt;IOCTL_CANCEL_IO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_cancel_io)"><strong>IOCTL_CANCEL_IO</strong></a></p></td>
<td><p>指定された USB 転送パイプでアクティビティをキャンセルします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_channel_align_rqst)"><strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a></p></td>
<td><p>読み取り、書き込み、および割り込み転送パイプの USB デバイスの最大パケット サイズを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_device_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_device_descriptor)"><strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>返しますベンダーとデバイスの id。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_pipe_configuration)"><strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>デバイスのサポートされているすべての転送パイプの説明を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_usb_descriptor" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_usb_descriptor)"><strong>IOCTL_GET_USB_DESCRIPTOR</strong></a></p></td>
<td><p>指定された USB 記述子を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_version" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_get_version)"><strong>IOCTL_GET_VERSION</strong></a></p></td>
<td><p>ドライバーのバージョン番号を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_read_registers" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_read_registers)"><strong>IOCTL_READ_REGISTERS</strong></a></p></td>
<td><p>コントロールのパイプを使用して、USB デバイス レジスタから読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_reset_pipe" data-raw-source="[&lt;strong&gt;IOCTL_RESET_PIPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_reset_pipe)"><strong>IOCTL_RESET_PIPE</strong></a></p></td>
<td><p>指定した USB 転送パイプをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_send_usb_request" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_send_usb_request)"><strong>IOCTL_SEND_USB_REQUEST</strong></a></p></td>
<td><p>コントロール パイプを使って、USB デバイスにベンダー定義の要求を送信し、必要に応じて送信または追加データを受信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SET_TIMEOUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_set_timeout)"><strong>IOCTL_SET_TIMEOUT</strong></a></p></td>
<td><p>USB 一括 IN、OUT、一括または割り込みパイプへのアクセスのタイムアウト値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_wait_on_device_event" data-raw-source="[&lt;strong&gt;IOCTL_WAIT_ON_DEVICE_EVENT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_wait_on_device_event)"><strong>IOCTL_WAIT_ON_DEVICE_EVENT</strong></a></p></td>
<td><p>USB の割り込みパイプで発生するイベントに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_write_registers" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbscan/ni-usbscan-ioctl_write_registers)"><strong>IOCTL_WRITE_REGISTERS</strong></a></p></td>
<td><p>コントロールのパイプを使用して、USB デバイス レジスタを書き込みます。</p></td>
</tr>
</tbody>
</table>

 

これらのコードが定義されている*usbscan.h*します。 これらの I/O 制御の詳細についてはコードを参照してください。

[USB 静止画像 I/O 制御コードします。](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_image/index)

 

 




