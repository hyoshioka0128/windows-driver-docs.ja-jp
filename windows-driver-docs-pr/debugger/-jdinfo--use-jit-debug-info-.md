---
title: .jdinfo (JIT_DEBUG_INFO の使用)
description: .Jdinfo コマンドは、例外とジャスト イン タイム (JIT) デバッグのコンテキストのソースとして JIT_DEBUG_INFO 構造体を使用します。
ms.assetid: C35A2A04-CF0E-475e-8471-2A8562BB3650
keywords:
- JIT_DEBUG_INFO (.jdinfo) コマンド---付録を使用します。
- JIT_DEBUG_INFO ----- Appendix
- .jdinfo (JIT_DEBUG_INFO を使用して) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .jdinfo (Use JIT_DEBUG_INFO)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 42874c723d864c0596ac225a4166d4ac220f0eb4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579771"
---
# <a name="jdinfo-use-jitdebuginfo"></a>.jdinfo (JIT を使用して、\_デバッグ\_情報)


**.Jdinfo**コマンドは、JIT を使用して\_デバッグ\_例外とジャスト イン タイム (JIT) デバッグのコンテキストのソースとして情報構造体。 構造体へのアドレスに渡される、 **.jdinfo** AeDebug レジストリ エントリで指定されている %p パラメーターを使用してコマンドします。

使用するレジストリ キーの詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。 レジスタのコンテキストの詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

```dbgcmd
.jdinfo Address 
```

## <a name="span-idddkapcmetausejitdebuginfodbgspanspan-idddkapcmetausejitdebuginfodbgspanparameters"></a><span id="ddk_apc_meta_use_jit_debug_info_dbg"></span><span id="DDK_APC_META_USE_JIT_DEBUG_INFO_DBG"></span>パラメーター


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *アドレス*   
JIT のアドレス指定\_デバッグ\_情報構造体。 構造体へのアドレスに渡される、 **.jdinfo** AeDebug レジストリ エントリで指定されている %p パラメーターを使用してコマンドします。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idexamplespanspan-idexamplespanspan-idexamplespanexample"></a><span id="Example"></span><span id="example"></span><span id="EXAMPLE"></span>例

この例のショー、WinDbg を使用する AeDebug レジストリ エントリを構成する方法は、JIT デバッガーとして使用できます。

```dbgcmd
Debugger = "Path\WinDbg.EXE -p %ld -e %ld -c ".jdinfo 0x%p"
```

次に、クラッシュが発生すると、構成済みの JIT デバッガーが呼び出され、%p パラメーターは、JIT のアドレスを渡すために使用\_デバッグ\_情報構造体を **.jdinfo**デバッガーの後に実行されるコマンドです開始されます。

```dbgcmd
nMicrosoft (R) Windows Debugger Version 10.0.10240.9 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

*** wait with pending attach
Executable search path is: 
...
ModLoad: 00000000`68a20000 00000000`68ac3000   C:\WINDOWS\WinSxS\amd64_microsoft.vc90.crt_1fc8b3b9a1e18e3b_9.0.30729.9247_none_08e394a1a83e212f\MSVCR90.dll
(153c.5d0): Break instruction exception - code 80000003 (first chance)
Processing initial command '.jdinfo 0x00000000003E0000'
ntdll!DbgBreakPoint:
00007ffc`81a986a0 cc              int     3
0:003> .jdinfo 0x00000000003E0000
----- Exception occurred on thread 0:15c8
ntdll!ZwWaitForMultipleObjects+0x14:
00007ffc`81a959a4 c3              ret

----- Exception record at 00000000`003e0028:
ExceptionAddress: 00007ff791d81014 (CrashAV_x64!wmain+0x0000000000000014)
   ExceptionCode: c0000005 (Access violation)
  ExceptionFlags: 00000000
NumberParameters: 2
   Parameter[0]: 0000000000000001
   Parameter[1]: 0000000000000000
Attempt to write to address 0000000000000000

----- Context record at 00000000`003e00c0:
rax=0000000000000000 rbx=0000000000000000 rcx=00007ffc81a954d4
rdx=0000000000000000 rsi=0000000000000000 rdi=0000000000000001
rip=00007ff791d81014 rsp=00000000006ff8b0 rbp=0000000000000000
 r8=00000000006ff808  r9=0000000000000000 r10=0000000000000000
r11=0000000000000000 r12=0000000000000000 r13=0000000000000000
r14=0000000000000000 r15=0000000000000000
iopl=0         nv up ei pl zr na po nc
cs=0033  ss=002b  ds=002b  es=002b  fs=0053  gs=002b             efl=00010246
CrashAV_x64!wmain+0x14:
00007ff7`91d81014 45891b          mov     dword ptr [r11],r11d ds:00000000`00000000=????????
```

<a name="remarks"></a>コメント
-------

**.Jdinfo**コマンドでは、 **AeDebug**レジストリ情報が Windows Vista で導入されました。 使用するレジストリ キーの詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。 **.Jdinfo**コマンドは、JIT のアドレスを受け取ります\_デバッグ\_情報用に、システム設定を**AeDebug**し、クラッシュの原因となった例外に、コンテキストを設定します。

使用することができます、 **.jdinfo**コマンドの代わりに **-g**で**AeDebug**のデバッガーに設定して、 **AeDebug**を必要とせずに state実行します。

