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
ms.openlocfilehash: 5abed19a2fc7f9095afbd5e0831460123496f494
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386615"
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

マルチプロセッサ システムでは、他の問題がこのコード フラグメントにあります。 エントリのこのルーチンが (右側に操作する) の所有権を前提としています。 この IRP します。 ルーチンを保存すると、 **Irp**グローバル構造にあるポインター**拡張機能 -&gt;WaitEventIrp**、別のスレッドは IRP アドレスはそのグローバル構造体から取得し、操作を実行IRP します。 この問題を防ぐためには、ドライバーは IRP が保留中の前にマーク IRP を保存し、への呼び出しを含める必要があります[ **IoMarkIrpPending** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iomarkirppending)と、インタロックされたシーケンスの割り当て。 A [*キャンセル*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel) IRP のルーチンは、必要な場合があります。

 

 




