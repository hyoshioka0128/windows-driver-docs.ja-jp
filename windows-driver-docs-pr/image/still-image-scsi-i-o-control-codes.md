---
title: 静止画像 SCSI I/O 制御コード
description: 静止画像 SCSI I/O 制御コード
ms.assetid: 8db15071-61ac-4bb3-9193-da854a15f376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fcdd2b9af03e348b66404cc8cf7928301a4e7e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371922"
---
# <a name="still-image-scsi-io-control-codes"></a>静止画像 SCSI I/O 制御コード





次の表は、一覧表示し、すべての SCSI バスの静止画像カーネル モード ドライバーによって認識される I/O 制御コードを記述します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd)"><strong>IOCTL_SCSISCAN_CMD</strong></a></p></td>
<td><p>カスタマイズされた SCSI コントロール記述子ブロックを作成し、SCSI バスの静止画像カーネル モード ドライバーに送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a></p></td>
<td><p>デバイス情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_LOCKDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice)"><strong>IOCTL_SCSISCAN_LOCKDEVICE</strong></a></p></td>
<td><p>Microsoft で使用するために予約されています。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_SET_TIMEOUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout)"><strong>IOCTL_SCSISCAN_SET_TIMEOUT</strong></a></p></td>
<td><p>デバイスにアクセスするときに、SCSI バスのカーネル モードの静止イメージ ドライバーによって使用されるタイムアウト値を変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_UNLOCKDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice)"><strong>IOCTL_SCSISCAN_UNLOCKDEVICE</strong></a></p></td>
<td><p>Microsoft で使用するために予約されています。</p></td>
</tr>
</tbody>
</table>

 

これらのコードが定義されている*scsiscan.h*します。

 

 




