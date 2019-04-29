---
title: データ ドリブン クラス
description: データ ドリブン クラス
ms.assetid: 2998D5BB-A873-4df9-86B2-88937736862F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cee3b8cc16d499907771381a5a00d44a003640c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385067"
---
# <a name="span-idtaefdata-drivenclassspandata-driven-class"></a><span id="taef.data-driven_class"></span>データ ドリブン クラス


TAEF の基本的な実行に精通し、このセクションに進む前にそれを使用してテストを作成する方法を理解することを確認してください。 単純なデータ ドリブン テストの例のチュートリアルを経由する可能性があります。 このセクションではデータ ドリブン テスト クラスに基づいていることは、*ベース テーブル*に適用されますが、同じ方法で、データ ドリブン テストでは、 *WMI ベース*または*ベース PICT*データ ドリブン テストします。

## <a name="span-idwhentouseddcspanspan-idwhentouseddcspanwhen-to-use-a-data-driven-class"></a><span id="whentouse_ddc"></span><span id="WHENTOUSE_DDC"></span>データ ドリブンのクラスを使用する場合ですか。


同じ入力データに複数のテストが依存場合もあります。 Api をテストするときに、API の動作の一貫性のあるビューを取得するために、同じデータで複数の API テストを実行したい場合があります。 シナリオ レベルのテストを実行するときに、同じデータの実際のシナリオでの手順をすべてテストされていることを確認したい場合があります。 これらの時間には、クラス レベルでのテスト データを指定すると便利です。

## <a name="span-idauthoringddcspanspan-idauthoringddcspanauthoring-data-driven-class"></a><span id="authoring_ddc"></span><span id="AUTHORING_DDC"></span>データ ドリブンのクラスを作成します。


特定のクラスは、データ ドリブンの特定のテストがデータ ドリブンであるを指定する方法と同様の方法では指定します。 適用する、 **DataSource**クラス レベルでのメタデータ。 値は、関心のある特定のデータ ソースを識別します。 次の例では、クラスのデータに基づくこれらのプロパティを指定する方法を示します。

### <a name="span-idnative1authoringspanspan-idnative1authoringspannative-code"></a><span id="native1_authoring"></span><span id="NATIVE1_AUTHORING"></span>ネイティブ コード

```cpp
1     class 2     {
2         BEGIN_TEST_CLASS(DataDrivenClassExample)
3             TEST_CLASS_PROPERTY(L"DataSource", L"Table:DataDrivenClassExample.xml#ClassTable")
4         END_TEST_CLASS()
5
6         TEST_METHOD(Test1);
7       {
8         int size;
9           if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"size", size)</span>))
10          {
11              VERIFY_ARE_NOT_EQUAL(size, 0);
12              Log::Comment(String().Format(L"Size retrieved was %d", size));
13          }
14  
15          String color;
16          if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"color", color)</span>))
17          {
18              Log::Comment(L"Color retrieved was " + color);
19          }
20      }
21         TEST_METHOD(Test2);
22      {
23          int size;
24          if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"size", size)</span>))
25          {
26              VERIFY_ARE_NOT_EQUAL(size, 0);
27              Log::Comment(String().Format(L"Size retrieved was %d", size));
28          }
29  
30          String color;
31          if (SUCCEEDED(<span class="style2">TestData::TryGetValue(L"color", color)</span>))
32          {
33              Log::Comment(L"Color retrieved was " + color);
34          }
35      } 
36    };
```

### <a name="span-idmanaged1authoringspanspan-idmanaged1authoringspanmanaged-code"></a><span id="managed1_authoring"></span><span id="MANAGED1_AUTHORING"></span>マネージ コード

```cpp
1     [TestClass]
2     public class CSharpDataDrivenClassExample
3     {
4         [ClassInitialize]
5         [DataSource("Table:CSharpDataDrivenClassExample.xml#ClassTable")]
6         public static void MyClassInitialize(Object testContext)
7         {
8         }
9
10        [TestMethod]
11        public void Test1()
12        {
13            int size = (int)m_testContext.DataRow["Size"];
14            Verify.AreNotEqual(size, 0);
15            Log.Comment("Size is " + size.ToString());
16
18            Log.Comment("Color is " + m_testContext.DataRow["Color"]);
19        }
20
21        [TestMethod]
22        public void Test2()
23        {
24            int size = (int)m_testContext.DataRow["Size"];
25            Verify.AreNotEqual(size, 0);
26            Log.Comment("Size is " + size.ToString());
27
28            Log.Comment("Color is " + m_testContext.DataRow["Color"]);
29        }
30
31        public TestContext TestContext
32        {
33            get { return m_testContext; }
34            set { m_testContext = value; }
35        }
36
37        private TestContext m_testContext;
38    }
```

