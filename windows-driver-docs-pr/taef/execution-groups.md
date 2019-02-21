---
title: グループの実行
description: グループの実行
ms.assetid: CC196843-A225-4193-9386-EE024B5D0B68
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 828b4728513b6a977ab3f085d5ca11661dba2543
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560893"
---
# <a name="execution-groups"></a>グループの実行


基本的な実行について理解しているかどうかを確認してください[TAEF](index.md)を理解して方法[作成者テスト](authoring-tests.md)、このセクションに進む前に使用します。 ユーザー ガイドに記載のいくつかデータ ドリブン テスト例のウォークスルーを経由する可能性があります。

## <a name="span-idscenario-basedtestingwithtaefspanspan-idscenario-basedtestingwithtaefspanspan-idscenario-basedtestingwithtaefspanscenario-based-testing-with-taef"></a><span id="Scenario-Based_Testing_with_TAEF"></span><span id="scenario-based_testing_with_taef"></span><span id="SCENARIO-BASED_TESTING_WITH_TAEF"></span>TAEF とシナリオ ベースのテスト


シナリオ レベルのテストについて説明するときに、次のテストを実行する意味のシナリオでは、前のテストが成功した場合にのみ、テストの一連の本当に話すことです。 場合によっては、前のテストが失敗した場合、次のテストを実行する必要があるすべての情報を必要もがありますされません。 このテスト メソッドのシナリオをテストすることができますと実行の単位を維持しながら TAEF をサポートしています"ExecutionGroup"s として知られる仕組み。 シナリオ ベースのテスト TAEF に関係なくながら、データ ドリブン テストなどの他の機能です。 データ ドリブン テストを活用するシナリオを設計する場合は、TAEF によって提供されるクラスのデータに基づく機能を使用してクラス レベルでデータ ドリブンのサポートを適用できます。 **クラス レベルでデータ ドリブンのサポートを適用すると、すべてのテスト クラス内で行ごとに順番に実行されることができます。**

このページは、"ExecutionGroup"として、クラス内でのテストの順序を指定する方法に集中します。

## <a name="span-idexecutiongroupsspanspan-idexecutiongroupsspanspan-idexecutiongroupsspanexecution-groups"></a><span id="Execution_Groups"></span><span id="execution_groups"></span><span id="EXECUTION_GROUPS"></span>グループの実行


実行のグループを説明する前にことに注意してくださいし、ことに注意して重要な**TAEF、クラス内でのテストの実行の順序は、注文をするには修飾されたそれらのテストとして\_METHOD(...) ネイティブ コード、または追加が発生した場合\[TestMethod\]マネージ コードが発生した場合、メソッドの前にプロパティ**します。 TAEF では、クラス自体の実行の順序は保証されません。

**ここで、シナリオ ベースのテストでのみ実行の順序を保証するための十分なできない可能性がありますのシナリオでは、次のテストに進む前に、シナリオですべての以前のテストが成功したことを保証する必要もあります。** これを使用するには、"ExecutionGroup"の概念を表示します。

ネイティブの例を検討してください。

```cpp
1     class ExecutionDependencyExample
2     {
3         BEGIN_TEST_CLASS(ExecutionDependencyExample)
4             TEST_CLASS_PROPERTY(L"ExecutionGroup", L"DependentTests")
5         END_TEST_CLASS()
6
7         TEST_METHOD(Test1)
8         {
9             Log::Comment(L"Test1 passes.");
10        }
11
12        TEST_METHOD(Test2)
13        {
14            Log::Comment(L"Test2 fails.");
15            VERIFY_ARE_EQUAL(2, 3);
16        }
17
18        TEST_METHOD(Test3)
19        {
20            Log::Comment(L"Test3 is blocked; so you shouldn&#39;t see this.");
21        }
22    };
```

上記の C++ ファイルのスニペットの 4 行目を参照してください。 このケースでは、"ExecutionGroup""DependentTests"と呼ばれるに属しているクラス ExecutionDependencyExample 内のすべてのテストを修飾します。 これは"Test1"、「test2.」および"Test3""DependentTests"グループの実行の一部であることを意味します。 前述のように、場合にのみ正常に実行を取得し、Test1、Test2 が実行を取得します。 同様に Test3 場合にのみ正常に実行を取得し、Test2 実行されます。

(14、15 行を参照してください) が失敗する Test2 が設計されていることが表示されます。

