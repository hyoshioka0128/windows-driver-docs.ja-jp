---
title: デッドロック - DRIVER_VERIFIER_DETECTED_VIOLATION (C4) をデバッグ 0x1001
description: Driver Verifier にスピン ロック階層違反、0x1001 のパラメーター 1 の値を持つ 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION をドライバー Verifiergenerates バグ チェックが検出した場合。
ms.assetid: 4C3ED1DB-5EDC-4386-B91C-CF86973EE1F6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3b49d9c51ca2141a12f518298bb56fd5505e94e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549729"
---
# <a name="span-iddevtestdebuggingdeadlocks-driververifierdetectedviolationc40x1001spandebugging-deadlocks---driververifierdetectedviolation-c4-0x1001"></a><span id="devtest.debugging_deadlocks_-_driver_verifier_detected_violation__c4___0x1001"></span>デッドロックのドライバーをデバッグ\_VERIFIER\_検出\_違反 (C4)。0x1001


ときに[Driver Verifier](driver-verifier.md) 、スピン ロック階層違反を検出、ドライバー Verifiergenerates [ **0xC4 のバグ チェック。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187) 0x1001 のパラメーター 1 の値。

デッドロック検出オプションがアクティブな場合 (デッドロック検出の Driver Verifier の標準オプションの一部)、 [Driver Verifier](driver-verifier.md)の割り当てられた各スピン ロックと順序を取得および解放を追跡します。 ロック階層の違反では、Driver Verifier の状況が検出されたことを意味を少なくとも 1 つの場合も、where、 *LockA*取得後、前に保持されている*LockB*は取得、および別の*LockB*取得後、前に保持されている*LockA*が必要です。

**重要な**たびに発生しますこのバグ チェック[Driver Verifier](driver-verifier.md)階層違反が発生したか、実際のデッドロックが発生しているときにない検出しました。 この違反を厳密に適用、ドライバーのさまざまなコンポーネント間で共有されるすべてのロックを取得および解放の 2 つのスレッドが不可能なデッドロックの発生は、この順序で常にする必要があることを強制します。



**Windows 8.1 の新機能**とき[Driver Verifier](driver-verifier.md)デバッガーをアタッチすると、デバッガーは直接入力エラーの場合、この違反を検出します。 Windows 8 および Windows の以前のバージョンでは、この違反は、即時のバグ チェックで発生します。

```
************ Verifier Detected a Potential Deadlock *************
**
** Type !deadlock in the debugger for more information.
**
*****************************************************************

*** Verifier assertion failed ***
(B)reak, (I)gnore, (W)arn only, (R)emove assert?
```

