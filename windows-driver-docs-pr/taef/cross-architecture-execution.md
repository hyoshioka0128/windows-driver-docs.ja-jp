---
title: クロス アーキテクチャの実行
description: クロス アーキテクチャの実行
ms.assetid: 6E7F53A0-7C6A-4063-8300-31E1853EDD04
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58e3bfad7f506ff4882566553bf70a0b1171e542
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527215"
---
# <a name="cross-architecture-execution"></a>クロス アーキテクチャの実行


テストを実行する OS をサポートしていること、TAEF はコマンド ライン - さまざまなアーキテクチャと同じからテストを実行する機能をサポートします。 つまり、たとえば、x64*と*x86 テスト (x64 OS) 1 つの 'te.exe' コマンドラインを使用して実行できます。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


'Te.exe' 自体よりも異なるアーキテクチャ用のテストを実行するには、アーキテクチャに TAEF バイナリは 'te.exe' に使用する必要があります。 ターゲット アーキテクチャには、いずれかを指定できます。

-   x86
-   x64
-   ia64

TAEF 'te.exe'、アーキテクチャに TAEF バイナリの元の基準としたターゲット アーキテクチャという名前のフォルダーとなります。

## <a name="span-idexecutingtestsforadifferentarchitecturespanspan-idexecutingtestsforadifferentarchitecturespanspan-idexecutingtestsforadifferentarchitecturespanexecuting-tests-for-a-different-architecture"></a><span id="Executing_Tests_for_a_Different_Architecture"></span><span id="executing_tests_for_a_different_architecture"></span><span id="EXECUTING_TESTS_FOR_A_DIFFERENT_ARCHITECTURE"></span>異なるアーキテクチャ用のテストの実行


追加の構成、異なるアーキテクチャ用のテストを実行する必要ありません - 'te.exe' に指定された DLL をパラメーターとして渡します。 TAEF は、バイナリを調べ、特定のターゲット アーキテクチャをロードし、テストを実行するために、適切なホスト プロセスのインスタンスを作成します。 'Te.exe' を検査できる、x86、x64 の DLL をテストおよび x64 が起動プロセス、テストを実行します。

**c:\\taef\\x86&gt;te x64\\Scenario.Tests.dll**

'Te.exe' コマンドラインは、複数のテスト DLL を実行できるため、アーキテクチャを混在させることができ、TAEF は、特定のテスト DLL の適切なホスト プロセスを選択します。

**c:\\taef\\x86&gt;te x64\\Scenario.Tests.dll x86\\Scenario.Tests.dll x64\\UI。>vstest.console.exe**

これにより、TAEF ユーザーがすべての結果が 1 つのログにロール アップを使って 1 つのコマンドラインから複数のテスト カバレッジを取得できます。 この機能がなければアーキテクチャごとにテストがまとめてに独自のコマンド ラインで、個別に実行する必要があり、実行のそれぞれから結果を結合します。

指定されたテスト ファイルがある場合*いない*アーキテクチャ固有 (など、C#純粋 IL にコンパイルされるバイナリ)、しに渡された 'te.exe' と同じアーキテクチャを使用して実行されます。

## <a name="span-idselectingtestsbyarchitecturespanspan-idselectingtestsbyarchitecturespanspan-idselectingtestsbyarchitecturespanselecting-tests-by-architecture"></a><span id="Selecting_Tests_by_Architecture"></span><span id="selecting_tests_by_architecture"></span><span id="SELECTING_TESTS_BY_ARCHITECTURE"></span>アーキテクチャでのテストを選択


TAEF では、'アーキテクチャ' メタデータが特定のアーキテクチャを必要とするテスト ファイルに自動的に適用されます。 'アーキテクチャ' メタデータの値は、アーキテクチャ、テストを実行するために必要なのいずれかになります。

-   x86
-   x64
-   ia64

特定のアーキテクチャ用のテストを選択するためには、'アーキテクチャ' のメタデータと一致するのに言語の選択を使用できます。 たとえば、'Tests' フォルダーにテスト ファイルの x86 および x64 の組み合わせが含まれている場合、次のコマンド ラインは実行 x64 のみテスト。

**c:\\taef\\x86&gt;te テスト\\\*します。>vstest.console.exe /select:@Architecture'x64' を =**

## <a name="span-iderrorsspanspan-iderrorsspanspan-iderrorsspanerrors"></a><span id="Errors"></span><span id="errors"></span><span id="ERRORS"></span>エラー


必要なターゲット アーキテクチャ バイナリの存在することがなく TAEF に異なるアーキテクチャ用コンパイルされたテスト ファイルを渡すと、エラー メッセージが発生します。 次の例は、x86 を示しています。 必要なバイナリが設定されて 'x64' サブフォルダーに、x64 を実行しようとしています。 ' te.exe' をテストします。

``` syntax
c:\>te x64\Scenario.Tests.dll
Test Authoring and Execution Framework v2.2 Build 6.1.7689.0 (release.091218-1251) for x86
Error: Please copy all x64 TAEF binaries to the 'c:\taef\x86\x64' directory in order to run x64 tests from this process. 
Error: Failed to create the ProcessHostController. TE.ProcessHost.exe may be unavailable. Terminating execution...
Error: No test cases were executed.
```

 

 





