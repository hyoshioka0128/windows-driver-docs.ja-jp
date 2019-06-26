---
title: 共有している状態情報へのアクセス
description: 共有している状態情報へのアクセス
ms.assetid: f3e5ac07-cab1-4f66-90e4-88b2e28079a5
keywords:
- クリティカル セクション ルーチン WDK カーネル
- タイマー カウンター WDK カーネル
- 共有状態情報の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8a3a21892aaba925d4987de51317c6d800cbe77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363448"
---
# <a name="accessing-shared-state-information"></a>共有している状態情報へのアクセス





次の一般的なガイドラインを使用して、設計および作成の[ *SynchCritSection* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ksynchronize_routine)状態を維持するルーチン。

-   ドライバーのルーチンを呼び出す必要がありますにもアクセス ISR データにアクセスする、 *SynchCritSection*ルーチン。 非クリティカル セクションのコードが中断されることができます。 Isr を特定の実行 DIRQL とスピン ロックを取得するために、isr を特定のアクセスも、データを保護するスピン ロックの取得を単純にするのに十分ではありません ([**KeAcquireSpinLock**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-keacquirespinlock)) のみを IRQL を発生させます。ディスパッチ\_レベル、割り込みを現在のプロセッサで ISR を呼び出します。

-   付けます*SynchCritSection*状態情報を担当して個別の状態変数のセットを保持するルーチン。 つまり、書き込みを回避する*SynchCritSection*重複を維持するルーチンに状態情報。

    これにより、競合、および場合によって競合状態、間*SynchCritSection*ルーチン (および ISR) がアクセスしようとしました。 状態を同時にします。

    これにより、各*SynchCritSection*ルーチンを返します制御可能な限り早くため、1 つ*SynchCritSection*ルーチンが同じ状態の一部を更新する別の待つ必要はありませんコントロールが返される情報。

-   1 つの大規模で汎用の書き込みを回避*SynchCritSection*ルーチンが実際に有用な処理よりも処理を決定する条件の詳細をテストします。 その一方で、回避が多数ある*SynchCritSection*ことはありませんので、更新プログラムの状態情報の 1 バイトだけに条件付きステートメントを実行するルーチン。

-   すべて*SynchCritSection*ルーチン返す必要があります制御可能な限り、早く実行しているため、 *SynchCritSection*ルーチンが、ドライバーの ISR 実行されないようにします。

タイマー カウンターでは、デバイスの拡張機能を維持するための手法を次に示します。 ドライバーは、I/O 操作がタイムアウトしてかどうかを決定するカウンターを使用するものとします。また、ドライバーには、I/O 操作が重複するいないとします。

-   ドライバーの[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンが I/O 要求ごとにカウンターをいくつかの初期値、タイマーを初期化します。 ドライバーの場合、デバイスのタイムアウト値に 2 つ目が追加されます、 [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチンにコントロールが返されるだけです。

-   ドライバーの ISR から 1 を引いたにこのタイマー カウンターを設定する必要があります。

-   ドライバーの[ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチンは time カウンタを読み取って、かどうか、ISR は既に設定してから 1 を引いたを決定する毎秒 1 回呼び出されます。 ない場合、 *IoTimer*ルーチンをデクリメントを使用して、カウンター [ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出す、SynchCritSection\_1 ルーチン。

    場合は、カウンターが、要求がタイムアウトしたことを示す 0 に、SynchCritSection\_1 ルーチンの呼び出しを SynchCritSection\_デバイスのリセット操作をプログラムする 2 つのルーチンです。 1 つのカウンターがの場合、 [ *IoTimer* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_timer_routine)ルーチンを単純に返します。

-   場合、ドライバーの[ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチンが部分的な転送操作を開始するデバイスを再設定する必要があります、として、タイマー カウンターを再初期化する必要がありますが、 [ *StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)ルーチンでした。

    [ *DpcForIsr* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_dpc_routine)ルーチンも使用する必要があります[ **KeSynchronizeExecution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesynchronizeexecution)を呼び出す、SynchCritSection\_2 ルーチンは、SynchCritSection 可能性がありますまたは\_転送操作をもう 1 つのデバイスのプログラミングの 3 つのルーチンです。

ドライバーでは、このシナリオでは 1 つ以上*SynchCritSection* 、それぞれ独立した、特定の責任; そのタイマー カウンターを維持するために 1 つと 1 つ以上他のユーザー、デバイスのプログラミング ルーチンです。 各*SynchCritSection*ルーチンを返せるコントロール迅速に、1 つの個別のタスクを実行するためです。

ドライバーは 1 つ SynchCritSection\_1 ルーチンは、ドライバーの ISR、と共にタイマー カウンターに状態を保持します。 したがって、いくつかの間で、タイマー カウンターへのアクセスの競合がない*SynchCritSection*ルーチンと ISR

 

 




