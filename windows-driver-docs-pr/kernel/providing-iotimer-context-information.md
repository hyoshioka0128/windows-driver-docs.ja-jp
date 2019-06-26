---
title: IoTimer コンテキスト情報の提供
description: IoTimer コンテキスト情報の提供
ms.assetid: a92a7c3d-1602-430b-8ae1-c79bfc9ac7f9
keywords:
- IoTimer
- IoInitializeTimer
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 295097a5b7e5d8af76591b0497be86b558a0c535
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378792"
---
# <a name="providing-iotimer-context-information"></a>IoTimer コンテキスト情報の提供





*コンテキスト*にポインターが渡される[ **IoInitializeTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioinitializetimer)コンテキスト領域を識別する、他のドライバー ルーチンと[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)自体、ルーチンが時刻指定の操作に関する状態を保持できます。 I/O マネージャー パス、*コンテキスト*ポインターが呼び出されるたびに、 *IoTimer*ルーチン。

*IoTimer* IRQL でルーチンを実行 = ディスパッチ\_レベル、そのコンテキストの領域は、常駐システム容量のメモリ内にある必要があります。 持つほとんどのドライバー *IoTimer*ルーチンを使用して、[デバイス拡張機能](device-extensions.md)として関連付けられているデバイス オブジェクトの*コンテキスト*-アクセス可能な領域が、コンテキストはことの代わりになり、コント ローラーの拡張機能ドライバーを使用している場合、[コント ローラー オブジェクト](using-controller-objects.md)またはドライバーによって割り当てられた非ページ プール。

**これらのガイドラインに従う、** *IoTimer * * * ルーチンのコンテキストの領域。* *

-   場合、 *IoTimer*ルーチンでは、ドライバーの ISR とそのコンテキストの領域を共有、使用する必要がある必要があります[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出す、 [ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)ルーチンをマルチプロセッサ セーフ方式でコンテキストの領域にアクセスします。 詳細については、次を参照してください。[クリティカル セクションを使用して](using-critical-sections.md)します。

-   場合、 *IoTimer*ルーチンは ISR とそのコンテキストの領域を共有していないが、別のドライバーのルーチンで共有は、ドライバーがコンテキストにアクセスするために初期化された executive スピン ロックを共有コンテキストの領域を保護する必要がありますマルチプロセッサの安全な方法で情報。 詳細については、次を参照してください。[スピン ロック](spin-locks.md)します。

 

 




