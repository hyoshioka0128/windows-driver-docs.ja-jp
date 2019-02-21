---
title: k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)
description: K のコマンドは、関連情報と共に、特定のスレッドのスタック フレームを表示します。
ms.assetid: 1061015f-cb0c-490b-b256-e0dedb659f22
keywords:
- k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace) Windows のデバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- k, kb, kc, kd, kp, kP, kv (Display Stack Backtrace)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fad326f48550d25c1e91a806e787b9da703e811d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553121"
---
# <a name="k-kb-kc-kd-kp-kp-kv-display-stack-backtrace"></a>k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)


<strong>K*\\</strong>** のコマンド関連の情報と共に、特定のスレッドのスタック フレームを表示する.

ユーザー モード、x86 プロセッサ

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr StackPtr InstructionPtr
[~Thread] kd [WordCount]
```

カーネル モードの x86 プロセッサ

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = BasePtr StackPtr InstructionPtr
[Processor] kd [WordCount]
```

ユーザー モードの x64 プロセッサ

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[~Thread] kd [WordCount]
```

カーネル モードの x64 プロセッサ

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[Processor] kd [WordCount]
```

ユーザー モードの ARM プロセッサ

```dbgcmd
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[~Thread] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[~Thread] kd [WordCount]
```

カーネル モードの ARM プロセッサ

```dbgcmd
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] [FrameCount]
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr FrameCount
[Processor] k[b|p|P|v] [c] [n] [f] [L] [M] = StackPtr InstructionPtr FrameCount
[Processor] kd [WordCount]
```

## <a name="span-idddkcmddisplaystackbacktracedbgspanspan-idddkcmddisplaystackbacktracedbgspanparameters"></a><span id="ddk_cmd_display_stack_backtrace_dbg"></span><span id="DDK_CMD_DISPLAY_STACK_BACKTRACE_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
スレッドのスタックが表示されることを指定します。 このパラメーターを省略した場合は、現在のスレッドのスタックが表示されます。 スレッドの構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *プロセッサ*   
プロセッサのスタックが表示されることを指定します。 プロセッサの構文の詳細については、次を参照してください。[マルチプロセッサ構文](multiprocessor-syntax.md)します。

<span id="_______b"></span><span id="_______B"></span> b  
スタック トレース内の各関数に渡される最初の 3 つのパラメーターが表示されます。

<span id="_______c"></span><span id="_______C"></span> c  
クリーンなスタック トレースを表示します。 各表示行には、モジュール名のみと関数名が含まれています。

<span id="_______p"></span><span id="_______P"></span> P  
スタック トレース内のすべての関数が呼び出されるごとにパラメーターが表示されます。 パラメーター リストには、各パラメーターのデータ型、名前、および値が含まれています。 -P オプションは、大文字小文字を区別します。 このパラメーターには、完全なシンボル情報が必要です。

<span id="_______P"></span><span id="_______p"></span> P  
P パラメーターなど、スタック トレース内のすべての関数が呼び出されるごとにパラメーターが表示されます。 ただし、p、関数のパラメーターに印刷されます、ディスプレイの 2 行目の代わりに、データの残りの部分と同じ行に。

<span id="_______v______"></span><span id="_______V______"></span> v   
フレーム ポインターの省略 (FPO) の情報が表示されます。 X86 ベースのプロセッサで、表示も含まれています規則の情報を呼び出すことです。

<span id="_______n______"></span><span id="_______N______"></span> n   
フレーム番号が表示されます。

<span id="_______f______"></span><span id="_______F______"></span> f   
隣接するフレームの間の距離が表示されます。 この距離は、実際のスタック フレームを分離するバイト数です。

<span id="_______L______"></span><span id="_______l______"></span> L   
表示のソース行を非表示にします。 L は大文字小文字を区別します。

<span id="_______M"></span><span id="_______m"></span> M  
出力を使用して表示[デバッガー Markup Language](debugger-markup-language-commands.md)します。 表示の場合は、各フレーム数は、リンク ローカルのコンテキストを設定し、ローカル変数を表示する をクリックしたことができますです。 ローカル コンテキストについては、次を参照してください。 [ **.frame**](-frame--set-local-context-.md)します。

<span id="_______FrameCount______"></span><span id="_______framecount______"></span><span id="_______FRAMECOUNT______"></span> *FrameCount*   
表示するスタック フレームの数を指定します。 使用して、基数を変更していない限り、16 進数形式では、この数を指定する必要があります、 [ **n (設定数の基本)** ](n--set-number-base-.md)コマンド。 既定値は 20 (0x14) を使用して、既定値を変更していない限り、 [ **.kframes (スタックの長さを設定)** ](-kframes--set-stack-length-.md)コマンド。

<span id="_______BasePtr______"></span><span id="_______baseptr______"></span><span id="_______BASEPTR______"></span> *BasePtr*   
スタック トレースの基本ポインターを指定します。 *BasePtr*パラメーターがコマンドの後に等号 (=) がある場合にのみ使用できます。

<span id="_______StackPtr______"></span><span id="_______stackptr______"></span><span id="_______STACKPTR______"></span> *StackPtr*   
スタック トレースのスタック ポインターを指定します。 省略した場合*StackPtr*と*InstructionPtr*コマンドは、スタック ポインター レジスタ rsp (または esp) を指定して、rip (または eip) レジスタを指定する命令ポインターを使用します。

