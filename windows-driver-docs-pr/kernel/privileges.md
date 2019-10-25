---
title: 権限
description: 権限
ms.assetid: 15deec90-73a3-4443-90b7-de4ec9673169
keywords:
- 権限 WDK オブジェクト
- プロセス特権 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a9682cae3c6d012df4e4dd3d3c4f5ea79ba8fbd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827590"
---
# <a name="privileges"></a>権限


*特権*は、オブジェクトではなく、プロセスに関連付けられている権限です。 一般的な特権の例として、 **Sebackupprivilege**があります。これは、ディスク上のファイルをバックアップする権限をプロセスに与えます。

いくつかのルーチンは、操作を完了する前に現在のプロセスの特権をチェックします。 ドライバールーチンがシステムプロセスによって実行される場合、操作は常に成功しますが、必要な特権を持たないユーザープロセスによってドライバールーチンが実行されると、操作が失敗する可能性があります。

次の表に、成功するために必要な特権とルーチンの例をいくつか示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Privilege</th>
<th>特権を必要とするルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>SeManageVolumePrivilege</strong></p></td>
<td><p><em>Fileinformationclass</em> = <strong>FileValidDataLengthInformation</strong>を使用した<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile" data-raw-source="[&lt;strong&gt;ZwSetInformationFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntsetinformationfile)"><strong>zwsetinformationfile</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>SeTakeOwnershipPrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>SeSecurityPrivilege</strong></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck" data-raw-source="[&lt;strong&gt;SeAccessCheck&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-seaccesscheck)"><strong>SeAccessCheck</strong></a></p></td>
</tr>
</tbody>
</table>

 

ほとんどのシステムルーチンでは、特権チェックは実行されません。

 

 




