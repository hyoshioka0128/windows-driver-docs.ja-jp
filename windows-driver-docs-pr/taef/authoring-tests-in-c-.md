---
title: C# でテストを作成する
description: C# でテストを作成する
ms.assetid: 4DD1D673-FEAF-44a4-8BAD-0E55318DC64B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb66992ef2f12ed5e6f9993827bc33e5edb76dbd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361802"
---
# <a name="authoring-tests-in-c"></a>C# でテストを作成する


次の例に、 C# .cs ファイル 1 つの単純なテスト クラスを使用してその demostratesC#テスト マークアップ。 (なお、この例は demonstrational 目的にのみ、コンパイルまたは実行できないようにします。)

```cpp
1    using Microsoft.VisualStudio.TestTools.UnitTesting;
2    using System;
3    using System.Collections;
4    using WEX.Logging.Interop;
5    using WEX.TestExecution;
6
7    [TestClass]
8    public class ManagedStartMenuTests
9    {
10       [AssemblyInitialize]
11       [TestProperty("Component", "Navigation")]
12       [TestProperty("SubComponent", "StartMenu")]
13       public static void RunModuleSetup(Object context)
14       {
15           defaultPolicy = SetObjectFactoryPolicy(PolicyClassic);
16       }
17
18       [AssemblyCleanup]
19       public static void RunModuleCleanup()
20       {
21           SetObjectFactoryPolicy(defaultPolicy);
22       }
23
24       [ClassInitialize]
25       [TestProperty("TeamOwner", "WEX")]
26       [TestProperty("GroupOwner", "MediaPlayerTest")]
27       public static void TestClassSetup(Object testContext)
28       {
29           objectFactory = new ObjectFactory();
30       }
31
32       [ClassCleanup]
33       public static void TestClassCleanup()
34       {
35           objectFactory.Dispose();
36       }
37
38       [TestInitialize]
39       public void TestMethodSetup()
40       {
41           startMenuObject = objectFactory.CreateObject();
42       }
43
44       [TestCleanup]
45       public void TestMethodCleanup()
46       {
47           startMenuObject.Dispose();
48       }
49
50
51       [TestMethod]
52       [Owner("Someone")]
53       [Priority(0)]
54       public void TestMethod1()
55       {
56           Verify.AreEqual(startMenuObject.size, expectedObjectSize);
57       }
58   }
```

C を宣言するため\#テスト、TAEF は VSTS のテスト マークアップ。

テスト クラスを宣言するC#を使用する\[TestClass\] 、通常の属性C#(7 行目) のクラスし、テスト メソッドの宣言を使用して\[TestMethod\]通常のクラスのメソッド (行 51 属性).

C#テストのマークアップには、セットアップおよび後処理用のメソッドの完全な範囲もサポートしています。

静的メソッドを\[AssemblyInitialize\]属性セットが他のクラスのメソッドの前に実行され、アセンブリ レベルの初期化 (行 10) を実行します。 そのため、アセンブリ クリーンアップ メソッド、静的メソッドがある\[AssemblyCleanup\]属性が他のすべてのメソッド (18 行) の完了後に実行される設定。

同様に、存在するクラスとテストのセットアップおよび後処理用のメソッド。 (24、32、38、44 の行を参照してください)異なり、C++ では、マネージ コードでクラスのセットアップおよび後処理用のメソッドを静的あります。

TAEFC#テスト マークアップは、テスト、クラス、およびモジュールのプロパティをサポートしています。

モジュールのプロパティを設定するには、アセンブリの初期化子で属性を設定 (11 と 12 行を参照してください)。 クラス レベルのプロパティを設定して、クラス初期化子のプロパティと同様に (25 および 26 行を参照してください)。 テスト メソッド レベル プロパティの特定のテスト メソッドにプロパティが適用だけです。 (52 ~ 53 行目を参照してください)

## <a name="span-idrunningundervstsspanspan-idrunningundervstsspanspan-idrunningundervstsspanrunning-under-vsts"></a><span id="Running_under_VSTS"></span><span id="running_under_vsts"></span><span id="RUNNING_UNDER_VSTS"></span>VSTS で実行されています。


