---
title: 通常の DPC からスレッド DPC への変換
description: 通常の DPC からスレッド DPC への変換
ms.assetid: 89a7a408-e01b-4543-9775-5ef542d05b75
keywords:
- スレッドの Dpc WDK カーネル
- Dpc を変換します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1aa526289ef27c6f6e91bb0d6d66fc15aa49a198
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348249"
---
# <a name="converting-an-ordinary-dpc-to-a-threaded-dpc"></a>通常の DPC からスレッド DPC への変換





スレッド DPC を通常の DPC に変換することは簡単です。 呼び出しを単純に置き換える[ **KeInitializeDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff552130) (DPC 初期化) をいずれかで[ **KeInitializeThreadedDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552166)を参照してください次の表を取得およびスピン ロックを解放する DPC ルーチン内の呼び出しを置き換えます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>通常の DPC 呼び出し</th>
<th>対応するスレッド DPC 呼び出し</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551921" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockAtDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551921)"><strong>KeAcquireSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551923" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551923)"><strong>KeAcquireSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553150" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockFromDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553150)"><strong>KeReleaseSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553148" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553148)"><strong>KeReleaseSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551908" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551908)"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551912" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551912)"><strong>KeAcquireInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553137" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553137)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff553133" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff553133)"><strong>KeReleaseInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
</tbody>
</table>

 

その他のスピン ロック ルーチンへの呼び出しを変更する必要はありません[ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)または[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899).

 

 




