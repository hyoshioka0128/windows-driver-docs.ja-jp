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
ms.openlocfilehash: 924291f98860cd57880e0679b54be08158b7dd84
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837819"
---
# <a name="controlling-breakpoint-flags-and-parameters"></a>ブレークポイントのフラグとパラメーターの制御


## <span id="controlling_breakpoint_flags_and_parameters"></span><span id="CONTROLLING_BREAKPOINT_FLAGS_AND_PARAMETERS"></span>


ブレークポイントに関する基本的な情報を決定するには、次のようなさまざまな方法があります。

-   [**GetId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getid)は、ブレークポイント ID を返します。

-   [**GetType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-gettype)は、ブレークポイントの種類 (ソフトウェアまたはプロセッサ) と、ブレークポイントが設定されている有効なプロセッサの種類を返します。

-   [**Getadder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)は、ブレークポイントを追加したクライアントを返します。

-   [**GetOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffset)は、ブレークポイントのアドレスを返します。

-   [**Getoffsetexpression**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getoffsetexpression)は、ブレークポイントの場所を指定する式文字列を返します。

ブレークポイントには、その場所とブレークポイントの種類に加え、動作を制御するいくつかのパラメーターがあります。

ブレークポイントパラメーターは、さまざまな特定の方法を使用して制御できます。 また、パラメーターのほとんどは、 [**Getparameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getparameters)を使用して一緒にクエリを行うことができます。

### <a name="span-idbreakpoint_flagsspanspan-idbreakpoint_flagsspanbreakpoint-flags"></a><span id="breakpoint_flags"></span><span id="BREAKPOINT_FLAGS"></span>ブレークポイントフラグ

ブレークポイントフラグは、1つの種類のブレークポイントパラメーターです。

ブレークポイントフラグは、 [**Getflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getflags)を使用して照会できます。 これらは、 [**Addflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags)、 [**removeflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-removeflags)、または[**setflags**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setflags)を使用して変更できます。

ブレークポイントフラグは、ビットフィールドを形成します。 このビットフィールドで使用できるフラグとその意味は、次のとおりです。

<span id="DEBUG_BREAKPOINT_ENABLED"></span><span id="debug_breakpoint_enabled"></span>デバッグ\_ブレークポイント\_有効  
このフラグが設定されている場合、ブレークポイントは*有効*になり、通常の効果が適用されます。 このフラグが設定されていない場合、ブレークポイントは*無効*になり、何の影響もありません。 ブレークポイントを一時的に非アクティブ化する場合は、このフラグを削除できます。このブレークポイントを再度有効にするときに、このフラグを簡単に追加できます。

