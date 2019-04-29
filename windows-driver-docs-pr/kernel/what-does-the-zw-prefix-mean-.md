---
title: Zw プレフィックスを意味します。
description: Zw プレフィックスを意味します。
ms.assetid: 9529cce9-9c46-4906-854d-d0aef9118a90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e2e5aa0bdff701eb7eda6713a6fce120902b0697
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391433"
---
# <a name="what-does-the-zw-prefix-mean"></a>Zw プレフィックスの意味


Windows のネイティブ システム サービス ルーチンは、プレフィックスで始まる名前を持つ**Nt**と**Zw**します。 **Nt**プレフィックスは、Windows NT の省略形が、 **Zw**プレフィックスに意味がありません。 **Zw**他の Api を使用した潜在的な名前付けの競合を回避して、将来必要可能性がある、役立つ可能性のある 2 文字プレフィックスを使用しないように部分的に部分的に選択しました。

多くは、 [Windows ドライバー サポート ルーチン](https://msdn.microsoft.com/library/windows/hardware/ff544200)2 または 3 文字プレフィックスで始まる名前があります。 これらのプレフィックスは、カーネル モード システム コンポーネント、ルーチンの実装を示します。 次の表には、いくつかの例が含まれています。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>プレフィックス</th>
<th>カーネル コンポーネント</th>
<th>例のルーチン</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>cm</strong></p></td>
<td><p>Configuration Manager</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff541921" data-raw-source="[&lt;strong&gt;CmRegisterCallbackEx&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff541921)"><strong>CmRegisterCallbackEx</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>例:</strong></p></td>
<td><p>役員</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff544501" data-raw-source="[&lt;strong&gt;ExAllocatePool&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544501)"><strong>ExAllocatePool</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>hal</strong></p></td>
<td><p>ハードウェア アブストラクション レイヤー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff546596" data-raw-source="[&lt;strong&gt;HalGetAdapter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff546596)"><strong>HalGetAdapter</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Io</strong></p></td>
<td><p>I/O マネージャー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff548257" data-raw-source="[&lt;strong&gt;IoAllocateIrp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548257)"><strong>IoAllocateIrp</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ke</strong></p></td>
<td><p>カーネルのコア</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553253" data-raw-source="[&lt;strong&gt;KeSetEvent&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553253)"><strong>KeSetEvent</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>mm</strong></p></td>
<td><p>メモリ マネージャー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556381" data-raw-source="[&lt;strong&gt;MmUnlockPages&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556381)"><strong>MmUnlockPages</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Ob</strong></p></td>
<td><p>オブジェクト マネージャー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff558678" data-raw-source="[&lt;strong&gt;ObReferenceObject&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff558678)"><strong>ObReferenceObject</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Po</strong></p></td>
<td><p>電源マネージャー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff559765" data-raw-source="[&lt;strong&gt;PoSetPowerState&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff559765)"><strong>PoSetPowerState</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><strong>Tm</strong></p></td>
<td><p>トランザクション マネージャー</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564665" data-raw-source="[&lt;strong&gt;TmCommitTransaction&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564665)"><strong>TmCommitTransaction</strong></a></p></td>
</tr>
<tr class="even">
<td><p><strong>Nt</strong>と<strong>Zw</strong></p></td>
<td><p>ネイティブのシステム サービス</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=157250" data-raw-source="[NtCreateFile](https://go.microsoft.com/fwlink/p/?linkid=157250)">NtCreateFile</a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff566424" data-raw-source="[&lt;strong&gt;ZwCreateFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566424)"> <strong>ZwCreateFile</strong></a></p></td>
</tr>
</tbody>
</table>

 

 

 




