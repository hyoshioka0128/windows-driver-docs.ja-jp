---
title: 静止画像 SCSI I/O 構造体
description: 静止画像 SCSI I/O 構造体
ms.assetid: 2cf17295-e3af-4109-bfdd-118aecf80bbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b29e25a911176defefcfde0d864fd332d91cfac8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63322216"
---
# <a name="still-image-scsi-io-structures"></a>静止画像 SCSI I/O 構造体





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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547972" data-raw-source="[&lt;strong&gt;SCSISCAN_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547972)"><strong>SCSISCAN_CMD</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542877" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542877)"> <strong>IOCTL_SCSISCAN_CMD</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff547981" data-raw-source="[&lt;strong&gt;SCSISCAN_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff547981)"><strong>SCSISCAN_INFO</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://msdn.microsoft.com/library/windows/desktop/aa363216" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/desktop/aa363216)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff542879" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff542879)"> <strong>IOCTL_SCSISCAN_GET_INFO</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造が定義されている*scsiscan.h*します。

 

 




