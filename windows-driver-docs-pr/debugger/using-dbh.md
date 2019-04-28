---
title: DBH の使用
description: DBH の使用
ms.assetid: c544013d-e925-40bf-b76d-bf9cefb9fd6d
keywords:
- DBH を使用して
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b11826f966fc73ef4f0404c93ab0f5f00e88027
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371586"
---
# <a name="using-dbh"></a>DBH の使用


DBH は DbgHelp API (dbghelp.dll) 内の関数の多くを公開するコマンド ライン ツールです。 シンボル ファイルの内容に関する情報を表示し、ファイルにシンボルの特定の詳細を表示、さまざまな条件に一致するシンボル ファイルを検索できます。

DBH によって提供される機能は WinDbg、KD、CDB 内などによって提供されるコマンドに似ていますが[ **(シンボルを調べる) x**](x--examine-symbols-.md)します。

### <a name="span-idrunningdbhininteractivemodespanspan-idrunningdbhininteractivemodespanrunning-dbh-in-interactive-mode"></a><span id="running_dbh_in_interactive_mode"></span><span id="RUNNING_DBH_IN_INTERACTIVE_MODE"></span>対話モードで実行中の DBH

ターゲット モジュールがシンボルを調査するを指定する、シンプルなコマンド ラインで DBH を開始します。 ターゲット モジュールには、プログラムを実行可能ファイルまたは PDB シンボル ファイルを使用できます。 プロセス ID (PID) を調査するを指定することもできます。 参照してください[ **DBH コマンド ライン オプション**](dbh-command-line-options.md)完全な構文です。

DBH の開始時に指定したモジュールのシンボルを読み込み、位置には、さまざまなコマンドを入力することができます、プロンプトが表示されます。 参照してください[DBH コマンド](dbh-commands.md)使用可能なコマンドの一覧についてはします。

たとえば、次のシーケンスのプロセス ID 4672、ターゲット プロセスを指定して DBH を起動を実行します、 **enum** DBH プロンプトでコマンドを表示する記号は、特定のパターンに一致して、を実行し、**q** DBH を終了するコマンド。

```console
C:\> dbh -p:4672 
            400000 : TimeTest
          77820000 : ntdll
          77740000 : kernel32

pid:4672 mod:TimeTest[400000]: enum TimeTest!ma* 

 index            address     name
     1             42cc56 :   main
     3             415810 :   malloc
     5             415450 :   mainCRTStartup

pid:4672 mod:TimeTest[400000]: q 

goodbye 
```

### <a name="span-idrunningdbhinbatchmodespanspan-idrunningdbhinbatchmodespanrunning-dbh-in-batch-mode"></a><span id="running_dbh_in_batch_mode"></span><span id="RUNNING_DBH_IN_BATCH_MODE"></span>バッチ モードで実行中の DBH

1 つの DBH コマンドのみを実行する場合は、コマンドラインの末尾に指定できます。 これにより、DBH を開始、指定したモジュールの読み込み、指定されたコマンドを実行してから終了します。

たとえば、1 つのコマンドラインを使用した前の例を置き換えることができます。

```console
C:\> dbh -p:4672 enum TimeTest!ma* 
           400000 : TimeTest
         77820000 : ntdll
         77740000 : kernel32

index            address     name
    1             42cc56 :   main
    3             415810 :   malloc
    5             415450 :   mainCRTStartup 
```

DBH を実行しているは、このメソッドが呼び出された*バッチモード*バッチ ファイルで簡単に使用できるため、します。 パイプでコマンドラインのこのバージョンを表示することも ( **|** ) DBH 出力を別のプログラムにリダイレクトします。

### <a name="span-idspecifyingthetargetspanspan-idspecifyingthetargetspanspecifying-the-target"></a><span id="specifying_the_target"></span><span id="SPECIFYING_THE_TARGET"></span>ターゲットを指定します。

DBH は 3 つの方法で、ターゲットを選択することができます。 実行中のプロセスのプロセス ID、、実行可能ファイルの名前またはシンボル ファイルの名前。 たとえば、MyProg.exe、ID 1234 のプロセスで実行中の 1 つのインスタンスがある場合、次のコマンドはこととほぼ同じであります。

```console
C:\> dbh -v -p:1234 
C:\> dbh -v c:\mydir\myprog.exe 
C:\> dbh -v c:\mydir\myprog.pdb 
```

これらのコマンドの 1 つの違いは、プロセス ID を指定して DBH を開始するときに DBH がこのプロセスによって使用されている実際の仮想アドレスを使用します。 実行可能ファイル名またはシンボル ファイルの名前を指定することによって DBH を開始するときに DBH はモジュールのベース アドレスが標準値 (たとえば、0x01000000) であると仮定します。 使用することができますし、**基本**のため、モジュール内のすべてのシンボルのアドレスをシフト、実際のベース アドレスを指定するコマンド。

DBH は、デバッガーが行うような方法でターゲット プロセスにはアタッチできません。 DBH を開始または終了、プロセスが発生することはできません。 またそのプロセスの実行方法に変更できます。 DBH そのプロセス ID を使用して、プロセスにアタッチするターゲット プロセスが実行されているがターゲット プロセスを終了して、そのシンボルにアクセスする DBH が引き続き DBH が開始されたら。

### <a name="span-iddecoratedandundecoratedsymbolsspanspan-iddecoratedandundecoratedsymbolsspandecorated-and-undecorated-symbols"></a><span id="decorated_and_undecorated_symbols"></span><span id="DECORATED_AND_UNDECORATED_SYMBOLS"></span>装飾と非装飾のシンボル

既定では、DBH は非装飾のシンボル名を表示すると、シンボルの検索を使用します。 無効にした場合、 [SYMOPT\_UNDNAME](symbol-options.md#symopt-undname)シンボルのオプション、または DBH コマンドラインで-d オプションを含める、装飾が含まれます。

シンボルの装飾については、次を参照してください。[パブリックおよびプライベート シンボルの](public-and-private-symbols.md)します。

### <a name="span-idexitingdbhspanspan-idexitingdbhspanexiting-dbh"></a><span id="exiting_dbh"></span><span id="EXITING_DBH"></span>DBH を終了します。

DBH を終了するには、使用、 **q** DBH プロンプトでコマンド。

 

 





