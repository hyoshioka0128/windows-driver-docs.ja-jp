---
title: スタック
description: スタックの拡張機能では、カーネル スタックに関する情報が表示されます。
ms.assetid: f0777609-4785-4a6b-a6f5-9efaeb608df7
keywords:
- Windows デバッグ履歴
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- stacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3fb605c7615cbec848300063f41a9281f4b26d20
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239149"
---
# <a name="stacks"></a>!stacks


**! スタック**拡張機能は、カーネル スタックに関する情報を表示します。

構文

```dbgcmd
!stacks [Detail [FilterString]] 
```

## <a name="span-idddkstacksdbgspanspan-idddkstacksdbgspanparameters"></a><span id="ddk__stacks_dbg"></span><span id="DDK__STACKS_DBG"></span>パラメーター


<span id="_______Detail______"></span><span id="_______detail______"></span><span id="_______DETAIL______"></span> *詳細*   
表示に使用する詳細レベルを指定します。 次の表に、有効な値*詳細*します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>現在のカーネル スタックの概要を表示します。 これが既定値です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>現在のカーネル スタックと同様に、ページは現在のスタックが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>すべてのスタック ページアウト現在スタックして現在のカーネル スタックのため完全なパラメーターが表示されます。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______FilterString______"></span><span id="_______filterstring______"></span><span id="_______FILTERSTRING______"></span> *FilterString*   
シンボルの指定された部分文字列が含まれているスレッドのみが表示されます。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

カーネル スタックの詳細については、次を参照してください。 *Microsoft Windows internals 』*、Mark Russinovich と David Solomon します。 

<a name="remarks"></a>注釈
-------

**! スタック**拡張機能がすべてのスレッドの状態の概要を示します。 代わりにこの拡張機能を使用することができます、 [ **! プロセス**](-process.md)リソースの競合やデッドロックなどのマルチ スレッドの問題をデバッグする場合は特に、システムの簡単な概要を取得する拡張機能。

[ **! Findstack** ](-findstack.md)ユーザー モードの拡張機能では、特定のスタックに関する情報も表示されます。

最も簡単な例を次に示します **! スタック**表示。

```dbgcmd
kd> !stacks 0
Proc.Thread  .Thread  ThreadState  Blocker
                                     [System]
   4.000050  827eea10  Blocked    +0xfe0343a5

                                     [smss.exe]

                                     [csrss.exe]
  b0.0000a8  82723b70  Blocked    ntoskrnl!_KiSystemService+0xc4
  b0.0000c8  82719620  Blocked    ntoskrnl!_KiSystemService+0xc4
  b0.0000d0  827d5d50  Blocked    ntoskrnl!_KiSystemService+0xc4
.....
```

最初の列には、プロセス ID と (ピリオドで区切られた) スレッド ID が表示されます。

2 番目の列は、スレッドの ETHREAD ブロックの現在のアドレスです。

3 番目の列には、(初期化、準備ができたら、実行中、スタンバイ、終了、遷移、またはブロック) のスレッドの状態が表示されます。

4 番目の列には、スレッドのスタックに最上位のアドレスが表示されます。

より詳細な例を示します **! スタック**出力。

```dbgcmd
kd> !stacks 1
Proc.Thread  .Thread  ThreadState  Blocker
                                     [System]
   4.000008  827d0030  Blocked    ntoskrnl!MmZeroPageThread+0x66
   4.000010  827d0430  Blocked    ntoskrnl!ExpWorkerThread+0x189
   4.000014  827cf030  Blocked    Stack paged out
   4.000018  827cfda0  Blocked    Stack paged out
   4.00001c  827cfb10  Blocked    ntoskrnl!ExpWorkerThread+0x189
.....
                                     [smss.exe]
  9c.000098  82738310  Blocked    Stack paged out
  9c.0000a0  826a5190  Blocked    Stack paged out
  9c.0000a4  82739d30  Blocked    Stack paged out

                                     [csrss.exe]
  b0.0000bc  826d0030  Blocked    Stack paged out
  b0.0000b4  826c9030  Blocked    Stack paged out
  b0.0000a8  82723b70  Blocked    ntoskrnl!_KiSystemService+0xc4
.....

kd> !stacks 2
Proc.Thread  .Thread  ThreadState  Blocker
                                     [System]
   4.000008  827d0030  Blocked    ntoskrnl!KiSwapThread+0xc5
                                  ntoskrnl!KeWaitForMultipleObjects+0x2b4
                                  ntoskrnl!MmZeroPageThread+0x66
                                  ntoskrnl!Phase1Initialization+0xd82
                                  ntoskrnl!PspSystemThreadStartup+0x4d
                                  ntoskrnl!CreateSystemRootLink+0x3d8
                                  +0x3f3f3f3f
   4.000010  827d0430  Blocked    ntoskrnl!KiSwapThread+0xc5
                                  ntoskrnl!KeRemoveQueue+0x191
.....
```

 

 





