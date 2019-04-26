---
title: ライトウェイト データ ドリブン テスト
description: ライトウェイト データ ドリブン テスト
ms.assetid: A7070E38-A545-4156-B441-C0E6ACE569F5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de8346e911d3ae47eb06e1b8e987c8b7df7cebcf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355504"
---
# <a name="span-idtaeflight-weightdata-driventestingspanlight-weight-data-driven-testing"></a><span id="taef.light-weight_data-driven_testing"></span>軽量データ ドリブン テスト


完全な XML データ ソースの場所のシナリオである可能性があるし、テーブル ベースのデータ ドリブン テストはテスト シナリオのニーズが重すぎる可能性があります。 テストのデータは単純なとメタデータとして簡単に表現できるときに、データ ドリブン テストのサポートを取得する迅速かつ簡単な方法は、軽量データ ドリブン テストできます。 使用例を確認しましょうか。

軽量のデータ ドリブン テストのデータは、一連のメタデータ (テスト、クラスまたはモジュール レベルで) として表されます。 このセット内の値ごとに、セット内の各値の関連付けられたセットアップと破棄メソッドと共に、問題のテスト メソッドが実行されます。 これをネイティブ コードで作成する方法を見てみましょう。

```cpp
1  #include "WexString.h"
2  #include "WexTestClass.h"
3
4  using namespace WEX::Common;
5  using namespace WEX::TestExecution;
6  using namespace WEX::Logging;

7  namespace WEX { namespace TestExecution { namespace Examples
8  {
9      class SimpleDataDrivenExample
10     {
11         TEST_CLASS(SimpleDataDrivenExample);
12         ...
13         BEGIN_TEST_METHOD(SetsOfDataTest)
14             TEST_METHOD_PROPERTY(L"Data:Color", L"{Purple, Maroon, Brown}")
15         END_TEST_METHOD()
16     };
```

テストのパラメーターの値に注意してください\_メソッド\_14 行目でのプロパティ。 テスト メタデータの値で始まる、"{"で終わると、"}"が既に指定されていること、コンマまたはセミコロン区切り値の一覧を示します。 TAEF は、テスト メソッドは、このセット内の各値に対して 1 回 SetsOfDataTest() 懸念事項を再実行されます。

メタデータの名前が始まることも、"データ:"です。 つまり、エントリのデータ ドリブン テスト パラメーターとで使用できる実際のテスト メソッドよりテーブルからデータのパラメーターはベース データ ドリブン テストと同様に、メタデータのセットはバリエーションが指定本当に次のようにします。

