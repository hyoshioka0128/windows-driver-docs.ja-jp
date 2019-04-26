---
title: TAEF を最大限に活用する
description: TAEF を最大限に活用する
ms.assetid: DCB06C5A-DF2C-4e1c-A297-C9AA5496D162
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bd97d7aca5a8888e413b1e5f0bab13f0c2d6db8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355514"
---
# <a name="making-the-most-of-taef"></a>TAEF を最大限に活用する


テストの作成と実行フレームワークは、作成して、テストを実行する強力なプラットフォームを提供します。 バック グラウンドで TAEF の詳細を最大限に活用するために機能しているいくつかを理解する価値がある場合があります。 このページでは、いくつかのヒントとする際に役立つ機能を最適化しで提供する TAEF を最大限に活用するためのテストを作成します。 作成と TAEF とテストの実行の基本を理解していることを確認してください。

## <a name="span-idset-uporinitializeandclean-upmethodsspanspan-idset-uporinitializeandclean-upmethodsspanspan-idset-uporinitializeandclean-upmethodsspanset-up-or-initialize-and-clean-up-methods"></a><span id="Set-up__or_Initialize__and_Clean-up_Methods"></span><span id="set-up__or_initialize__and_clean-up_methods"></span><span id="SET-UP__OR_INITIALIZE__AND_CLEAN-UP_METHODS"></span>設定 (または Initialize) とクリーンアップ メソッド


アセンブリ レベルでセットアップおよび後処理用のメソッド (とも呼ばれます*フィクスチャ*)、DLL の実行ごとに 1 回実行を取得します。 同様に、クラスがセットアップをレベルし、クリーンアップ メソッドは、クラスあたり 1 回実行を取得します。 テスト レベル セットアップおよび後処理用のメソッドは、同じクラス内のすべてのテストとクラスのすべてのテストの前後に 1 回呼び出されます。

ある可能性がありますのみ 1 つのアセンブリ レベルのセットアップとアセンブリごとにクリーンアップのメソッド、クラス レベルの設定が 1 つと、クラスごとにクリーンアップ メソッドおよびクラスごとに 1 つのテストのセットアップとクリーンアップ メソッド。 クラスのセットアップおよび後処理用のメソッドはマネージ コードで静的は C++ コードで静的でないことに注意してください。

例外が有効になっている場合 (既定では、)、任意のメソッドの実行に終了しましたが失敗した最初の検証呼び出し。 例外ベースの検証呼び出しを明示的に無効するかどうか (詳細についてはテストの作成で確認セクション参照)、検証の呼び出しが失敗した後、制御フローを制御する条件付きステートメントの明示的なを指定する必要があります。

セットアップの方法で、障害が発生した場所の場合 (ベースの例外を使用して、エラーを確認します。 いずれかまたはセットアップでエラーを明示的に返します)、に従うしたテストの"ブロック"と見なされますとようログに記録します。 など、クラス レベルのセットアップ メソッドが失敗した場合、クラス内のすべてのテスト メソッドは「ブロック」と見なされ、それぞれが記録されますようです。 さらにでそのセットアップの方法で、障害が発生した場合は、クリーンアップ メソッドを呼び出すはありません。

## <a name="span-idtestmethodspanspan-idtestmethodspanspan-idtestmethodspantest-method"></a><span id="Test_Method"></span><span id="test_method"></span><span id="TEST_METHOD"></span>テスト メソッド


テスト結果を明示的にログインする必要はありません。 テストでのすべての検証呼び出しが成功した場合、テストが「合格」として記録されます。 失敗した最初の検証呼び出し、テスト メソッドの実行が終了 (例外ベースの検証の呼び出しを明示的に無効にした - この場合、条件付きステートメント、制御フローが後に関係なく、によって以下が決まります保持している場合)、テストは、"Failed"とマークされます。

同様に、検証がある場合 (戻り値の型と成功の判断基準に依存) ヘルパー メソッドの呼び出しラッパーは、明示的に確認し、その結果をログする必要はありません。

## <a name="span-idspecifyingmetadataspanspan-idspecifyingmetadataspanspan-idspecifyingmetadataspanspecifying-metadata"></a><span id="Specifying_Metadata"></span><span id="specifying_metadata"></span><span id="SPECIFYING_METADATA"></span>メタデータを指定します。


