---
title: テストの実行の概要
description: テストの実行の概要
ms.assetid: 3D58D074-DC06-4b01-9EB5-7A17E69D6935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3b6196e70854fc3a97653834bfecc154557edf2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355488"
---
# <a name="overview-of-executing-tests"></a>テストの実行の概要


単純な; は、TAEF を使用してテストを実行します。コマンド"TE でのテスト ファイルを指定するだけです。EXE"。 たとえば、"CPP 内のすべてのテストを実行するには。Basic.Examples.dll"テスト ファイルを行うことができます。

``` syntax
TE.exe CPP.Basic.Examples.dll
```

別の方法でマークされているテストが含まれている場合でも、複数のテスト ファイルを指定できます。 たとえば、次のコマンドは、"CPP でのすべてのテストを実行は。異なる言語で書かれている場合でも、Basic.Examples.dll"と"CSharp.Basic.Examples.dll"ファイルします。

``` syntax
TE.exe CPP.Basic.Examples.dll CSharp.Basic.Examples.dll
```

実行するファイルの選択にワイルドカードを使用することもできます。

``` syntax
TE.exe *.Examples.dll
```

相対パスを指定することもできます。

``` syntax
TE.exe Examples\*
```

すべてのテストが含まれていないコマンド プロンプトで、ファイルが指定されて場合 TE の間で、エラー メッセージが報告されます。

## <a name="span-idorderofexecutionspanspan-idorderofexecutionspanspan-idorderofexecutionspanorder-of-execution"></a><span id="Order_of_Execution"></span><span id="order_of_execution"></span><span id="ORDER_OF_EXECUTION"></span>実行の順序


コマンド プロンプトで指定されたテスト ファイルは、指定した順序で処理されます。

## <a name="span-idoutofprocessexecutionspanspan-idoutofprocessexecutionspanspan-idoutofprocessexecutionspanout-of-process-execution"></a><span id="OutOfProcessExecution"></span><span id="outofprocessexecution"></span><span id="OUTOFPROCESSEXECUTION"></span>プロセスの実行


既定では、TAEF がテスト プロセスの外を実行します -"TE を使用しています。テストを実行するプロセスを ProcessHost.exe"。 これにより、1 つ別のテストが以前のテストを受けていることを防ぐから分離するテストができます。 "TE.exe"プロセスでテストを実行するかどうかは、指定することができます、 **"/inproc"** TE.exe のオプション。

## <a name="span-idselectingtestsspanspan-idselectingtestsspanspan-idselectingtestsspanselecting-tests"></a><span id="Selecting_Tests"></span><span id="selecting_tests"></span><span id="SELECTING_TESTS"></span>テストの選択


使って特定のテストを選択することができます、 **「/選択」** オプション、クエリ、および指定して ' 選択 '。 [選択](selection.md)ページで選択クエリを使用して実行する特定のテストを選択する方法を説明します。 使用することを選択するテストの名前のみに基づいて場合、 **「/名前を」** オプションを使用します。 詳細については、選択 ページを参照してください。

## <a name="span-idspecifyingpartofcommandasenvironmentvariabletecmdspanspan-idspecifyingpartofcommandasenvironmentvariabletecmdspanspan-idspecifyingpartofcommandasenvironmentvariabletecmdspanspecifying-part-of-command-as-environment-variable-tecmd"></a><span id="Specifying_part_of_command_as_environment_variable__te_cmd"></span><span id="specifying_part_of_command_as_environment_variable__te_cmd"></span><span id="SPECIFYING_PART_OF_COMMAND_AS_ENVIRONMENT_VARIABLE__TE_CMD"></span>環境変数とコマンドの一部を指定する: **te\_cmd**


環境変数を活用できる場合は、同じも te.exe するためのコマンド オプションの一部は常に、 **te\_cmd**します。 どのような te\_に設定されている cmd te.exe 実行するためのコマンドに追加されます。 "*設定 te\_cmd =/一覧*"、コマンド プロンプトで指定されたバイナリの実行とテストの一覧を常に表示されます。

## <a name="span-idlistingtestsspanspan-idlistingtestsspanspan-idlistingtestsspanlisting-tests"></a><span id="Listing_Tests"></span><span id="listing_tests"></span><span id="LISTING_TESTS"></span>テストを一覧表示します。


指定する、 **"/list"** テスト ファイルと併せてオプションは、クラスの名前を一覧し、コンソール上のテスト ファイルでテスト メソッドをコマンド。 バイナリ、クラスとテストのメソッド名の指定された各バイナリのみを一覧表示され、実行されませんに注意してください。 詳細については、セットアップとクリーンアップの方法、メタデータ、レベルごとに指定されたプロパティなどの一覧を表示して、データが発生した場合、提供されたデータ駆動テストを使用している場合、 **"/list プロパティ"** コマンド オプションを代わりにします。

## <a name="span-idtestresultsspanspan-idtestresultsspanspan-idtestresultsspantest-results"></a><span id="Test_Results"></span><span id="test_results"></span><span id="TEST_RESULTS"></span>テスト結果


ジェネリック、テスト_ケースのテスト結果は異なるかどうかを確認してください呼び出しが成功したか失敗しました。 Api の使用可能なその他の詳細を確認するには[[確認]](verify.md)します。 テスト中には、検証の呼び出しは行われません、テスト結果は TAEF で提供されるログのサブスクライバーの「合格」に既定値は。 指定することができます、 **"DefaultTestResult"** 明示的にテストを作成する際にします。 参照してください[オーサリング テスト](authoring-tests.md)の詳細。

## <a name="span-idhelp-commandoptionsspanspan-idhelp-commandoptionsspanspan-idhelp-commandoptionsspanhelp---command-options"></a><span id="Help_-_Command_Options"></span><span id="help_-_command_options"></span><span id="HELP_-_COMMAND_OPTIONS"></span>ヘルプ/コマンド オプション


指定することで利用できるすべてのコマンド オプションの explantions が見つかります、 **「/?」** TE.exe のオプションです。 拡張の説明については、次を参照してください。 [Te.exe コマンド オプション](te-exe-command-line-parameters.md)します。

 

 