<span id="_______InstructionPtr______"></span><span id="_______instructionptr______"></span><span id="_______INSTRUCTIONPTR______"></span> *InstructionPtr*   
スタック トレースの命令ポインターを指定します。 省略した場合*StackPtr*と*InstructionPtr*コマンドは、スタック ポインター レジスタ rsp (または esp) を指定して、rip (または eip) レジスタを指定する命令ポインターを使用します。

<span id="_______WordCount______"></span><span id="_______wordcount______"></span><span id="_______WORDCOUNT______"></span> *WordCount*   
DWORD の数を指定\_をダンプするスタック内の PTR の値。 既定値は 20 (0x14) を使用して、既定値を変更していない限り、 [ **.kframes (スタックの長さを設定)** ](-kframes--set-stack-length-.md)コマンド。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>モード</p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット</p></td>
<td align="left"><p>ライブ、クラッシュ ダンプ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>プラットフォーム</p></td>
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformation1spanspan-idadditionalinformation1spanadditional-information"></a><span id="additional_information1"></span><span id="ADDITIONAL_INFORMATION1"></span>追加情報

レジスタのコンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

<a name="remarks"></a>注釈
-------

発行するとき、 **k**、 **kb**、 **kp**、 **kP**、または**kv**コマンド、スタック トレースが表形式で表示されます形式です。 行の読み込みが有効になっている場合と、ソースのモジュールと行番号も表示されます。

スタック トレースには、スタック フレーム、リターン アドレス、および関数名の基本ポインターが含まれています。

使用する場合、 **kp**または**kP**コマンドを各スタック トレースで呼び出される関数の完全なパラメーターが表示されます。 パラメーター リストには、各パラメーターのデータ型、名前、および値が含まれています。

このコマンドは、低速な可能性があります。 たとえば、 **MyFunction1**呼び出し**MyFunction2**、デバッガーには、完全なシンボル情報が必要です**MyFunction1**これに渡されるパラメーターを表示するには。呼び出します。 このコマンドでは、公開されていない内部の Microsoft Windows ルーチンは完全にはパブリック シンボルで表示されません。

使用する場合、 **kb**または**kv**コマンドを各関数に渡される最初の 3 つのパラメーターが表示されます。 使用する場合、 **kv**コマンド、FPO データも表示されます。

X86 ベースのプロセッサでは、上、 **kv**コマンドでは、呼び出し元の規則の情報も表示されます。

使用すると、 **kv**コマンド、FPO 情報は、次の形式で行の末尾に追加されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">FPO テキスト</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">FPO: [Fpo 以外]</td>
<td align="left"><p>フレームの FPO データがありません。</p></td>
</tr>
<tr class="even">
<td align="left">FPO: [N1、N2、N3]</td>
<td align="left"><p><em>N1</em>パラメーターの合計数です。</p>
<p><em>N2</em> DWORD 値をローカル変数の数です。</p>
<p><em>N3</em>は保存されているレジスタの数です。</p></td>
</tr>
<tr class="odd">
<td align="left">FPO: [N1, N2] TrapFrame @ アドレス</td>
<td align="left"><p><em>N1</em>パラメーターの合計数です。</p>
<p><em>N2</em> DWORD 値の数をローカル変数です。</p>
<p><em>アドレス</em>トラップ フレームのアドレスです。</p></td>
</tr>
<tr class="even">
<td align="left">FPO:TaskGate セグメント: 0</td>
<td align="left"><p><em>セグメント</em>タスク ゲートのセグメントのセレクターが。</p></td>
</tr>
<tr class="odd">
<td align="left">FPO: [EBP 0xBase]</td>
<td align="left"><p><em>基本</em>フレームの基本ポインターです。</p></td>
</tr>
</tbody>
</table>

 

**Kd**コマンド スタックの生データを表示します。 各 DWORD 値は、個別の行に表示されます。 シンボル情報には、関連付けられているシンボルと共にそれらの行が表示されます。 この形式は、他のより詳細な一覧を作成します。 **k * * *\** コマンド。 **Kd**コマンドを実行すると、 [ **dds (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドをパラメーターとしてのスタック アドレスを使用します。

使用する場合、 **k**不適切な結果を受信する (前に、関数プロローグが実行された) 関数の先頭にあるコマンドします。 デバッガーでは、フレームのレジスタを使用して、現在のバックを計算して、このレジスタ正しく設定されていない関数のプロローグが実行されるまでです。

ユーザー モードでは、スタック トレースを現在のスレッドのスタックに基づきます。 スレッドの詳細については、次を参照してください。[を制御するプロセスとスレッド](controlling-processes-and-threads.md)します。

カーネル モードでスタック トレースは、現在に基づいて[コンテキストを登録](changing-contexts.md#register-context)します。 特定のスレッド、コンテキストのレコードを一致するように登録するコンテキストを設定したり、フレームをトラップします。

### <a name="span-idadditionalinformation2spanspan-idadditionalinformation2spanadditional-information"></a><span id="additional_information2"></span><span id="ADDITIONAL_INFORMATION2"></span>追加情報

レジスタのコンテキストとその他のコンテキストの設定の詳細については、次を参照してください。[変更コンテキスト](changing-contexts.md)します。

 

 





