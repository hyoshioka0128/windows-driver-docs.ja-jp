---
title: クリティカル セクションのタイムアウト
description: クリティカル セクションのタイムアウト
ms.assetid: 736ec6e9-e822-49aa-8f1c-7e5e43779dbd
keywords:
- クリティカル セクション、厳しいタイムアウト時間がクリティカル セクションのデバッグ
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90563b4284a138aae520e14b6da72bf2e82d90a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374437"
---
# <a name="critical-section-time-outs"></a>クリティカル セクションのタイムアウト


## <span id="ddk_critical_section_time_outs_dbg"></span><span id="DDK_CRITICAL_SECTION_TIME_OUTS_DBG"></span>


クリティカル セクションのタイムアウトは、ルーチンを示すスタック トレースで識別できます**RtlpWaitForCriticalSection**スタックの上部にあります。 クリティカル セクション タイムアウトになるさまざまなもう 1 つは、デッドロックが発生アプリケーション エラーです。 クリティカル セクションのタイムアウトを正しくデバッグ、CDB または WinDbg 必要があります。

リソースのタイムアウトと同様、 **! ntsdexts.locks**拡張機能が現在保持されているロックと、所有するスレッドの一覧に表示されます。 リソースのタイムアウトとは異なり、指定されたスレッド Id はすぐに便利ですが。 これらは、システム CDB で使用されるスレッドの番号に直接マップされていない Id です。

同様<strong>ExpWaitForResource * Xxx</strong><em>、ロックの識別子は、最初のパラメーターに **RtlpWaitForCriticalSection</em>* します。 ループが見つかるか、または最後のスレッドがクリティカル セクションのタイムアウトを待機していないまでの待機チェーンのトレースを続行します。

### <a name="span-idexampleofdebuggingacriticaltimeoutspanspan-idexampleofdebuggingacriticaltimeoutspanexample-of-debugging-a-critical-time-out"></a><span id="example_of_debugging_a_critical_time_out"></span><span id="EXAMPLE_OF_DEBUGGING_A_CRITICAL_TIME_OUT"></span>重要なタイムアウトのデバッグの例

スタックを表示することで開始します。

```dbgcmd
0:024> kb

ChildEBP RetAddr  Args to Child
0569fca4 77f79c78 77f71000 002a6b88 7fffffff ntdll!_DbgBreakPoint
0569fd04 77f71048 5ffa9f9c 5fef0b4b 5ffa9f9c ntdll!_RtlpWaitForCriticalSection+0x89
0569fd0c 5fef0b4b 5ffa9f9c 002a6b88 002a0019 ntdll!_RtlEnterCriticalSection+0x48
0569fd70 5fedf83f 002a6b88 0569fdc0 0000003e winsrv!_StreamScrollRegion+0x1f0
0569fd8c 5fedfa5b 002a6b88 00190000 00000000 winsrv!_AdjustCursorPosition+0x8e
0569fdc0 5fedf678 0569ff18 0031c200 0335ee88 winsrv!_DoWriteConsole+0x104

0569fefc 5fe6311b 0569ff18 0569ffd0 00000005 winsrv!_SrvWriteConsole+0x96
0569fff4 00000000 00000000 00000024 00000024 csrsrv!_CsrApiRequestThread+0x4ff 
```

使用して、 [ **! ntsdexts.locks** ](-locks---ntsdexts-locks-.md)クリティカル セクションを検索する拡張機能。

```dbgcmd
0:024> !locks 
CritSec winsrv!_ScrollBufferLock at 5ffa9f9c        5ffa9f9c is the first one 
LockCount          5
RecursionCount     1
OwningThread       88         // here's the owning thread ID 
EntryCount         11c
ContentionCount    135
*** Locked

CritSec winsrv!_gcsUserSrv+0 at 5ffa91b4     //second critical section found below 

LockCount          8
RecursionCount     1
OwningThread       6d         // second owning thread 
EntryCount         1d6c
ContentionCount    1d47
*** Locked 
```

今すぐ 0x6D ID 番号を持つスレッドを検索します。

