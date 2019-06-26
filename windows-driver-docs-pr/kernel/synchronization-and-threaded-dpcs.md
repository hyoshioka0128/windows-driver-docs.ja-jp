---
title: 同期とスレッド DPC
description: 同期とスレッド DPC
ms.assetid: b4f2c77b-226c-4229-bcbb-5eebabdc28a4
keywords:
- スレッドの Dpc WDK カーネル
- 同期の WDK カーネル、割り込み
- スピン ロック WDK カーネルをキューに登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78273ec2a8baf4a70098b662d45edb91c00bb3a4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385105"
---
# <a name="synchronization-and-threaded-dpcs"></a>同期とスレッド DPC





内外の両方の内部からアクセスするメモリ位置へのアクセスを同期する、 [ *CustomThreadedDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542976) 、日常的なドライバーを通常スピン ロックを使用してまたはスピン ロックをキューに登録します。 ドライバーが正しく IRQL で同期する特定の規則に従う必要がありますこれを行うときに = パッシブ\_レベルおよび IRQL = ディスパッチ\_レベル、ため、 *CustomThreadedDpc*ルーチンは、両方の Irql が実行できます。

通常のスピン ロックでは、次の規則が適用されます。

-   ドライバーを呼び出すことができますを取得し、スピン ロックを解除、 [ **KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)と[ **KeReleaseSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)内外からと外側、 *CustomThreadedDpc*ルーチン。

-   ドライバーが呼び出せる[ **KeAcquireSpinLockForDpc** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551923(v=vs.85))と[ **KeReleaseSpinLockForDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfordpc)から内で、 *CustomThreadedDpc*ルーチン。 なお、 *CustomThreadedDpc*ルーチンを呼び出してはならない[ **KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)または[ **KeReleaseSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)、これらのルーチンは、IRQL でのみ安全に呼び出すことがあるためディスパッチ =\_レベル。

キューに置かれたスピン ロックの規則に似ています。

-   ドライバーを呼び出すことができますを取得し、スピン ロックを解放、 [ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))と[ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)の内部と外部両方から、 *CustomThreadedDpc*ルーチン。

-   ドライバーが呼び出せる[ **KeAcquireInStackQueuedSpinLockForDpc** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551912(v=vs.85))と[ **KeReleaseInStackQueuedSpinLockForDpc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfordpc)から内で、*CustomThreadedDpc*ルーチン。 なお、 *CustomThreadedDpc*ルーチンを呼び出してはならない[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))または[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)、これらのルーチンは、IRQL でのみ安全に呼び出すことがあるためディスパッチ =\_レベル。

**KeAcquireSpinLockForDpc**と**KeAcquireInStackQueuedSpinLockForDpc**ディスパッチで呼び出されたときに、IRQL をリセットしない\_レベルが高速に実行よりも**KeAcquireSpinLock**と**KeAcquireInStackQueuedSpinLock**、それぞれします。

スピン ロックについての詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

 

 




