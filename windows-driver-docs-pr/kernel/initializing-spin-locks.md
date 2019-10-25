---
title: スピン ロックの初期化
description: スピン ロックの初期化
ms.assetid: 7ed27e43-4406-4e64-b2c9-42b8a883efdb
keywords:
- スピンロックの初期化
- スピンロック WDK カーネル
- Ke初期化の固定 Inlock
- executive スピンロック WDK カーネル
- 割り込みスピンロックの WDK カーネル
- キューに置かれたスピンロック WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 189beb3afabc77525658d99a913c1154ec159d63
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828290"
---
# <a name="initializing-spin-locks"></a>スピン ロックの初期化





呼び出し元から提供された executive スピンロックへのアクセスを必要とするサポートルーチンを呼び出す前に、ドライバーは[**keinitializer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)を呼び出して、対応する executive スピンロックを初期化する必要があります。 初期化された executive スピンロックを必要とするサポートルーチンには、次のようなものがあります。

- [**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)と、その後の[ **KeReleaseSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)

- [**KeAcquireSpinLockAtDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel)と、その後の[ **KeReleaseSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)

- [**KeAcquireInStackQueuedSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551899(v=vs.85))と、その後の[ **KeReleaseInStackQueuedSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlock)

- [**KeAcquireInStackQueuedSpinLockAtDpcLevel**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551908(v=vs.85))と、その後の[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleaseinstackqueuedspinlockfromdpclevel)

- **Exinterlocked ロック * Xxx*** ルーチン

[**Ioconnectinterrupt**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)と[**KeSynchronizeExecution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)を呼び出す前に、最下位レベルのドライバーで keinitializer が適用される[**inlock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializespinlock)を呼び出して、ストレージを提供する割り込みスピンロックを初期化する必要があります。

 

 




