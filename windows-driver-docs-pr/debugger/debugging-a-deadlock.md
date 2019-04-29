---
title: デッドロックのデバッグ
description: デッドロックのデバッグ
ms.assetid: ee7990d9-2d4e-4e48-9214-539eebd1d8db
keywords:
- デッドロック
- スレッド準備完了スレッドがありません。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fb6f4a43ca88b22df52362f4f56b11b489027f1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324634"
---
# <a name="debugging-a-deadlock"></a>デッドロックのデバッグ


## <span id="ddk_debugging_deadlocks_no_ready_threads__dbg"></span><span id="DDK_DEBUGGING_DEADLOCKS_NO_READY_THREADS__DBG"></span>


要求スレッドにコードまたはその他のリソースへの排他アクセスが必要がある場合、*ロック*します。 可能な場合、Windows は、スレッドにこのロックを指定することにより応答します。 この時点では、システムの他に何もロックされているコードにアクセスできます。 これが常に発生し、適切に記述された、マルチ スレッド アプリケーションの正常な処理は、します。 特定のコード セグメントは 1 つのロックを同時がだけことができます、複数のコード セグメントの各ことができます独自のロック。

A*デッドロック*2 つまたは複数のスレッドは、互換性のないシーケンスで、2 つ以上のリソースにロックを要求した場合に発生します。 たとえば、1 つのスレッドのことが A のリソースのロックを取得および B のリソースへのアクセスを要求し、その一方で、2 つのスレッドがリソース B でロックを取得し、リソース A へのアクセスを要求し、どちらのスレッドは、まで、その他のスレッドのロックを開放し、そのため、どちらのスレッドが進むことができますに進むことができます。

1 つのアプリケーションの複数のスレッドが互いのと同じリソースへのアクセスをブロックされたときに、ユーザー モードのデッドロックが発生します。 (同じプロセスまたは個別のプロセスを使用して) 複数のスレッドが互いの同じカーネル リソースへのアクセスをブロックされたときに、カーネル モードのデッドロックが発生します。 デッドロックのデバッグに使用するプロシージャは、ユーザー モードまたはカーネル モードで、デッドロックが発生したかどうかによって異なります。

### <a name="span-iddebuggingausermodedeadlockspanspan-iddebuggingausermodedeadlockspandebugging-a-user-mode-deadlock"></a><span id="debugging_a_user_mode_deadlock"></span><span id="DEBUGGING_A_USER_MODE_DEADLOCK"></span>ユーザー モードのデッドロックのデバッグ

ユーザー モードでデッドロックが発生したときに、デバッグを行う、次の手順を使用します。

1.  問題、 [ **! ntsdexts.locks** ](-locks---ntsdexts-locks-.md)拡張機能。 ユーザー モードで入力するだけ済みます **! ロック**デバッガー プロンプト、 **ntsdexts**プレフィックスが使用されます。

2.  この拡張機能では、所有しているスレッドの ID と各クリティカル セクションのロック数と共に、現在のプロセスに関連付けられているすべての重要なセクションが表示されます。 クリティカル セクションのロック カウントが 0 の場合は、そのような操作はロックされません。 使用して、 [ **~ (スレッド ステータス)** ](---thread-status-.md)コマンドをその他の重要なセクションを所有するスレッドに関する情報を参照してください。

3.  使用して、 [ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)の他の重要なセクションを待機しているかどうかを判断するこれらのスレッドの各コマンド。

4.  これらの出力を使用して**kb**コマンド、デッドロックを見つけることができます。 他のスレッドによって保持されている、ロックで待機している各は 2 つのスレッド。 まれなケースで循環パターンは、ロックを保持する 3 つ以上のスレッドでデッドロックが考えられますが、2 つだけのスレッドがほとんどデッドロックに関係します。

この手順の図を次に示します。 まず、 **! ntdexts.locks**拡張機能。

```dbgcmd
0:006>  !locks 
CritSec ftpsvc2!g_csServiceEntryLock+0 at 6833dd68
LockCount          0
RecursionCount     1
OwningThread       a7
EntryCount         0
ContentionCount    0
*** Locked
 
CritSec isatq!AtqActiveContextList+a8 at 68629100
LockCount          2
RecursionCount     1
OwningThread       a3
EntryCount         2
ContentionCount    2
*** Locked
 
CritSec +24e750 at 24e750
LockCount          6
RecursionCount     1
OwningThread       a9
EntryCount         6
ContentionCount    6
*** Locked 
```

