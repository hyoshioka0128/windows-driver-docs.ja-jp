---
title: RunFixtureAs
description: TAEF では、対応するテストとは異なるコンテキスト内でのテスト フィクスチャを実行するためのメカニズムを提供します。
ms.assetid: FAFF5265-5268-412E-86A5-149B187B1376
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 098241eb5ad4ed03950eff668265d9db41e9d57b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324737"
---
# <a name="runfixtureas"></a>RunFixtureAs


TAEF は RunFixtureAs を使用して、対応するテスト以外のコンテキストで (モジュール、クラス、およびテスト レベルのセットアップおよびクリーンアップの機能) のテスト フィクスチャを実行します。

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件


-   [Te.Service](te-service.md)をインストールし、管理者特権以外 Te.exe プロセスでは、管理者特権でのテスト フィクスチャを実行するために、またはローカル システムとしてテスト フィクスチャを実行するコンピューター上で実行します。

## <a name="span-idoverviewspanspan-idoverviewspanspan-idoverviewspanoverview"></a><span id="Overview"></span><span id="overview"></span><span id="OVERVIEW"></span>概要


RunFixtureAs は、モジュール、クラス、またはテスト レベルで適用することができ、テスト ツリーに沿って継承されます。 RunFixtureAs ツリーで特定のレベル RunFixtureAs 継承を無効にする機能をサポートするために:\[スコープ\]メタデータもサポートされています。

たとえば、RunFixtureAs モジュールが付いている場合は、= システム、RunFixtureAs:Test としてマークできますクラス (ClassA) = 既定値。 このような場合は、モジュールとクラスのフィクスチャがシステムとして実行されますが ClassA 内でテスト レベル フィクスチャがで実行しなければ Te.exe と同じコンテキストで (がまだテストとは異なるプロセス)。

RunFixtureAs:\[スコープ\]メタデータ値はテスト ツリーの下位に継承されません。 指定したスコープにのみ適用されます。

## <a name="span-iddeterministicguaranteesspanspan-iddeterministicguaranteesspanspan-iddeterministicguaranteesspandeterministic-guarantees"></a><span id="Deterministic_Guarantees"></span><span id="deterministic_guarantees"></span><span id="DETERMINISTIC_GUARANTEES"></span>決定論的保証


-   既定 (RunFixtureAs 値が指定されていない) 場合、テスト フィクスチャ、同じプロセス内で実行する保証されます。
-   フィクスチャには、'Test' 以外の有効な RunFixtureAs 値でマークされていると、フィクスチャをテストとは異なるプロセスで実行されます。 つまり、テストには、RunAs が付いている場合でも管理者特権と RunFixtureAs = = 管理者特権で、テストが昇格されたプロセスで実行され、そのフィクスチャが別の管理者特権でプロセスで実行されます。
-   一致する指定されたスコープのフィクスチャのペアは、(たとえば、クラスのセットアップとクリーンアップ フィクスチャが実行する同じプロセス内で) 同じプロセス内で常に実行されます。

## <a name="span-idrunfixtureastypesspanspan-idrunfixtureastypesspanspan-idrunfixtureastypesspanrunfixtureas-types"></a><span id="RunFixtureAs_Types_"></span><span id="runfixtureas_types_"></span><span id="RUNFIXTUREAS_TYPES_"></span>RunFixtureAs 型


TAEF は、RunFixtureAs はテスト メタデータで指定されている、次の種類をサポートします。

<span id="System"></span><span id="system"></span><span id="SYSTEM"></span>**システム**  
TAEF は、ローカル システムとして、フィクスチャを実行します。

**注**  UI を作成しないでくださいローカル システムとして実行することをテスト フィクスチャ。 場合は、フィクスチャは、作成、UI と対話したりする必要があります、CreateProcessAsUser を使用して、テストから、デスクトップで起動される実行可能ファイルに、UI 関連のコードを移動する必要があります。

 

<span id="Elevated"></span><span id="elevated"></span><span id="ELEVATED"></span>**管理者特権**  
TAEF が確実に必要な場合は、フィクスチャを実行するための管理者特権でのプロセスによって昇格されたプロセスで、フィクスチャを実行します。

**注**  RunFixtureAs でマークされたフィクスチャを実行するには、administrators グループのメンバーである TAEF を実行するユーザー管理者特権でを = です。 これは、管理者以外のユーザーには、昇格する分割トークンはありません。 にあるためにです。

 

<span id="Default"></span><span id="default"></span><span id="DEFAULT"></span>**既定値**  
TAEF は、Te.exe として (ただし、テストとは異なるプロセス内である) は、同じコンテキストで、フィクスチャを実行します。

