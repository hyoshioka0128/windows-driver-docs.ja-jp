---
title: 待機/ウェイク Irp の IoCompletion ルーチン
description: 待機/ウェイク Irp の IoCompletion ルーチン
ms.assetid: 61239398-2d37-4163-8128-7a4a0916a262
keywords:
- 受信側の待機またはスリープ解除 Irp
- 待機/ウェイク Irp WDK の電源管理の受信
- IoCompletion ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f2df22314f662f05957524c8da7e39890b00453
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558441"
---
# <a name="iocompletion-routines-for-waitwake-irps"></a>待機/ウェイク Irp の IoCompletion ルーチン





I/O マネージャーがドライバーの待機またはスリープ解除を呼び出す[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチン デバイス スタックの次の下位ドライバー待機/ウェイク IRP の完了後します。 各関数し、待機/ウェイク IRP がハンドルを設定する必要があります (FDO) ドライバーをフィルター処理、 *IoCompletion* IRP のルーチンです。

各関数またはフィルター ドライバーの設定、 *IoCompletion*処理時に、待機/ウェイク IRP デバイス スタックには、その方法で日常的な。 デバイスの電源ポリシー所有者、IRP を送信する場合がありますので、 *IoCompletion*コールバック ルーチンに加えルーチン。 後に呼び出されるコールバック ルーチンに注意してください、 *IoCompletion*ルーチンと 2 つに異なる要件があります。 詳細については、[待機/ウェイク コールバック ルーチン](wait-wake-callback-routines.md)を参照してください。

待機またはスリープ解除に必要なアクション*IoCompletion*ルーチンは、デバイスとドライバーの種類によって異なります。 次に、ドライバーは、その待機またはスリープ解除を実行する必要がありますアクション*IoCompletion*ルーチン。

1.  デバイスの拡張機能内の関連するフィールドをリセットします。 たとえば、待機/ウェイク IRP が保留中の場合は、ほとんどのドライバーは、フラグを設定し、デバイス拡張機能の IRP にポインターを保持すること。

2.  リセット、 [*キャンセル*](https://msdn.microsoft.com/library/windows/hardware/ff540742) IRP が呼び出すことによって、存在する場合は、ルーチン[ **IoSetCancelRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff549674)を指定して、 **NULL**ルーチンへのポインター。

3.  呼び出す**IoCompleteRequest**、IO を指定する\_いいえ\_IRP の完了をインクリメントします。

連続する各ドライバーでは、IRP が完了すると、I/O マネージャー通過コントロールを*IoCompletion*スタック上に戻って、次に高いドライバーの日常的な。

呼び出した後、 *IoCompletion*待機/ウェイク IRP デバイス スタックを渡されるときに、ドライバーによって設定のルーチンに渡されたコールバック ルーチンを呼び出すと I/O マネージャー [ **PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)ドライバー IRP を送信します。 詳細については、[待機/ウェイク コールバック ルーチン](wait-wake-callback-routines.md)を参照してください。

 

 