表示される最初の重要なセクションでは、ロックがないと、そのため、無視できます。

表示されている 2 番目の重要なセクションは、2 のロック カウントを備えが、そのため、デッドロックの可能性があります。 所有しているスレッドは、0xA3 のスレッド ID を持ちます。

すべてのスレッドをリストすることによってこのスレッドを見つけることができます、 [ **~ (スレッド ステータス)** ](---thread-status-.md)コマンド、および、この ID を持つスレッドを検索します。

```dbgcmd
0:006>  ~ 
   0  Id: 1364.1330 Suspend: 1 Teb: 7ffdf000 Unfrozen
   1  Id: 1364.17e0 Suspend: 1 Teb: 7ffde000 Unfrozen
   2  Id: 1364.135c Suspend: 1 Teb: 7ffdd000 Unfrozen
   3  Id: 1364.1790 Suspend: 1 Teb: 7ffdc000 Unfrozen
   4  Id: 1364.a3 Suspend: 1 Teb: 7ffdb000 Unfrozen
   5  Id: 1364.1278 Suspend: 1 Teb: 7ffda000 Unfrozen
.  6  Id: 1364.a9 Suspend: 1 Teb: 7ffd9000 Unfrozen
   7  Id: 1364.111c Suspend: 1 Teb: 7ffd8000 Unfrozen
   8  Id: 1364.1588 Suspend: 1 Teb: 7ffd7000 Unfrozen 
```

この表示では、最初の項目は、デバッガーの内部スレッドの数です。 2 番目の項目 (、`Id`フィールド) を小数点で区切られた 2 つの 16 進数値が含まれています。 小数点の前に数値はプロセス ID です。数、小数点がスレッドの id。 この例では、スレッド ID 0xA3 がスレッド番号 4 に対応する表示されます。