<span id="Broker"></span><span id="broker"></span><span id="BROKER"></span>**Broker**  
TAEF '没入型ブローカー' プロセスで、フィクスチャを実行します。

**注:**  
-   'ブローカー' は、Windows 8 以降のオペレーティング システムでのみサポートされます。
-   システムでは、テスト署名ポリシーを有効にする必要があります。 詳細については、 [「ブート構成オプションを TESTSIGNING](https://msdn.microsoft.com/library/windows/hardware/ff553484)します。
-   使用してリモートでテストを実行している ' RunFixtureAs ブローカーを =' は現在サポートされていません。
-   実行するときに ' RunFixtureAs ブローカーを =' TAEF では、"TE を使用します。フィクスチャの実行で"TE ProcessHost.Broker.exe"プロセス。ProcessHost.exe"。

 

<span id="UIAccess"></span><span id="uiaccess"></span><span id="UIACCESS"></span>**UIAccess**  
TAEF は、UIAccess 実行レベル マーク アップのプロセスで、フィクスチャを実行します。 UI オートメーション アプリケーションの UIAccess については、次を参照してください。、 [Windows 整合性メカニズム デザイン](https://msdn.microsoft.com/library/bb625963)します。

**注:**  
-   UIAccess は、Vista 以降のオペレーティング システムでのみサポートされます。
-   TAEF バイナリは、コンピューターの Program Files フォルダーの下のフォルダーから実行する必要があります。
-   使用してリモートでテストを実行している ' RunFixtureAs = UIAccess' は現在サポートされていません。
-   実行するときに ' RunFixtureAs = UIAccess' TAEF は"TE を使用します。フィクスチャの実行で"TE ProcessHost.UIAccess.exe"プロセス。ProcessHost.exe"。

 

<span id="Test"></span><span id="test"></span><span id="TEST"></span>**テスト**  
TAEF は、テストとして、同じプロセスまたはコンテキスト内のフィクスチャを実行します。

**注**  RunFixtureAs 設定が指定されていない場合、既定の TAEF 動作になります。

 

## <a name="span-idrunfixtureasscopespanspan-idrunfixtureasscopespanspan-idrunfixtureasscopespanrunfixtureasscope"></a><span id="RunFixtureAs__scope_"></span><span id="runfixtureas__scope_"></span><span id="RUNFIXTUREAS__SCOPE_"></span>RunFixtureAs:\[スコープ\]


TAEF 次 RunFixtureAs をサポートしています:\[スコープ\]、テスト メタデータで指定された値。

<span id="RunFixtureAs_Module__RunFixtureAs_Assembly__or_RunFixtureAs_Dll"></span><span id="runfixtureas_module__runfixtureas_assembly__or_runfixtureas_dll"></span><span id="RUNFIXTUREAS_MODULE__RUNFIXTUREAS_ASSEMBLY__OR_RUNFIXTUREAS_DLL"></span>**RunFixtureAs:Module**、 **RunFixtureAs:Assembly**、または**RunFixtureAs:Dll**  
RunFixtureAs 値は、テスト階層内のモジュール レベルのノードにのみ適用されます。

<span id="RunFixtureAs_Class"></span><span id="runfixtureas_class"></span><span id="RUNFIXTUREAS_CLASS"></span>**RunFixtureAs:Class**  
RunFixtureAs 値は、テスト階層のクラス レベルのノードにのみ適用されます。

<span id="RunFixtureAs_Method_or_RunFixtureAs_Test"></span><span id="runfixtureas_method_or_runfixtureas_test"></span><span id="RUNFIXTUREAS_METHOD_OR_RUNFIXTUREAS_TEST"></span>**RunFixtureAs:Method**または**RunFixtureAs:Test**  
RunFixtureAs 値は、テストの階層構造のテスト レベルのノードにのみ適用されます。

## <a name="span-idmarkingtestswithrunfixtureasspanspan-idmarkingtestswithrunfixtureasspanspan-idmarkingtestswithrunfixtureasspanmarking-tests-with-runfixtureas"></a><span id="Marking_Tests_with_RunFixtureAs"></span><span id="marking_tests_with_runfixtureas"></span><span id="MARKING_TESTS_WITH_RUNFIXTUREAS"></span>RunFixtureAs でテストをマークします。


```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    TEST_CLASS(MyTests);

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   MyTestSetup と MyTestCleanup で管理者特権で実行します。
-   MyClassSetup と MyClassCleanup (MyTestMethod と同じプロセス) 内のシステムとして実行
-   MyModuleSetup と MyModuleCleanup (MyTestMethod と同じプロセス) 内のシステムとして実行

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   MyTestSetup と MyTestCleanup で管理者特権で実行します。
-   MyClassSetup と MyClassCleanup で管理者特権で実行します。
-   MyModuleSetup と MyModuleCleanup (MyTestMethod と同じプロセス) 内のシステムとして実行

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"System")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   制限付きとして MyTestMethod が実行されます。
-   MyTestSetup と MyTestCleanup で管理者特権で実行します。
-   MyClassSetup と MyClassCleanup システムとして実行します。
-   MyModuleSetup と MyModuleCleanup (MyTestMethod と同じプロセス) 内で制限付きとして実行

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"System")
        TEST_METHOD_PROPERTY(L"RunFixtureAs:Test", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   制限付きとして MyTestMethod2 が実行されます。
-   MyTestSetup と MyTestCleanup; 管理者特権で実行します。MyTests クラス内のすべてのテスト メソッドに適用される RunFixtureAs:Test スコープ
-   MyClassSetup と MyClassCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行
-   MyModuleSetup と MyModuleCleanup が、それぞれのコンテキスト内でのテスト (MyTestMethod のシステム) および MyTestMethod2 の制限付きのプロセスを実行します。

```ManagedCPlusPlus
MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"System")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   制限付きとして MyTestMethod2 が実行されます。
-   MyTestSetup と MyTestCleanup MyTestMethod のシステムと MyTestMethod2 の管理者特権でを実行します。
-   MyClassSetup と MyClassCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行
-   MyModuleSetup と MyModuleCleanup が、それぞれのコンテキスト内でのテスト (MyTestMethod のシステム) および MyTestMethod2 の制限付きのプロセスを実行します。

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Default")
        TEST_CLASS_PROPERTY(L"RunFixtureAs:Test", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   制限付きとして MyTestMethod2 が実行されます。
-   MyTestSetup と MyTestCleanup MyTestMethod と MyTestMethod2 の両方の管理者特権で実行
-   MyClassSetup と MyClassCleanup 既定として実行 (Te.exe と同じコンテキスト内で現在実行している、まだ MyTestMethod と MyTestMethod2 とは異なるプロセス内で)
-   MyModuleSetup と MyModuleCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
    MODULE_PROPERTY(L"RunFixtureAs:Test", L"Test")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   制限付きとして MyTestMethod2 が実行されます。
-   MyTestSetup と MyTestCleanup MyTestMethod と MyTestMethod2 と同じプロセス内で実行
-   MyClassSetup と MyClassCleanup で管理者特権で実行します。
-   MyModuleSetup と MyModuleCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
    MODULE_PROPERTY(L"RunFixtureAs:Test", L"Test")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
        TEST_METHOD_PROPERTY(L"RunFixtureAs", L"Elevated")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

前の例は、次のようにテストとフィクスチャ実行されます。

-   MyTestMethod は System として実行します。
-   制限付きとして MyTestMethod2 が実行されます。
-   MyTestSetup と MyTestCleanup MyTestMethod2 MyTestMethod として、昇格されたプロセスでは、同じプロセス内で実行
-   MyClassSetup と MyClassCleanup で管理者特権で実行します。
-   MyModuleSetup と MyModuleCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行

```ManagedCPlusPlus
BEGIN_MODULE()
    MODULE_PROPERTY(L"RunFixtureAs", L"System")
END_MODULE()

MODULE_SETUP(MyModuleSetup);
MODULE_CLEANUP(MyModuleCleanup);

class MyTests
{
    BEGIN_TEST_CLASS(MyTests)
        TEST_CLASS_PROPERTY(L"RunFixtureAs:Class", L"Elevated")
    END_TEST_CLASS()

    BEGIN_TEST_METHOD(MyTestMethod)
        TEST_METHOD_PROPERTY(L"RunAs", L"System")
    END_TEST_METHOD()

    BEGIN_TEST_METHOD(MyTestMethod2)
        TEST_METHOD_PROPERTY(L"RunAs", L"Restricted")
    END_TEST_METHOD()

    TEST_METHOD_SETUP(MyTestSetup);
    TEST_METHOD_CLEANUP(MyTestCleanup);

    TEST_CLASS_SETUP(MyClassSetup);
    TEST_CLASS_CLEANUP(MyClassCleanup);
};
```

上記の例では、テストとフィクスチャを次のように実行するは。

-   MyTestMethod は System として実行します。
-   制限付きとして MyTestMethod2 が実行されます。
-   MyTestSetup と MyTestCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行
-   MyClassSetup と MyClassCleanup で管理者特権で実行します。
-   MyModuleSetup と MyModuleCleanup (MyTestMethod とは異なるプロセス) 内のシステムとして実行

 

 





