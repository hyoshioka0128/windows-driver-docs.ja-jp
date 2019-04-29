---
title: スタック オーバーフローのデバッグ
description: スタック オーバーフローのデバッグ
ms.assetid: fc67effa-88c9-4915-a5a8-8c094595c6c5
keywords:
- スタック オーバーフロー
- コール スタック、スタック オーバーフローのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f96477c41a79a1695d5123e404ceea89eebd92d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324595"
---
# <a name="debugging-a-stack-overflow"></a>スタック オーバーフローのデバッグ


## <span id="ddk_debugging_a_stack_overflow_dbg"></span><span id="DDK_DEBUGGING_A_STACK_OVERFLOW_DBG"></span>


スタック オーバーフローは、ユーザー モード スレッドが発生するエラーです。 このエラーの考えられる原因を次の 3 つあります。

-   スレッド スタック全体が用に予約を使用します。 これは多くの場合、無限再帰が原因します。

-   スレッドは、ページファイルに達し、したがって他のページはコミットされませんスタックを拡張するために、スタックを拡張できません。

-   スレッドは、システムがページファイルを拡張するために使用する簡単な期間内にあるため、スタックを拡張できません。

スレッドで実行されている関数がローカル変数を割り当てるとき、変数はスレッドのコール スタックに配置されます。 関数に必要なスタック領域の量は、すべてのローカル変数のサイズの合計と同じ大きさ可能性があります。 ただし、コンパイラでは、通常、関数に必要なスタック領域を削減する最適化を実行します。 たとえば、この 2 つの変数が異なるスコープである場合は、コンパイラはこれらの変数の両方に同じスタック メモリを使用できます。 コンパイラは、計算を最適化することによって完全にいくつかのローカル変数を排除することもあります。

最適化の量は、ビルド時に適用されるコンパイラ設定が反映されます。 たとえば、デバッグ ビルドとリリース ビルドをさまざまな最適化レベルがあります。 デバッグ ビルドでの関数に必要なスタック領域の量は、リリース ビルドでその同じ関数で必要なスタック領域の量を超える可能性があります。

スタック オーバーフローをデバッグする方法の例を次に示します。 この例では、NTSD はターゲット アプリケーションと同じコンピューター上で実行し、ホスト コンピューターの KD をその出力のリダイレクトは。 参照してください[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)詳細についてはします。

最初の手順は、どのようなイベントがデバッガーに割り込む原因となった参照してください。

```dbgcmd
0:002> .lastevent 
Last event: Exception C00000FD, second chance 
```

Microsoft Windows SDK と Windows Driver Kit (WDK) では、例外コード 0xC00000FD を調べることができます。 この例外コード状態は、\_スタック\_オーバーフローが発生します。