Windows 8.1 を実行するコンピューターでこの違反をデバッグするには、選択**B** (中断)、推奨されるデバッガー コマンドを入力します ([**! デッドロック**](https://msdn.microsoft.com/library/windows/hardware/ff562326))。

```
kd> !deadlock
issue: 00001001 97dd800c 86858ce0 00000000 

Deadlock detected (2 locks in 2 threads):

Thread 0: A B.
Thread 1: B A.

Where:

Thread 0 = TERMINATED.
Thread 1 = c4ae2040.

Lock A =   97dd800c (MyTestDriver!AlphaLock+0x00000000) - Type 'Spinlock'.
Lock B =   97dd8008 (MyTestDriver!BravoLock+0x00000000) - Type 'Spinlock'.
```

[ **! デッドロック**](https://msdn.microsoft.com/library/windows/hardware/ff562326) **3**コマンドの詳細情報を表示、最後の時点でのスタックを含めて取得することもできます。

```
kd> !deadlock 3
issue: 00001001 97dd800c 86858ce0 00000000 

Deadlock detected (2 locks in 2 threads):
# 

Thread 0: TERMINATED took locks in the following order:

Lock A =     97dd800c (MyTestDriver!AlphaLock+0x00000000) - Type 'Spinlock'.

    Node:    8685acd8

    Stack:   97dd65b7 MyTestDriver!SystemControlIrpWorker+0x00000027 
             97dd605a MyTestDriver!Dispatch_SystemControl+0x0000001a 
             820c4b4d nt!IovCallDriver+0x000002cc 
             81ca3772 nt!IofCallDriver+0x00000062 
             81eb165e nt!IopSynchronousServiceTail+0x0000016e 
             81eb5518 nt!IopXxxControlFile+0x000003e8 
             81eb4516 nt!NtDeviceIoControlFile+0x0000002a 
             81d27e17 nt!KiSystemServicePostCall+0x00000000 

Lock B =     97dd8008 (MyTestDriver!BravoLock+0x00000000) - Type 'Spinlock'.

    Node:    86833578

    Stack:   97dd65c5 MyTestDriver!SystemControlIrpWorker+0x00000a4a 
             97dd605a MyTestDriver!Dispatch_SystemControl+0x0000001a 
             820c4b4d nt!IovCallDriver+0x000002cc 
             81ca3772 nt!IofCallDriver+0x00000062 
             81eb165e nt!IopSynchronousServiceTail+0x0000016e 
             81eb5518 nt!IopXxxControlFile+0x000003e8 
             81eb4516 nt!NtDeviceIoControlFile+0x0000002a 
             81d27e17 nt!KiSystemServicePostCall+0x00000000
# 

Thread 1: c4ae2040 (ThreadEntry = 86833a08) took locks in the following order:

Lock B =     97dd8008 (MyTestDriver!BravoLock+0x00000000) - Type 'Spinlock'.

    Node:    86858ce0

    Stack:   97dd65ef MyTestDriver!DeviceControlIrpWorker+0x0000005f 
             97dd605a MyTestDriver!Dispatch_DeviceControl+0x0000001a 
             820c4b4d nt!IovCallDriver+0x000002cc 
             81ca3772 nt!IofCallDriver+0x00000062 
             81eb165e nt!IopSynchronousServiceTail+0x0000016e 
             81eb5518 nt!IopXxxControlFile+0x000003e8 
             81eb4516 nt!NtDeviceIoControlFile+0x0000002a 
             81d27e17 nt!KiSystemServicePostCall+0x00000000 

Lock A =     97dd800c (MyTestDriver!AlphaLock+0x00000000) - Type 'Spinlock'.

    Stack:   << Current stack trace - use kb to display it >>
```

使用して、デバッガーの提案、 [ **kb (Stack Backtrace の表示)** ](https://msdn.microsoft.com/library/windows/hardware/ff551943)コマンドを現在のスタック トレースを表示します。

```
kd> kb
ChildEBP RetAddr  Args to Child              
89b2cac4 820da328 97dd800c 86858ce0 00000000 nt!VfReportIssueWithOptions+0x86
89b2caf4 820d92a2 00000001 00000000 97dd65fd nt!ViDeadlockAnalyze+0x1d1
89b2cb7c 820d424e 86858ce0 00000000 97dd65fd nt!VfDeadlockAcquireResource+0x2fd
89b2cb9c 97dd65fd 00007780 89b2cbbc 97dd605a nt!VerifierKfAcquireSpinLock+0x8c
89b2cba8 97dd605a 9a9e7780 88d08f48 00000000 MyTestDriver!DeviceControlIrpWorker+0x54a
89b2cbbc 820c4b4d 9a9e7780 88d08f48 820c4881 MyTestDriver!Dispatch_DeviceControl+0x1a
(Inline) -------- -------- -------- -------- nt!IopfCallDriver+0x47
89b2cbe0 81ca3772 81eb165e b3c9ff80 88d08f48 nt!IovCallDriver+0x2cc
89b2cbf4 81eb165e 88d08fdc 88d08f48 00000000 nt!IofCallDriver+0x62
```

デバッガーの出力と示して ことドライバーの問題の取得とロック A を保持する 1 つのスレッドにロック B を取得する前に、このルールに違反してとようになりましたロック B を買収しました。 別のスレッドでロック A を取得しようとしては。 取得と後続リリースのこれら 2 つのロックが発生した時点でドライバーのイメージが読み込まれてから、最初のスレッド (Thread 0) が終了になっていることに注意してください。

ドライバーのテスト用の適切なシンボルが読み込まれると、デバッガーは時にロックが取得された関数を表示します。 この例では、偶然にロック A とロック B の両方を同じ関数で取得します。 0 のスレッドの両方で取得される*SystemControlIrpWorker*します。 スレッドの 1 の両方で取得される*DeviceControlIrpWorker* (ロック B からの出力に示すように **! デッドロック 3**と現在のスタックの出力 (**kb**)。

この時点では、各関数のソース コードのレビューは、ロックを取得して、このような順序で、コード パスが存在することが表示されます。

両方*MyTestDriver!AlphaLock*と*MyTestDriver!BravoLock*オブジェクトをドライバーでグローバルに利用できるには。

```
include "MyTestDriverHeader.h"

// Locks used to control access to various objects
extern KSPIN_LOCK AlphaLock;
extern KSPIN_LOCK BravoLock;
```

関数の内部で*SystemControlIrpWorker*、パスが存在する場所 AlphaLock (ロック A で、 **! デッドロック**出力) 取得後、BravoLock (ロック B) が取得されるときに保持されています。 ロックが獲得している逆の順序で適切に解放される注目すべきです。 (次のコードはこのシナリオの生成に必要な要素のみを表示する頻度の高い編集します。)

```ManagedCPlusPlus
NTSTATUS SystemControlIrpWorker(_In_ PIRP Irp)
{
    KIRQL IrqlAlpha;
    KIRQL IrqlBravo;
    // <<Other local variable declarations removed>>

    // <<Various lines of code not shown>>

    KeAcquireSpinLock (&AlphaLock, &IrqlAlpha);

    // <<Various lines of code not shown>>

    KeAcquireSpinLock (&BravoLock, &IrqlBravo);

    // <<Various lines of code not shown>>

    KeReleaseSpinLock (&BravoLock, IrqlBravo);
    KeReleaseSpinLock (&AlphaLock, IrqlAlpha);

    // <<Various lines of code not shown>>
}
```

次に、確認する場合*DeviceControlIrpWorker*関数の例を逆の順序で、ロックを取得することは確認できます。 つまり、BravoLock を取得したり AlphaLock の取得を試みたときに保持されています。 次の例は、簡体字が、違反が生じる可能なパスがあることを示しています。

```ManagedCPlusPlus
NTSTATUS DeviceControlIrpWorker(_In_ PIRP Irp, 
                                _In_ BOOLEAN bSomeCondition)
{
    KIRQL IrqlAlpha;
    KIRQL IrqlBravo;
    // <<Other local variable declarations removed>>

    if (bSomeCondition == FALSE)
    {
        //
        // Note that if bSomeCondition is FALSE, then AlphaLock is acquired here
        // If bSomeCondition is TRUE, it is not needed to be acquired right now
        //
        KeAcquireSpinLock (&AlphaLock, &IrqlAlpha);
    }

    // <<Various lines of code not shown>>

    KeAcquireSpinLock (&BravoLock, &IrqlBravo);

    // <<Various lines of code not shown>>

    if (bSomeCondition == TRUE)
    { 
        //
        // Need to acquire AlphaLock here for upcoming code logic
        //
        KeAcquireSpinLock (&AlphaLock, &IrqlAlpha);

        // <<Various lines of code not shown>>

        KeReleaseSpinLock (&AlphaLock, IrqlAlpha);
    }

    // <<Various lines of code not shown>>

    KeReleaseSpinLock (&BravoLock, IrqlBravo);

    if (bSomeCondition == FALSE)
    {
        //
        // Release the AlphaLock, which was acquired much earlier
        //
        KeReleaseSpinLock (&AlphaLock, IrqlAlpha);
    }

    // <<Various lines of code not shown>>
}
```

この潜在的な違反を修正するのには、いることを確認、ドライバーが AlphaLock の取得を試みると、そのチェック BravoLock が保持されないようにを正しい操作ですがあります。 最も簡単な修正プログラムは、単に BravoLock を解放し、再度 AlphaLock が取得されるとすぐに取得できます。 より重要なコード変更 AlphaLock と BravoLock の再取得を待機中に、BravoLock を保護する任意のデータが変更されないことが重要である場合に必要な場合があります。

スピン ロックやその他の同期方法の詳細については、[スピン ロック](https://msdn.microsoft.com/library/windows/hardware/ff563830)を参照してください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[スピン ロック](https://msdn.microsoft.com/library/windows/hardware/ff563830)

[**バグ チェック 0xC4 の。ドライバー\_VERIFIER\_検出\_違反**](https://msdn.microsoft.com/library/windows/hardware/ff560187)

[**!deadlock**](https://msdn.microsoft.com/library/windows/hardware/ff562326)










