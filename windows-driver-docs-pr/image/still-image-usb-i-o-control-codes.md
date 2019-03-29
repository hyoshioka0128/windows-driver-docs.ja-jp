---
title: 静止画像 USB I/O 制御コード
description: 静止画像 USB I/O 制御コード
ms.assetid: 66a06a25-2fcb-4b14-85e2-485d2d4ac9d5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7af73ac8fd940d7222975b7d0d72225a8ecd9517
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348611"
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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542843" data-raw-source="[&lt;strong&gt;IOCTL_CANCEL_IO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542843)"><strong>IOCTL_CANCEL_IO</strong></a></p></td>
<td><p>指定された USB 転送パイプでアクティビティをキャンセルします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542849" data-raw-source="[&lt;strong&gt;IOCTL_GET_CHANNEL_ALIGN_RQST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542849)"><strong>IOCTL_GET_CHANNEL_ALIGN_RQST</strong></a></p></td>
<td><p>読み取り、書き込み、および割り込み転送パイプの USB デバイスの最大パケット サイズを返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542856" data-raw-source="[&lt;strong&gt;IOCTL_GET_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542856)"><strong>IOCTL_GET_DEVICE_DESCRIPTOR</strong></a></p></td>
<td><p>返しますベンダーとデバイスの id。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542859" data-raw-source="[&lt;strong&gt;IOCTL_GET_PIPE_CONFIGURATION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542859)"><strong>IOCTL_GET_PIPE_CONFIGURATION</strong></a></p></td>
<td><p>デバイスのサポートされているすべての転送パイプの説明を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542864" data-raw-source="[&lt;strong&gt;IOCTL_GET_USB_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542864)"><strong>IOCTL_GET_USB_DESCRIPTOR</strong></a></p></td>
<td><p>指定された USB 記述子を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542866" data-raw-source="[&lt;strong&gt;IOCTL_GET_VERSION&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542866)"><strong>IOCTL_GET_VERSION</strong></a></p></td>
<td><p>ドライバーのバージョン番号を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542869" data-raw-source="[&lt;strong&gt;IOCTL_READ_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542869)"><strong>IOCTL_READ_REGISTERS</strong></a></p></td>
<td><p>コントロールのパイプを使用して、USB デバイス レジスタから読み取ります。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542872" data-raw-source="[&lt;strong&gt;IOCTL_RESET_PIPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542872)"><strong>IOCTL_RESET_PIPE</strong></a></p></td>
<td><p>指定した USB 転送パイプをリセットします。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542900" data-raw-source="[&lt;strong&gt;IOCTL_SEND_USB_REQUEST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542900)"><strong>IOCTL_SEND_USB_REQUEST</strong></a></p></td>
<td><p>コントロール パイプを使って、USB デバイスにベンダー定義の要求を送信し、必要に応じて送信または追加データを受信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542908" data-raw-source="[&lt;strong&gt;IOCTL_SET_TIMEOUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542908)"><strong>IOCTL_SET_TIMEOUT</strong></a></p></td>
<td><p>USB 一括 IN、OUT、一括または割り込みパイプへのアクセスのタイムアウト値を設定します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542917" data-raw-source="[&lt;strong&gt;IOCTL_WAIT_ON_DEVICE_EVENT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542917)"><strong>IOCTL_WAIT_ON_DEVICE_EVENT</strong></a></p></td>
<td><p>USB の割り込みパイプで発生するイベントに関する情報を返します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542920" data-raw-source="[&lt;strong&gt;IOCTL_WRITE_REGISTERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542920)"><strong>IOCTL_WRITE_REGISTERS</strong></a></p></td>
<td><p>コントロールのパイプを使用して、USB デバイス レジスタを書き込みます。</p></td>
</tr>
</tbody>
</table>

 

これらのコードが定義されている*usbscan.h*します。 これらの I/O 制御の詳細についてはコードを参照してください。

[USB 静止画像 I/O 制御コードします。](https://msdn.microsoft.com/library/windows/hardware/ff548569)

 

 




