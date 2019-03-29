---
title: wt (データのトレースとウォッチ)
description: Wt コマンドでは、関数全体を実行し、関数呼び出しの先頭で次のコマンドを実行するときに、統計情報を表示します。
ms.assetid: 2dd62a7f-67d9-4b13-b04e-5cd02e6ef9f0
keywords:
- wt (トレースとデータの監視) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wt (Trace and Watch Data)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d8208441e26b826ae15708fdff3621eb4c25ab14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572024"
---
# <a name="wt-trace-and-watch-data"></a>wt (データのトレースとウォッチ)


**Wt**コマンドは、関数全体を実行し、関数呼び出しの先頭で次のコマンドを実行するときに、統計情報を表示します。

```dbgcmd
wt [WatchOptions] [= StartAddress] [EndAddress] 
```

## <a name="span-idddkcmdtraceandwatchdatadbgspanspan-idddkcmdtraceandwatchdatadbgspanparameters"></a><span id="ddk_cmd_trace_and_watch_data_dbg"></span><span id="DDK_CMD_TRACE_AND_WATCH_DATA_DBG"></span>パラメーター


<span id="_______WatchOptions______"></span><span id="_______watchoptions______"></span><span id="_______WATCHOPTIONS______"></span> *WatchOptions*   
表示を変更する方法を指定します。 次のオプションのいずれかを使用することができます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>-l</strong> <em>深さ</em></p></td>
<td align="left"><p>(ユーザー モードのみ)表示する呼び出しの最大の深さを指定します。 以上であるすべての呼び出し<em>深さ</em>開始点よりも深いレベルをサイレント モードで実行されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-m</strong> <em>モジュール</em></p></td>
<td align="left"><p>(ユーザー モードのみ)指定したモジュールとモジュールから行われた呼び出しの最初のレベル内のコードには、表示を制限します。 複数のモジュールとその他のモジュールからコードを表示する複数の-m オプションを含めることができます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-i</strong> <em>モジュール</em></p></td>
<td align="left"><p>(ユーザー モードのみ)指定したモジュール内のコードは無視されます。 複数 i を含めることができますを複数のモジュールからのコードを無視するオプション。 デバッガーはすべて無視、-m オプションを使用する場合にオプションです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ni</strong></p></td>
<td align="left"><p>(ユーザー モードのみ)-M に起因無視されているコードへのすべてのエントリが表示されないまたは-i オプション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-nc</strong></p></td>
<td align="left"><p>個々 の呼び出し情報は表示されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-ns</strong></p></td>
<td align="left"><p>概要情報は表示されません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>-nw</strong></p></td>
<td align="left"><p>トレース中に警告は表示されません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>-oa</strong></p></td>
<td align="left"><p>(ユーザー モードのみ)呼び出しサイトの実際のアドレスが表示されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>- または</strong></p></td>
<td align="left"><p>(ユーザー モードのみ)既定の基数をベースとして使用して、呼び出された関数の戻り値のレジスタの値が表示されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>- または</strong></p></td>
<td align="left"><p>(ユーザー モードのみ)表示をそれぞれ適切な型で、呼び出された関数の戻り値のレジスタの値は、値を返します。</p></td>
</tr>
</tbody>
</table>

 

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
デバッガーが実行を開始する位置のアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______EndAddress______"></span><span id="_______endaddress______"></span><span id="_______ENDADDRESS______"></span> *endAddress*   
トレースの終了位置のアドレスを指定します。 使用しない場合*EndAddress*、1 つの命令または関数呼び出しが実行されます。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>環境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>モード</strong></p></td>
<td align="left"><p>ユーザー モードでは、カーネル モード</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ターゲット</strong></p></td>
<td align="left"><p>ライブ デバッグのみ</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>プラットフォーム</strong></p></td>
<td align="left"><p></p>
<strong>ユーザー モード:</strong>すべて<strong>カーネル モード:</strong> x86 ベースのみ</td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

発行の詳細については、 **wt**コマンドとの概要については、関連するコマンドを参照してください[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>コメント
-------

**Wt**コマンドは、特定の関数の動作に関する情報を表示する関数をステップしたくない場合に便利です。 代わりに、その関数の先頭に移動し、発行し、 **wt**コマンド。

プログラム カウンターがモジュールに関数またはエントリ ポイントの先頭) などのシンボルに対応するポイントにある場合、 **wt**コマンドでは、現在の戻り値のアドレスに到達するまでをトレースします。 プログラム カウンターがある場合、**呼び出す**、命令、 **wt**トレースを現在の場所に戻るまでコマンドします。 このトレースでプロファイリングが実行されて、[デバッガー コマンド ウィンドウ](debugger-command-window.md)と共に出力をコマンドが発生したさまざまな呼び出しについて説明します。

