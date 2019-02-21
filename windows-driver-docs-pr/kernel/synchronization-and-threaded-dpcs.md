---
title: 同期とスレッド Dpc
description: 同期とスレッド Dpc
ms.assetid: b4f2c77b-226c-4229-bcbb-5eebabdc28a4
keywords:
- スレッドの Dpc WDK カーネル
- 同期の WDK カーネル、割り込み
- スピン ロック WDK カーネルをキューに登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43c99ddab8dde7102ad0ab4fc8d6762c5b4f1709
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532340"
---
# <a name="synchronization-and-threaded-dpcs"></a>同期とスレッド Dpc





内外の両方の内部からアクセスするメモリ位置へのアクセスを同期する、 [ *CustomThreadedDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff542976) 、日常的なドライバーを通常スピン ロックを使用してまたはスピン ロックをキューに登録します。 ドライバーが正しく IRQL で同期する特定の規則に従う必要がありますこれを行うときに = パッシブ\_レベルおよび IRQL = ディスパッチ\_レベル、ため、 *CustomThreadedDpc*ルーチンは、両方の Irql が実行できます。

通常のスピン ロックでは、次の規則が適用されます。

-   ドライバーを呼び出すことができますを取得し、スピン ロックを解除、 [ **KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)と[ **KeReleaseSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553145)内外からと外側、 *CustomThreadedDpc*ルーチン。

-   ドライバーが呼び出せる[ **KeAcquireSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff551923)と[ **KeReleaseSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553148)から内で、 *CustomThreadedDpc*ルーチン。 なお、 *CustomThreadedDpc*ルーチンを呼び出してはならない[ **KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)または[ **KeReleaseSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553150)、これらのルーチンは、IRQL でのみ安全に呼び出すことがあるためディスパッチ =\_レベル。

キューに置かれたスピン ロックの規則に似ています。

-   ドライバーを呼び出すことができますを取得し、スピン ロックを解放、 [ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)と[ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130)の内部と外部両方から、 *CustomThreadedDpc*ルーチン。

-   ドライバーが呼び出せる[ **KeAcquireInStackQueuedSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff551912)と[ **KeReleaseInStackQueuedSpinLockForDpc** ](https://msdn.microsoft.com/library/windows/hardware/ff553133)から内で、*CustomThreadedDpc*ルーチン。 なお、 *CustomThreadedDpc*ルーチンを呼び出してはならない[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551908)または[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)、これらのルーチンは、IRQL でのみ安全に呼び出すことがあるためディスパッチ =\_レベル。

**KeAcquireSpinLockForDpc**と**KeAcquireInStackQueuedSpinLockForDpc**ディスパッチで呼び出されたときに、IRQL をリセットしない\_レベルが高速に実行よりも**KeAcquireSpinLock**と**KeAcquireInStackQueuedSpinLock**、それぞれします。

スピン ロックについての詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

 

 




