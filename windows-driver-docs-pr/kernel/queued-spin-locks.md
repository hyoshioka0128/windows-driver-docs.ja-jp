---
title: キューを使用するスピン ロック
description: キューを使用するスピン ロック
ms.assetid: 7ccec366-5436-4e69-9fb7-f0090cf2adcb
keywords:
- スピン ロック WDK カーネルをキューに登録
- 最初は先着スピン ロック WDK カーネル
- KeAcquireInStackQueuedSpinLock
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58bbf93eea990f4faad80174daf554af592a773a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378772"
---
# <a name="queued-spin-locks"></a>キューを使用するスピン ロック





*スピン ロックをキューに置かれた*はマルチプロセッサ コンピューターでのロックの競合が増加の方が効率的なスピン ロックの一種です。 マルチプロセッサ コンピューターで、キューに置かれたスピンを使用してプロセッサが 1 つ目は先着ごとに、スピン ロックを取得することの保証をロックします。 Windows XP および Windows の以降のバージョン用のドライバーでは、通常のスピン ロックではなくキューに置かれたスピン ロックを使用する必要があります。

ドライバーは、スピン ロックのストレージを提供しで初期化[ **KeInitializeSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)します。 ドライバーを使用して[ **KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85)) 、キューに置かれたスピン ロックを取得し、 [ **KeReleaseInStackQueuedSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)解放します。

ドライバーを割り当てます、 [ **KLOCK\_キュー\_処理**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体を指すポインターにより渡される**KeAcquireInStackQueuedSpinLock**します。 ドライバーでは、同じ構造を渡すを指すポインターにより**KeReleaseInStackQueuedSpinLock**スピン ロックを解放する場合。 ドライバーは、ロックを取得するたびに、スタックにある構造体を通常割り当てる必要があります。

ドライバーでは、キューに置かれたスピン ロックのルーチンは、通常への呼び出しを混在させないこと**Ke*Xxx*スピンロック**で同じルーチン スピン ロックします。

ドライバーが既に IRQL である場合は、ディスパッチを =\_呼び出すことができます、レベル[ **KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))と[ **KeReleaseInStackQueuedSpinLockFromDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)代わりにします。

 

 