注: VSTS バイナリへの依存関係を減らすためには、現在クラスとアセンブリのセットアップ メソッド オブジェクトをパラメーターとして受け取る最初。

VSTS からテストを実行したい場合にそのオブジェクトの種類を変更してください**TestContext**型。 これで依存関係を追加することに留意してください*microsoft.visualstudio.qualitytools.unittestframework.dll*と*microsoft.visualstudio.qualitytools.resource.dll*します。

VSTS で実行されているときに、手順が若干異なります。 非管理対象の依存関係をコピーするローカル テストの実行設定を設定する必要があります。 これを行うに移動します。

-   テスト -&gt;編集は、次のテスト実行の構成-&gt;ローカル テストの実行
-   テストごとにコピーする必要がある dll Deployment.Enter をクリックします。
    -   Wex.Logger.dll
    -   Wex.Common.dll
    -   Wex.Common.Managed.dll
    -   Wex.Communication.dll
    -   Wex.Logger.Interop.dll

これは、機能は、原因という事実に VSTS が新しいディレクトリに行い経由でファイルをコピーするが、テスト_ケースを実行するたびに必要です。 コンピューターにこれらのディレクトリをプロジェクト フォルダーに兄弟フォルダーとして参照できます。

## <a name="span-idrunningmanagedtestsinthedefaultapplicationdomainspanspan-idrunningmanagedtestsinthedefaultapplicationdomainspanspan-idrunningmanagedtestsinthedefaultapplicationdomainspanrunning-managed-tests-in-the-default-application-domain"></a><span id="Running_managed_tests_in_the_default_application_domain"></span><span id="running_managed_tests_in_the_default_application_domain"></span><span id="RUNNING_MANAGED_TESTS_IN_THE_DEFAULT_APPLICATION_DOMAIN"></span>既定のアプリケーション ドメインで実行されている管理対象のテスト


既定では、テスト コードの分離、TAEF には、特別なテストのアプリケーション ドメインで、管理対象のテストが実行されます。 ただし、既定以外のアプリケーション ドメインを使用する場合で、ネイティブ コードがマネージ コード (例: ネイティブのコールバック関数がマネージ コードで使用) を呼び出すシナリオ エラーになるメッセージ。「渡すことはできません、GCHandle の Appdomain で」。 これらのシナリオでは、強制を使用して、既定のアプリケーション ドメインで実行する管理対象のテスト、 [/defaultAppDomain](te-exe-command-line-parameters.md#defaultappdomain)スイッチします。

管理対象の実行に注意してください。 既定のアプリケーション ドメイン内のテストがと互換性がない[アセンブリ Config ファイル](assembly-config-files.md)します。

## <a name="span-idsupportforasynctestmethodsspanspan-idsupportforasynctestmethodsspanspan-idsupportforasynctestmethodsspansupport-for-async-test-methods"></a><span id="Support_for_async_test_methods"></span><span id="support_for_async_test_methods"></span><span id="SUPPORT_FOR_ASYNC_TEST_METHODS"></span>テスト メソッドの非同期のサポート


TAEF の NetFX 4.5 のバイナリは、async TAEF テスト メソッドの実行をサポートします。 つまり、TAEF テストでマークされている、 **async**キーワードは、 **await**非同期操作。

**注**  TAEF の NetFX 2.0 および 3.5 のバイナリを持つこの機能を活用しようとはしないでください。 NetFX 4.5 バイナリのみがこの機能をサポートします。

 

TAEF が非同期の両方をサポートしている**void**と非同期**タスク**テスト メソッドの (両方が同じ機能で発生)。

```CSharp
            [TestMethod]
            public async Task MyAsyncTest()
            {
                await AsyncAPICall1();
                var result = await AsyncAPICall2();
                Verify.IsTrue(result);
            }
```

別の方法として。

```CSharp
            [TestMethod]
            public async void MyAsyncTest2()
            {
                await AsyncAPICall1();
                var result = await AsyncAPICall2();
                Verify.IsTrue(result);
            }
```

 

 





