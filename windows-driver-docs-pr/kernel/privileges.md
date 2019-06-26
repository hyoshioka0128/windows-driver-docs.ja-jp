---
title: 権限
description: 権限
ms.assetid: 15deec90-73a3-4443-90b7-de4ec9673169
keywords:
- WDK のオブジェクトの権限
- プロセスの特権 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 383775111031460620f0a1bba0903787b42e6016
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378831"
---
# <a name="privileges"></a>権限


A*特権*はオブジェクトではなく、プロセスに関連付けされる権限。 特権の典型的な例は**SeBackupPrivilege**ディスク上のファイルをバックアップする権限のプロセスですが。

いくつかのルーチンでは、操作を完了する前に、現在のプロセスの特権を確認します。 ドライバーのルーチンは、システム プロセスによって実行される、常に操作が成功が、ドライバーのルーチンは、必要な特権がないユーザー プロセスで実行する場合、操作は失敗します。

次の表では、特権と成功することが必要になるルーチンの例を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Privilege</th>
<th>特権が必要になるルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SeManageVolumePrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntsetinformationfile)"><strong>ZwSetInformationFile</strong></a> with <em>FileInformationClass</em> = <strong>FileValidDataLengthInformation</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>SeTakeOwnershipPrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SeSecurityPrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-seaccesscheck)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
</tbody>
</table>

 

システム ルーチンのほとんどでは、権限チェックは実行されません。

 

 




