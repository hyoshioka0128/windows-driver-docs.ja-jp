---
title: 通常の DPC からスレッド DPC への変換
description: 通常の DPC からスレッド DPC への変換
ms.assetid: 89a7a408-e01b-4543-9775-5ef542d05b75
keywords:
- スレッドの Dpc WDK カーネル
- Dpc を変換します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05741c291337af537cec7e31cfa2e7be985e1d23
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377188"
---
# <a name="converting-an-ordinary-dpc-to-a-threaded-dpc"></a>通常の DPC からスレッド DPC への変換





スレッド DPC を通常の DPC に変換することは簡単です。 呼び出しを単純に置き換える[ **KeInitializeDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializedpc) (DPC 初期化) をいずれかで[ **KeInitializeThreadedDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializethreadeddpc)を参照してください次の表を取得およびスピン ロックを解放する DPC ルーチン内の呼び出しを置き換えます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)"><strong>KeAcquireSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))"><strong>KeAcquireSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)"><strong>KeReleaseSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfordpc)"><strong>KeReleaseSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)"><strong>KeReleaseInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
</tbody>
</table>

 

その他のスピン ロック ルーチンへの呼び出しを変更する必要はありません[ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)または[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)).

 

 




