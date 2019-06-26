---
title: ブレークポイントのフラグとパラメーターの制御
description: ブレークポイントのフラグとパラメーターの制御
ms.assetid: ed702f01-2a30-4ffb-a804-167cf3b19936
keywords:
- ブレークポイント、フラグ、およびパラメーター
- DEBUG_BREAK_READ
- DEBUG_BREAK_WRITE
- DEBUG_BREAK_EXECUTE
- DEBUG_BREAK_IO
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6076b76f8db4b8c0f8050fa7730218fb7d60147
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361450"
---
# <a name="controlling-breakpoint-flags-and-parameters"></a>ブレークポイントのフラグとパラメーターの制御


## <span id="controlling_breakpoint_flags_and_parameters"></span><span id="CONTROLLING_BREAKPOINT_FLAGS_AND_PARAMETERS"></span>


ブレークポイントに関する基本的な情報を決定するために使用するメソッドを数多くあります。

-   [**GetId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getid)ブレークポイント ID を返します。

-   [**GetType** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-gettype)ブレークポイントの種類 (ソフトウェアまたはプロセッサ) と、ブレークポイントが設定されている有効なプロセッサの種類を返します。

-   [**GetAdder** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)ブレークポイントを追加するクライアントに返します。

-   [**GetOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffset)ブレークポイントのアドレスを返します。

-   [**GetOffsetExpression** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffsetexpression)ブレークポイントの場所を指定する式の文字列を返します。

その場所とブレークポイントの種類だけでなくは、ブレークポイントは、その動作を制御するいくつかのパラメーターを持ちます。

ブレークポイントのパラメーターは、特定のメソッドのさまざまなを通じて制御できます。 さらに、ほとんどのパラメーターをクエリすることを使用して[ **GetParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getparameters)します。

### <a name="span-idbreakpointflagsspanspan-idbreakpointflagsspanbreakpoint-flags"></a><span id="breakpoint_flags"></span><span id="BREAKPOINT_FLAGS"></span>ブレークポイントのフラグ

ブレークポイントのフラグは、1 つの種類のブレークポイントのパラメーターです。

使用してブレークポイントのフラグを照会できます[ **GetFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getflags)します。 使用してこれらを変更する[ **AddFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags)、 [ **RemoveFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-removeflags)、または[ **SetFlags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setflags).

ブレークポイントのフラグは、ビット フィールドを形成します。 このビット フィールドとその意味で使用できる可能なフラグは次のとおりです。

<span id="DEBUG_BREAKPOINT_ENABLED"></span><span id="debug_breakpoint_enabled"></span>デバッグ\_ブレークポイント\_有効  
このフラグが設定されている場合、ブレークポイントは、*有効になっている*通常その影響が大きいとします。 このフラグが設定されていない場合、ブレークポイントは、*無効になっている*し、任意の影響はありません。 このフラグは; を削除するにはブレークポイントを一時的に非アクティブ化する場合は、このブレークポイントを再度有効にするときに、このフラグを追加する簡単です。

