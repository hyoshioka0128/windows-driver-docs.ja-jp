---
title: キャンセルおよび終了コードを同期します。
description: キャンセルおよび終了コードを同期します。
ms.assetid: 4c302fc5-cb14-46e5-80c8-8dbf62486905
keywords:
- 要求の WDK KMDF、キャンセル要求を処理します。
- I/O 要求のキャンセルの WDK KMDF
- WDK KMDF の同期
- WDK KMDF を要求する I/O の完了
- WDK KMDF、同期処理を要求します。
- I/O は、WDK KMDF、同期を要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bbd7a7fc72fca3d137c1ab605be0779a18da0c3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558055"
---
# <a name="synchronizing-cancel-and-completion-code"></a>キャンセルおよび終了コードを同期します。





ドライバーを呼び出す場合[ **WdfRequestMarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff549983)または[ **WdfRequestMarkCancelableEx** ](https://msdn.microsoft.com/library/windows/hardware/ff549984)する I/O 要求をキャンセル可能ながあります同期の問題の潜在的なです。 など、ドライバーとデバイスの方法では、非同期的にデバイス I/O 操作を実行可能性があります[ *EvtInterruptIsr* ](https://msdn.microsoft.com/library/windows/hardware/ff541735)と[ *EvtInterruptDpc*](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数、および、 *EvtInterruptDpc*と[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)コールバック関数が呼び出しを含む可能性があります[**WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)します。

ドライバーを呼び出す必要があります[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) 1 回だけするか、完了またはキャンセル要求。 しかし、 [ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)と[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)コールバック関数が、相互フレームワークと同期されていません。呼び出すことができますいずれか、その他の実行中にします。

簡単に、ドライバー、フレームワークを使用している場合は、この問題を回避する[自動同期](using-automatic-synchronization.md)自動同期により、コールバック関数が呼び出される 1 つずつためです。

使用できる場合は、ドライバーでは、framework の自動同期を使用しない[framework ロック](using-framework-locks.md)キャンセルおよび終了コードを同期します。

かどうか、ドライバーのフレームワークの自動同期が使用または独自同期化も、ドライバーを提供します[ *EvtRequestCancel* ](https://msdn.microsoft.com/library/windows/hardware/ff541817)コールバック関数を呼び出す必要があります[  **。WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)要求をキャンセルします。 ドライバーの[ *EvtInterruptDpc* ](https://msdn.microsoft.com/library/windows/hardware/ff541721)コールバック関数を呼び出す必要があります[ **WdfRequestUnmarkCancelable** ](https://msdn.microsoft.com/library/windows/hardware/ff550035)次のようにします。

```cpp
Status = WdfRequestUnmarkCancelable(Request);
if( Status != STATUS_CANCELLED ) {
    WdfRequestComplete(Request, RequestStatus);
    }
```

このコードにより、ドライバーは呼び出しません[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)ドライバーが既に呼び出されている要求をキャンセルする場合は、要求を完了します。

呼び出しには、ドライバーは従う必要があるときにルールの詳細については**WdfRequestUnmarkCancelable**を参照してください[ **WdfRequestUnmarkCancelable**](https://msdn.microsoft.com/library/windows/hardware/ff550035)します。

 

 





