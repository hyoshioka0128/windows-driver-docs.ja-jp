---
title: TAEF テストをデバッグする
description: TAEF テストをデバッグする
ms.assetid: 0239547F-EF29-45e0-BACF-ED0F6C07DB99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a0ee06c32bdc2d28ccc8f4186e8b8181bff24c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391372"
---
# <a name="debugging-taef-tests"></a>TAEF テストをデバッグする


## <a name="span-iddebuggerconfigurationspanspan-iddebuggerconfigurationspanspan-iddebuggerconfigurationspandebugger-configuration"></a><span id="Debugger_configuration"></span><span id="debugger_configuration"></span><span id="DEBUGGER_CONFIGURATION"></span>デバッガーの構成


既定では、テスト_ケースは TE.exe より別のプロセスで実行されます。TE.ProcessHost.exe.

## <a name="span-iddebuggingchildprocessesofteexewindbgcdbonlyspanspan-iddebuggingchildprocessesofteexewindbgcdbonlyspandebugging-child-processes-of-teexe-windbgcdb-only"></a><span id="debugging_child_processes_of_te.exe__windbg_cdb_only_"></span><span id="DEBUGGING_CHILD_PROCESSES_OF_TE.EXE__WINDBG_CDB_ONLY_"></span>子プロセスの TE.exe (windbg/cdb のみ) のデバッグ


単に渡すことができます、cdb、windbg などのデバッガーを使用する場合、'-デバッガーにスイッチの o '。 これは、自動的に、子プロセスをデバッグするデバッガーすべて withinin 同じデバッガー インスタンスで構成されます。

例:

``` syntax
windbg -o te.exe MyTests.dll
```

テストを実行するプロセスに切り替えるを使用して、|(パイプ) コマンド。 プロセスの切り替えのパイプ コマンドとして使用される exaclty、~ スレッドを切り替える (tilda) コマンド。

次に、例を示します。

``` syntax
|1s - sets the current process to the second loaded process.
```

## <a name="span-idrunningtestsinprocvisualstudiowindbgcdbspanspan-idrunningtestsinprocvisualstudiowindbgcdbspanspan-idrunningtestsinprocvisualstudiowindbgcdbspanrunning-tests-inproc-visual-studiowindbgcdb"></a><span id="Running_Tests__InProc___Visual_Studio_windbg_cdb_"></span><span id="running_tests__inproc___visual_studio_windbg_cdb_"></span><span id="RUNNING_TESTS__INPROC___VISUAL_STUDIO_WINDBG_CDB_"></span>テストの実行"InProc"(Visual Studio/windbg/cdb)


Visual Studio を使用して、デバッグを実行する場合は、上記のメソッドが機能しません。 この場合、デバッガーを TE.exe を実行し、テスト_ケースの適切なブレークポイントを設定し、TE.exe に/inproc スイッチを渡すだけを構成します。 これにより、TE.exe 内ですべてのテストを実行する新しいプロセスを作成するのではなく処理します。

例:

``` syntax
start devenv /debugexe te.exe MyTests.dll /inproc
```

上記のコマンドは、Visual Studio が起動します。 次に、テスト_ケースのソース コードを開き、適切なブレークポイントを設定します。 最後に、f5 キーを押してテスト_ケースを開始するは、(、シンボルが正しく読み込まれている) 場合、最初のブレークポイントで中断する必要があります。

前述の手順は、Visual Studio で設定する適切なシンボルでのみ動作します。 少なくとも、シンボルをデバッグしているテスト dll に設定する必要があります。 Visual Studio でシンボルを設定します。

-   [ツール] メニューを選択します。
-   オプションの選択.
-   左側のツリー風のメニューでデバッグを選択します。
-   デバッグ シンボルを選択します。
-   シンボル ファイルのシンボル パスを入力します (\*.pdb) の場所: セクション
-   設定を保存します。

## <a name="span-idautomaticallybreakingintothedebuggerbreakoncreateandbreakoninvokespanspan-idautomaticallybreakingintothedebuggerbreakoncreateandbreakoninvokespanspan-idautomaticallybreakingintothedebuggerbreakoncreateandbreakoninvokespanautomatically-breaking-into-the-debugger-breakoncreate-and-breakoninvoke"></a><span id="Automatically_Breaking_into_the_Debugger___breakOnCreate__and__breakOnInvoke__"></span><span id="automatically_breaking_into_the_debugger___breakoncreate__and__breakoninvoke__"></span><span id="AUTOMATICALLY_BREAKING_INTO_THE_DEBUGGER___BREAKONCREATE__AND__BREAKONINVOKE__"></span>("BreakOnCreate"および"breakOnInvoke") のデバッガーで自動的に中断


デバッグ プロセスが容易になります、するためには、Taef は、各テスト クラスがインスタンス化や、各テストの前にメソッドが呼び出される前に、デバッガーを自動的に解除する機能を提供します。

次に、例を示します。

``` syntax
cdb -gG te.exe MyTests.dll /inproc /breakOnCreate /breakOnInvoke
```

上記のコマンドでは、cdb で Te.exe が起動します。 Taef はデバッガーに割り込む適切な各テスト クラスのインスタンスを作成し、各テストの前にメソッドが呼び出される前にします。

**注:** デバッガーとも指定/inProc オプション Te.exe の実行中にこの機能を使用することをお勧めします。

 

 