この状態は、通常の状況では、ユーザー モード例外が発生したときに、次のシーケンスが発生したため、便利です。

1.  Microsoft Windows オペレーティング システムでは、アプリケーションの実行を停止します。

2.  事後分析のデバッガーが開始されます。

3.  デバッガーは、アプリケーションにアタッチします。

4.  デバッガーでは、"Go"コマンドを発行します。 (このコマンドが原因で発生、 **-g**で、 **AeDebug**キー)。

5.  ターゲットを実行しようと、可能性があります。 またはと、同じ例外が発生しません。

6.  この例外は、デバッガーを中断します。

これらのイベントが原因で発生することがいくつかの問題があります。

-   例外常に、繰り返し可能性がありますが再起動されると、例外が存在しない一時的な状態が原因です。

-   別の例外などの別のイベントが発生する可能性があります。 元のイベントと同じかどうかを知る方法はありません。

-   デバッガーをアタッチするには、スレッドでローダー ロックが保持している場合にブロックされることが、新しいスレッドを挿入する必要があります。 新しいスレッドを挿入すると、プロセスの重要な国内騒乱状態を指定できます。

使用する場合 **-c .jdinfo**の代わりに **-g**で、 **AeDebug**キー、実行は行われません。 JIT から例外情報を取得する代わりに、\_デバッグ\_%p 変数を使用して情報構造体。

たとえば、次**AeDebug**キー。

```dbgcmd
ntsd -p %ld -e %ld -c ".jdinfo 0x%p"
```

次の例は、さらに少なくします。 **-Pv**スイッチによって noninvasively、アタッチするデバッガー ターゲットには新しいスレッドを挿入できません。

```dbgcmd
ntsd -pv -p %ld -e %ld -c ".jdinfo 0x%p"
```

この待合室オプションを使用する場合、デバッガーを終了しても、プロセスは終了しません。 使用することができます、 [ **.kill (プロセスの強制終了)** ](-kill--kill-process-.md)プロセスを終了するコマンド。

使用する必要がありますダンプ ファイルのデバッグにこれを使用する場合は、 [ **.dump/j** ](-dump--create-dump-file-.md) JIT を追加する\_デバッグ\_ダンプ ファイルの作成時にダンプ ファイルに情報の構造体。

JIT\_デバッグ\_情報の構造は次のように定義されます。

```dbgcmd
typedef struct _JIT_DEBUG_INFO {
    DWORD dwSize;
    DWORD dwProcessorArchitecture;
    DWORD dwThreadID;
    DWORD dwReserved0;
    ULONG64 lpExceptionAddress;
    ULONG64 lpExceptionRecord;
    ULONG64 lpContextRecord;
} JIT_DEBUG_INFO, *LPJIT_DEBUG_INFO;
```

Dt コマンドを使用するには、JIT を表示する\_デバッグ\_情報構造体。

```dbgcmd
0: kd> dt JIT_DEBUG_INFO
nt!JIT_DEBUG_INFO
   +0x000 dwSize           : Uint4B
   +0x004 dwProcessorArchitecture : Uint4B
   +0x008 dwThreadID       : Uint4B
  +0x00c dwReserved0      : Uint4B
   +0x010 lpExceptionAddress : Uint8B
   +0x018 lpExceptionRecord : Uint8B
   +0x020 lpContextRecord  : Uint8B
```

**例外レコード、呼び出し履歴および LastEvent WinDbg を使用して表示します。**

エラーの瞬間にコンテキストを設定する .jdinfo コマンドが使用された後は、原因を調査する次のように .jdinfo、呼び出し履歴、および、lastevent によって返される例外レコードを表示できます。

```dbgcmd
0:000> .jdinfo  0x00000000003E0000
----- Exception occurred on thread 0:15c8
ntdll!NtWaitForMultipleObjects+0x14:
00007ffc`81a959a4 c3              ret

----- Exception record at 00000000`003e0028:
ExceptionAddress: 00007ff791d81014 (CrashAV_x64!wmain+0x0000000000000014)
   ExceptionCode: c0000005 (Access violation)
  ExceptionFlags: 00000000
NumberParameters: 2
   Parameter[0]: 0000000000000001
   Parameter[1]: 0000000000000000
Attempt to write to address 0000000000000000
...

0:000> k
  *** Stack trace for last set context - .thread/.cxr resets it
# Child-SP          RetAddr           Call Site
00 00000000`006ff8b0 00007ff7`91d811d2 CrashAV_x64!wmain+0x14 [c:\my\my_projects\crash\crashav\crashav.cpp @ 14]
01 00000000`006ff8e0 00007ffc`7fa38364 CrashAV_x64!__tmainCRTStartup+0x11a [f:\dd\vctools\crt_bld\self_64_amd64\crt\src\crtexe.c @ 579]
02 00000000`006ff910 00007ffc`81a55e91 KERNEL32!BaseThreadInitThunk+0x14
03 00000000`006ff940 00000000`00000000 ntdll!RtlUserThreadStart+0x21

0:000> .lastevent
Last event: 153c.5d0: Break instruction exception - code 80000003 (first chance)
  debugger time: Thu Sep  8 12:55:08.968 2016 (UTC - 7:00)
```

 

 





