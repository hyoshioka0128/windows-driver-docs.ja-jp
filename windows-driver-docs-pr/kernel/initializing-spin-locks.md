---
title: スピン ロックの初期化
description: スピン ロックの初期化
ms.assetid: 7ed27e43-4406-4e64-b2c9-42b8a883efdb
keywords:
- スピン ロックの初期化
- スピン ロック WDK カーネル
- KeInitializeSpinLock
- executive スピン ロック WDK カーネル
- 割り込みスピン ロック WDK カーネル
- スピン ロック WDK カーネルをキューに登録
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ad9eee4f77a68f0d5e8e466b149a7805113bbe2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369785"
---
# <a name="initializing-spin-locks"></a>スピン ロックの初期化





呼び出し元が指定の executive スピン ロックへのアクセスを必要とする任意のサポート ルーチンを呼び出す前に、ドライバーを呼び出す必要があります[ **KeInitializeSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)を対応する executive スピン ロックを初期化します。 初期化された executive スピン ロックを必要とするサポート ルーチンを以下に示します。

- [**KeAcquireSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)し、続いて[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlock)

- [**KeAcquireSpinLockAtDpcLevel** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlockatdpclevel)し、続いて[ **KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleasespinlockfromdpclevel)

- [**KeAcquireInStackQueuedSpinLock** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))し、続いて[ **KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlock)

- [**KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))し、続いて[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)

- **ExInterlocked * Xxx*** ルーチン

呼び出しの前に[ **IoConnectInterrupt** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioconnectinterrupt)と[ **KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)、最下位レベルのドライバーを呼び出す必要があります[**KeInitializeSpinLock** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keinitializespinlock)ストレージを提供する割り込みスピン ロックを初期化します。

 

 




