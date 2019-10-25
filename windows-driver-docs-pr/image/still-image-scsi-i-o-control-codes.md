---
title: 静止画像 SCSI I/O 制御コード
description: 静止画像 SCSI I/O 制御コード
ms.assetid: 8db15071-61ac-4bb3-9193-da854a15f376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a84993c6149d9b614936fe9ccae94b7f7b3dadd8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840744"
---
# <a name="still-image-scsi-io-control-codes"></a>静止画像 SCSI I/O 制御コード





次の表は、SCSI バス用のカーネルモードのイメージドライバーで認識されるすべての i/o 制御コードを示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>I/o 制御コード</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd)"><strong>IOCTL_SCSISCAN_CMD</strong></a></p></td>
<td><p>カスタマイズされた SCSI コントロール記述子ブロックを作成し、SCSI バス用のカーネルモードのイメージドライバーに送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a></p></td>
<td><p>デバイス情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_LOCKDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_lockdevice)"><strong>IOCTL_SCSISCAN_LOCKDEVICE</strong></a></p></td>
<td><p>Microsoft が使用するために予約されています。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_SET_TIMEOUT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_set_timeout)"><strong>IOCTL_SCSISCAN_SET_TIMEOUT</strong></a></p></td>
<td><p>デバイスにアクセスするときに、SCSI バスのカーネルモード静止イメージドライバーで使用されるタイムアウト値を変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_UNLOCKDEVICE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/scsiscan/ni-scsiscan-ioctl_scsiscan_unlockdevice)"><strong>IOCTL_SCSISCAN_UNLOCKDEVICE</strong></a></p></td>
<td><p>Microsoft が使用するために予約されています。</p></td>
</tr>
</tbody>
</table>

 

これらのコードは*scsiscan*で定義されています。

 

 




