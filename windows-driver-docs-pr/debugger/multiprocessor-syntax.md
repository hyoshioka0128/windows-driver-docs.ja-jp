---
title: マルチプロセッサの構文
description: このトピックでは、マルチプロセッサの構文について説明します
ms.assetid: 71adc522-f078-457c-8bc9-9e971e914a41
keywords: マルチプロセッサコンピューター、マルチプロセッサ、コマンド構文、デュアルプロセッサコンピューター、コマンドの構文規則、プロセッサ識別子
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c76c200699c287359f4d50167f4a8d58175b2da
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242791"
---
# <a name="multiprocessor-syntax"></a>マルチプロセッサの構文


## <span id="ddk_multiprocessor_syntax_dbg"></span><span id="DDK_MULTIPROCESSOR_SYNTAX_DBG"></span>


KD およびカーネルモードの WinDbg では、複数のプロセッサデバッグがサポートされています。 この種のデバッグは、任意のマルチプロセッサプラットフォームで実行できます。

プロセッサには、0から*n*までの番号が付けられます。

現在のプロセッサがプロセッサ0の場合 (つまり、現在デバッガーがアクティブになっているプロセッサの場合)、他の非現在のプロセッサ (プロセッサ 1 ~ *n*) を調べることができます。 ただし、現在のプロセッサ以外では変更できません。 状態を表示することしかできません。

### <a name="span-idselecting_a_processorspanspan-idselecting_a_processorspanselecting-a-processor"></a><span id="selecting_a_processor"></span><span id="SELECTING_A_PROCESSOR"></span>プロセッサの選択

[**Echocpunum (CPU 番号の表示)** ](-echocpunum--show-cpu-number-.md)コマンドを使用して、現在のプロセッサのプロセッサ番号を表示できます。 このコマンドからの出力を使用すると、カーネルデバッグプロンプトのテキストによって複数のプロセッサシステムを操作しているときにすぐに通知できます。

次の例では、 **0:** **&gt;** プロンプトの前に、コンピューターの最初のプロセッサをデバッグしていることを示します。

```dbgcmd
0: kd>
```

次の例に示すように、 [ **~ s (現在のプロセッサの変更)** ](-s--change-current-processor-.md)コマンドを使用してプロセッサを切り替えます。

```dbgcmd
0: kd> ~1s
1: kd>
```

ここで、コンピューターの2番目のプロセッサをデバッグします。

中断が発生し、スタックトレースを理解できない場合は、マルチプロセッサシステムのプロセッサを変更することが必要になる場合があります。 中断が別のプロセッサで発生した可能性があります。

### <a name="span-idspecifying_processors_in_other_commandsspanspan-idspecifying_processors_in_other_commandsspanspecifying-processors-in-other-commands"></a><span id="specifying_processors_in_other_commands"></span><span id="SPECIFYING_PROCESSORS_IN_OTHER_COMMANDS"></span>他のコマンドでのプロセッサの指定

プロセッサ番号は、いくつかのコマンドの前に追加できます。 この数値の前には、 **~ S**コマンドを除き、チルダ ( **~** ) は付きません。

**注**   ユーザーモードのデバッグでは、チルダを使用してスレッドを指定します。 この構文の詳細については、「 [Thread 構文](thread-syntax.md)」を参照してください。

 

プロセッサ Id が明示的に参照されている必要はありません。 代わりに、プロセッサ ID に対応する整数に解決される数値式を使用できます。 式をプロセッサとして解釈する必要があることを示すには、次の構文を使用します。

```dbgcmd
||[Expression]
```

この構文では、角かっこが必要で、 *Expression*はプロセッサ ID に対応する整数に解決される任意の数値式を表します。

次の例では、プロセッサはユーザー定義の擬似レジスタの値に応じて変化します。

```dbgcmd
||[@$t0]
```

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

次の例では、 [**k (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを使用して、プロセッサ2のスタックトレースを表示します。

```dbgcmd
1: kd> 2k 
```

次の例では、 [**r (レジスタ)** ](r--registers-.md)コマンドを使用して、プロセッサ3の**eax**レジスタを表示します。

```dbgcmd
1: kd> 3r eax 
```

ただし、次のコマンドでは構文エラーが発生します。これは、現在のプロセッサ以外のプロセッサの状態を変更できないためです。

```dbgcmd
1: kd> 3r eax=808080 
```

### <a name="span-idbreakpointsspanspan-idbreakpointsspanbreakpoints"></a><span id="breakpoints"></span><span id="BREAKPOINTS"></span>区切り

カーネルデバッグ中、 [**bp、bu、bm (ブレークポイントの設定)** ](bp--bu--bm--set-breakpoint-.md) 、および[**ba (アクセス時の中断)** ](ba--break-on-access-.md)の各コマンドは、複数のプロセッサを搭載したコンピューターのすべてのプロセッサに適用されます。

たとえば、現在のプロセッサが3の場合、次のコマンドを入力して、ブレークポイントを任意の**アドレス**に配置できます。

```dbgcmd
1: kd> bp SomeAddress 
```

その後、そのアドレスで実行されるプロセッサ (プロセッサ1だけでなく) は、ブレークポイントトラップを発生させます。

### <a name="span-iddisplaying_processor_informationspanspan-iddisplaying_processor_informationspandisplaying-processor-information"></a><span id="displaying_processor_information"></span><span id="DISPLAYING_PROCESSOR_INFORMATION"></span>プロセッサ情報の表示

[ **! 実行中**](-running.md)の拡張機能を使用して、ターゲットコンピューター上の各プロセッサの状態を表示できます。 各プロセッサについて、 **! を実行**すると、プロセス制御ブロック (prcb) の現在のスレッドフィールドと次のスレッドフィールド、16個の組み込みキュースピンロックの状態、およびスタックトレースを表示することもできます。

[ **! Cpu 情報**](-cpuinfo.md)と[ **! cpuid**](-cpuid.md)拡張機能を使用して、プロセッサ自体に関する情報を表示できます。

 

 





