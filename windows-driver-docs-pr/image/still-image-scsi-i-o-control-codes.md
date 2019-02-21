---
title: イメージ SCSI I/O 制御コードはまだ
description: イメージ SCSI I/O 制御コードはまだ
ms.assetid: 8db15071-61ac-4bb3-9193-da854a15f376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f22e6c97679b2dd4334e1f5733c1b06cc4d2b2a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556737"
---
# <a name="still-image-scsi-io-control-codes"></a>イメージ SCSI I/O 制御コードはまだ





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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542877" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542877)"><strong>IOCTL_SCSISCAN_CMD</strong></a></p></td>
<td><p>カスタマイズされた SCSI コントロール記述子ブロックを作成し、SCSI バスの静止画像カーネル モード ドライバーに送信します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542879" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542879)"><strong>IOCTL_SCSISCAN_GET_INFO</strong></a></p></td>
<td><p>デバイス情報を返します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542885" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_LOCKDEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542885)"><strong>IOCTL_SCSISCAN_LOCKDEVICE</strong></a></p></td>
<td><p>Microsoft で使用するために予約されています。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542886" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_SET_TIMEOUT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542886)"><strong>IOCTL_SCSISCAN_SET_TIMEOUT</strong></a></p></td>
<td><p>デバイスにアクセスするときに、SCSI バスのカーネル モードの静止イメージ ドライバーによって使用されるタイムアウト値を変更します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff542895" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_UNLOCKDEVICE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542895)"><strong>IOCTL_SCSISCAN_UNLOCKDEVICE</strong></a></p></td>
<td><p>Microsoft で使用するために予約されています。</p></td>
</tr>
</tbody>
</table>

 

これらのコードが定義されている*scsiscan.h*します。

 

 