<span id="DEBUG_BREAKPOINT_ADDER_ONLY"></span><span id="debug_breakpoint_adder_only"></span>デバッグ\_ブレークポイント\_ADDER\_のみ  
ブレークポイントは、このフラグが設定されている場合、*プライベート ブレークポイント*します。 このブレークポイントは、追加のクライアントにのみ表示されます。 ここでは、他のクライアントは、ブレークポイントのエンジンのクエリを実行できませんし、エンジンは、ブレークポイントを他のクライアントによって生成されたイベントを送信しません。 すべてのコールバック (イベントと[出力](using-input-and-output.md#output)) に関連するこのブレークポイントは、このクライアントにのみ送信されます。 参照してください[ **GetAdder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)します。

<span id="DEBUG_BREAKPOINT_GO_ONLY"></span><span id="debug_breakpoint_go_only"></span>デバッグ\_ブレークポイント\_移動\_のみ  
このフラグが設定されている場合、ターゲットが無制限の実行の場合、ブレークポイントのみがトリガーされます。 これはトリガーされない場合は、エンジンがターゲットの手順をステップ実行します。

<span id="DEBUG_BREAKPOINT_ONE_SHOT"></span><span id="debug_breakpoint_one_shot"></span>デバッグ\_ブレークポイント\_1 つ\_ショット  
このフラグが設定されている場合、ブレークポイントは自動的に削除自体、トリガーは最初の時刻。

<span id="DEBUG_BREAKPOINT_DEFERRED"></span><span id="debug_breakpoint_deferred"></span>デバッグ\_ブレークポイント\_遅延  
このフラグが設定されている場合、ブレークポイントは、*遅延*します。 このフラグは、ブレークポイントのオフセットを指定する、シンボリック式を使用すると、エンジンは、式を評価できません、エンジンによって設定されます。 たびに、モジュールが読み込まれるか、ターゲットは、エンジンでフリータイプは試行、式の再評価の式を使用している場所が指定されたすべてのブレークポイント。 フラグが設定を評価することはできませんが、遅延。 このフラグは、任意のクライアントから変更できません。

### <a name="span-idotherbreakpointparametersspanspan-idotherbreakpointparametersspanother-breakpoint-parameters"></a><span id="other_breakpoint_parameters"></span><span id="OTHER_BREAKPOINT_PARAMETERS"></span>その他のブレークポイント パラメーター

ブレークポイントのパラメーターがあります。

<span id="Pass_count"></span><span id="pass_count"></span><span id="PASS_COUNT"></span>*パスの数*  
ブレークポイントに関連付けられているパスの数がある場合はターゲットは、指定した回数だけに、ブレークポイントが経過するまで、認証はされません。 使用して設定されていたパスの数を検出できる[ **GetPassCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getpasscount)します。 数時間の残りがアクティブになる前に、エンジンが、ブレークポイントを渡すことがあります[ **GetCurrentPassCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getcurrentpasscount)します。 パスの数は、使用して新しい値にリセットできる[ **SetPassCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setpasscount)します。

<span id="Match_thread"></span><span id="match_thread"></span><span id="MATCH_THREAD"></span>*一致するスレッド*  
ブレークポイントに関連付けられているスレッドがある場合は、他のスレッドで発生エンジンによって無視されます。 使用して、スレッドが見つかりません[ **GetMatchThreadId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getmatchthreadid)を使用して変更できる[ **SetMatchThreadId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setmatchthreadid)します。

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*コマンド*  
ブレークポイントは、関連付けられているコマンドがあります。 ブレークポイントがアクティブになると、コマンドが実行されます。 このコマンドを使用して検出できます[ **GetCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getcommand)を使用して変更できる[ **SetCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setcommand)します。

<span id="Size"></span><span id="size"></span><span id="SIZE"></span>*サイズ*  
ブレークポイントがプロセッサのブレークポイントの場合は、指定されたサイズが必要です。 メモリ アクセスには、ブレークポイントがアクティブ化のブロックのサイズを指定します--ブロックの先頭は、ブレークポイントの場所。 使用して、サイズが見つかりません[ **GetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)を使用して変更できる[ **SetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)します。

<span id="Access_type"></span><span id="access_type"></span><span id="ACCESS_TYPE"></span>*アクセスの種類*  
ブレークポイントがプロセッサのブレークポイントの場合は、アクセスの種類が必要です。 これは、ブレークポイントがアクティブ化のアクセスの種類を決定します。 たとえば、ターゲットから読み取り、書き込む、または、ブレークポイントによって指定されたメモリを実行する場合、ブレークポイントをアクティブに可能性があります。 使用して、アクセスの種類を検出できる[ **GetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)を使用して変更できる[ **SetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)します。

### <a name="span-idvalidparametersforprocessorbreakpointsspanspan-idvalidparametersforprocessorbreakpointsspanvalid-parameters-for-processor-breakpoints"></a><span id="valid_parameters_for_processor_breakpoints"></span><span id="VALID_PARAMETERS_FOR_PROCESSOR_BREAKPOINTS"></span>プロセッサのブレークポイントの有効なパラメーター

次のアクセスの種類はプロセッサのブレークポイントを使用できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_READ</p></td>
<td align="left"><p>CPU ブレークポイントのメモリ ブロックにメモリを読み取るとき、ブレークポイントがトリガーされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_WRITE</p></td>
<td align="left"><p>ブレークポイントのメモリ ブロックに、CPU、メモリに書き込み、ブレークポイントがトリガーされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
DEBUG_BREAK_READ | DEBUG_BREAK_WRITE</td>
<td align="left"><p>CPU の読み取りまたはブレークポイントのメモリ ブロックにメモリを書き込み時に、ブレークポイントがトリガーされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_EXECUTE</p></td>
<td align="left"><p>CPU ブレークポイントのメモリ ブロックに命令をフェッチしたときに、ブレークポイントがトリガーされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_IO</p></td>
<td align="left"><p>ブレークポイントのメモリ ブロックの I/O ポートにアクセスする場合、ブレークポイントがトリガーされます。 (Windows XP および Microsoft Windows Server 2003 のみ、カーネル モードのみ、x86 のみ)</p></td>
</tr>
</tbody>
</table>

 

すべてのプロセッサでは、すべてのアクセスの種類とサイズがサポートされています。 次のアクセスの種類とサイズがサポートされています。

<span id="x86"></span><span id="X86"></span>X86  
すべてのアクセスの種類がサポートされています。 デバッグ\_中断\_読み取りは、デバッグと同様に動作\_中断\_読み取り |デバッグ\_中断\_を記述します。 サイズは、1、2、または 4 である必要があります。 ブレークポイントのアドレスは、サイズの倍数である必要があります。

<span id="x64"></span><span id="X64"></span>x64  
すべてのアクセスの種類がサポートされています。 デバッグ\_中断\_読み取りは、デバッグと同様に動作\_中断\_読み取り |デバッグ\_中断\_を記述します。 サイズは、1、2、4、または 8 である必要があります。 ブレークポイントのアドレスは、サイズの倍数である必要があります。

<span id="Itanium"></span><span id="itanium"></span><span id="ITANIUM"></span>Itanium  
デバッグ以外の型をアクセスすべて\_中断\_IO がサポートされています。 サイズが 2 の累乗にする必要があります。デバッグの\_中断\_EXECUTE、サイズは 16 である必要があります。 ブレークポイントのアドレスは、サイズの倍数である必要があります。

<span id="Itanium_running_in_x86_mode"></span><span id="itanium_running_in_x86_mode"></span><span id="ITANIUM_RUNNING_IN_X86_MODE"></span>X86 で実行されている Itanium モード  
X86、そのデバッグ以外の場合と同様、\_中断\_IO はサポートされていません。

 

 





