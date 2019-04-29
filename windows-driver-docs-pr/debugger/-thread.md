---
title: スレッド (thread)
description: スレッドの拡張機能では、ETHREAD ブロックを含め、ターゲット システム上のスレッドに関する概要情報が表示されます。 このコマンドは、カーネル モードのデバッグ中にのみ使用できます。
ms.assetid: 5d3cf2f7-02bf-4a94-b542-826ad2b66a6f
keywords:
- Windows デバッグ スレッド
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- thread
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7c9c5218b648e32736a70323cca9d32920b1d51a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338744"
---
# <a name="thread"></a>!thread


**! スレッド**拡張子 ETHREAD ブロックを含め、ターゲット システム上のスレッドに関する概要情報が表示されます。 このコマンドは、カーネル モードのデバッグ中にのみ使用できます。

この拡張機能のコマンドと同じではない、 [ **.thread (登録コンテキストの設定)** ](-thread--set-register-context-.md)コマンド。

構文

```dbgcmd
!thread [-p] [-t] [Address [Flags]]
```

## <a name="span-idddkthreaddbgspanspan-idddkthreaddbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>パラメーター


<span id="_______-p______"></span><span id="_______-P______"></span> **-p**   
スレッドを所有するプロセスに関する概要情報が表示されます。

<span id="_______-t______"></span><span id="_______-T______"></span> **-t**   
このオプションは、含まれているときに*アドレス*スレッド id、スレッドのアドレスではありません。

<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
ターゲット コンピューター上のスレッドの 16 進数のアドレスを指定します。 場合*アドレス*は-1 です。 または、省略すると、現在のスレッドを示します。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *フラグ*   
表示する詳細レベルを指定します。 *フラグ*次のビットの組み合わせにすることができます。 場合*フラグ*は 0、最小限の情報のみが表示されます。 0x6 を既定値には。

<span id="Bit_1__0x2_"></span><span id="bit_1__0x2_"></span><span id="BIT_1__0X2_"></span>ビット 1 (0x2)  
スレッドの待機状態が表示されます。

<span id="Bit_2__0x4_"></span><span id="bit_2__0x4_"></span><span id="BIT_2__0X4_"></span>ビット 2 (0x4)  
このビット ビット 1 (0x2) を使用する場合、影響を与えません。 ビット 1 にこのビットが使用されている場合は、スレッドに、スタック トレースが表示されます。

<span id="Bit_3__0x8_"></span><span id="bit_3__0x8_"></span><span id="BIT_3__0X8_"></span>ビット 3 (0x8)  
戻り値のアドレスでは、スタック ポインターを追加し、(Itanium システム) 上、 **bsp**値を関数ごとに表示される情報を登録して、関数の引数を表示しません。

<span id="Bit_4__0x10_"></span><span id="bit_4__0x10_"></span><span id="BIT_4__0X10_"></span>ビット 4 (0x10)  
このコマンドの実行中に指定したスレッドを所有するプロセスと同じプロセスのコンテキストを設定します。 これにより、スレッド スタックのより正確に表示します。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

スレッドがカーネル モードについては、次を参照してください。[変更コンテキスト](changing-contexts.md)します。 プロセスとスレッドの分析に関する詳細については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。

<a name="remarks"></a>コメント
-------

Windows 10 の使用例を次に示します。

```dbgcmd
0: kd> !thread 0xffffcb088f0a4480            
THREAD ffffcb088f0a4480  Cid 0e34.3814  Teb: 0000001a27ca6000 Win32Thread: 0000000000000000 RUNNING on processor 0
Not impersonating
DeviceMap                 ffffb80842016c20
Owning Process            ffffcb08905397c0       Image:         MsMpEng.exe
Attached Process          N/A            Image:         N/A
Wait Start TickCount      182835891      Ticks: 0
Context Switch Count      5989           IdealProcessor: 3             
UserTime                  00:00:01.046
KernelTime                00:00:00.296
Win32 Start Address 0x00007ffb3b2fd1b0
Stack Init ffff95818476add0 Current ffff958184769d30
Base ffff95818476b000 Limit ffff958184765000 Call 0000000000000000
Priority 8 BasePriority 8 PriorityDecrement 0 IoPriority 2 PagePriority 5
Child-SP          RetAddr           : Args to Child                                                           : Call Site
fffff802`59858c68 fffff801`b56d24aa : ffffcb08`8fd68010 00000000`00000000 fffff802`58259600 00000000`00000008 : nt!DbgBreakPointWithStatus [d:\rs2\minkernel\ntos\rtl\amd64\debugstb.asm @ 130] 
fffff802`59858c70 ffffcb08`8fd68010 : 00000000`00000000 fffff802`58259600 00000000`00000008 ffffcb08`8f0a4400 : 0xfffff801`b56d24aa
fffff802`59858c78 00000000`00000000 : fffff802`58259600 00000000`00000008 ffffcb08`8f0a4400 00000000`00000019 : 0xffffcb08`8fd68010
```

コマンドを使用して[ **! プロセス**](-process.md)アドレスを見つけるか、興味のあるスレッドのスレッド ID。

有用な情報、 **! スレッド**表示は次の表で説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>スレッドのアドレス</strong></p></td>
<td align="left"><p>16 進数の単語の後<em>スレッド</em>ETHREAD ブロックのアドレスです。 前の例では、スレッドのアドレスは、0xffffcb088f0a4480 が。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>スレッド ID</strong></p></td>
<td align="left"><p>単語の後の 2 つの 16 進数値<em>Cid</em>はプロセス ID とスレッド ID:<em>プロセス ID.thread ID</em>します。 前の例では、プロセス ID は、0x0e34、スレッド ID は 0x3814 です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>スレッド環境ブロックの終了</strong></p></td>
<td align="left"><p>16 進数の単語の後<em>Teb</em>終了スレッド環境ブロックのアドレスです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>システム サービスのディスパッチ テーブル</strong></p></td>
<td align="left"><p>16 進数の単語の後<em>Win32Thread</em>システム サービスのディスパッチ テーブルのアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>スレッドの状態</strong></p></td>
<td align="left"><p>スレッドの状態がという単語で始まる行の最後に表示される<em>を実行している</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>プロセスを所有しています。</strong></p></td>
<td align="left"><p>単語の後に 16 進数<em>を所有しているプロセス</em>はこのスレッドを所有するプロセスの」プロセスのアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>開始アドレス</strong></p></td>
<td align="left"><p>単語の後に 16 進数<em>開始アドレス</em>は、スレッドの開始アドレスです。 これは、シンボリック フォームに表示可能性があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ユーザー スレッド関数</strong></p></td>
<td align="left"><p>単語の後に 16 進数<em>Win32 開始アドレス</em>ユーザー スレッドの関数のアドレスです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>優先順位</strong></p></td>
<td align="left"><p>スレッドの優先度の情報に依存して、word<em>優先度</em>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>スタック トレース</strong></p></td>
<td align="left"><p>この表示の末尾に、スレッドのスタック トレースが表示されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





