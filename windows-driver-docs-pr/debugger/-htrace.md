---
title: htrace
description: Htrace 拡張機能が表示されますスタック トレース情報の 1 つまたは複数のハンドル。
ms.assetid: 1da92c8d-8f77-4b30-a908-bcc33ad05cce
keywords:
- ハンドル、htrace 拡張機能
- Windows デバッグ htrace
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- htrace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e74f5d92ba334153c61b8c92c0d49c7619d71287
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336477"
---
# <a name="htrace"></a>!htrace


**! Htrace**ハンドルの 1 つまたは複数の拡張機能が表示されますスタック トレース情報。

ユーザー モードの構文

```dbgcmd
!htrace [Handle [Max_Traces]] 
!htrace -enable [Max_Traces]
!htrace -snapshot
!htrace -diff
!htrace -disable
!htrace -? 
```

カーネル モードの構文

```dbgcmd
    !htrace [Handle [Process [Max_Traces]]] 
!htrace -? 
```

## <a name="span-idddkhtracedbgspanspan-idddkhtracedbgspanparameters"></a><span id="ddk__htrace_dbg"></span><span id="DDK__HTRACE_DBG"></span>パラメーター


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span> *ハンドル*   
スタック トレースが表示されるハンドルを指定します。 場合*処理*が 0 または省略すると、プロセス内のすべてのハンドルのスタック トレースが表示されます。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span> *プロセス*   
(カーネル モードのみ)表示されるハンドルを持つプロセスを指定します。 場合*プロセス*が 0 または省略すると、現在プロセスが使用されます。 ユーザー モードでは、現在のプロセスが常に使用します。

<span id="_______Max_Traces______"></span><span id="_______max_traces______"></span><span id="_______MAX_TRACES______"></span> *最大\_トレース*   
表示するスタック トレースの最大数を指定します。 ユーザー モードで、このパラメーターを省略した場合、ターゲット プロセスのすべてのスタック トレースが表示されます。

<span id="_______-enable______"></span><span id="_______-ENABLE______"></span> **-enable**   
(ユーザー モードのみ)ハンドルのトレースを有効にし、初期状態として使用するハンドル情報の最初のスナップショットを取得、 **- 差分**オプション。

<span id="_______-snapshot______"></span><span id="_______-SNAPSHOT______"></span> **-snapshot**   
(ユーザー モードのみ)現在のハンドルを初期状態として使用する情報のスナップショットを取得、 **- 差分**オプション。

<span id="_______-diff______"></span><span id="_______-DIFF______"></span> **差分-**   
(ユーザー モードのみ)取得されたハンドル情報の最後のスナップショットを使用して現在のハンドル情報を比較します。 まだ開いているすべてのハンドルを表示します。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span> **-を無効にします。**   
(ユーザー モードだけです。Windows Server 2003 および以降のみ) を無効には、トレースを処理します。 Windows XP では、ターゲット プロセスを終了することによってのみハンドルのトレースを無効にできます。

<span id="_______-_______"></span> **-?**   
デバッガー コマンド ウィンドウで、この拡張機能の簡単なヘルプ テキストを表示します。

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
<td align="left"><p></p>
Kdexts.dll Ntsdexts.dll</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ハンドルの詳細については、Microsoft Windows SDK のドキュメントを参照してくださいと*Microsoft Windows internals 』* Mark Russinovich と David Solomon します。 (これらのリソースできない場合がありますのいくつかの言語および国。)さらに特定のハンドルに関する情報を表示するには、使用、 [ **! 処理**](-handle.md)拡張機能。

<a name="remarks"></a>注釈
-------

前に **! htrace**使用できる処理は、トレースを有効にする必要があります。 ハンドルのトレースを有効にする方法の 1 つは、入力する、 **! htrace-有効にする**コマンド。 スタック トレース情報がそれぞれ保存はハンドルのトレースが有効にすると、プロセスが、ハンドルを開いたときは、ハンドルを閉じるか、または無効なハンドルを参照します。 このスタック トレース情報を **! htrace**が表示されます。

**注**  ハンドル Application Verifier をターゲット プロセスのアクティブ化を選択してトレースを有効することも、**処理**オプション。

 

によって報告されたトレースの一部 **! htrace**別のプロセスのコンテキストからがあります。 この場合、戻り値のアドレスは、プロセスの現在のコンテキストで正しく解決できない場合がありますか、間違ったシンボルに解決する可能性があります。

次の例では、プロセス 0x81400300 ですべてハンドルに関する情報が表示されます。

```dbgcmd
kd> !htrace 0 81400300
Process 0x81400300
ObjectTable 0xE10CCF60
## 

Handle 0x7CC - CLOSE:
0x8018FCB9: ntoskrnl!ExDestroyHandle+0x103
0x801E1D12: ntoskrnl!ObpCloseHandleTableEntry+0xE4
0x801E1DD9: ntoskrnl!ObpCloseHandle+0x85
0x801E1EDD: ntoskrnl!NtClose+0x19
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7CC - OPEN:
0x8018F44A: ntoskrnl!ExCreateHandle+0x94
0x801E3390: ntoskrnl!ObpCreateUnnamedHandle+0x10C
0x801E7317: ntoskrnl!ObInsertObject+0xC3
0x77DE23B2: KERNEL32!CreateSemaphoreA+0x66
0x010011C5: badhandle!main+0x45
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7DC - BAD REFERENCE:
0x8018F709: ntoskrnl!ExMapHandleToPointerEx+0xEA
0x801E10F2: ntoskrnl!ObReferenceObjectByHandle+0x12C
0x801902BE: ntoskrnl!NtSetEvent+0x6C
0x80154965: ntoskrnl!_KiSystemService+0xC4
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7DC - CLOSE:
0x8018FCB9: ntoskrnl!ExDestroyHandle+0x103
0x801E1D12: ntoskrnl!ObpCloseHandleTableEntry+0xE4
0x801E1DD9: ntoskrnl!ObpCloseHandle+0x85
0x801E1EDD: ntoskrnl!NtClose+0x19
0x010012C1: badhandle!mainCRTStartup+0xE3
## 0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D

Handle 0x7DC - OPEN:
0x8018F44A: ntoskrnl!ExCreateHandle+0x94
0x801E3390: ntoskrnl!ObpCreateUnnamedHandle+0x10C
0x801E7317: ntoskrnl!ObInsertObject+0xC3
0x77DE265C: KERNEL32!CreateEventA+0x66
0x010011A0: badhandle!main+0x20
0x010012C1: badhandle!mainCRTStartup+0xE3
0x77DE0B2F: KERNEL32!BaseProcessStart+0x3D
## 

Parsed 0x6 stack traces.
Dumped 0x5 stack traces.
```

 

 