スタックがオーバーフローしたことを確認して、使用することができます、 [ **k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

```dbgcmd
0:002> k 
ChildEBP RetAddr
009fdd0c 71a32520 COMCTL32!_chkstk+0x25
009fde78 77cf8290 COMCTL32!ListView_WndProc+0x4c4
009fde98 77cfd634 USER32!_InternalCallWinProc+0x18
009fdf00 77cd55e9 USER32!UserCallWinProcCheckWow+0x17f
009fdf3c 77cd63b2 USER32!SendMessageWorker+0x4a3
009fdf5c 71a45b30 USER32!SendMessageW+0x44
009fdfec 71a45bb0 COMCTL32!CCSendNotify+0xc0e
009fdffc 71a1d688 COMCTL32!CICustomDrawNotify+0x2a
009fe074 71a1db30 COMCTL32!Header_Draw+0x63
009fe0d0 71a1f196 COMCTL32!Header_OnPaint+0x3f
009fe128 77cf8290 COMCTL32!Header_WndProc+0x4e2
009fe148 77cfd634 USER32!_InternalCallWinProc+0x18
009fe1b0 77cd4490 USER32!UserCallWinProcCheckWow+0x17f
009fe1d8 77cd46c8 USER32!DispatchClientMessage+0x31
009fe200 77f7bb3f USER32!__fnDWORD+0x22
009fe220 77cd445e ntdll!_KiUserCallbackDispatcher+0x13
009fe27c 77cfd634 USER32!DispatchMessageWorker+0x3bc
009fe2e4 009fe4a8 USER32!UserCallWinProcCheckWow+0x17f
00000000 00000000 0x9fe4a8 
```

対象のスレッドが COMCTL32 に分割します。\_chkstk で、スタックの問題を示します。 これでターゲット プロセスのスタック使用量を調べる必要があります。 そのため最初にこのスレッドを識別、プロセスには、複数のスレッドが、重要なは、オーバーフローが発生しました。

```dbgcmd
0:002> ~*k

   0  id: 570.574   Suspend: 1 Teb 7ffde000 Unfrozen
   .....

   1  id: 570.590   Suspend: 1 Teb 7ffdd000 Unfrozen
   .....

. 2  id: 570.598   Suspend: 1 Teb 7ffdc000 Unfrozen
ChildEBP RetAddr
 009fdd0c 71a32520 COMCTL32!_chkstk+0x25 
.....

   3  id: 570.760   Suspend: 1 Teb 7ffdb000 Unfrozen 
```

スレッド 2 を調査する必要があります。 この行の左側にある期間は、現在のスレッドであることを示します。

履歴情報は、0x7FFDC000 で TEB (スレッド環境ブロック) に含まれます。 表示する最も簡単な方法を使用して[ **! teb**](-teb.md)します。 ただし、適切なシンボルが必要です。 最大の汎用性のシンボルを持っていないと仮定します。

```dbgcmd
0:002> dd 7ffdc000 L4 
7ffdc000   009fdef0 00a00000 009fc000 00000000 
```

これを解釈するには、TEB データ構造体の定義を検索する必要があります。 完全なシンボルがある場合は使用できます[ **dt TEB** ](dt--display-type-.md)これを行う。 ここでは、Microsoft Windows SDK の ntpsapi.h ファイルを見てする必要がありますには。 このファイルには、次の情報が含まれています。

```cpp
typedef struct _TEB {
    NT_TIB NtTib;
    PVOID  EnvironmentPointer;
    CLIENT_ID ClientId;
    PVOID ActiveRpcHandle;
    PVOID ThreadLocalStoragePointer;
    PPEB ProcessEnvironmentBlock;
    ULONG LastErrorValue;
    .....
    PVOID DeallocationStack;
    .....
} TEB;

typedef struct _NT_TIB {
    struct _EXCEPTION_REGISTRATION_RECORD *ExceptionList;
    PVOID StackBase;
    PVOID StackLimit;
    .....
} NT_TIB; 
```

これは、構造、下部にあると、スタックの一番上のポイントをそれぞれ TEB で 2 番目と 3 番目の Dword を示します。 この場合、これらのアドレスは、0x00A00000 と 0x009FC000 は。 (スタックは下方に拡大メモリ内。)使ってスタック サイズを計算することができます、 [**でしょうか。(式の評価)** ](---evaluate-expression-.md)コマンド。

```dbgcmd
0:002> ? a00000-9fc000
Evaluate expression: 16384 = 00004000 
```

これは、スタック サイズが 16 k. は示しています。最大スタック サイズが、フィールドに格納されている**DeallocationStack**します。 いくつかの計算後に、このフィールドのオフセットが 0xE0C を確認できます。

```dbgcmd
0:002> dd 7ffdc000+e0c L1 
7ffdce0c   009c0000 

0:002> ? a00000-9c0000 
Evaluate expression: 262144 = 00040000 
```

これは、最大スタック サイズが 256 K は、十分なスタック領域が残ってよりも多くの意味を示しています。

さらに、このプロセスでは、クリーン - 無限の再帰または過度に大規模なスタック ベースのデータ構造を使用して、そのスタック スペースを超えるにないです。

ここで KD に分割し、全体的なシステムのメモリ使用量を確認、 [ **! vm** ](-vm.md)拡張機能コマンド。

```dbgcmd
0:002> .breakin 
Break instruction exception - code 80000003 (first chance)
ntoskrnl!_DbgBreakPointWithStatus+4:
80148f9c cc               int     3

kd> !vm 

*** Virtual Memory Usage ***
        Physical Memory:     16268   (   65072 Kb)
        Page File: \??\C:\pagefile.sys
           Current:    147456Kb Free Space:     65988Kb
           Minimum:     98304Kb Maximum:       196608Kb
        Available Pages:      2299   (    9196 Kb)
        ResAvail Pages:       4579   (   18316 Kb)
        Locked IO Pages:        93   (     372 Kb)
        Free System PTEs:    42754   (  171016 Kb)
        Free NP PTEs:         5402   (   21608 Kb)
        Free Special NP:       348   (    1392 Kb)
        Modified Pages:        757   (    3028 Kb)
        NonPagedPool Usage:    811   (    3244 Kb)
        NonPagedPool Max:     6252   (   25008 Kb)
        PagedPool 0 Usage:    1337   (    5348 Kb)
        PagedPool 1 Usage:     893   (    3572 Kb)
        PagedPool 2 Usage:     362   (    1448 Kb)
        PagedPool Usage:      2592   (   10368 Kb)
        PagedPool Maximum:   13312   (   53248 Kb)
        Shared Commit:        3928   (   15712 Kb)
        Special Pool:         1040   (    4160 Kb)
        Shared Process:       3641   (   14564 Kb)
        PagedPool Commit:     2592   (   10368 Kb)
        Driver Commit:         887   (    3548 Kb)
        Committed pages:     45882   (  183528 Kb)
        Commit limit:        50570   (  202280 Kb)

        Total Private:       33309   (  133236 Kb)
         ..... 
```

非ページとページ プールの使用状況を見て最初に。 これらは、問題の原因ではありませんので、制限内でどちらもです。

次に、コミットされたページの数になります。202280 外 183528 します。 これは非常に制限に近付くします。 点に注意する必要がありますが、この表示では、この数の制限では、完全には示されませんが、ユーザー モードのデバッグを実行している間に、その他のプロセスが、システムで実行されています。 毎回、NTSD コマンドを実行すると、これらの他のプロセスもの割り当てと解放メモリ。 正確にどのようなメモリの状態がのようにスタック オーバーフローが発生した時点でわからないことを意味します。 コミットされたページ数は制限を閉じる方法を指定するには、これが最後にある時点でページのファイルが使用されたことと、これには、スタック オーバーフローが発生しました妥当です。

これは一般的でない場合であり、対象アプリケーションは、この本当に障害ことはできません。 頻繁に発生した場合、障害が発生したアプリケーションの最初のスタックのコミットメントを上げることを検討したい場合があります。

### <a name="span-idanalyzingasinglefunctioncallspanspan-idanalyzingasinglefunctioncallspananalyzing-a-single-function-call"></a><span id="analyzing_a_single_function_call"></span><span id="ANALYZING_A_SINGLE_FUNCTION_CALL"></span>1 つの関数呼び出しの分析

特定の関数呼び出しの割り当ては正確にスタック領域の量を確認することもできます。

これを行うには、最初のいくつかの手順を逆アセンブルし、命令を探して`sub esp`*数*します。 これが効果的に予約、スタック ポインターを移動*数*ローカル データのバイト数。

以下に例を示します。

```dbgcmd
0:002> k 
ChildEBP RetAddr
009fdd0c 71a32520 COMCTL32!_chkstk+0x25
009fde78 77cf8290 COMCTL32!ListView_WndProc+0x4c4
009fde98 77cfd634 USER32!_InternalCallWinProc+0x18
009fdf00 77cd55e9 USER32!UserCallWinProcCheckWow+0x17f
009fdf3c 77cd63b2 USER32!SendMessageWorker+0x4a3
009fdf5c 71a45b30 USER32!SendMessageW+0x44
009fdfec 71a45bb0 COMCTL32!CCSendNotify+0xc0e
009fdffc 71a1d688 COMCTL32!CICustomDrawNotify+0x2a
009fe074 71a1db30 COMCTL32!Header_Draw+0x63
009fe0d0 71a1f196 COMCTL32!Header_OnPaint+0x3f
009fe128 77cf8290 COMCTL32!Header_WndProc+0x4e2

0:002> u COMCTL32!Header_Draw
 COMCTL32!Header_Draw :
71a1d625 55               push    ebp
71a1d626 8bec             mov     ebp,esp
71a1d628 83ec58           sub     esp,0x58
71a1d62b 53               push    ebx
71a1d62c 8b5d08           mov     ebx,[ebp+0x8]
71a1d62f 56               push    esi
71a1d630 57               push    edi
71a1d631 33f6             xor     esi,esi 
```

これは、ことを示しています**ヘッダー\_描画**0x58 バイトのスタック領域が割り当てられます。

 

 