使用して、 [ **kb (Stack Backtrace の表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)スレッド番号 4 に対応するスタックを表示するコマンド。

```dbgcmd
0:006>  ~4 kb 
  4  id: 97.a3   Suspend: 0 Teb 7ffd9000 Unfrozen
ChildEBP RetAddr  Args to Child
014cfe64 77f6cc7b 00000460 00000000 00000000 ntdll!NtWaitForSingleObject+0xb
014cfed8 77f67456 0024e750 6833adb8 0024e750 ntdll!RtlpWaitForCriticalSection+0xaa 
014cfee0 6833adb8 0024e750 80000000 01f21cb8 ntdll!RtlEnterCriticalSection+0x46
014cfef4 6833ad8f 01f21cb8 000a41f0 014cff20 ftpsvc2!DereferenceUserDataAndKill+0x24
014cff04 6833324a 01f21cb8 00000000 00000079 ftpsvc2!ProcessUserAsyncIoCompletion+0x2a
014cff20 68627260 01f21e0c 00000000 00000079 ftpsvc2!ProcessAtqCompletion+0x32
014cff40 686249a5 000a41f0 00000001 686290e8 isatq!I_TimeOutContext+0x87
014cff5c 68621ea7 00000000 00000001 0000001e isatq!AtqProcessTimeoutOfRequests_33+0x4f
014cff70 68621e66 68629148 000ad1b8 686230c0 isatq!I_AtqTimeOutWorker+0x30
014cff7c 686230c0 00000000 00000001 000c000a isatq!I_AtqTimeoutCompletion+0x38
014cffb8 77f04f2c 00000000 00000001 000c000a isatq!SchedulerThread_297+0x2f
00000001 000003e6 00000000 00000001 000c000a kernel32!BaseThreadStart+0x51
```

このスレッドの呼び出しには、 **WaitForCriticalSection**関数は、ロックがあるだけでなく、他のものによってロックされているコードを待機しています。 重要なセクションへの呼び出しの最初のパラメーターを調べることで待機していることを確認できます。 **WaitForCriticalSection**します。 これは、最初のアドレスで**の子に Args**:"24e750"。 したがって、クリティカル セクション アドレス 0x24E750 でこのスレッドが待機しています。 これは、3 番目のクリティカル セクションごとに一覧表示、 **! ロック**以前に使用した拡張機能。

つまり、2 番目の重要なセクションが所有するスレッド、4 は、3 番目のクリティカル セクション待機しています。 またがロックされている 3 番目の重要なセクションに、注意を有効にするようになりました。 所有しているスレッドは、スレッド ID 0xA9 を持ちます。 出力を返す、 **~** コマンドの前に表示した、この ID を持つスレッドがスレッド番号 6 であることに注意してください。 このスレッドのスタック バック トレースが表示されます。

```dbgcmd
0:006>  ~6 kb 
ChildEBP RetAddr  Args to Child
0155fe38 77f6cc7b 00000414 00000000 00000000 ntdll!NtWaitForSingleObject+0xb
0155feac 77f67456 68629100 6862142e 68629100 ntdll!RtlpWaitForCriticalSection+0xaa 
0155feb4 6862142e 68629100 0009f238 686222e1 ntdll!RtlEnterCriticalSection+0x46
0155fec0 686222e1 0009f25c 00000001 0009f238 isatq!ATQ_CONTEXT_LISTHEAD__RemoveFromList
0155fed0 68621412 0009f238 686213d1 0009f238 isatq!ATQ_CONTEXT__CleanupAndRelease+0x30
0155fed8 686213d1 0009f238 00000001 01f26bcc isatq!AtqpReuseOrFreeContext+0x3f
0155fee8 683331f7 0009f238 00000001 01f26bf0 isatq!AtqFreeContext+0x36
0155fefc 6833984b ffffffff 00000000 00000000 ftpsvc2!ASYNC_IO_CONNECTION__SetNewSocket
0155ff18 6833adcd 77f05154 01f26a58 00000000 ftpsvc2!USER_DATA__Cleanup+0x47
0155ff28 6833ad8f 01f26a58 000a3410 0155ff54 ftpsvc2!DereferenceUserDataAndKill+0x39
0155ff38 6833324a 01f26a58 00000000 00000040 ftpsvc2!ProcessUserAsyncIoCompletion+0x2a
0155ff54 686211eb 01f26bac 00000000 00000040 ftpsvc2!ProcessAtqCompletion+0x32
0155ff88 68622676 000a3464 00000000 000a3414 isatq!AtqpProcessContext+0xa7
0155ffb8 77f04f2c abcdef01 ffffffff 000ad1b0 isatq!AtqPoolThread+0x32
0155ffec 00000000 68622644 abcdef01 00000000 kernel32!BaseThreadStart+0x51
```

このスレッドは、解放するクリティカル セクションを待機しています。 この場合、0x68629100 にクリティカル セクションを待機しています。 これは、重要な 2 つ目のセクションによって以前に生成されたリストで、 **! ロック**拡張機能。

これは、デッドロックです。 2 番目の重要なセクションが所有するスレッド、4 は、3 番目のクリティカル セクションで待機しています。 3 番目の重要なセクションが所有するスレッド 6 は、2 番目の重要なセクションを待機しています。

このデッドロックの性質を確定すると、通常のデバッグ手法を使用して、4 と 6 のスレッドを分析します。

### <a name="span-iddebuggingakernelmodedeadlockspanspan-iddebuggingakernelmodedeadlockspandebugging-a-kernel-mode-deadlock"></a><span id="debugging_a_kernel_mode_deadlock"></span><span id="DEBUGGING_A_KERNEL_MODE_DEADLOCK"></span>カーネル モードのデッドロックのデバッグ

カーネル モードでデッドロックのデバッグに役立ついくつかのデバッガー拡張機能があります。

-   [ **! Kdexts.locks** ](-locks---kdext--locks-.md)拡張機能は、カーネルのリソースとこれらのロックを保持しているスレッドで保持されているすべてのロックに関する情報を表示します。 (カーネル モードで入力するだけ済みます **! ロック**デバッガー プロンプト、 **kdexts**プレフィックスが使用されます)。

-   [ **! Qlocks** ](-qlocks.md)拡張機能には、すべてのキューに置かれたスピン ロックの状態が表示されます。

-   [ **! Wdfkd.wdfspinlock** ](-deadlock.md)拡張機能には、カーネル モード ドライバー フレームワーク (KMDF) スピン ロック オブジェクトに関する情報が表示されます。

-   [ **! デッドロック**](-deadlock.md)拡張機能は、デッドロックが発生する可能性のあるコードでロックの一貫性のない使用を検出するためにドライバーの検証ツールと組み合わせて使用します。

カーネル モードでデッドロックが発生した場合、使用、 **! kdexts.locks**拡張機能を現在のスレッドによって取得されたすべてのロックを一覧表示します。

通常、実行中のスレッドで必要とされるリソースに排他ロックを保持する 1 つの実行中でないスレッドを検索して、デッドロックを特定できます。 ほとんどのロックが共有されます。

 

 





