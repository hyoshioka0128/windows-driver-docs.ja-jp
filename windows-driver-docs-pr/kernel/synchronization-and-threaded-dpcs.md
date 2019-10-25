---
title: 同期とスレッド DPC
description: 同期とスレッド DPC
ms.assetid: b4f2c77b-226c-4229-bcbb-5eebabdc28a4
keywords:
- スレッド Dpc WDK のカーネル
- 同期 WDK カーネル、割り込み
- キューに置かれたスピンロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89bc7f1685dafc0972c552dc4af28aaa45f2c8bc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838397"
---
# <a name="synchronization-and-threaded-dpcs"></a>同期とスレッド DPC





[*CustomThreadedDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542976)ルーチンの内部および外部からアクセスされるメモリ位置へのアクセスを同期するために、ドライバーは通常のスピンロックまたはキューに置かれたスピンロックを使用できます。 この場合、 *CustomThreadedDpc*ルーチンは両方の IRQLs で実行できるため、ドライバーは、IRQL = パッシブ\_レベルおよび IRQL = ディスパッチ\_レベルで正しく同期するために、特定の規則に従う必要があります。

通常のスピンロックでは、次の規則が適用されます。

-   スピンロックを取得して解放するために、ドライバーは、 *CustomThreadedDpc*ルーチンの内部と外部の両方から[**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)と[**KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)を呼び出すことができます。

-   ドライバーは、 *CustomThreadedDpc*ルーチン内から[**KeAcquireSpinLockForDpc**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))と[**KeReleaseSpinLockForDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfordpc)を呼び出すことができます。 *CustomThreadedDpc*ルーチンは[**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)または[**KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)を呼び出すことができないことに注意してください。これらのルーチンは、IRQL = DISPATCH\_レベルでのみ呼び出すことができるためです。

キューに置かれたスピンロックのルールは次のようになります。

-   スピンロックを取得して解放するために、ドライバーは、 *CustomThreadedDpc*ルーチンの内部と外部の両方から[**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))と[**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)を呼び出すことができます。

-   ドライバーは、 *CustomThreadedDpc*ルーチン内から[**KeAcquireInStackQueuedSpinLockForDpc**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))と[**KeReleaseInStackQueuedSpinLockForDpc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)を呼び出すことができます。 *CustomThreadedDpc*ルーチンは[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))または[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)を呼び出すことができないことに注意してください。これらのルーチンは、IRQL =\_DISPATCH でのみ呼び出すことができます。平準.

**KeAcquireSpinLockForDpc**と**KeAcquireInStackQueuedSpinLockForDpc**はディスパッチ\_レベルで呼び出されると IRQL をリセットしないため、 **KeAcquireSpinLock**と KeAcquireInStackQueuedSpinLock よりも高速に実行されます。それぞれ。

スピンロックの詳細については、「[スピンロック](spin-locks.md)」を参照してください。

 

 




