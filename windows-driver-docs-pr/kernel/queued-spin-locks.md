---
title: キューに置かれたスピン ロック
description: キューに置かれたスピン ロック
ms.assetid: 7ccec366-5436-4e69-9fb7-f0090cf2adcb
keywords:
- スピン ロック WDK カーネルをキューに登録
- 最初は先着スピン ロック WDK カーネル
- KeAcquireInStackQueuedSpinLock
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bce42cba22d0ba89839cc8db85d02dedf144ae5f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530994"
---
# <a name="queued-spin-locks"></a>キューに置かれたスピン ロック





*スピン ロックをキューに置かれた*はマルチプロセッサ コンピューターでのロックの競合が増加の方が効率的なスピン ロックの一種です。 マルチプロセッサ コンピューターで、キューに置かれたスピンを使用してプロセッサが 1 つ目は先着ごとに、スピン ロックを取得することの保証をロックします。 Windows XP および Windows の以降のバージョン用のドライバーでは、通常のスピン ロックではなくキューに置かれたスピン ロックを使用する必要があります。

ドライバーは、スピン ロックのストレージを提供しで初期化[ **KeInitializeSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff552160)します。 ドライバーを使用して[ **KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899) 、キューに置かれたスピン ロックを取得し、 [ **KeReleaseInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff553130)解放します。

ドライバーを割り当てます、 [ **KLOCK\_キュー\_処理**](https://msdn.microsoft.com/library/windows/hardware/ff554247)構造体を指すポインターにより渡される**KeAcquireInStackQueuedSpinLock**します。 ドライバーでは、同じ構造を渡すを指すポインターにより**KeReleaseInStackQueuedSpinLock**スピン ロックを解放する場合。 ドライバーは、ロックを取得するたびに、スタックにある構造体を通常割り当てる必要があります。

ドライバーでは、キューに置かれたスピン ロックのルーチンは、通常への呼び出しを混在させないこと**Ke*Xxx*スピンロック**で同じルーチン スピン ロックします。

ドライバーが既に IRQL である場合は、ディスパッチを =\_呼び出すことができます、レベル[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551908)と[ **KeReleaseInStackQueuedSpinLockFromDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff553137)代わりにします。

 

 




