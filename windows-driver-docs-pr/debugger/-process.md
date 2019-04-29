---
title: プロセス
description: プロセスの拡張機能では、指定されたプロセスまたは」プロセス ブロックを含め、すべてのプロセスに関する情報が表示されます。
ms.assetid: 57f55632-8320-47cc-8a20-5a2cf3b42b3a
keywords:
- Windows デバッグ プロセス
ms.date: 08/02/2018
topic_type:
- apiref
api_name:
- process
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2740945a72b1b77f7b4c6db84e8fca2b1e9567b5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334354"
---
# <a name="process"></a>!process


! 処理拡張機能については、指定されたプロセスまたは」プロセス ブロックを含め、すべてのプロセスについて、情報を表示します。

この拡張機能は、カーネル モードのデバッグ中にのみ使用できます。

構文

```dbgcmd
!process [/s Session] [/m Module] [Process [Flags]]
!process [/s Session] [/m Module] 0 Flags ImageName
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


<span id="_s_Session"></span><span id="_s_session"></span><span id="_S_SESSION"></span>**/s** **** *セッション*  
目的のプロセスを所有しているセッションを指定します。

<span id="_m_Module"></span><span id="_m_module"></span><span id="_M_MODULE"></span>**/m** **** *モジュール*  
目的のプロセスを所有するモジュールを指定します。

<span id="_Process"></span><span id="_process"></span><span id="_PROCESS"></span> *プロセス*  
ターゲット コンピューターで 16 進数のアドレスまたはプロセスのプロセス ID を指定します。

値*プロセス*決定かどうか、! プロセスの拡張機能は、プロセスのアドレスまたはプロセス ID が表示されます。 場合*プロセス*を省略するとデバッガーが、現在のシステム プロセスのみに関するデータを表示する Windows の任意のバージョンでは、します。 場合*プロセス*は 0 と*ImageName*は省略すると、デバッガーはアクティブなすべてのプロセスに関する情報が表示されます。 -1 が指定されて場合*プロセス*現在のプロセスに関する情報が表示されます。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>*フラグ*  
表示する詳細レベルを指定します。 *フラグ*次のビットの組み合わせにすることができます。 場合*フラグ*は 0、最小限の情報のみが表示されます。 既定値は、Windows のバージョンとの値によって異なります。*プロセス*します。 場合、既定値は 0x3*プロセス*を省略すると場合、または*プロセス*は 0 または-1。 それ以外の場合、既定では 0 xf。

<span id="Bit_0__0x1_"></span><span id="bit_0__0x1_"></span><span id="BIT_0__0X1_"></span>ビット 0 (0x1)  
時間と優先順位の統計情報が表示されます。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
状態のプロセスと、待機に関連付けられているスレッドとイベントの一覧が表示されます。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
プロセスに関連付けられているスレッドの一覧を表示します。 これは、ビット 1 (0x2) では、各スレッドが 1 行に表示されます。 これがビット 1 と共に含まれる場合は、各スレッドにスタック トレースが表示されます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
 返送先住所と関数の引数を抑制する各関数のスタック ポインターが表示されます。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
 このコマンドの実行中に、指定されたプロセスと同じプロセスのコンテキストを設定します。 これにより、スレッド スタックのより正確に表示します。 このフラグを使用すると、ため[ **.process/p/r** ](-process--set-process-context-.md)指定のプロセスでは、既存のユーザー モード モジュール一覧は破棄されます。 場合*プロセス*ゼロ、デバッガーを表示するすべてのプロセス、それぞれのプロセスのコンテキストが変更されました。 1 つのプロセスのみを表示して、ユーザー モードの状態が既に更新されている場合 (たとえば、 **.process/p/r**)、このフラグを使用する必要はありません。 このフラグでは、効果的なは、ビット 0 (0x1) で使用する場合のみです。

<span id="ImageName"></span><span id="imagename"></span><span id="IMAGENAME"></span>*ImageName*  
表示するプロセスの名前を指定します。 デバッガーが実行可能イメージの名前と一致するすべてのプロセスを表示する*ImageName*します。 イメージの名前と一致しなければなりません」プロセス ブロックにします。 一般に、ファイル拡張子 (通常は .exe) を含む、15 文字の後に切り捨ては、プロセスを開始する呼び出された実行可能ファイルの名前です。 スペースを含むイメージの名前を指定する方法はありません。 ときに*ImageName*が指定されている*プロセス*0 にする必要があります。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL


Kdexts.dll

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報


カーネル モードでのプロセスについては、次を参照してください。[変更コンテキスト](changing-contexts.md)します。 プロセスとスレッドの分析に関する詳細については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>注釈
-------

例を次に、 **! process 0 0**表示。

```dbgcmd
kd> !process 0 0
**** NT ACTIVE PROCESS DUMP ****
PROCESS 80a02a60  Cid: 0002    Peb: 00000000  ParentCid: 0000
    DirBase: 00006e05  ObjectTable: 80a03788  TableSize: 150.
    Image: System
