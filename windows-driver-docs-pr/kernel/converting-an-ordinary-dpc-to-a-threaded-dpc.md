---
title: 通常の DPC からスレッド DPC への変換
description: 通常の DPC からスレッド DPC への変換
ms.assetid: 89a7a408-e01b-4543-9775-5ef542d05b75
keywords:
- スレッド Dpc WDK のカーネル
- 変換 (Dpc を)
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c924affbb4d81c416c79731468e84250c277ac7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828476"
---
# <a name="converting-an-ordinary-dpc-to-a-threaded-dpc"></a>通常の DPC からスレッド DPC への変換





通常の DPC をスレッド DPC に変換するのは簡単です。 (DPC を初期化する) [**Keinitializer Edpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializedpc)への呼び出しを1つの[**KeInitializeThreadedDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializethreadeddpc)に置き換え、次の表を参照して、スピンロックの取得と解放を行う dpc ルーチン内の呼び出しを置き換えます。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)"><strong>KeAcquireSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))"><strong>KeAcquireSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)"><strong>KeReleaseSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc)"><strong>KeReleaseSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockAtDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockAtDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85)" data-raw-source="[&lt;strong&gt;KeAcquireInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))"><strong>KeAcquireInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockFromDpcLevel&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)"><strong>KeReleaseInStackQueuedSpinLockFromDpcLevel</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc" data-raw-source="[&lt;strong&gt;KeReleaseInStackQueuedSpinLockForDpc&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)"><strong>KeReleaseInStackQueuedSpinLockForDpc</strong></a></p></td>
</tr>
</tbody>
</table>

 

[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)や[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))など、他のスピンロックルーチンの呼び出しを変更する必要はありません。

 

 




