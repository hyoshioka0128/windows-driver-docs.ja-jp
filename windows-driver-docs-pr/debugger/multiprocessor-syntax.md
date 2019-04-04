---
title: マルチプロセッサの構文
description: このトピックでは、マルチプロセッサ構文をについて説明します
ms.assetid: 71adc522-f078-457c-8bc9-9e971e914a41
keywords: マルチプロセッサ コンピューターで、マルチプロセッサ、コマンド構文、デュアル プロセッサ コンピューターでは、コマンド、プロセッサの識別子の構文規則
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c76c200699c287359f4d50167f4a8d58175b2da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560200"
---
# <a name="multiprocessor-syntax"></a>マルチプロセッサの構文


## <span id="ddk_multiprocessor_syntax_dbg"></span><span id="DDK_MULTIPROCESSOR_SYNTAX_DBG"></span>


KD とカーネル モード WinDbg は複数のプロセッサのデバッグをサポートします。 この種の任意のマルチプロセッサ プラットフォームでデバッグを行うことができます。

プロセッサの番号付けは 0 ~ *n*します。

現在のプロセッサがプロセッサ (は、現在のプロセッサである場合の原因となった、デバッガーをアクティブにする) 0 の場合は、現在ではない他のプロセッサを調べることができます (を通じて 1 つのプロセッサ*n*)。 ただし、現在ではないプロセッサ内のあらゆるものを変更することはできません。 のみ、その状態を表示できます。

### <a name="span-idselectingaprocessorspanspan-idselectingaprocessorspanselecting-a-processor"></a><span id="selecting_a_processor"></span><span id="SELECTING_A_PROCESSOR"></span>プロセッサを選択します。

使用することができます、 [ **.echocpunum (CPU 数を表示)** ](-echocpunum--show-cpu-number-.md)コマンドを現在のプロセッサのプロセッサ数を表示します。 このコマンドの出力では、カーネル デバッグ プロンプトのテキストで、複数のプロセッサ システムで作業している場合にすぐに通知することができます。

次の例では、 **0:** の前、 **kd&gt;** プロンプトは、コンピューターの最初のプロセッサをデバッグしていることを示します。

```dbgcmd
0: kd>
```

使用して、 [ **~ s (変更の現在のプロセッサ)** ](-s--change-current-processor-.md)として次の例は、プロセッサ間で切り替えコマンド。

```dbgcmd
0: kd> ~1s
1: kd>
```

コンピューターで 2 つ目のプロセッサをデバッグします。

中断が発生して、スタック トレースを理解することはできませんがある場合は、マルチプロセッサ システム上のプロセッサを変更する必要があります。 中断は、別のプロセッサで発生した可能性があります。

### <a name="span-idspecifyingprocessorsinothercommandsspanspan-idspecifyingprocessorsinothercommandsspanspecifying-processors-in-other-commands"></a><span id="specifying_processors_in_other_commands"></span><span id="SPECIFYING_PROCESSORS_IN_OTHER_COMMANDS"></span>他のコマンド プロセッサを指定します。

いくつかのコマンドの前に、プロセッサ番号を追加することができます。 この番号がない前にティルダ (**~**) を除く、 **~ S**コマンド。

**注**  ユーザー モードのデバッグ、チルダは、スレッドの指定に使用されます。 この構文の詳細については、[スレッド構文](thread-syntax.md)を参照してください。

 

プロセッサ Id は、明示的に参照する必要はありません。 プロセッサ ID に対応する整数値に解決される数値式を使用する代わりに、 プロセッサとして式を解釈することを示すには、次の構文を使用します。

```dbgcmd
||[Expression]
```

この構文で、角かっこが必要なおよび*式*プロセッサ ID に対応する整数値に解決される任意の数値式の略

次の例では、プロセッサは、ユーザー定義の擬似レジスタの値によって変わります。

```dbgcmd
||[@$t0]
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次の例では、 [ **k (Stack Backtrace の表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)プロセッサ 2 からスタック トレースを表示するコマンド。

```dbgcmd
1: kd> 2k 
```

次の例では、 [ **r (レジスタ)** ](r--registers-.md)を表示するコマンド、 **eax** 3 つのプロセッサのレジスタ。

```dbgcmd
1: kd> 3r eax 
```

ただし、次のコマンドは、以外、現在のプロセッサのプロセッサの状態を変更できないため、構文エラーを示します。

```dbgcmd
1: kd> 3r eax=808080 
```

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>ブレークポイント

カーネルのデバッグ中に、 [ **bp、bu、bm (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md)と[ **ba (アクセスの切断)** ](ba--break-on-access-.md)コマンドのすべてのプロセッサに適用されます、複数のプロセッサ コンピューターです。

たとえば、現在のプロセッサが 3 つの場合でブレークポイントを設定するには、次のコマンドを入力できます**SomeAddress**します。

```dbgcmd
1: kd> bp SomeAddress 
```

次に、そのアドレスでを実行するすべてのプロセッサ (1 つプロセッサだけでなく) では、ブレークポイントのトラップが発生します。

### <a name="span-iddisplayingprocessorinformationspanspan-iddisplayingprocessorinformationspandisplaying-processor-information"></a><span id="displaying_processor_information"></span><span id="DISPLAYING_PROCESSOR_INFORMATION"></span>プロセッサ情報を表示します。

使用することができます、 [ **! を実行している**](-running.md)ターゲット コンピューターの各プロセッサの状態を表示する拡張機能。 プロセッサごとに **! を実行している**プロセス制御ブロック (PRCB)、16 の状態からスレッドの現在および次のフィールドを表示することも組み込みには、スピンロック、およびスタック トレースがキューに登録します。

使用することができます、 [ **! cpuinfo** ](-cpuinfo.md)と[ **! cpuid** ](-cpuid.md)プロセッサ自体に関する情報を表示する拡張機能。

 

 





