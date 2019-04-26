---
title: ロック kdext
description: Kdextx86.dll と Kdexts.dll ロックの拡張機能では、カーネル ÷ リソースのロックに関する情報が表示されます。
ms.assetid: c1be6c6c-0028-459f-9c92-61df52cbc4b6
keywords:
- kdext ロックの拡張機能
- 次のロック
- デッドロック
- Windows デバッグ kdext .locks をロックします。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( kdext .locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6bcef64132d52b5f0d4af99fbb45c4353e5dd25b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336163"
---
# <a name="locks-kdextlocks"></a>! ロック (! kdext\*.locks)


**! ロック**Kdextx86.dll と Kdexts.dll で拡張機能には、カーネル ÷ リソースのロックに関する情報が表示されます。

この拡張機能のコマンドと混同しないで、 [ **! ntsdexts.locks** ](-locks---ntsdexts-locks-.md)拡張機能コマンド。

```dbgcmd
!locks [Options] [Address]
```

## <a name="span-idddkkdextlocksdbgspanspan-idddkkdextlocksdbgspanparameters"></a><span id="ddk__kdext__locks_dbg"></span><span id="DDK__KDEXT__LOCKS_DBG"></span>パラメーター


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span> *オプション*   
表示される情報の量を指定します。 次のオプションの任意の組み合わせを使用できます。

<span id="-v"></span><span id="-V"></span>**-v**  
各ロックについての詳細を表示します。

<span id="-p"></span><span id="-P"></span>**-p**  
パフォーマンスの統計情報をなど、ロックに関する情報をすべてを表示します。

<span id="-d"></span><span id="-D"></span>**-d**  
すべてのロックに関する情報を表示します。 それ以外の場合、競合とロックだけが表示されます。)

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
表示する次のロックの 16 進数のアドレスを指定します。 場合*アドレス*が 0 または省略すると、システム内のすべてのスケジュール作成ロックに関する情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

**! ロック**拡張機能は、スレッドがリソースで保持されているすべてのロックを表示します。 ロックを共有することができます、他のスレッドは意味がないことができますにアクセスしたりそのリソース。 この情報は、システムでデッドロックが発生する場合に便利です。 実行中のスレッドが必要なリソースに対する排他ロックを保持する 1 つの実行中でないスレッドでデッドロックが発生します。

通常、実行中のスレッドで必要とされるリソースに排他ロックを保持する 1 つの実行中でないスレッドを検索して Microsoft Windows 2000 のデッドロックを特定できます。 ほとんどのロックが共有されます。

基本的な例を次に示します **! ロック**出力。

```dbgcmd
kd> !locks
**** DUMP OF ALL RESOURCE OBJECTS ****
KD: Scanning for held locks......

Resource @ 0x80e97620    Shared 4 owning threads
     Threads: ff688da0-01<*> ff687da0-01<*> ff686da0-01<*> ff685da0-01<*> 
KD: Scanning for held locks.......................................................

Resource @ 0x80e23f38    Shared 1 owning threads
     Threads: 80ed0023-01<*> *** Actual Thread 80ed0020
KD: Scanning for held locks.

Resource @ 0x80d8b0b0    Shared 1 owning threads
     Threads: 80ed0023-01<*> *** Actual Thread 80ed0020
2263 total locks, 3 locks currently held
```

表示される各スレッドのアドレスがそのスレッドの数 (たとえば、「-01」) に続くことに注意してください。 スレッドが続く場合"&lt;\*&gt;"、スレッドがロックの所有者のいずれかであります。 場合によっては、最初のスレッドのアドレスには、オフセットが含まれています。 その場合は、実際のスレッドのアドレスがも表示されます。

これらのリソース オブジェクトのいずれかの詳細について参照する場合は、次のアドレスを使用して、"リソース @"以降のコマンドの引数として。 前の例に示すように 2 番目のリソースを調査するために使用する可能性があります[ **dt ÷ リソース 80d8b0b0** ](dt--display-type-.md)または[ **! スレッド 80ed0020** ](-thread.md). 使用することもできます、 **! ロック**拡張機能を使用して、 **-v**オプション。

```dbgcmd
kd> !locks -v 80d8b0b0

Resource @ 0x80d8b0b0    Shared 1 owning threads
     Threads: 80ed0023-01<*> *** Actual Thread 80ed0020

     THREAD 80ed0020  Cid 4.2c  Teb: 00000000 Win32Thread: 00000000 WAIT: (WrQueue) KernelMode Non-Alertable
         8055e100  Unknown
     Not impersonating
GetUlongFromAddress: unable to read from 00000000
     Owning Process 80ed5238
     WaitTime (ticks)          44294977
     Context Switch Count      147830             
     UserTime                  0:00:00.0000
     KernelTime                0:00:02.0143
     Start Address nt!ExpWorkerThread (0x80506aa2)
     Stack Init fafa4000 Current fafa3d18 Base fafa4000 Limit fafa1000 Call 0
     Priority 13 BasePriority 13 PriorityDecrement 0
ChildEBP RetAddr  
fafa3d30 804fe997 nt!KiSwapContext+0x25 (FPO: [EBP 0xfafa3d48] [0,0,4]) [D:\NT\base\ntos\ke\i386\ctxswap.asm @ 139]
fafa3d48 80506a17 nt!KiSwapThread+0x85 (FPO: [Non-Fpo]) (CONV: fastcall) [d:\nt\base\ntos\ke\thredsup.c @ 1960]
fafa3d78 80506b36 nt!KeRemoveQueue+0x24c (FPO: [Non-Fpo]) (CONV: stdcall) [d:\nt\base\ntos\ke\queueobj.c @ 542]
fafa3dac 805ad8bb nt!ExpWorkerThread+0xc6 (FPO: [Non-Fpo]) (CONV: stdcall) [d:\nt\base\ntos\ex\worker.c @ 1130]
fafa3ddc 8050ec72 nt!PspSystemThreadStartup+0x2e (FPO: [Non-Fpo]) (CONV: stdcall) [d:\nt\base\ntos\ps\create.c @ 2164]
00000000 00000000 nt!KiThreadStartup+0x16 [D:\NT\base\ntos\ke\i386\threadbg.asm @ 81]

1 total locks, 1 locks currently held
```

 

 