場合、 **wt**コマンドが、関数の先頭以外のどこかから発行された、コマンドのように動作、 [ **p (ステップ)** ](p--step-.md)コマンド。 ただし、指定した場合*EndAddress*アドレスに達すること、多くの手順をプログラムし、関数呼び出しの場合でも、この実行では、まで実行が続行されます。

元のモードでデバッグする場合は、関数本体の開きかっこを表示するポイントにのみ、関数にトレースする必要があります。 次に、使用、 **wt**コマンド。 (通常を簡単に、関数の最初の行にブレークポイントを挿入または使用が[デバッグ |カーソルまで実行](debug---run-to-cursor.md)、しを使用して、 **wt**コマンド)。

の出力を**wt**長くなることが、出力を記録するログ ファイルを使用する場合があります。

次の例では、一般的なログ ファイルを示します。

```dbgcmd
0:000> l+                  Source options set to show source lines
Source options are f:
     1/t - Step/trace by source line
     2/l - List source line for LN and prompt
     4/s - List source code at prompt
     8/o - Only show source code at prompt
0:000> p                   Not yet at the function call: use "p"
>  44:       minorVariableOne = 12;
0:000> p
>  45:       variableOne = myFunction(2, minorVariable);
0:000> t                   At the function call: now use "t"
MyModule!ILT+10(_myFunction):
0040100f e9cce60000      jmp     MyModule!myFunction (0040f6e0)
0:000> t
>  231:    { 
0:000> wt                  At the function beginning:  now use "wt"
Tracing MyModule!myFunction to return address 00401137

  105     0 [  0] MyModule!myFunction
    1     0 [  1]   MyModule!ILT+1555(_printf)
    9     0 [  1]   MyModule!printf
    1     0 [  2]     MyModule!ILT+370(__stbuf)
   11     0 [  2]     MyModule!_stbuf
    1     0 [  3]       MyModule!ILT+1440(__isatty)
   14     0 [  3]       MyModule!_isatty
   50    15 [  2]     MyModule!_stbuf
   17    66 [  1]   MyModule!printf
    1     0 [  2]     MyModule!ILT+980(__output)
   59     0 [  2]     MyModule!_output
   39     0 [  3]       MyModule!write_char
  111    39 [  2]     MyModule!_output
   39     0 [  3]       MyModule!write_char

....

   11     0 [  5]           kernel32!__SEH_epilog4
   54 11675 [  4]         kernel32!ReadFile
  165 11729 [  3]       MyModule!_read
  100 11895 [  2]     MyModule!_filbuf
   91 11996 [  1]   MyModule!fgets
54545 83789 [  0] MyModule!myFunction
    1     0 [  1]   MyModule!ILT+1265(__RTC_CheckEsp)
    2     0 [  1]   MyModule!_RTC_CheckEsp
54547 83782 [  0] MyModule!myFunction

112379 instructions were executed in 112378 events (0 from other threads)

Function Name                               Invocations MinInst MaxInst AvgInst
MyModule!ILT+1265(__RTC_CheckEsp)                     1       1       1       1
MyModule!ILT+1440(__isatty)                          21       1       1       1
MyModule!ILT+1540(__ftbuf)                           21       1       1       1
....
ntdll!memcpy                                         24       1      40      19
ntdll!memset                                          2      29      29      29

23 system calls were executed

Calls  System Call
   23  ntdll!KiFastSystemCall
```

トレースの一覧で、最初の数値が実行された命令の数を指定します、2 番目の数値を関数の子プロセスが実行された命令の数を指定して (角かっこ) では、3 番目の数字の深さを指定します、(0 と最初の関数を取得)、スタック内の関数。 関数名のインデントは、呼び出しの深さを示しています。

前の例では、 **MyModule! myFunction**など、いくつかのサブルーチンを呼び出す前に、105 命令を実行**printf**と**fgets**、しを実行しますこれらの関数を呼び出した後は、いくつかのより多くの呼び出しを発行する前に、54545 のことに追加手順です。 ただし、最終的なカウントが表示されますが**myFunction**この数に、すべての手順が含まれているために、112,379 命令を実行する**myFunction**し、その子の実行します。 (、*子*の**myFunction**関数から呼び出される**myFunction**、直接または間接的にします)。

前の例では、なお**クラスルーム + 1440 (\_\_isatty)** は 21 回呼び出されます。 メソッドが呼び出された回数に最小限の手順については、1 回の実行で、手順については、1 回の実行での最大数、および命令の数の平均値、最終的なカウントでこの関数の動作の概要を示しています各実行します。

すべてのシステム呼び出しが行われた場合は、カウンターに表示され、コマンドの出力の最後にもう一度表示されます。

 

 