メタデータの参照が階層です。 かどうか、select ステートメントは、つまり**選択/:"@Priority= 2"** TAEF をそれを含んでいるクラスの検索は、TestMethod が優先度を指定しない場合。 クラス レベルのメタデータでは指定がない場合、TAEF はアセンブリ レベルでを検索します。

したがって、同じ"Priority"または"の所有者は、入手できますをクラス レベルでのみ指定することたとえば、クラスで、ほとんどすべてのテストをする場合です。 このルールの例外である 1 つまたはいくつかのテストでは、"TestMethod"レベルでメタデータを明示的に指定することができます。 詳細については、次のテストを参照してください。

```cpp
1    namespace WEX { namespace UnitTests { namespace Samples
2    {
3        //
4        // Declare module level properties
5        //
6        BEGIN_MODULE() //This metadata applies to all the classes and tests in this module or assembly
7            MODULE_PROPERTY(L"GroupOwner", L"SomeGroup")
8        END_MODULE()
9        class PremiumBankAccountTests
10       {
11           //
12           // Declare this class to be a test class with an'advanced' declaration
13           // Use advanced declaration when you want to set metadata on the class
14           //
15           BEGIN_TEST_CLASS(PremiumBankAccountTests) //This metadata applies to all the test in this class
16               TEST_CLASS_PROPERTY(L"Priority", L"2")
17               TEST_CLASS_PROPERTY(L"DevOwner", L"Someone")
18               TEST_CLASS_PROPERTY(L"PMOwner", L"Someone")
19           END_TEST_CLASS()
20           //
21           // Declare class setup - a method that runs after class constructor
22           // and before any test class methods and test setup method
23           //
24           TEST_CLASS_SETUP(SetDefaultAccountType);
25           //
26           // Declare class cleanup - a methods that runs after all the class test methods and test setup method
27           // and before the class destructor
28           //
29           TEST_CLASS_CLEANUP(ResetDefaultAccountType);
30           //
31           // Declare test setup and cleanup - methods that run before and after the execution
32           // of every test method correspondingly
33           //
34           TEST_METHOD_SETUP(CreateBankAccount);
35           TEST_METHOD_CLEANUP(DestroyBankAccount);
36           //
37           // Declare test methods with an 'advanced' declaration
38           // Use advanced declaration when you want to set metadata on the methods
39           //
40           BEGIN_TEST_METHOD(DebitTest)
41               TEST_METHOD_PROPERTY(L"BVT", L"TRUE")
42               TEST_METHOD_PROPERTY(L"PERF", L"TRUE")
43               TEST_METHOD_PROPERTY(L"STRESS", L"FALSE")
44               TEST_METHOD_PROPERTY(L"Priority", L"1") //Overrides the Class level Priority value
45           END_TEST_METHOD()
46           BEGIN_TEST_METHOD(CreditTest)
47               TEST_METHOD_PROPERTY(L"BVT", L"TRUE")
48               TEST_METHOD_PROPERTY(L"PERF", L"FALSE")
49               TEST_METHOD_PROPERTY(L"STRESS", L"TRUE")
50               TEST_METHOD_PROPERTY(L"GroupOwner", L"SomeGroupTest") //Overrides the GroupOwner specified at the Module level
51           END_TEST_METHOD()
52   
53           std::unique_ptr<BankAccount> m_spBankAccount;
54           BankAccountType m_defaultType;
55       };
56   } /* namespace Samples */ } /* namespace UnitTests */ } /* namespace WEX */
```

注: 管理対象のテストの作成は同様にで行います。 モジュール レベルはアセンブリ レベルのマークアップと同じでは、管理します。 ***アセンブリ レベルまたはマネージ コードでクラス レベルのメタデータの仕様では、マークアップは、静的初期化子メソッドの前に指定するのには。*** テストがあるまだない場合は、空の初期化子を提供する必要がありますがあります。 この設計は、VSTS の互換性を確保する特別に構成されています。

ベース テーブルのデータ ドリブン テストをこのステップをさらにして上書きが発生した場合、行レベルで指定することにより、レベルのメタデータをテストします。 参照してください[メタデータをオーバーライドするデータ ドリブン テスト例](metadata-overriding-data-driven-test-example.md)詳細についてはします。

 

 