PROCESS 80986f40  Cid: 0012    Peb: 7ffde000  ParentCid: 0002
    DirBase: 000bd605  ObjectTable: 8098fce8  TableSize:  38.
    Image: smss.exe
PROCESS 80958020  Cid: 001a    Peb: 7ffde000  ParentCid: 0012
    DirBase: 0008b205  ObjectTable: 809782a8  TableSize: 150.
    Image: csrss.exe
PROCESS 80955040  Cid: 0020    Peb: 7ffde000  ParentCid: 0012
    DirBase: 00112005  ObjectTable: 80955ce8  TableSize:  54.
    Image: winlogon.exe
PROCESS 8094fce0  Cid: 0026    Peb: 7ffde000  ParentCid: 0020
    DirBase: 00055005  ObjectTable: 80950cc8  TableSize: 222.
    Image: services.exe
PROCESS 8094c020  Cid: 0029    Peb: 7ffde000  ParentCid: 0020
    DirBase: 000c4605  ObjectTable: 80990fe8  TableSize: 110.
    Image: lsass.exe
PROCESS 809258e0  Cid: 0044    Peb: 7ffde000  ParentCid: 0026
    DirBase: 001e5405  ObjectTable: 80925c68  TableSize:  70.
    Image: SPOOLSS.EXE
```

次の表では、要素の一部について説明します、 **! process 0 0**出力します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要素</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>プロセスのアドレス</p></td>
<td align="left"><p>プロセスの単語の後の 8 文字の 16 進数では、」プロセス ブロックのアドレスです。 前の例の最終的なエントリ、0x809258E0 はプロセスのアドレスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>プロセス ID (PID)</p></td>
<td align="left"><p>Cid の単語の後に 16 進数。 前の例の最終的なエントリ、PID は 0x44、または 10 進 68。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プロセスの環境ブロック (PEB)</p></td>
<td align="left"><p>Peb 単語の後に 16 進数では、プロセスの環境ブロックのアドレスです。 前の例の最終的なエントリを PEB はアドレス 0x7FFDE000 にあります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>親プロセスの PID</p></td>
<td align="left"><p>ParentCid 単語の後に 16 進数が、親プロセスの pid を調べます。 前の例で親プロセス PID が 0x26 の最終的なエントリまたは 10 進数の 38 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Image</p></td>
<td align="left"><p>プロセスを所有するモジュールの名前。 前の例の最終的なエントリでは、所有者は、spoolss.exe です。 最初のエントリでは、所有者は、オペレーティング システム自体です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>プロセス オブジェクトのアドレス</p></td>
<td align="left"><p>ObjectTable 単語の後に 16 進数。 前の例の最終的なエントリでは、プロセス オブジェクトのアドレスは、0x80925c68 です。</p></td>
</tr>
</tbody>
</table>

 

1 つのプロセスの完全な詳細情報を表示する設定*フラグ*7 にします。 設定して、プロセス自体を指定できます*プロセス*設定、プロセスのアドレスに等しい*プロセス*プロセス ID、または設定に一致*ImageName*と等しく、実行可能イメージの名前。 以下に例を示します。

```dbgcmd
kd> !process fb667a00 7
PROCESS fb667a00 Cid: 0002  Peb: 00000000 ParentCid: 0000
  DirBase: 00030000 ObjectTable: e1000f88 TableSize: 112.
  Image: System
  VadRoot fb666388 Clone 0 Private 4. Modified 9850. Locked 0.
  FB667BBC MutantState Signalled OwningThread 0
  Token               e10008f0
  ElapsedTime            15:06:36.0338
  UserTime             0:00:00.0000
  KernelTime            0:00:54.0818
  QuotaPoolUsage[PagedPool]     1480
