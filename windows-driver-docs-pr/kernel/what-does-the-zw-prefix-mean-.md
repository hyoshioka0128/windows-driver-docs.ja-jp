---
title: Zw プレフィックスの意味
description: Zw プレフィックスの意味
ms.assetid: 9529cce9-9c46-4906-854d-d0aef9118a90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6125ce1094d6b97c35f089b0ab66defb8ace2106
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835760"
---
# <a name="what-does-the-zw-prefix-mean"></a>Zw プレフィックスの意味


Windows ネイティブシステムサービスルーチンには、プレフィックス**Nt**と**Zw**で始まる名前が付いています。 **Nt**プレフィックスは Windows Nt の省略形ですが、 **Zw**プレフィックスは意味がありません。 **Zw**は、他の api との名前の競合の可能性を回避するために一部選択されています。また、将来的に必要になる可能性のある2文字のプレフィックスを使用しないようにしました。

[Windows ドライバーのサポートルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)の多くは、2文字または3文字のプレフィックスで始まる名前を持っています。 これらのプレフィックスは、どのカーネルモードシステムコンポーネントがルーチンを実装しているかを示します。 次の表に例をいくつか示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>プレフィックス</th>
<th>カーネルコンポーネント</th>
<th>ルーチンの例</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Cm</strong></p></td>
<td><p>構成マネージャー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex" data-raw-source="[&lt;strong&gt;CmRegisterCallbackEx&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)"><strong>Cmregisterの例</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>エックス</strong></p></td>
<td><p>責任</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool" data-raw-source="[&lt;strong&gt;ExAllocatePool&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepool)"><strong>ExAllocatePool</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Hal.dll</strong></p></td>
<td><p>ハードウェアアブストラクションレイヤー</p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)" data-raw-source="[&lt;strong&gt;HalGetAdapter&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff546644(v=vs.85))"><strong>HalGetAdapter</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Io</strong></p></td>
<td><p>I/o マネージャー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)"><strong>IoAllocateIrp</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ke</strong></p></td>
<td><p>カーネルコア</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)"><strong>KeSetEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>297</strong></p></td>
<td><p>メモリマネージャー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunlockpages)"><strong>MmUnlockPages</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ob</strong></p></td>
<td><p>オブジェクトマネージャー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)"><strong>Obreferenceobject へ</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Po</strong></p></td>
<td><p>電源マネージャー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate" data-raw-source="[&lt;strong&gt;PoSetPowerState&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)"><strong>PoSetPowerState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>メモリ</strong></p></td>
<td><p>トランザクションマネージャー</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmcommittransaction" data-raw-source="[&lt;strong&gt;TmCommitTransaction&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-tmcommittransaction)"><strong>TmCommitTransaction</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Nt</strong>と<strong>Zw</strong></p></td>
<td><p>ネイティブシステムサービス</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157250" data-raw-source="[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)">Ntcreatefile</a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)"> <strong>zwcreatefile</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