Test2 は、"DependentTests""ExecutionGroup"で失敗すると、ため Test3 は実行されませんし、ブロックとしてマークされた代わりにします。 上記のテストし、これが実際に実行することができます。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll
Test Authoring and Execution Framework v2.93k for x86

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1
Test1 passes.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1 
    [Passed]

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2
Test2 fails.
Error: Verify: AreEqual(2, 3) - Values (2, 3) [File: >f:source\executiondependencyexample\executiondependencyexample.cpp,
Function: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2, Line:21] 
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2[Failed] 

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test3
Blocked: This test belongs to an execution group and depends on the previous test being executed in the same environment successfully. The dependent test must be selected for execution, must request the same execution environment (e.g. 'ThreadingModel') and must be executed successfully.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test3 [Blocked]

Non-passing Tests:
    WEX::TestExecution::Examples::ExecutionDependencyExample::Test2 [Failed]
    WEX::TestExecution::Examples::ExecutionDependencyExample::Test3 [Blocked]

Summary: Total=3, Passed=1, Failed=1, Blocked=1, Not Run=0, Skipped=0
```

予測、として Test1 が渡される、Test2 が失敗し、Test3 がブロックされたに注意してください。 Test3 で TAEF Test3 が属するグループの実行と、前のテストが正常に実行されなかったことを示すメッセージを記録します。

このエラー メッセージは、同じ ExecutionGroup に属することが、現在テストが実行される前にすべてのテストを選択することも述べています。 つまり、Test2 のみを実行しようとする場合、選択条件を使用して、実行時に、見つかります Test2 がブロックされることは実行 Test1 に依存する同じ ExecutionGroup の一部であります。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll /name:*Test2*
Test Authoring and Execution Framework v2.9.3k for x86

StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2
Blocked: This test belongs to an execution group and depends on the previous test being executed in the same environment successfully. The dependent test must be selected for execution, must request the same execution environment (e.g. 'ThreadingModel') and must be executed successfully.

EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test2 [Blocked]

Summary: Total=1, Passed=0, Failed=0, Blocked=1, Not Run=0, Skipped=0
```

ただし、ExecutionGroup の最初のテストである、Test1 を選択する場合、正常に実行されます。

``` syntax
te Examples\CPP.ExecutionDependency.Example.dll /name:*Test1*
Test Authoring and Execution Framework v2.9.3k for x86
StartGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1
Test1 passes.
EndGroup: WEX::TestExecution::Examples::ExecutionDependencyExample::Test1 [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

また、ExecutionGroup に属していないテストした場合が実行して続行して ExecutionGroup 内のテストの実行結果に関係なく。 クラス内で 1 つ以上の ExecutionGroup させることもできます。 ただし、クラス間に ExecutionGroup をまたがることはできません。 これを行う場合、代わりとして見なすクラスごとに 1 つずつ、2 つの個別 ExecutionGroups します。

メッセージは、Test3 を Test2 と同じ環境で実行することも述べています。 この側面で少し詳しく理解しようとすることができます。 シナリオ ベースのテストの一部に、ExecutionGroup の一員になること、ため、すべてのテストが要求して、同一の環境で実行するために重要になります。 たとえば、ExecutionGroup 内で、スレッド処理モデルが変更された場合は、ブロックされているテストが表示されます。 たとえば、上記の例では、Test2 が正常に実行する設計されたは、'ThreadingModel' プロパティが 'MTA' に設定した場合 Test3 もブロックされます。

別の例を考えてみましょう。例\\TAEF\\CSharp\\ExecutionDependentGroupsExample (最新の TAEF リリース共有を参照してください)

```cpp
1     [TestClass]
2     public class CSharpExecutionDependentGroupsExample
3     {
4         //First Execution Group: Test1, Test2
5         [TestMethod]
6         [TestProperty("ExecutionGroup", "First Execution Group")]
7         public void Test1()
8         {
9             Log.Comment("Part of First Execution Group");
10        }
11        [TestMethod]
12        [TestProperty("ExecutionGroup", "First Execution Group")]
13        public void Test2()
14        {
15            Log.Comment("Part of First Execution Group");
16        }
17
18        //Second Execution Group: Test3, Test4. Test4 fails
19        [TestMethod]
20        [TestProperty("ExecutionGroup", "Second Execution Group")]
21        public void Test3()
22        {
23            Log.Comment("Part of Second Execution Group");
24        }
25        [TestMethod]
26        [TestProperty("ExecutionGroup", "Second Execution Group")]
27        public void Test4()
28        {
29            Log.Comment("Part of Second Execution Group - last in group fails");
30            Verify.IsTrue(false);
31        }
32
33        //Third Execution Group: Test5, Test6, Test7. Test6 fails, Test7 will be blocked.
34        [TestMethod]
35        [TestProperty("ExecutionGroup", "Third Execution Group")]
36        public void Test5()
37        {
38            Log.Comment("Part of Third Execution Group");
39        }
40        [TestMethod]
41        [TestProperty("ExecutionGroup", "Third Execution Group")]
42        public void Test6()
43        {
44            Log.Comment("Part of Third Execution Group - middle in this set of 3 fails");
45            Verify.IsTrue(false);
46        }
47        [TestMethod]
48        [TestProperty("ExecutionGroup", "Third Execution Group")]
49        public void Test7()
50        {
51            Log.Comment("Part of Third Execution Group");
52        }
53
54        //Fourth Execution Group: Test8, Test9
55        [TestMethod]
56        [TestProperty("ExecutionGroup", "Fourth Execution Group")]
57        public void Test8()
58        {
59            Log.Comment("Part of Fourth Execution Group");
60        }
61        [TestMethod]
62        [TestProperty("ExecutionGroup", "Fourth Execution Group")]
63        public void Test9()
64        {
65            Log.Comment("Part of Fourth Execution Group");
66        }
67    }
```

この例では、4 つの異なる実行グループがあります。

-   「最初の実行グループ」には、Test1、Test2; が含まれています。どちらも正常に渡す必要があります。
-   「2 番目の実行のグループ」には、Test3 と Test4 が含まれています。 Test4 はこの ExecutionGroup の最後のテストと失敗します。
-   「3 つ目の実行グループ」には、Test5、Test6 および Test7 が含まれています。 Test5 を実行し、以前 ExecutionGroup から Test4 失敗が正常に渡します。 Test6 は、ブロックされる Test7 引き起こしますが失敗し、設計されています。
-   「4 つ目の実行グループ」には、Test8 と Test9 が含まれています。 もう一度、Test8 で正常に実行がすべて Test6 失敗を期限前 ExecutionGroup から Test7 がブロックされた、および Test9 する際にします。

この例でより良い ExecutionGroups を理解するこの例ではプロパティの一覧してみましょう。

``` syntax
te Examples\CSharp.ExecutionDependentGroups.Example.dll /listproperties
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ \Examples\CSharp.ExecutionDependentGroups.Example.dll
            WEX.Examples.CSharpExecutionDependentGroupsExample
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test1
                        Property[ExecutionGroup] = First Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test2
                        Property[ExecutionGroup] = First Execution Group

                WEX.Examples.CSharpExecutionDependentGroupsExample.Test3
                        Property[ExecutionGroup] = Second Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test4
                        Property[ExecutionGroup] = Second Execution Group

                WEX.Examples.CSharpExecutionDependentGroupsExample.Test5
                        Property[ExecutionGroup] = Third Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test6
                        Property[ExecutionGroup] = Third Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test7
                        Property[ExecutionGroup] = Third Execution Group

                WEX.Examples.CSharpExecutionDependentGroupsExample.Test8
                        Property[ExecutionGroup] = Fourth Execution Group
                WEX.Examples.CSharpExecutionDependentGroupsExample.Test9
                        Property[ExecutionGroup] = Fourth Execution Group
