---
title: kdext をロックする
description: Kdextx86 と Kdexts の locks 拡張機能によって、カーネルの負荷ロックに関する情報が表示されます。
ms.assetid: c1be6c6c-0028-459f-9c92-61df52cbc4b6
keywords:
- kdext ロック拡張機能
- ÷のロック
- デッドロック
- kdext をロックします。 Windows のデバッグをロックします。
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- locks ( kdext .locks)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9292368e6a9b374518c6c260a75db387836c646f
ms.sourcegitcommit: 73a693bf52f07169f38e6a2a68bccaa8db8faf2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68341191"
---
# <a name="locks-kdextlocks"></a>! locks (! kdext\*. locks)


Kdextx86 と Kdexts の **! locks**拡張機能には、カーネルのバージョンのロックに関する情報が表示されます。

この拡張コマンドは、 [ **! ntsdexts. locks**](-locks---ntsdexts-locks-.md)拡張コマンドと混同しないようにしてください。

```dbgcmd
!locks [Options] [Address]
```

## <a name="span-idddkkdextlocksdbgspanspan-idddkkdextlocksdbgspanparameters"></a><span id="ddk__kdext__locks_dbg"></span><span id="DDK__KDEXT__LOCKS_DBG"></span>パラメータ


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*オプション*   
表示する情報の量を指定します。 次のオプションの任意の組み合わせを使用できます。

<span id="-v"></span><span id="-V"></span> **-v**  
各ロックに関する詳細情報を表示します。

<span id="-p"></span><span id="-P"></span> **-p**  
パフォーマンス統計を含む、ロックに関する利用可能なすべての情報を表示します。

<span id="-d"></span><span id="-D"></span> **-d.ddd...e**  
すべてのロックに関する情報を表示します。 そうしないと、競合が発生したロックのみが表示されます)。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*アドレス*   
表示する場合は、表示するときには、の16進形式のアドレスを指定します。 *Address*が0または省略されている場合は、システム内のすべてのについての情報が表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 以降</strong></p></td>
<td align="left"><p>Kdexts .dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

**! Locks**拡張機能は、リソースに保持されているすべてのロックをスレッド別に表示します。 ロックは共有または排他的に使用できます。つまり、他のスレッドがそのリソースにアクセスできないことを意味します。 この情報は、システムでデッドロックが発生した場合に役立ちます。 デッドロックは、実行中のスレッドが必要とするリソースに対して排他ロックを保持している、実行中でないスレッドがあることが原因で発生します。

通常、実行中のスレッドが必要とするリソースに排他ロックを保持する非実行スレッドを1つ見つけることによって、Microsoft Windows 2000 でデッドロックを特定できます。 ほとんどのロックは共有されています。

基本的な **! locks**出力の例を次に示します。

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

表示される各スレッドのアドレスの後にスレッドカウントが続きます (たとえば、"-01")。 スレッドの後に "&lt;\*&gt;" が続く場合、そのスレッドはロックの所有者の1つです。 場合によっては、最初のスレッドアドレスにオフセットが含まれます。 その場合は、実際のスレッドアドレスも表示されます。

これらのリソースオブジェクトの1つに関する詳細情報を検索する場合は、後のコマンドの\@引数として "resource" に続くアドレスを使用します。 前の例で示した2番目のリソースを調査するには、 [**dt の 80d8b0b0**](dt--display-type-.md)または[ **! thread 80ed0020**](-thread.md)を使用します。 または、 **-v**オプションを使用して、 **! locks**拡張機能をもう一度使用することもできます。

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

 

 





