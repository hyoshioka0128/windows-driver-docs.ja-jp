---
title: ドライバーの状態の確認エラー
description: ドライバーの状態の確認エラー
ms.assetid: 963f79f6-2282-41bd-9cf4-bd5bc02a510e
keywords:
- 信頼性 WDK のカーネル ドライバーの状態を確認
- ドライバーの状態をチェック
- ドライバーの状態を確認
- ドライバーの状態を確認しています
- 正しいデバイス状態の WDK カーネル
- デバイスの状態の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06dbe787b4d97fbe17beb6972464de943f7b37f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360026"
---
# <a name="failure-to-check-a-drivers-state"></a>ドライバーの状態の確認エラー





次の例では、ドライバーを使用して、 **ASSERT**チェックのビルドで適切なデバイスの状態をチェックするマクロが無料のビルドでデバイス状態をチェックします。

```cpp
   case IOCTL_WAIT_FOR_EVENT:

      ASSERT((!Extension->WaitEventIrp));
      Extension->WaitEventIrp = Irp;
      IoMarkIrpPending(Irp);
      status = STATUS_PENDING;
```

チェックのビルドで、ドライバーが既に保留中、IRP を保持している場合、システムはアサートされます。 無料のビルドで、ただし、ドライバーが確認しないこのエラーの。 同じ IOCTL 原因、ドライバーが失われる 2 つの呼び出しは IRP を追跡します。

マルチプロセッサ システムでは、他の問題がこのコード フラグメントにあります。 エントリのこのルーチンが (右側に操作する) の所有権を前提としています。 この IRP します。 ルーチンを保存すると、 **Irp**グローバル構造にあるポインター**拡張機能 -&gt;WaitEventIrp**、別のスレッドは IRP アドレスはそのグローバル構造体から取得し、操作を実行IRP します。 この問題を防ぐためには、ドライバーは IRP が保留中の前にマーク IRP を保存し、への呼び出しを含める必要があります[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)と、インタロックされたシーケンスの割り当て。 A [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) IRP のルーチンは、必要な場合があります。

 

 