<span id="DEBUG_BREAKPOINT_ADDER_ONLY"></span><span id="debug_breakpoint_adder_only"></span>デバッグ\_ブレークポイントを\_に\_のみ)  
このフラグが設定されている場合、ブレークポイントは*プライベートブレークポイント*です。 このブレークポイントは、それを追加したクライアントに対してのみ表示されます。 この場合、他のクライアントは、エンジンに対してブレークポイントのクエリを実行できません。また、ブレークポイントによって生成されたイベントは、他のクライアントに送信されません。 このブレークポイントに関連するすべてのコールバック (イベントと[出力](using-input-and-output.md#output)) は、このクライアントにのみ送信されます。 「 [**Getadder**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getadder)表示する」を参照してください。

<span id="DEBUG_BREAKPOINT_GO_ONLY"></span><span id="debug_breakpoint_go_only"></span>デバッグ\_ブレークポイント\_ジャンプ\_のみ  
このフラグが設定されている場合、ブレークポイントはターゲットが無制限に実行されている場合にのみトリガーされます。 エンジンがターゲットの命令をステップ実行している場合は、トリガーされません。

<span id="DEBUG_BREAKPOINT_ONE_SHOT"></span><span id="debug_breakpoint_one_shot"></span>デバッグ\_ブレークポイント\_1\_ショット  
このフラグが設定されている場合、ブレークポイントは、最初にトリガーされたときに自動的に削除されます。

<span id="DEBUG_BREAKPOINT_DEFERRED"></span><span id="debug_breakpoint_deferred"></span>デバッグ\_ブレークポイント\_遅延  
このフラグが設定されている場合、ブレークポイントは*遅延*されます。 このフラグは、ブレークポイントのオフセットがシンボリック式を使用して指定されていて、エンジンが式を評価できない場合に、エンジンによって設定されます。 ターゲットにモジュールが読み込まれるか unleaded されるたびに、式を使用して位置が指定されているすべてのブレークポイントの式が再評価されます。 評価できないものには、遅延としてフラグが設定されます。 このフラグは、どのクライアントでも変更できません。

### <a name="span-idother_breakpoint_parametersspanspan-idother_breakpoint_parametersspanother-breakpoint-parameters"></a><span id="other_breakpoint_parameters"></span><span id="OTHER_BREAKPOINT_PARAMETERS"></span>その他のブレークポイントパラメーター

ブレークポイントのパラメーターには次のものも含まれます。

<span id="Pass_count"></span><span id="pass_count"></span><span id="PASS_COUNT"></span>*パス数*  
ブレークポイントに関連付けられているパスカウントがある場合は、ターゲットが指定された回数だけブレークポイントに到達するまで、アクティブ化されません。 最初に設定されたパスカウントは、 [**Getpass count**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getpasscount)を使用して見つけることができます。 エンジンがアクティブ化される前にブレークポイントに到達する残りの回数は、 [**Getcurrentpass count**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getcurrentpasscount)を使用して見つけることができます。 パスカウントは、 [**Setpass count**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setpasscount)を使用して新しい値にリセットできます。

<span id="Match_thread"></span><span id="match_thread"></span><span id="MATCH_THREAD"></span>*一致するスレッド*  
ブレークポイントにスレッドが関連付けられている場合は、他のスレッドによって検出されると、エンジンによって無視されます。 スレッドは、 [**Getmatchthreadid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getmatchthreadid)を使用して見つけることができ、 [**setmatchthreadid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setmatchthreadid)を使用して変更できます。

<span id="Command"></span><span id="command"></span><span id="COMMAND"></span>*メニュー*  
ブレークポイントには、コマンドが関連付けられている場合があります。 このコマンドは、ブレークポイントがアクティブになったときに実行されます。 このコマンドは、 [**Getcommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getcommand)を使用して見つけることができます。また、 [**setcommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setcommand)を使用して変更できます。

<span id="Size"></span><span id="size"></span><span id="SIZE"></span>*幅*  
ブレークポイントがプロセッサのブレークポイントの場合は、サイズが指定されている必要があります。 これにより、アクセスがブレークポイントをアクティブにするメモリブロックのサイズが決まります。ブロックの先頭はブレークポイントの位置です。 サイズは[**GetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)を使用して見つけることができ、 [**SetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)を使用して変更できます。

<span id="Access_type"></span><span id="access_type"></span><span id="ACCESS_TYPE"></span>*アクセスの種類*  
ブレークポイントがプロセッサのブレークポイントである場合は、アクセスの種類が必要です。 これにより、ブレークポイントをアクティブ化するアクセスの種類が決まります。 たとえば、ブレークポイントによって指定されたメモリをターゲットが読み取り、書き込み、または実行する場合は、ブレークポイントをアクティブにすることができます。 アクセスの種類は[**GetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-getdataparameters)を使用して見つけることができ、 [**SetDataParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setdataparameters)を使用して変更できます。

### <a name="span-idvalid_parameters_for_processor_breakpointsspanspan-idvalid_parameters_for_processor_breakpointsspanvalid-parameters-for-processor-breakpoints"></a><span id="valid_parameters_for_processor_breakpoints"></span><span id="VALID_PARAMETERS_FOR_PROCESSOR_BREAKPOINTS"></span>プロセッサブレークポイントの有効なパラメーター

プロセッサブレークポイントでは、次のアクセスの種類を使用できます。

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
<td align="left"><p>ブレークポイントは、CPU がブレークポイントのメモリブロック内のメモリを読み取るとトリガーされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_WRITE</p></td>
<td align="left"><p>ブレークポイントは、CPU がブレークポイントのメモリブロックにメモリを書き込んだときにトリガーされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>
DEBUG_BREAK_READ |DEBUG_BREAK_WRITE</td>
<td align="left"><p>ブレークポイントは、CPU がブレークポイントのメモリブロック内のメモリを読み書きするときにトリガーされます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_BREAK_EXECUTE</p></td>
<td align="left"><p>ブレークポイントは、CPU がブレークポイントのメモリブロック内の命令をフェッチしたときにトリガーされます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_BREAK_IO</p></td>
<td align="left"><p>ブレークポイントは、ブレークポイントメモリブロック内の i/o ポートにアクセスしたときにトリガーされます。 (Windows XP および Microsoft Windows Server 2003 のみ、カーネルモードのみ、x86 のみ)</p></td>
</tr>
</tbody>
</table>

 

すべてのアクセスの種類とサイズがすべてのプロセッサでサポートされているわけではありません。 次のアクセスの種類とサイズがサポートされています。

<span id="x86"></span><span id="X86"></span>86  
すべてのアクセスの種類がサポートされています。 デバッグ\_中断\_読み取りの動作 (デバッグ\_中断\_読み取り |デバッグ\_中断\_書き込み。 サイズは1、2、または4である必要があります。 ブレークポイントのアドレスは、サイズの倍数である必要があります。

<span id="x64"></span><span id="X64"></span>x64  
すべてのアクセスの種類がサポートされています。 デバッグ\_中断\_読み取りの動作 (デバッグ\_中断\_読み取り |デバッグ\_中断\_書き込み。 サイズは1、2、4、または8である必要があります。 ブレークポイントのアドレスは、サイズの倍数である必要があります。

<span id="Itanium"></span><span id="itanium"></span><span id="ITANIUM"></span>Itanium  
すべてのアクセスの種類 (デバッグ\_中断\_IO を除く) がサポートされています。 サイズは2の累乗でなければなりません。デバッグ\_中断\_実行の場合、サイズは16である必要があります。 ブレークポイントのアドレスは、サイズの倍数である必要があります。

<span id="Itanium_running_in_x86_mode"></span><span id="itanium_running_in_x86_mode"></span><span id="ITANIUM_RUNNING_IN_X86_MODE"></span>X86 モードで実行されている Itanium  
は、x86 の場合と同じです。ただし、デバッグ\_中断\_IO はサポートされていません。

 

 