これらの例では、行 3 に、**ネイティブ コード**例と 5 行目に、**マネージ コード**の例は TAEF でデータ ドリブン テスト クラスのデータ ソースを指定することをお勧めの方法です。

**マネージ コード**上記の例、13、18、24、および 28 行がデータにマネージ コード用のテスト メソッドを使用可能な配布する方法を表示します。

次のコード例では、4、11、20、および 27 行は、データにネイティブ コード用のテスト メソッドを使用可能な配布する方法を説明します。 注意***ようにまったく同じ方法でデータ ドリブン テストのクラス (Test1、Test2) でテスト メソッドを使用可能なデータに基づくクラス テーブル (行) で定義されているデータを表示します。***

### <span id="native2_authoring"></span><span id="NATIVE2_AUTHORING"></span>

構築する、 **DataSource**でデータ ドリブン テストの場合とまったく同じデータに基づくクラスの XML ファイル。 次の例では、ネイティブおよびマネージ クラスの XML ファイルを表示します。

### <a name="span-idnative3authoringspanspan-idnative3authoringspannative"></a><span id="native3_authoring"></span><span id="NATIVE3_AUTHORING"></span>ネイティブ

```cpp
1 <?xml version="1.0"?>
2 <Data>
3   <Table Id="ClassTable">
4     <ParameterTypes>
5       <ParameterType Name="Size">int</ParameterType>
6     </ParameterTypes>
7     <Row>
8       <Parameter Name="Size">4</Parameter>
9       <Parameter Name="Color">White</Parameter>
10    </Row>
11    <Row>
12      <Parameter Name="Size">10</Parameter>
13      <Parameter Name="Color">Black</Parameter>
14    </Row>
15    <Row>
16      <Parameter Name="Size">9</Parameter>
17      <Parameter Name="Color">Orange</Parameter>
18    </Row>
19    <Row>
20      <Parameter Name="Size">9</Parameter>
21      <Parameter Name="Color">Blue</Parameter>
22    </Row>
23  </Table>
24</Data>
```

### <a name="span-idmanged2authoringspanspan-idmanged2authoringspanmanaged"></a><span id="manged2_authoring"></span><span id="MANGED2_AUTHORING"></span>管理されています。

```cpp
1 <?xml version="1.0"?>
2 <Data>
3   <Table Id="ClassTable">
4     <ParameterTypes>
5       <ParameterType Name="Size">Int32</ParameterType>
6       <ParameterType Name="Color">String</ParameterType>
7     </ParameterTypes>
8     <Row>
9      <Parameter Name="Size">4</Parameter>
10      <Parameter Name="Color">White</Parameter>
11    </Row>
12    <Row>
13      <Parameter Name="Size">10</Parameter>
14      <Parameter Name="Color">Black</Parameter>
15    </Row>
16    <Row>
17      <Parameter Name="Size">9</Parameter>
18      <Parameter Name="Color">Orange</Parameter>
19    </Row>
20    <Row>
21      <Parameter Name="Size">9</Parameter>
22      <Parameter Name="Color">Blue</Parameter>
23    </Row>
24  </Table>
25</Data>
```

## <a name="span-idbehindsceneddcspanspan-idbehindsceneddcspanbehind-the-scenes-or-what-to-expect"></a><span id="behindscene_ddc"></span><span id="BEHINDSCENE_DDC"></span>バック グラウンドまたは注意点でしょうか。 の背後にあります。


既定では、TAEF でのテストを作成するときに実行順序、クラス内では、クラスでテスト メソッドをコーディングした順序と同じです。 前の例ではそのため、 **Test1**常に実行する前に**Test2**します。 クラスを格納しているため、 **Test1**と**Test2**メソッドは、各データで定義されている行の 1 回実行されますクラスのすべてのデータ ドリブン クラスで**DataSource**します。 つまり、 **Test1**と**Test2**行に対して実行\#0。 行の順序でこれらのメソッドを実行し、 \#TAEF がすべての行が実行されるまでこれには 1 です。

## <a name="span-idexecutingddcspanspan-idexecutingddcspanexecuting-tests-in-a-data-driven-class"></a><span id="executing_ddc"></span><span id="EXECUTING_DDC"></span>データ ドリブンのクラスでテストの実行


使用例のテスト バイナリを実行する場合、 **/list**コマンド オプションでは、前のセクションの実行順序が明らかになります。

### <a name="span-idnative1executingspanspan-idnative1executingspannative"></a><span id="native1_executing"></span><span id="NATIVE1_EXECUTING"></span>ネイティブ

