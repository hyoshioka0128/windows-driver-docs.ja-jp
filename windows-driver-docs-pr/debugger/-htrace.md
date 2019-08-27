---
title: htrace
description: Htrace 拡張機能では、1つまたは複数のハンドルのスタックトレース情報が表示されます。
ms.assetid: 1da92c8d-8f77-4b30-a908-bcc33ad05cce
keywords:
- ハンドル、htrace 拡張機能
- htrace Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- htrace
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4245fa9056c587f1592d52e4e678c2f15a8145f6
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025237"
---
# <a name="htrace"></a>!htrace


**! Htrace**拡張機能は、1つまたは複数のハンドルのスタックトレース情報を表示します。

ユーザーモードの構文

```dbgcmd
!htrace [Handle [Max_Traces]] 
!htrace -enable [Max_Traces]
!htrace -snapshot
!htrace -diff
!htrace -disable
!htrace -? 
```

カーネルモード構文

```dbgcmd
    !htrace [Handle [Process [Max_Traces]]] 
!htrace -? 
```

## <a name="span-idddk__htrace_dbgspanspan-idddk__htrace_dbgspanparameters"></a><span id="ddk__htrace_dbg"></span><span id="DDK__HTRACE_DBG"></span>パラメータ


<span id="_______Handle______"></span><span id="_______handle______"></span><span id="_______HANDLE______"></span>*ハンドル*   
スタックトレースを表示するハンドルを指定します。 *Handle*が0または省略された場合、プロセス内のすべてのハンドルのスタックトレースが表示されます。

<span id="_______Process______"></span><span id="_______process______"></span><span id="_______PROCESS______"></span>*プロセス*   
(カーネルモードのみ)ハンドルを表示するプロセスを指定します。 *Process*が0であるか省略されている場合は、現在のプロセスが使用されます。 ユーザーモードでは、現在のプロセスが常に使用されます。

<span id="_______Max_Traces______"></span><span id="_______max_traces______"></span><span id="_______MAX_TRACES______"></span>*最大\_トレース数*   
表示するスタックトレースの最大数を指定します。 ユーザーモードでは、このパラメーターを省略すると、ターゲットプロセスのすべてのスタックトレースが表示されます。

<span id="_______-enable______"></span><span id="_______-ENABLE______"></span> **-enable**   
(ユーザーモードのみ)ハンドルトレースを有効にし、 **-diff**オプションによって初期状態として使用するハンドル情報の最初のスナップショットを取得します。

<span id="_______-snapshot______"></span><span id="_______-SNAPSHOT______"></span> **-スナップショット**   
(ユーザーモードのみ) **-Diff**オプションによって初期状態として使用される、現在のハンドル情報のスナップショットを取得します。

<span id="_______-diff______"></span><span id="_______-DIFF______"></span> **-diff**   
(ユーザーモードのみ)現在のハンドル情報を、取得したハンドル情報の最後のスナップショットと比較します。 開いているすべてのハンドルを表示します。

<span id="_______-disable______"></span><span id="_______-DISABLE______"></span> **-disable**   
(ユーザーモードのみです。Windows Server 2003 以降のみ) ハンドルトレースを無効にします。 Windows XP では、ハンドルトレースはターゲットプロセスを終了することによってのみ無効にできます。

<span id="_______-_______"></span> **-?**    
デバッガーコマンドウィンドウにこの拡張機能の簡単なヘルプテキストを表示します。

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
Kdexts .dll (.dll)</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

ハンドルの詳細については、Microsoft Windows SDK のドキュメントと、Mark Russinovich と David ソロモンを参照してください。 特定のハンドルに関する詳細情報を表示するには、 [ **! handle**](-handle.md)拡張を使用します。

<a name="remarks"></a>コメント
-------

**! Htrace**を使用する前に、ハンドルのトレースを有効にする必要があります。 ハンドルトレースを有効にする方法の1つとして、 **! htrace-enable**コマンドを入力する方法があります。 ハンドルトレースが有効になっている場合、プロセスがハンドルを開くかハンドルを閉じるか、または無効なハンドルを参照するたびに、スタックトレース情報が保存されます。 このスタックトレース情報は、 **! htrace**によって表示されます。

また、ターゲットプロセスのアプリケーション検証ツールをアクティブ化し、[ハンドル] オプションを選択して、ハンドルトレースを有効にすることもできます。   

 

**! Htrace**によって報告されたトレースのいくつかは、別のプロセスコンテキストからのものである可能性があります。 この場合、現在のプロセスコンテキストで返されるアドレスが正しく解決されないか、間違ったシンボルに解決される可能性があります。

次の例では、プロセス0x81400300 のすべてのハンドルに関する情報を表示します。

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

 

 





