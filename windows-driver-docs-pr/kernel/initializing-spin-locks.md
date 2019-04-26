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
ms.openlocfilehash: 13a8d9c1b1a861209ee36b5d80865fc93d81107e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341084"
---
# <a name="initializing-spin-locks"></a>スピン ロックの初期化





呼び出し元が指定の executive スピン ロックへのアクセスを必要とする任意のサポート ルーチンを呼び出す前に、ドライバーを呼び出す必要があります[ **KeInitializeSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff552160)を対応する executive スピン ロックを初期化します。 初期化された executive スピン ロックを必要とするサポート ルーチンを以下に示します。

- [**KeAcquireSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551917)し、続いて[ **KeReleaseSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553145)

- [**KeAcquireSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551921)し、続いて[ **KeReleaseSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553150)

- [**KeAcquireInStackQueuedSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff551899)し、続いて[ **KeReleaseInStackQueuedSpinLock**](https://msdn.microsoft.com/library/windows/hardware/ff553130)

- [**KeAcquireInStackQueuedSpinLockAtDpcLevel** ](https://msdn.microsoft.com/library/windows/hardware/ff551908)し、続いて[ **KeReleaseInStackQueuedSpinLockFromDpcLevel**](https://msdn.microsoft.com/library/windows/hardware/ff553137)

- **ExInterlocked * Xxx*** ルーチン

呼び出しの前に[ **IoConnectInterrupt** ](https://msdn.microsoft.com/library/windows/hardware/ff548371)と[ **KeSynchronizeExecution**](https://msdn.microsoft.com/library/windows/hardware/ff553302)、最下位レベルのドライバーを呼び出す必要があります[**KeInitializeSpinLock** ](https://msdn.microsoft.com/library/windows/hardware/ff552160)ストレージを提供する割り込みスピン ロックを初期化します。

 

 