Working Set Sizes (now,min,max) (3, 50, 345)
  PeakWorkingSetSize        118
  VirtualSize            1 Mb
  PeakVirtualSize          1 Mb
  PageFaultCount          992
  MemoryPriority          BACKGROUND
  BasePriority           8
  CommitCharge           8

    THREAD fb667780 Cid 2.1 Teb: 00000000 Win32Thread: 80144900 WAIT: (WrFreePage) KernelMode Non-Alertable
    80144fc0 SynchronizationEvent
    Not impersonating
    Owning Process fb667a00
    WaitTime (seconds)   32278
    Context Switch Count  787
    UserTime         0:00:00.0000
    KernelTime        0:00:21.0821
    Start Address Phase1Initialization (0x801aab44)
    Initial Sp fb26f000 Current Sp fb26ed00
    Priority 0 BasePriority 0 PriorityDecrement 0 DecrementCount 0

    ChildEBP RetAddr Args to Child
    fb26ed18 80118efc c0502000 804044b0 00000000 KiSwapThread+0xb5
    fb26ed3c 801289d9 80144fc0 00000008 00000000 KeWaitForSingleObject+0x1c2
```

など、他の拡張機能への入力として使用できるプロセス オブジェクトのアドレスに注意してください[ **! 処理**](-handle.md)、さらに情報を取得します。

次の表では、前の例では、内の要素の一部について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要素</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">待機</td>
<td align="left">このヘッダーの後にかっこで囲まれたコメントは、待機理由を説明します。 コマンドは、 <strong><a href="dt--display-type-.md" data-raw-source="[dt nt!_KWAIT_REASON](dt--display-type-.md)">dt nt! _KWAIT_REASON</a></strong>すべて待機理由の一覧が表示されます。</td>
</tr>
<tr class="even">
<td align="left"><p>経過時間</p></td>
<td align="left"><p>プロセスが作成されてから経過した時間の量を示します。 これは、Hours:Minutes:Seconds.Milliseconds の単位で表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>UserTime</p></td>
<td align="left"><p>プロセスがユーザー モードで実行された時間の量を示します。 UserTime の値が非常に高い場合は、システム リソースを奪うがいるプロセスの特定に可能性があります。 単位は、経過時間のものと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>KernelTime</p></td>
<td align="left"><p>プロセスがカーネル モードで実行された時間の量を示します。 KernelTime の値が非常に高い場合は、システム リソースを奪うがいるプロセスの特定に可能性があります。 単位は、経過時間のものと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>作業セット サイズ</p></td>
<td align="left"><p>ページで、プロセスでは、現在、最小および最大ワーキング セットのサイズを一覧表示します。 非常に大きい作業セットのサイズは、メモリ リークが発生またはシステム リソースを奪うされているプロセスの兆候であることができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>QuotaPoolUsage エントリ</p></td>
<td align="left"><p>プロセスによって使用されるページおよび非ページ プールの一覧を表示します。 システムでメモリ リーク、すべてのプロセスで過度の非ページ プールの使用状況を探してわかりますのどのプロセスが、メモリ リークが発生します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>複製</p></td>
<td align="left"><p>POSIX または Interix サブシステムによって、プロセスが作成されたかどうかを示します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Private</p></td>
<td align="left"><p>プロセスによって現在使用されているプライベートの (非共有可能) ページの数を示します。 これでページとページ メモリの両方が含まれます。</p></td>
</tr>
</tbody>
</table>

 

だけでなく、プロセスの一覧については、スレッドの情報には、スレッドがロックするリソースの一覧が含まれています。 この情報は、スレッドのヘッダーの後の出力の 3 行目に表示されます。 この例では、スレッドは、SynchronizationEvent 80144 fc 0 のアドレスを持つ、1 つのリソースでのロックを保持します。 このアドレスによって表示されるロックの一覧を比較することによって、 [ **! kdext\*.locks** ](-locks---kdext--locks-.md)拡張機能では、どのスレッドがリソースに排他ロックをいるを確認できます。

[ **! スタック**](-stacks.md)拡張機能がすべてのスレッドの状態の概要を示します。 これは、代わりに使用できる、! リソースの競合やデッドロックなどのマルチ スレッドの問題をデバッグする場合は特に、システムの簡単な概要を取得する拡張機能を処理します。

 

 





