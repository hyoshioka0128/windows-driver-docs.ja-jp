---
title: 静止画像 SCSI I/O 構造体
description: 静止画像 SCSI I/O 構造体
ms.assetid: 2cf17295-e3af-4109-bfdd-118aecf80bbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fdc0c612f0a9af57053b25faa205cdc26ca8b1fd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371918"
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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ns-scsiscan-_scsiscan_cmd" data-raw-source="[&lt;strong&gt;SCSISCAN_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ns-scsiscan-_scsiscan_cmd)"><strong>SCSISCAN_CMD</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_CMD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_cmd)"> <strong>IOCTL_SCSISCAN_CMD</strong></a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ns-scsiscan-_scsiscan_info" data-raw-source="[&lt;strong&gt;SCSISCAN_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ns-scsiscan-_scsiscan_info)"><strong>SCSISCAN_INFO</strong></a></p></td>
<td><p>パラメーターとして使用<a href="https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol" data-raw-source="[&lt;strong&gt;DeviceIoControl&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)"> <strong>DeviceIoControl</strong></a>ときに、指定した I/O 制御コードは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info" data-raw-source="[&lt;strong&gt;IOCTL_SCSISCAN_GET_INFO&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/scsiscan/ni-scsiscan-ioctl_scsiscan_get_info)"> <strong>IOCTL_SCSISCAN_GET_INFO</strong></a>します。</p></td>
</tr>
</tbody>
</table>

 

これらの構造が定義されている*scsiscan.h*します。

 

 




