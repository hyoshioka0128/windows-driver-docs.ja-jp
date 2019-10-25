---
title: キューを使用するスピン ロック
description: キューを使用するスピン ロック
ms.assetid: 7ccec366-5436-4e69-9fb7-f0090cf2adcb
keywords:
- キューに置かれたスピンロック WDK カーネル
- 初回提供のスピンロック WDK カーネル
- KeAcquireInStackQueuedSpinLock
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: eab4518863f437a054f4a16ef81727f8ac1306aa
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838480"
---
# <a name="queued-spin-locks"></a>キューを使用するスピン ロック





*キューに置かれたスピンロック*は、マルチプロセッサコンピューターでの競合の多いロックに対して効率的なスピンロックの一種です。 マルチプロセッサコンピューターでは、キューに置かれたスピンロックを使用することで、プロセッサが最初に提供されるスピンロックを取得することが保証されます。 Windows XP 以降のバージョンの Windows のドライバーでは、通常のスピンロックではなく、キューに置かれたスピンロックを使用する必要があります。

ドライバーは、スピンロックのストレージを提供し、 [**keinitializer の Inlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)で初期化します。 ドライバーは、 [**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))を使用して、キューに置かれたスピンロックを取得し、 [**KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)を解放します。

ドライバーは、 **KeAcquireInStackQueuedSpinLock**へのポインターによって渡される[ **\_キュー\_ハンドル**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)構造体を割り当てます。 ドライバーは、スピンロックを解除するときに、 **KeReleaseInStackQueuedSpinLock**へのポインターによって同じ構造体を渡します。 通常、ドライバーは、ロックを取得するたびに、スタックに構造体を割り当てます。

ドライバーは、同じスピンロックで、キューに置かれたスピンロックルーチンと通常の**Ke*Xxx*スピン**ロックのルーチンの呼び出しを混在させることはできません。

ドライバーが既に IRQL = ディスパッチ\_レベルにある場合は、代わりに[**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))と[**KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)を呼び出すことができます。

 

 




