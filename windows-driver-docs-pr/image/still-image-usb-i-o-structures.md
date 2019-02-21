---
title: USB I/O 構造体を静止画像します。
description: USB I/O 構造体を静止画像します。
ms.assetid: d70c5c11-c8f2-4196-a7f5-d97ceef10ca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ffad556ddc7b2b202c7621b54d3ee7484749f26
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560199"
---
# <a name="still-image-usb-io-structures"></a>USB I/O 構造体を静止画像します。





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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539466" data-raw-source="[&lt;strong&gt;CHANNEL_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539466)"><strong>CHANNEL_INFO</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542849" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542849)"> <strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540576" data-raw-source="[&lt;strong&gt;DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540576)"><strong>DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542856" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542856)"> <strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541204" data-raw-source="[&lt;strong&gt;DRV_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541204)"><strong>DRV_VERSION</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542866" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542866)"> <strong>IOCTL_GET_VERSION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542924" data-raw-source="[&lt;strong&gt;IO_BLOCK&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542924)"><strong>IO_BLOCK</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542869" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542869)"> <strong>IOCTL_READ_REGISTERS</strong> </a>または<a href="https://msdn.microsoft.com/library/windows/hardware/ff542920" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542920)"> <strong>IOCTL_WRITE_REGISTERS</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542928" data-raw-source="[&lt;strong&gt;IO_BLOCK_EX&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542928)"><strong>IO_BLOCK_EX</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542900" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542900)"> <strong>IOCTL_SEND_USB_REQUEST</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548534" data-raw-source="[&lt;strong&gt;USBSCAN_GET_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548534)"><strong>USBSCAN_GET_DESCRIPTOR</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542864" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542864)"> <strong>IOCTL_GET_USB_DESCRIPTOR</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548541" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548541)"><strong>USBSCAN_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542859" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542859)"> <strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548547" data-raw-source="[&lt;strong&gt;USBSCAN_PIPE_INFORMATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548547)"><strong>USBSCAN_PIPE_INFORMATION</strong></a></p></td>
<td><p>静止画像デバイス用の USB 転送パイプの記述に使用します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548554" data-raw-source="[&lt;strong&gt;USBSCAN_TIMEOUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548554)"><strong>USBSCAN_TIMEOUT</strong></a></p></td>
<td><p>USB 一括と一括操作では、タイムアウト値を格納し、中断します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造が定義されている*usbscan.h*します。 詳細についてはこれらの構造体を参照してください。

[USB 静止画像構造体](https://msdn.microsoft.com/library/windows/hardware/ff548574)

 

 