```cpp
11     ...
12
13     void SimpleDataDrivenExample::SetsOfDataTest()
14     {
15         String color;
16         if (SUCCEEDED(TestData::TryGetValue(L"color", color)))
17         {
18             Log::Comment(L"Color retrieved was " + color);
19         }
20     }
21 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

マネージ コードの操作中に、データ セットの取得と仕様はネイティブの例と同様です。 では、始めましょう。

```cpp
1  namespace WEX.Examples
2  {
3      using Microsoft.VisualStudio.TestTools.UnitTesting;
4      using System;
5      using System.Collections;
6      using System.Data;
7      using WEX.Logging.Interop;
8      using WEX.TestExecution;
9
10     [TestClass]
11     public class CSharpDataDrivenSimpleExample
12     {
13         ...
14         [TestMethod]
15         [TestProperty("Data:Color", "{Red, Green, Blue}")]
16         public void SetsOfMetadataTest()
17         {
18             Log.Comment("Color is " + m_testContext.DataRow["Color"]);
19         }
20
21         public TestContext TestContext
22         {
23             get { return m_testContext; }
24             set { m_testContext = value; }
25         }
26
27         private TestContext m_testContext;
28     }
29 }
```

同じようにテーブルの場合ベースのデータ ドリブン テスト メタデータとして指定されたデータのセットが取得できるようにするための TestContext.DataRow 経由。**ことデータ ドリブン テスト ライト ウェイトを保持するには、パラメーターの型を常にする (ネイティブ コード) で WEX::Common::String と文字列 (でマネージ コード) に注意してください。**

**データ値の倍数を指定する場合は、catersian 製品の使用可能なすべての値が取得され、の組み合わせごとに、テスト メソッドが呼び出されます。**

一部のメタデータ セットを含めることは可能ではさらに (など[ThreadingModel メタデータ セット](threading-models.md)) と同じテスト メソッドに指定されたデータ セット。 TAEF により生成されるすべてのメタデータ セットとデータ セットの組み合わせの展開では、このような場合と、すべての組み合わせで問題のテスト メソッドが呼び出されます。

## <a name="span-idmetadataexpansionspanspan-idmetadataexpansionspanspan-idmetadataexpansionspanspecial-cases---data-driven-test-with-a-sets-of-metadata-or-data"></a><span id="metadataExpansion"></span><span id="metadataexpansion"></span><span id="METADATAEXPANSION"></span>特殊なケース - データ ドリブン テストのメタデータやデータのセット


テスト メソッドのベース テーブルに依存するデータ ドリブン テストがある可能性がありのデータまたはメタデータのセットを指定することもします。 など、テスト メソッドにパラメーター「サイズ」と「色」テーブルで指定されたベースのデータ ドリブン テストと false に設定し、および「透過性」パラメーターが true に設定を 1 回実行するすべての行を挿入します。 このような場合は、データ ドリブン テストの「透過性」セット"{true, false}"として指定できました。 **内訳を設定、メタデータ内のパラメーターの競合が発生した場合に注意してください。 テーブルに基づくデータに基づく行、行レベルのパラメーターの型と値の設定値のメタデータはオーバーライドは重要です。**

## <a name="span-idexecutingtestswithsetsofdatametadataspanspan-idexecutingtestswithsetsofdatametadataspanspan-idexecutingtestswithsetsofdatametadataspanexecuting-tests-with-sets-of-data--metadata"></a><span id="Executing_tests_with_Sets_of_data___metadata"></span><span id="executing_tests_with_sets_of_data___metadata"></span><span id="EXECUTING_TESTS_WITH_SETS_OF_DATA___METADATA"></span>データのセットとテストの実行/メタデータ


データのセットを含むテストの実行は非常に直感的なです。 この例のテスト/listproperties 出力を見てみましょう。

``` syntax
1   te Examples\CPP.DataDriven.Example.dll /name:*SetsOfDataTest* /listproperties
2
3   Test Authoring and Execution Framework v2.9.3k for x64
4
5           f:\ Examples\CPP.SimpleDataDriven.Example.dll
6               WEX::TestExecution::Examples::SimpleDataDrivenExample<
7                   WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet0
8                           Property[Data:Color] = {Purple, Maroon, Brown}
9
10                          Data[Color] = Purple
11
12                  WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet1
13                          Property[Data:Color] = {Purple, Maroon, Brown}
14
15                          Data[Color] = Maroon
16
17                  WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet2
18                          Property[Data:Color] = {Purple, Maroon, Brown}
19
20                          Data[Color] = Brown
```

7、12、および上記の例では 17 行に注意してください。 メタデータのセットのインデックスを取得、データ セット内の値を持つテスト メソッドの呼び出しのたびに追加されます。 形式は、このインデックスです。

```cpp
<namespace qualified test method name>#metadataSet<metadataIndex>
```

8、13、および 18 行では、この軽量データ ドリブン テストのサポートが指定されているメタデータのセットを表示します。 この場合、セットは、色紫、茶色および brown で構成されます。 10、15、および 20 行では、テストの現在の呼び出しのアクティブなこのセットから実際の値を表示します。 SetsOfMetadataTest 場合\#metadataSet1、このメソッドは、セットからのアクティブなパラメーター値の 2 番目の呼び出しは「茶色」

データ値を選択またはテーブルにすることも同様の名前ベースのデータ ドリブン テストします。 たとえば SetsOfDataTest を選択することができます\#などの選択クエリによって metadataSet1  **/select:@Data:Color= '茶色'** または **/name:\*\#metadataSet1**

クイック リファレンスは、管理のテストの例から/listproperties 出力は、以下に示します。

``` syntax
te Examples\CSharp.DataDriven.Example.dll /name:*SetsOfMetadataTest* /listproperties

Test Authoring and Execution Framework v2.9.3k for x64

        f:\ Examples\CSharp.DataDrivenSimple.Example.dll
            WEX.Examples.CSharpDataDrivenSimpleExample
                WEX.Examples.CSharpDataDrivenSimpleExample.NonDataDrivenTest
                WEX.Examples.CSharpDataDrivenSimpleExample.SetsOfMetadataTest#metadataSet0
                        Property[Data:Color] = {Red, Green, Blue}

                        Data[Color] = Red

                WEX.Examples.CSharpDataDrivenSimpleExample.SetsOfMetadataTest#metadataSet1
                        Property[Data:Color] = {Red, Green, Blue}

                        Data[Color] = Green

                WEX.Examples.CSharpDataDrivenSimpleExample.SetsOfMetadataTest#metadataSet2
                        Property[Data:Color] = {Red, Green, Blue}

                        Data[Color] = Blue
```

 

 