``` syntax
TE.exe Examples\CPP.AdvancedDataDriven.Examples.dll /name:*class* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CPP.AdvancedDataDriven.Examples.dll
            WEX::TestExecution::Examples::DataDrivenClassExample#0
                WEX::TestExecution::Examples::DataDrivenClassExample#0::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#0::Test2
            WEX::TestExecution::Examples::DataDrivenClassExample#1
                WEX::TestExecution::Examples::DataDrivenClassExample#1::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#1::Test2
            WEX::TestExecution::Examples::DataDrivenClassExample#2
                WEX::TestExecution::Examples::DataDrivenClassExample#2::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#2::Test2
            WEX::TestExecution::Examples::DataDrivenClassExample#3
                WEX::TestExecution::Examples::DataDrivenClassExample#3::Test1
                WEX::TestExecution::Examples::DataDrivenClassExample#3::Test2
```

### <a name="span-idmanaged1executingspanspan-idmanaged1executingspanmanaged"></a><span id="managed1_executing"></span><span id="MANAGED1_EXECUTING"></span>管理されています。

``` syntax
TE.exe Examples\CSharp.AdvancedDataDriven.Examples.dll /name:*class* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CSharp.AdvancedDataDriven.Examples.dll
            WEX.Examples.CSharpDataDrivenClassExample#0
                WEX.Examples.CSharpDataDrivenClassExample#0.Test1
                WEX.Examples.CSharpDataDrivenClassExample#0.Test2
            WEX.Examples.CSharpDataDrivenClassExample#1
                WEX.Examples.CSharpDataDrivenClassExample#1.Test1
                WEX.Examples.CSharpDataDrivenClassExample#1.Test2
            WEX.Examples.CSharpDataDrivenClassExample#2
                WEX.Examples.CSharpDataDrivenClassExample#2.Test1
                WEX.Examples.CSharpDataDrivenClassExample#2.Test2
            WEX.Examples.CSharpDataDrivenClassExample#3
                WEX.Examples.CSharpDataDrivenClassExample#3.Test1
                WEX.Examples.CSharpDataDrivenClassExample#3.Test2
```

上記の例でインデックスがデータ ドリブン テストのようなことに注意してください。 データ ドリブン クラス内の各行は、インデックスによって識別されます。 データ ドリブン テストでは、ように**わかりやすい短い形式の任意の行を提供することもできます*名前*を XML ファイルで、行レベルでメタデータを指定し、一覧表示または実行時にインデックスではなく、その名前を印刷テストします。**

同様に、使用、 **/listproperties**データが実際に指定し、使用可能なクラス レベルのことを確認するにはオプションです。

### <a name="span-idnative2executingspanspan-idnative2executingspannative"></a><span id="native2_executing"></span><span id="NATIVE2_EXECUTING"></span>ネイティブ

``` syntax
F:\ Examples\CPP.AdvancedDataDriven.Examples.dll
    WEX::TestExecution::Examples::DataDrivenClassExample#0
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = White
            Data[Size] = 4
        WEX::TestExecution::Examples::DataDrivenClassExample#0::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#0::Test2

    WEX::TestExecution::Examples::DataDrivenClassExample#1
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = Black
            Data[Size] = 10
        WEX::TestExecution::Examples::DataDrivenClassExample#1::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#1::Test2

    WEX::TestExecution::Examples::DataDrivenClassExample#2
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = Orange
            Data[Size] = 9
        WEX::TestExecution::Examples::DataDrivenClassExample#2::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#2::Test2

    WEX::TestExecution::Examples::DataDrivenClassExample#3
            Property[DataSource] =  Table:DataDrivenClassExample.xml#ClassTable

            Data[Color] = Blue
            Data[Size] = 9
        WEX::TestExecution::Examples::DataDrivenClassExample#3::Test1
        WEX::TestExecution::Examples::DataDrivenClassExample#3::Test2
```

### <a name="span-idmanaged2executingspanspan-idmanaged2executingspanmanaged"></a><span id="managed2_executing"></span><span id="MANAGED2_EXECUTING"></span>管理されています。

``` syntax
F:\ Examples\CSharp.AdvancedDataDriven.Examples.dll
    WEX.Examples.CSharpDataDrivenClassExample#0
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = White
            Data[Size] = 4
        WEX.Examples.CSharpDataDrivenClassExample#0.Test1
        WEX.Examples.CSharpDataDrivenClassExample#0.Test2

    WEX.Examples.CSharpDataDrivenClassExample#1
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = Black
            Data[Size] = 10
        WEX.Examples.CSharpDataDrivenClassExample#1.Test1
        WEX.Examples.CSharpDataDrivenClassExample#1.Test2

    WEX.Examples.CSharpDataDrivenClassExample#2
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = Orange
            Data[Size] = 9
        WEX.Examples.CSharpDataDrivenClassExample#2.Test1
        WEX.Examples.CSharpDataDrivenClassExample#2.Test2

    WEX.Examples.CSharpDataDrivenClassExample#3
            Setup: MyClassInitialize
            Property[DataSource] =  Table:CSharpDataDrivenClassExample.xml#ClassTable

            Data[Color] = Blue
            Data[Size] = 9
        WEX.Examples.CSharpDataDrivenClassExample#3.Test1
        WEX.Examples.CSharpDataDrivenClassExample#3.Test2
```

