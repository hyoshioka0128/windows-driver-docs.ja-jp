---
title: デッドロック (deadlock)
description: デッドロックの拡張機能は、Driver Verifier のデッドロック検出オプションによって収集されたデッドロック情報を表示します。
ms.assetid: c0e6074f-8afe-4526-a30f-427aac67ab99
keywords:
- デッドロックの検出 (Driver Verifier)
- Windows デバッグ デッドロック
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- deadlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3df3c218a781e2d42d3e1b7bb1477059bad8e97c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336843"
---
# <a name="deadlock"></a>!deadlock


**! デッドロック**拡張機能によって収集されたデッドロックに関する情報を表示する、**デッドロック検出**Driver Verifier のオプション。

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
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

Driver Verifier については、Windows Driver Kit (WDK) ドキュメントを参照してください。

<a name="remarks"></a>注釈
-------

場合は、この拡張機能に有用な情報は提供のみ Driver Verifier の**デッドロック検出**オプションがロック階層の違反を検出し、発行[**バグ チェック 0xC4** ](bug-check-0xc4--driver-verifier-detected-violation.md)(ドライバー\_VERIFIER\_検出\_違反)。

任意の引数を指定せず、 **! デッドロック**拡張子が原因で表示する基本的なロック階層のトポロジ。 問題は、単純な cyclical デッドロックではありません、このコマンドは、状況が発生したことを説明します。

**! デッドロック 1**拡張により、スタック トレースを表示します。 表示されるスタックは、ロックが取得された時点でのアクティブなになります。

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

これは、どのスレッドと、どのロックが関係しています。 ただしは、概要と、状況を適切にデバッグするのに十分な情報ができない可能性があります。

使用 **! デッドロック 1**デッドロックに参加している各ロックが取得された時点で呼び出し履歴の内容を印刷します。 これらは実行時のスタック トレースであるためチェック ビルドが使用されている場合より完全なされます。 無料のビルドで、わずか 1 行の後に切り捨てられます可能性があります。

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

この情報により、ほぼ現在のスタックを除く、必要なすべてがあります。

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

これから、どのロックが関連しているし、取得されたを確認できます。 デッドロックをデバッグするための十分な情報があります。 ソース コードを使用できる場合は、正確に問題の発生場所を表示する、デバッガーを使用できます。

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

ソース ファイルと取得が行われた行番号の名前です。 この場合、ソース ファイルのスレッドが次のように動作しないことが表示されます。

-   スレッドの 1。**DummyActivateVcComplete**かかりました、**ダミー**ミニポート ロックします。 呼び出された**dummyQueueRecvBuffers**、かかりました、**ダミー**グローバル ロックします。

-   スレッド 2: **dummyRxInterruptOnCompletion**グローバル ロックがかかりました。 次に、わずか数行ミニポート ロックかかった後で、します。

この時点で、デッドロックはまったく明確になります。

 

 





