---
title: テストの実行の概要
description: テストの実行の概要
ms.assetid: 3D58D074-DC06-4b01-9EB5-7A17E69D6935
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7095fdbfbd80bfbc954db6a6a2697407b8edd6c
ms.sourcegitcommit: 97a8d24b1b48602e4ccaa63a113f7c8cdb0c6df5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/16/2020
ms.locfileid: "84812441"
---
# <a name="overview-of-executing-tests"></a>テストの実行の概要

TAEF を使用してテストを実行するには、コマンド**TE.EXE**を使用してテストファイルを指定します。これは%: Kits\10\Testing\Runtimes\TAEF. ファイル (x86) \windows にあります。 たとえば、 **CPP.Basic.Examples.dll**テストファイル内ですべてのテストを実行するには、次のように実行します。

``` syntax
TE.exe CPP.Basic.Examples.dll
```

異なる方法でマークアップされたテストが含まれている場合でも、複数のテストファイルを指定できます。 たとえば、次のコマンドは、さまざまな言語で記述されている場合でも、 **CPP.Basic.Examples.dll**ファイルと**CSharp.Basic.Examples.dll**ファイル内のすべてのテストを実行します。

``` syntax
TE.exe CPP.Basic.Examples.dll CSharp.Basic.Examples.dll
```

また、ワイルドカードを使用して、実行するファイルを選択することもできます。

``` syntax
TE.exe *.Examples.dll
```

また、相対パスを指定することもできます。

``` syntax
TE.exe Examples\*
```

コマンドプロンプトで、テストが含まれていないファイルを指定した場合は、TE.exe によってエラーメッセージが報告されます。

## <a name="order-of-execution"></a>実行の順序

コマンドプロンプトで指定されたテストファイルは、指定された順序で処理されます。

## <a name="out-of-process-execution"></a>アウトプロセスの実行

既定では、TAEF はアウトプロセスでテストを実行します。 TAEF は、 **TE.ProcessHost.exe**プロセスを使用してテストを実行します。 これにより、テストが相互に分離され、テストが以前のテストの影響を受けないようにすることができます。 **TE.exe**プロセスでテストを実行するには、 **TE.exe**の **"/inproc"** オプションを指定します。

## <a name="selecting-tests"></a>テストの選択

特定のテストを選択するには、 **"/select"** オプションを使用して、"選択クエリ" を指定します。 テストの名前のみに基づいてを選択する場合は、代わりに **"/name"** オプションを使用します。 選択クエリを使用して実行する特定のテストを選択する方法の詳細については、「 [selection](selection.md)」を参照してください。

## <a name="specifying-part-of-command-as-environment-variable-te_cmd"></a>コマンドの一部を環境変数として指定する: **te \_ cmd**

te.exe のコマンドオプションの一部が常に同じである場合は、環境変数**te \_ cmd**を利用できます。 \_Cmd がに設定されている場合は、te.exe 実行のコマンドに追加されます。 "*Set te \_ cmd =/list*" を使用すると、コマンドプロンプトで指定されたバイナリの実行に対して常にテストの一覧が表示されます。

## <a name="listing-tests"></a>テストの一覧表示

テストファイルと共に **"/list"** コマンドオプションを指定すると、コンソールのテストファイルにクラスとテストメソッドの名前が一覧表示されます。 これにより、指定された各バイナリのバイナリ、クラス、およびテストメソッドの名前のみが一覧表示され、実行されないことに注意してください。 セットアップとクリーンアップの方法、各レベルで指定されたメタデータまたはプロパティなどの詳細を一覧表示する場合や、データドリブンテストの場合は、代わりに **"/listproperties"** コマンドオプションを使用してください。

## <a name="test-results"></a>テスト結果

一般的なテストケースの場合、テスト結果は検証呼び出しが成功したか失敗したかによって異なります。 使用可能な Api とその他の詳細については、 [「Verify」](verify.md)を参照してください。 テスト中に検証呼び出しが行われない場合は、TAEF で提供されるログサブスクライバーに対して、テスト結果の既定値が "成功" になります。 テストの作成時に **"Defaulttestresult"** を明示的に指定することもできます。 詳細については、「[テストの作成](authoring-tests.md)」を参照してください。

## <a name="help---command-options"></a>Help-Command オプション

**"/?"** を指定して、使用可能なすべてのコマンドオプションの explantions を検索します。 TE.exe のオプション。 詳細については、「 [Te.exe コマンドオプション](te-exe-command-line-parameters.md)」を参照してください。