```

上記のテストを実行するときに、次の出力は予測の実行順序を確認します。

``` syntax
te Examples\CSharp.ExecutionDependentGroups.Example.dll
Test Authoring and Execution Framework v2.9.3k for x86

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test1

Part of First Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test1 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test2

Part of First Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test2 [Passed]

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test3

Part of Second Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test3 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test4

Part of Second Execution Group - last in group fails
Error: Verify: IsTrue [File: Need_Symbols, Function: Test4, Line: 0] 
Error: [HRESULT: 0x80131604]. Operation failed: 'WEX.Examples.CSharpExecutionDependentGroupsExample.Test4'.
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test4 [Failed]

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test5

Part of Third Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test5 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test6

Part of Third Execution Group - middle in this set of 3 fails
Error: Verify: IsTrue [File: Need_Symbols, Function: Test6, Line: 0] 
Error: [HRESULT: 0x80131604]. Operation failed: 'WEX.Examples.CSharpExecutionDependentGroupsExample.Test6'.
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test6 [Failed] 
Error: WEX.Examples.CSharpExecutionDependentGroupsExample.Test7 belongs to an execution group and depends
       on the previous test being executed in the same environment successfully.
Error: Please make sure that the dependent test is selected for execution, requests the same execution .
       environment metadata(e.g. 'ThreadingModel') and that it executed successfully.
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test7
Blocked EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test7 [Blocked]

StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test8

Part of Fourth Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test8 [Passed]
StartGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test9

Part of Fourth Execution Group
EndGroup: WEX.Examples.CSharpExecutionDependentGroupsExample.Test9 [Passed]

Failed Tests:
    WEX.Examples.CSharpExecutionDependentGroupsExample.Test4
    WEX.Examples.CSharpExecutionDependentGroupsExample.Test6

Summary: Total=9, Passed=6, Failed=2, Blocked=1, Not Run=0, Skipped=0
```

テストの実行順序が想定どおりのことに注意してください。

 

 





