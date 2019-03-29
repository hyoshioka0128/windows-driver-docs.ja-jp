---
title: プロセッサ消費の追跡
description: プロセッサ消費の追跡
ms.assetid: 8ecd000d-34e6-4471-a040-b50627915a20
keywords:
- プロセッサの消費
- プロセッサの占有
- アプリケーションを枯渇させてください。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 239a417a979d1509bdca7b8b0ffc0421b5075eb5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571466"
---
# <a name="tracking-down-a-processor-hog"></a>プロセッサ消費の追跡


## <span id="ddk_tracking_down_a_processor_hog_dbg"></span><span id="DDK_TRACKING_DOWN_A_PROCESSOR_HOG_DBG"></span>


(「占有」) に 1 つのアプリケーションが消費しているすべてのプロセッサの注意を他のプロセスが終了「飢え死に」とを実行できません。

この種のバグを修正するのにには、次の手順を使用します。

**すべての CPU サイクルを使用しているアプリケーションのデバッグ**

1.  **この問題の原因であるアプリケーションを識別します。** 使用**タスク マネージャー**または**Perfmon** 99% または 100% のプロセッサのサイクルのどのプロセスを使用して検索します。 問題のあるスレッドもが指示可能性があります。

2.  このプロセスに WinDbg、KD、CDB をアタッチします。

3.  **どのスレッドが問題の原因を特定します。** 問題のあるアプリケーションを分割します。 使用して、 [ **! runaway 3** ](-runaway.md) where の「スナップショット」のすべての CPU 時間を取得する拡張機能を移動します。 使用[ **g (移動)** ](g--go-.md)数秒待っているとします。 その後、中断して **! runaway 3**もう一度です。

    ```dbgcmd
    0:002> !runaway 3
     User Mode Time
     Thread    Time
     4e0        0:12:16.0312
     268        0:00:00.0000
     22c        0:00:00.0000
     Kernel Mode Time
     Thread    Time
     4e0        0:00:05.0312
     268        0:00:00.0000
     22c        0:00:00.0000

    0:002> g

    0:001> !runaway 3
     User Mode Time
     Thread    Time
     4e0        0:12:37.0609
     3d4        0:00:00.0000
     22c        0:00:00.0000
     Kernel Mode Time
     Thread    Time
     4e0        0:00:07.0421
     3d4        0:00:00.0000
     22c        0:00:00.0000
    ```

    2 つの数値のセットを比較しがユーザー モード時間またはカーネル モード時間を持つ最も増加したスレッドを探します。 **! ランナウェイ**CPU 時間、問題が発生したスレッドを降順で並べ替えますが、一覧の上部にある 1 つでは、通常します。 この場合、スレッド 0x4E0 が問題の原因です。

4.  使用して、 [ **~ (スレッド ステータス)** ](---thread-status-.md)と[ **~ s (現在のスレッドの設定)** ](-s--set-current-thread-.md)コマンド、現在のスレッドにします。
    ```dbgcmd
    0:001> ~
       0  Id: 3f4.3d4 Suspend: 1 Teb: 7ffde000 Unfrozen
    .  1  Id: 3f4.22c Suspend: 1 Teb: 7ffdd000 Unfrozen
     2  Id: 3f4.4e0 Suspend: 1 Teb: 7ffdc000 Unfrozen

    0:001> ~2s
    ```

5.  使用[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)このスレッドのスタック トレースを取得します。
    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffc74  77f6c600  000000c8.00000000 77fa5ad0 BuggyProgram!CreateMsgFile+0x1b
    0b4ffce4  01836060  0184f440 00000001 0b4ffe20 BuggyProgram!OpenDestFileStream+0xb3
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76
    ```

6.  現在実行中の関数の戻り値のアドレスには、ブレークポイントを設定します。 この場合、戻り値のアドレスは、0x77F6C600 として最初の行に表示されます。 戻り値のアドレスは、2 行目に示すように、関数のオフセットと同じです (**BuggyProgram!OpenDestFileStream + 0xB3**)。 アプリケーションで使用できるシンボルがない場合は、関数名が表示されない場合があります。 使用して、 [ **g (移動)** ](g--go-.md)シンボリックまたは 16 進数のいずれかのアドレスを使用して、この戻り値のアドレスが到達するまでに実行するコマンド。
    ```dbgcmd
    0:002> g BuggyProgram!OpenDestFileStream+0xb3
    ```

7.  このブレークポイントにヒットした場合は、プロセスを繰り返します。 たとえば、このブレークポイントにヒットします。 次の手順を実行する必要があります。

    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffce4  01836060  0184f440 00000001 0b4ffe20 BuggyProgram!OpenDestFileStream+0xb3
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76

    0:002> g BuggyProgram!SaveMsgToDestFolder+0xb3
    ```

    これにヒットした場合に進みます。

    ```dbgcmd
    0:002> kb
    FramePtr  RetAddr   Param1   Param2   Param3   Function Name
    0b4ffd20  01843eba  02b5b920 00000102 02b1e0e0 BuggyProgram!SaveMsgToDestFolder+0xb3
    0b4ffe20  01855924  0b4ffef0 00145970 0b4ffef0 BuggyProgram!DispatchToConn+0xa4
    0b4ffe5c  77e112e6  01843e16 0b4ffef0 0b4fff34 RPCRT4!DispatchToStubInC+0x34
    0b4ffeb0  77e11215  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStubWorker@RPC_INTERFACE@@AAEJPAU_RPC_MESSAGE@@IPAJ@Z+0xb0
    0b4ffed0  77e1a3b1  0b4ffef0 00000000 0b4fff34 RPCRT4!?DispatchToStub@RPC_INTERFACE@@QAEJPAU_RPC_MESSAGE@Z+0x41
    0b4fff40  77e181e4  02b1e0b0 00000074 0b4fff90 RPCRT4!?ReceiveOriginalCall@OSF_SCONNECTION@Z+0x14b
    0b4fff60  77e1a5df  02b1e0b0 00000074 00149210 RPCRT4!?DispatchPacket@OSF_SCONNECTION@+0x91
    0b4fff90  77e1ac1c  77e15eaf 00149210 0b4fffec RPCRT4!?ReceiveLotsaCalls@OSF_ADDRESS@@QAEXXZ+0x76

    0:002> g BuggyProgram!DispatchToConn+0xa4
    ```

8.  最後にブレークポイントがヒットしないを紹介します。 ここと考えてくださいを最後**g**コマンドが実行されているターゲットを設定し、それを破壊しません。 つまり、 **SaveMsgToDestFolder()** 関数が返すことはありません。

9.  もう一度、スレッドに分割し、ブレークポイントを設定**BuggyProgram!SaveMsgToDestFolder + 0xB3**で、 [ **bp (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)コマンド。 使用して、 **g**繰り返しコマンドします。 このブレークポイントがすぐにヒットした場合、ターゲットを実行する回数に関係なくは問題のある関数を識別している可能性があります。
    ```dbgcmd
    0:002> bp BuggyProgram!SaveMsgToDestFolder+0xb3

    0:002> g 

    0:002> g 
    ```

10. 使用して、 [ **p (ステップ)** ](p--step-.md)ループの一連の命令が、場所を特定するまでに、関数を続行するコマンド。 スピン中のスレッドの原因を識別するために、アプリケーションのソース コードを分析できます。 ロジックで問題が発生する原因は通常に、**中**、**は-中に**、 **goto**、または**の**ループします。

 

 





