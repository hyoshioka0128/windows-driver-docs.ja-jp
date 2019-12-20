---
title: デッドロック (deadlock)
description: デッドロック拡張機能は、ドライバーの検証ツールのデッドロック検出オプションによって収集されたデッドロックに関する情報を表示します。
ms.assetid: c0e6074f-8afe-4526-a30f-427aac67ab99
keywords:
- デッドロック検出 (ドライバーの検証ツール)
- デッドロック Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- deadlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 541c9a0ae1ab9c980c3f5009f1e027dff13f929c
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209127"
---
# <a name="deadlock"></a>!deadlock


**! デッドロック**拡張機能は、ドライバーの検証ツールの**デッドロック検出**オプションによって収集されたデッドロックに関する情報を表示します。

```dbgcmd
!deadlock 
!deadlock 1
```

## <span id="ddk__deadlock_dbg"></span><span id="DDK__DEADLOCK_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>利用不可</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ドライバーの検証機能の詳細については、Windows Driver Kit (WDK) のドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

この拡張機能では、ドライバー検証ツールの**デッドロック検出**オプションによってロック階層違反が検出され、[**バグチェック 0xc4**](bug-check-0xc4--driver-verifier-detected-violation.md) (ドライバー\_検証\_検出された\_違反) が検出された場合にのみ、有用な情報が提供されます。

引数を指定しない場合、 **! デッドロック**拡張によって、基本的なロック階層トポロジが表示されます。 この問題が単純な循環デッドロックでない場合は、このコマンドによって発生した状況が記述されます。

**! デッドロック 1**拡張により、スタックトレースが表示されます。 表示されるスタックは、ロックが取得された時点でアクティブになっています。

以下に例を示します。

```dbgcmd
0:kd> !deadlock

Deadlock detected (2 resources in 2 threads):

Thread 0: A B
Thread 1: B A

Where:
Thread 0 = 8d3ba030
Thread 1 = 8d15c030
Lock A =   bba2af30 Type 'Spinlock'
Lock B =   dummy!GlobalLock Type 'Spinlock'
```

これにより、どのスレッドとどのロックが関係しているかがわかります。 ただし、これは概要であり、状況を適切にデバッグするのに十分な情報ではない可能性があります。

デッドロックに関与している各ロックが取得されたときに、 **! デッドロック 1**を使用して呼び出し履歴の内容を出力します。 これらは実行時のスタックトレースであるため、チェックされたビルドが使用されている場合はより完全です。 チェックされたビルドは、Windows 10 バージョン1803より前の以前のバージョンの Windows で使用できました。 無料のビルドでは、1行だけの後に切り捨てられる場合があります。

```dbgcmd
0:kd> !deadlock 1

Deadlock detected (2 resources in 2 threads):

Thread 0 (8D14F750) took locks in the following order:

    Lock A -- b7906f30 (Spinlock)
    Stack:   dummy!DummyActivateVcComplete+0x63
             dummy!dummyOpenVcChannels+0x2E1
             dummy!DummyAllocateRecvBufferComplete+0x436
             dummy!DummyAllocateComplete+0x55
             NDIS!ndisMQueuedAllocateSharedHandler+0xC9
             NDIS!ndisWorkerThread+0xEE

    Lock B -- dummy!GlobalLock (Spinlock)
    Stack:   dummy!dummyQueueRecvBuffers+0x2D
             dummy!DummyActivateVcComplete+0x90
             dummy!dummyOpenVcChannels+0x2E1
             dummy!DummyAllocateRecvBufferComplete+0x436
             dummy!DummyAllocateComplete+0x55

Thread 1 (8D903030) took locks in the following order:

    Lock B -- dummy!GlobalLock (Spinlock)
    Stack:   dummy!dummyRxInterruptOnCompletion+0x25D
             dummy!DummyHandleInterrupt+0x32F
             NDIS!ndisMDpcX+0x3C
             ntkrnlpa!KiRetireDpcList+0x5D

    Lock A -- b7906f30 (Spinlock)
    Stack:   << Current stack >>
```

この情報を使用すると、現在のスタックを除き、必要なものがほぼすべて揃います。

```dbgcmd
0: kd> k
ChildEBP RetAddr
f78aae6c 80664c58 ntkrnlpa!DbgBreakPoint
f78aae74 8066523f ntkrnlpa!ViDeadlockReportIssue+0x2f
f78aae9c 806665df ntkrnlpa!ViDeadlockAnalyze+0x253
f78aaee8 8065d944 ntkrnlpa!VfDeadlockAcquireResource+0x20b
f78aaf08 bfd6df46 ntkrnlpa!VerifierKeAcquireSpinLockAtDpcLevel+0x44
f78aafa4 b1bf2d2d dummy!dummyRxInterruptOnCompletion+0x2b5
f78aafc4 bfde9d8c dummy!DummyHandleInterrupt+0x32f
f78aafd8 804b393b NDIS!ndisMDpcX+0x3c
f78aaff4 804b922b ntkrnlpa!KiRetireDpcList+0x5d
```

これにより、どのロックが関係しており、どこで取得されたかを確認できます。 これにより、デッドロックをデバッグするための十分な情報が得られます。 ソースコードが使用可能な場合は、デバッガーを使用して、問題が発生した場所を正確に確認できます。

```dbgcmd
0: kd> .lines
Line number information will be loaded

0: kd> u dummy!DummyActivateVcComplete+0x63 l1
dummy!DummyActivateVcComplete+63 [d:\nt\drivers\dummy\vc.c @ 2711]:
b1bfe6c9 837d0c00         cmp     dword ptr [ebp+0xc],0x0

0: kd> u dummy!dummyQueueRecvBuffers+0x2D l1
dummy!dummyQueueRecvBuffers+2d [d:\nt\drivers\dummy\receive.c @ 2894]:
b1bf4e39 807d0c01         cmp     byte ptr [ebp+0xc],0x1

0: kd> u dummy!dummyRxInterruptOnCompletion+0x25D l1
dummy!dummyRxInterruptOnCompletion+25d [d:\nt\drivers\dummy\receive.c @ 1424]:
b1bf5d05 85f6             test    esi,esi

0: kd> u dummy!dummyRxInterruptOnCompletion+0x2b5 l1
dummy!dummyRxInterruptOnCompletion+2b5 [d:\nt\drivers\dummy\receive.c @ 1441]:
b1bf5d5d 8b4648           mov     eax,[esi+0x48]
```

これで、ソースファイルの名前と、取得が行われた行番号がわかりました。 この場合、ソースファイルには、次のようにスレッドが動作していることが示されます。

-   スレッド 1: **DummyActivateVcComplete**は**ダミー**ミニポートロックを受け取りました。 その後、 **dummyQueueRecvBuffers**という名前が付いています。これは、**ダミー**のグローバルロックを受け取りました。

-   スレッド 2: **dummyRxInterruptOnCompletion**がグローバルロックを受け取りました。 その後、いくつかの行でミニポートロックがかかっていました。

この時点で、デッドロックは完全に明確になります。

 

 