```dbgcmd
0:024> ~ 
  0  id: 16.15   Teb 7ffdd000 Unfrozen
  1  id: 16.13   Teb 7ffdb000 Unfrozen
  2  id: 16.30   Teb 7ffda000 Unfrozen
  3  id: 16.2f   Teb 7ffd9000 Unfrozen
  4  id: 16.2e   Teb 7ffd8000 Unfrozen
  5  id: 16.6c   Teb 7ff6c000 Unfrozen
  6  id: 16.6d   Teb 7ff68000 Unfrozen    // this thread owns the second critical section
  7  id: 16.2d   Teb 7ffd7000 Unfrozen
  8  id: 16.33   Teb 7ffd6000 Unfrozen
  9  id: 16.42   Teb 7ff6f000 Unfrozen
 10  id: 16.6f   Teb 7ff6e000 Unfrozen
 11  id: 16.6e   Teb 7ffd5000 Unfrozen
 12  id: 16.52   Teb 7ff6b000 Unfrozen
 13  id: 16.61   Teb 7ff6a000 Unfrozen
 14  id: 16.7e   Teb 7ff69000 Unfrozen
 15  id: 16.43   Teb 7ff67000 Unfrozen
 16  id: 16.89   Teb 7ff50000 Unfrozen
 17  id: 16.95   Teb 7ff65000 Unfrozen
 18  id: 16.90   Teb 7ff64000 Unfrozen
 19  id: 16.71   Teb 7ff63000 Unfrozen
 20  id: 16.bb   Teb 7ff62000 Unfrozen
 21  id: 16.88   Teb 7ff61000 Unfrozen    // this thread owns the first critical section
 22  id: 16.cd   Teb 7ff5e000 Unfrozen
 23  id: 16.c1   Teb 7ff5f000 Unfrozen
 24  id: 16.bd   Teb 7ff5d000 Unfrozen 
```

21 のスレッドには、最初の重要なセクションが所有しています。 アクティブ スレッドを作成してスタック トレースを取得します。

```dbgcmd
0:024> ~21s
ntdll!_ZwWaitForSingleObject+0xb:
77f71bfb c20c00           ret     0xc

0:021> kb

ChildEBP RetAddr  Args to Child
0556fc44 77f79c20 00000110 00000000 77fa4700 ntdll!_ZwWaitForSingleObject+0xb
0556fcb0 77f71048 5ffa91b4 5feb4f7e 5ffa91b4 ntdll!_RtlpWaitForCriticalSection+0x31
0556fcb8 5feb4f7e 5ffa91b4 0556fd70 77f71000 ntdll!_RtlEnterCriticalSection+0x48
0556fcf4 5fef0b76 01302005 00000000 fffffff4 winsrv!__ScrollDC+0x14
0556fd70 5fedf83f 002bd880 0556fdc0 00000025 winsrv!_StreamScrollRegion+0x21b
0556fd8c 5fedfa5b 002bd880 00190000 00000000 winsrv!_AdjustCursorPosition+0x8e

0556fdc0 5fedf678 0556ff18 002bdf70 002a4d58 winsrv!_DoWriteConsole+0x104
0556fefc 5fe6311b 0556ff18 0556ffd0 00000005 winsrv!_SrvWriteConsole+0x96
0556fff4 00000000 00000000 00000024 00000024 csrsrv!_CsrApiRequestThread+0x4ff 
```

6 スレッドには、2 番目の重要なセクションが所有しています。 そのスタックを確認します。

```dbgcmd
0:021> ~6s
winsrv!_PtiFromThreadId+0xd:
5fe8429a 394858           cmp     [eax+0x58],ecx    ds:0023:7f504da8=000000f8

0:006> kb

ChildEBP RetAddr  Args to Child
01ecfeb4 5fecd0d7 00000086 00000000 7f5738e0 winsrv!_PtiFromThreadId+0xd
01ecfed0 5feccf62 00000086 01ecfff4 00000113 winsrv!__GetThreadDesktop+0x12
01ecfefc 5fe6311b 01ecff18 01ecffd0 00000005 winsrv!___GetThreadDesktop+0x8b
01ecfff4 00000000 00000000 00000024 00000024 csrsrv!_CsrApiRequestThread+0x4ff 
```

21 のスレッドが**RtlpWaitForCriticalSection**そのスタックの上部にあります。 6 スレッドは提供されません。 したがって 21 のスレッドが原因です。

 

 





