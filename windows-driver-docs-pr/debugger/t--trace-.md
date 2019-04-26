---
title: t (トレース)
description: T コマンドでは、1 つの命令またはソース行を実行し、必要に応じてすべてのレジスタとフラグの結果の値が表示されます。
ms.assetid: 0cb3ac96-5d5c-4ebd-8ef1-2fbb066e6458
keywords:
- t (トレース) の Windows デバッグ
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- t (Trace)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d2cd6116ac3d69a4e5c8c0076c699a4fd6b452e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335457"
---
# <a name="t-trace"></a>t (トレース)


**T**コマンドは、1 つの命令またはソース行を実行し、必要に応じてレジスタとフラグのすべての結果の値を表示します。 ときにサブルーチンの呼び出しまたは割り込みが発生する、その手順のそれぞれにもトレースされます。

ユーザー モード

```dbgcmd
[~Thread] t [r] [= StartAddress] [Count] ["Command"] 
```

カーネル モード

```dbgcmd
t [r] [= StartAddress] [Count] ["Command"] 
```

## <a name="span-idddkcmdtracedbgspanspan-idddkcmdtracedbgspanparameters"></a><span id="ddk_cmd_trace_dbg"></span><span id="DDK_CMD_TRACE_DBG"></span>パラメーター


<span id="_______Thread______"></span><span id="_______thread______"></span><span id="_______THREAD______"></span> *スレッド*   
スレッドの凍結を解除するを指定します。 その他のすべてのスレッドが固定されています。 この構文の詳細については、次を参照してください。[スレッド構文](thread-syntax.md)します。 スレッドは、ユーザー モードでのみ指定できます。

<span id="_______r______"></span><span id="_______R______"></span> **r**   
オンとオフのレジスタとフラグの表示を切り替えます。 既定では、レジスタとフラグが表示されます。 使用して登録の表示を無効にすることができます、 [ **pr**](p--step-.md)、 **tr**、または .prompt\_-reg コマンドを許可します。 これらのコマンドの 3 つすべてが同じ設定を制御し、これらのいずれかを使用して、すべて以前を使用してこれらのコマンドを上書きすることができます。

L os コマンドを使用して登録表示無効にすることもできます。 この設定は、その他の 3 つのコマンドとは別です。 コントロールのどのレジスタとフラグが表示される、使用する、 [ **rm (登録マスク)** ](rm--register-mask-.md)コマンド。

<span id="_______StartAddress______"></span><span id="_______startaddress______"></span><span id="_______STARTADDRESS______"></span> *StartAddress*   
実行を開始するアドレスを指定します。 使用しない場合*StartAddress*命令を命令ポインターが指すから実行が開始します。 構文の詳細については、次を参照してください。[アドレスとアドレス範囲の構文](address-and-address-range-syntax.md)します。

<span id="_______Count______"></span><span id="_______count______"></span><span id="_______COUNT______"></span> *カウント*   
指示または停止する前にトレースするソース行の数を指定します。 別のアクションとして各ステップが表示されます、[デバッガー コマンド ウィンドウ](debugger-command-window.md)します。 既定値は、1 つ。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *コマンド*   
トレースの実行後に実行するデバッガー コマンドを指定します。 このコマンドは、標準の前に実行**t**結果が表示されます。 使用する場合は*カウント*、すべてのトレースが完了した後 (ただし、最終的なトレースの結果が表示される前に) このコマンドを実行します。

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
<td align="left"><p>すべての</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>追加情報

発行する方法について、 **t**コマンドとの概要については、関連するコマンドを参照してください[ターゲットを制御する](controlling-the-target.md)します。

<a name="remarks"></a>コメント
-------

指定すると*カウント*、ステップ実行には、それぞれの命令が表示されます。

各トレースは、1 つのアセンブリ命令またはモードのアセンブリまたはソース モードでデバッガーがかどうかに応じて、1 つのソース行を実行します。 使用して、 [ **l + t** ](l---l---set-source-options-.md) l t コマンドまたは WinDbg ツールバーのボタンと、これらのモードを切り替えます。

使用することができますが、ほとんどの関数呼び出しをトレースする、特定の呼び出しをスキップする場合は、 [ **.step\_フィルター (ステップ フィルターの設定)** ](-step-filter--set-step-filter-.md)を経由での手順への呼び出しを示します。

使用することができます、 **t** ROM にある手順をトレースするコマンド

WinDbg で何度もをすぐにトレースするときは、各トレースの後にデバッグ情報ウィンドウが更新されます。 この更新プログラムには、低速の応答時間が発生する場合は、使用[**明解\_ui (WinDbg インターフェイスの中断)** ](-suspend-ui--suspend-windbg-interface-.md)をこれらのウィンドウの更新を一時停止します。

 

 