データ ドリブン クラスには、すべての実行のルールを適用できます。 表示できるもので、選択クエリを作成できます、 **/listproperties**オプション。

## <a name="span-idddtestsddcspanspan-idddtestsddcspandata-driven-tests-in-a-data-driven-class"></a><span id="ddtests_ddc"></span><span id="DDTESTS_DDC"></span>データ ドリブンのクラスでデータ ドリブン テスト


データ ドリブンのクラス内でデータ ドリブン テストを持つ任意の方法に限りません。 API のテストを記述する場合、この方法は役に立ちます。 クラスですべてのテストの一般的なデータを維持するには、クラス レベルで**DataSource**します。 テスト メソッドで特定のデータを指定する、 **DataSource**データ ドリブンをマークするメソッドのメタデータ。

注: このような場合は、実行順序はやや複雑です。

次の例で、前の 2 つの例のバイナリのレンダリング、 */list*コマンド オプション。

### <a name="span-idnative1ddtestsspanspan-idnative1ddtestsspannative"></a><span id="native1_ddtests"></span><span id="NATIVE1_DDTESTS"></span>ネイティブ

``` syntax
TE.exe Examples\CPP.AdvancedDataDriven.Examples.dll /name:*nested* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CPP.AdvancedDataDriven.Examples.dll
            WEX::TestExecution::Examples::NestedDataDrivenExample#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#0::Test2#3
            WEX::TestExecution::Examples::NestedDataDrivenExample#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#1::Test2#3
            WEX::TestExecution::Examples::NestedDataDrivenExample#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#2::Test2#3
            WEX::TestExecution::Examples::NestedDataDrivenExample#3
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test1
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#0
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#1
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#2
                WEX::TestExecution::Examples::NestedDataDrivenExample#3::Test2#3
```

### <a name="span-idmanaged1ddtestsspanspan-idmanaged1ddtestsspanmanaged"></a><span id="managed1_ddtests"></span><span id="MANAGED1_DDTESTS"></span>管理されています。

``` syntax
TE.exe Examples\CSharp.AdvancedDataDriven.Examples.dll /name:*nested* /list
Test Authoring and Execution Framework v2.9.3k for x86

        F:\ Examples\CSharp.AdvancedDataDriven.Examples.dll
            WEX.Examples.CSharpDataDrivenNestedExample#0
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#0.Test2#3
            WEX.Examples.CSharpDataDrivenNestedExample#1
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#1.Test2#3
            WEX.Examples.CSharpDataDrivenNestedExample#2
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#2.Test2#3
            WEX.Examples.CSharpDataDrivenNestedExample#3
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test1
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#0
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#1
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#2
                WEX.Examples.CSharpDataDrivenNestedExample#3.Test2#3
```

**注:** 唯一の制限はここで 2 つの例については、テーブルが同じにすることはできません、 **DataSource ファイル**します。 つまり、 **DataSource**データに基づくクラスとデータ ドリブン テスト メソッドを別にする必要がありますが含まれています。

そのメソッドに注目してください**Test2**の例では、データ ドリブン クラス内でデータ ドリブン テストします。 行にはたとえば、**かかえるします。Examples.CSharpDataDrivenNestedExample\#3.Test2\#0**、  **\#3** 、クラスのインデックスと **\#0**インデックスそのクラス内でデータ ドリブン テストします。 **Test2**両方のテーブルにアクセスできます: クラスのインスタンスの行のデータの所属先の独自の現在の行データと**DataSource**テーブル。 つまり、**が一緒に集計され、テスト メソッドの実行中に利用クラス レベルのデータとテスト メソッドのレベルのデータ。**

クラス レベルとメソッド レベルの両方で同じデータ名が指定されている場合の競合するデータは、の場合はどうなりますか。 TAEF は、メタデータのプロパティを処理するのと同様に、この条件を処理します。 **メソッド レベルでの行で指定されているデータは、クラス レベルでの行で指定されているデータを上書きします。**

たとえば、という名前のパラメーターがある場合を考えます**サイズ**レベルおよびテスト方法レベルは、クラスの両方を指定します。 クラス レベルでは、**サイズ**に定義されますが*文字列配列*型が、あるテスト メソッド レベルでは、定義が、 *int*します。ここで、 *int*上書きを入力、*文字列配列*およびテスト メソッド レベルでは、型、**セットアップ**と**破棄**テストのためのメソッド。 ただしで、**セットアップ**と**破棄**メソッド、クラス レベルで**サイズ**が、*文字列配列*データ型。

コードで、このようなデータの競合があれば、TAEF が実行中に警告が表示し、プロパティの一覧が、失敗、データの競合は発生しません。

 

 





