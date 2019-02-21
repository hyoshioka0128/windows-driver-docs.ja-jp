---
title: 単純なデータ ドリブン テストの例
description: 単純なデータ ドリブン テストの例
ms.assetid: 59A897C3-C9CD-4e1c-B4BA-F81B3B3E4532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 507620097df485986b2281923014ee0c22dbdd14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531187"
---
# <a name="simple-data-driven-test-example"></a>単純なデータ ドリブン テストの例


このセクションでは、データ ドリブン テストのいくつかの例を説明し、各例では、特定の機能について説明します。

最初の例では、SimpleDataDrivenExample と呼ばれる、基本的なデータ ドリブン テストです。

管理対象の例では、次のような XML ファイルが表示されます。

```cpp
    1  <?xml version="1.0"?>
    2  <Data>
    3    <Table Id="Table1">
    4      <ParameterTypes>
    5        <ParameterType Name="Size">Int32</ParameterType>
    6        <ParameterType Name="Color">String</ParameterType>
    7      </ParameterTypes>
    8      <Row>
    9        <Parameter Name="Size">4</Parameter>
    10       <Parameter Name="Color">White</Parameter>
    11     </Row>
    12     <Row>
    13       <Parameter Name="Size">10</Parameter>
    14       <Parameter Name="Color">Black</Parameter>
    15     </Row>
    16     <Row>
    17       <Parameter Name="Size">9</Parameter>
    18       <Parameter Name="Color">Orange</Parameter>
    19     </Row>
    20     <Row>
    21       <Parameter Name="Size">9</Parameter>
    22       <Parameter Name="Color">Blue</Parameter>
    23     </Row>
    24   </Table>
    25 </Data>
```

この XML ファイルでは、データのパラメーターを使用するには、このデータ ドリブン テストを定義します。 最上位の XML ノードは、 **&lt;データ&gt;** タグを含むことができる**1 つまたは複数&lt;テーブル&gt;** 内に定義されているタグ。 **すべてのテーブルは、一意の"ID"属性に関連付ける必要があります。** テスト関数は、XML ファイルで使用する特定のテーブルを識別するためにテーブルの ID 値を使用します。

内で、&lt;テーブル&gt;タグがある、省略可能な**&lt;も存在しない&gt;** セクション。 使用して指定されたパラメーターのデータ型を明示的に指定するここ**&lt;も存在しない&gt;** タグ。 上記の例では、明示的に指定する"Int32"型のパラメーター「サイズ」は、パラメーター"Color"は文字列です。 要約。**存在しないセクションは省略可能です。既定では、パラメーターの型情報が指定されていない場合は、保存されますを文字列として。**

マネージとネイティブの例と比較すると、ことを確認する 2 つの唯一の違い、 **&lt;も存在しない&gt;** ブロックします。 ネイティブ XML ファイルでは、"int"ネイティブ整数型のサイズを指定し、色の種類を指定しないことで既定の WEX::Common::String の種類を使用します。 便宜上は、次の例は、ネイティブの例から XML ファイルを示します。

```cpp
    1  <?xml version="1.0"?>
    2  <Data>
    3    <Table Id="SimpleTable">
    4      <ParameterTypes>
    5        <ParameterType Name="Size">int</ParameterType>
    6      </ParameterTypes>
    7      <Row>
    8        <Parameter Name="Size">4</Parameter>
    9        <Parameter Name="Color">White</Parameter>
    10     </Row>
    11     <Row>
    12       <Parameter Name="Size">10</Parameter>
    13       <Parameter Name="Color">Black</Parameter>
    14     </Row>
    15     <Row>
    16       <Parameter Name="Size">9</Parameter>
    17       <Parameter Name="Color">Orange</Parameter>
    18     </Row>
    19     <Row>
    20       <Parameter Name="Size">9</Parameter>
    21       <Parameter Name="Color">Blue</Parameter>
    22     </Row>
    23   </Table>
    24 </Data>
```

サポートされるパラメーター型**ネイティブ**と**マネージ**コードは、一覧表示されます[ここ](parameter-types-in-table-data-sources.md)します。

その他の任意のデータ型を指定すると、テストは警告がスロー文字列であることだとします。

XML を継続的バックアップ ファイルの後、&lt;も存在しない&gt;ブロック、XML ファイルの両方で、同一のセットがある**&lt;行&gt;s**、内のデータの 1 つのセットに対応する各どちらのマネージ コードとネイティブの例です。 このケースで 4 を使用して定義されているデータの 4 つのセットがある&lt;行&gt;をブロックするを使用してパラメーターの値を指定する各、 **&lt;パラメーター&gt;** タグ。

データのソース ファイルのさまざまな部分の基本について説明します。 これで、上記の XML ファイルで指定した値を取得する方法を見てみましょう。

## <a name="span-idauthoringtesttobeadatadriventestspanspan-idauthoringtesttobeadatadriventestspanspan-idauthoringtesttobeadatadriventestspanauthoring-test-to-be-a-data-driven-test"></a><span id="Authoring_test_to_be_a_data_driven_test"></span><span id="authoring_test_to_be_a_data_driven_test"></span><span id="AUTHORING_TEST_TO_BE_A_DATA_DRIVEN_TEST"></span>データ ドリブン テストにテストの作成


これで、データを指定すると、コードを関連付けるか、XML ファイルでこのデータを使用してデータを使用するメソッドをテストする方法必要があります。 これを行う - どちら、マネージ コードとネイティブの例で、指定することによって、 **"DataSource"** メタデータ。 データ ソースのメタデータには、次の 3 つの部分に分かれてがあります。

1.  ' テーブル:'-これは XML テーブルとしてデータ ソースを識別します。
2.  'DataDrivenTests.xml' の XML テーブルを含むファイルです。
3.  '\#Table2' - 次の'\#' 区切り、'Table2' 値が使用する XML ドキュメント内で特定のテーブルを識別します。 1 つのテーブルの XML データ ソースは、複数のテーブルを含めることができます。 TAEF は、指定した値に一致する 'Id' 属性を持つ Table 要素の XML ファイルを参照します。

もう一度、上記の側面を網羅するコードを簡単に見てことができます。

### <a name="span-idnativecodespanspan-idnativecodespanspan-idnativecodespannative-code"></a><span id="Native_code"></span><span id="native_code"></span><span id="NATIVE_CODE"></span>ネイティブ コード

```cpp
1   class SimpleDataDrivenExample
2   {
3      BEGIN_TEST_CLASS(SimpleDataDrivenExample)
4        TEST_CLASS_PROPERTY(L"Description", L"Simple example in table-based data-driven tests")
5      END_TEST_CLASS()
6   
7      TEST_METHOD_CLEANUP(TestCleanup);
8      TEST_METHOD_SETUP(TestSetup);
9    
10     BEGIN_TEST_METHOD(DataDrivenTest)
11       TEST_METHOD_PROPERTY(L"DataSource", L"Table:SimpleDataDrivenExample.xml#SimpleTable")
11     END_TEST_METHOD()
12     ...
```

### <a name="span-idmanagedcodespanspan-idmanagedcodespanspan-idmanagedcodespanmanaged-code"></a><span id="Managed_code"></span><span id="managed_code"></span><span id="MANAGED_CODE"></span>マネージ コード

```cpp
    1 [TestMethod]
    2 [DataSource("Table:CSharpDataDrivenSimpleExample.xml#SimpleTable")]
    3 public void DataDrivenTest()
    4 {
    5  ...
    6 }
```

「データ ソース」は、Microsoft.VisualStudio.TestTools.UnitTesting の既知のプロパティです。

上記のほかには、マネージ コードでデータ ドリブン テストのいくつか追加の手順が必要です。 プライベート TestContext プロパティ - VSTS をお勧めなどを定義する必要があります (<https://msdn2.microsoft.com/library/ms404699(VS.80).aspx>)。 このプロパティにパブリック assessors も定義します。 内部的にして、データにアクセスできるように、TAEF はこの TestContext プロパティを設定します。 コードのこの部分で簡単に検討することができます。

```cpp
    1 public TestContext TestContext
    2 {
    3     get;
    4     set;
    5 }
```

## <a name="span-idretrievingdatainthetestmethodspanspan-idretrievingdatainthetestmethodspanspan-idretrievingdatainthetestmethodspanretrieving-data-in-the-test-method"></a><span id="Retrieving_data_in_the_Test_method"></span><span id="retrieving_data_in_the_test_method"></span><span id="RETRIEVING_DATA_IN_THE_TEST_METHOD"></span>テスト メソッドでデータを取得します。


取得 Api は、マネージ コードとネイティブ コードで異なります。 まず理解、**ネイティブの取得 API**:

```cpp
    1  void SimpleDataDrivenExample::DataDrivenTest()
    2  {
    3          int size;
    4          if (SUCCEEDED(TestData::TryGetValue(L"size", size)))
    5          {
    6              VERIFY_ARE_NOT_EQUAL(size, 0);
    7              Log::Comment(String().Format(L"Size retrieved was %d", size));
    8          }
    9
    10         String color;
    11         if (SUCCEEDED(TestData::TryGetValue(L"color", color)))
    12         {
    13             Log::Comment(L"Size retrieved was " + color);
    14         }
    15
    16         unsigned int index;
    17         if (SUCCEEDED(TestData::TryGetValue(L"index", index)))
    18         {
    19             Log::Comment(String().Format(L"At index %d", index));
    20         }
    21 }
```

4、11、および 17 行に特に注意します。 これらの行ごとに、前に取得するデータを保存するローカル変数を定義します。 ここにある型を取得するのには重要です。 「サイズ」を XML ファイルで、"int"型を定義するために取得する型は int のローカル変数を定義する必要があります。 検索 API では、最初のパラメーターとして文字列値として取得するパラメーターの名前を受け取ります。 2 番目のパラメーターは、ローカル変数の参照によって渡され、TAEF コードで設定です。

定義されているこの検索 API **TestData.h** TAEF のすべてのテストを含む WexTestClass.h ヘッダーが含まれているとします。

データを取得する**マネージ コード**、ことを定義した TestContext プロパティを使用します。 次のコードで (または例では) を参照してください。

```cpp
    1  public void DataDrivenTest()
    2  {
    3     int size = (int)m_testContext.DataRow["Size"];
    4     Verify.AreNotEqual(size, 0);
    5     Log.Comment("Size is " + size.ToString());
    6
    7     Log.Comment("Color is " + m_testContext.DataRow["Color"]);
    8     UInt32 index = (UInt32)m_testContext.DataRow["Index"];
    9     Log.Comment("At index " + index.ToString());
    10 }
```

VSTS に慣れている場合、上記の例はのようなことが表示されます。 DataRow を取得しようとしているパラメーターの名前と列名を指定します。

例で確認する場合、同じクラスの非データ ドリブン テストもあります。 つまり、**同じテスト クラスでテストをデータ ドリブンと NonDataDriven を組み合わせることのできる柔軟性があります。**

## <a name="span-idrunningsimpledatadrivenexamplewithtaefspanspan-idrunningsimpledatadrivenexamplewithtaefspanspan-idrunningsimpledatadrivenexamplewithtaefspanrunning-simpledatadrivenexample-with-taef"></a><span id="Running_SimpleDataDrivenExample_with_TAEF"></span><span id="running_simpledatadrivenexample_with_taef"></span><span id="RUNNING_SIMPLEDATADRIVENEXAMPLE_WITH_TAEF"></span>TAEF を SimpleDataDrivenExample を実行しています。


方法を理解しているかどうかを確認**作成者データ ドリブン テスト**する方法と**TAEF でテストを実行**のヒントとテクニック DataDrivenTests TAEF での実行を開始する前にします。 方法上のメモリを更新すると便利**選択**TAEF で動作します。

データ ドリブン テストの実行中のコマンド プロンプトは TAEF で汎用テストを実行すると大きく異なります。 説明した例 (ネイティブとマネージ) を実行するには、次のコマンドを実行だけです。

<span id="TE.exe_Examples_CPP.DataDriven.Example.dll_Examples_CSharp.DataDriven.Example.dll__________________________name__Simple_"></span><span id="te.exe_examples_cpp.datadriven.example.dll_examples_csharp.datadriven.example.dll__________________________name__simple_"></span><span id="TE.EXE_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL__________________________NAME__SIMPLE_"></span>TE.exe 例\\CPP します。DataDriven.Example.dll 例\\CSharp.DataDriven.Example.dll/name:\*単純な\*  

'/Name' 名に基づく選択条件を追加し、興味のあるクラスのみを選択します。 クラス内から実行するテストを選択するには、すべての dll のプロパティを一覧表示する必要があります最初。 次に、選択条件として使用するプロパティを決定できます。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /name:*Simple* /listproperties
f:\Examples\CPP.DataDriven.Example.dll
        WEX::TestExecution::Examples::SimpleDataDrivenExample
                Property[Description] = Simple example in table-based data-driven tests

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#0
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = White
                    Data[Size] = 4

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#1
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = Black
                    Data[Size] = 10

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#2
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest#3
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[DataSource] = Table:SimpleDataDrivenExample.xml#SimpleTable

                    Data[Color] = Blue
                    Data[Size] = 9

            WEX::TestExecution::Examples::SimpleDataDrivenExample::FirstNonDataDrivenTest
                    Setup: TestSetup
                    Teardown: TestCleanup

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet0
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[Data:Color] = {Purple, Maroon, Brown}

                    Data[Color] = Purple

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet1
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[Data:Color] = {Purple, Maroon, Brown}

                    Data[Color] = Maroon

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SetsOfDataTest#metadataSet2
                    Setup: TestSetup
                    Teardown: TestCleanup
                    Property[Data:Color] = {Purple, Maroon, Brown}

                    Data[Color] = Brown

            WEX::TestExecution::Examples::SimpleDataDrivenExample::SecondNonDataDrivenTest
                    Setup: TestSetup
                    Teardown: TestCleanup


        f:\Examples\CSharp.DataDriven.Example.dll
        WEX.Examples.CSharpDataDrivenSimpleExample
                Setup: MyClassInitialize
                Property[Description] = Simple example in table-based data-driven tests

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#0
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = White
                    Data[Size] = 4

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#1
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = Black
                    Data[Size] = 10

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#2
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX.Examples.CSharpDataDrivenSimpleExample.DataDrivenTest#3
                    Property[DataSource] = Table:CSharpDataDrivenSimpleExample.xml#SimpleTable

                    Data[Color] = Blue
                    Data[Size] = 9

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

ここでは、SetsOfMetadataTest や上に示した SetsOfDataTest は無視してみましょう。 これらについて調べる場合は詳細を読む[軽量データ ドリブン テスト](light-weight-data-driven-testing.md)します。 さまざまなプロパティとデータ パラメーターの名前と値がわかったら、その指定に基づいて特定のテストを選択できます。 実際に試してみて、選択内容を確認する作業を進めるにします。

非データ駆動テストのみを実行するには、次のコマンドを実行します。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And_not__DataSource____"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and_not__datasource____"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND_NOT__DATASOURCE____"></span>TE.exe Examples\\CSharp.DataDriven.Example.dll Examples\\CPP.DataDriven.Example.dll /select:"@Name='\*Simple\*' And not(@DataSource=\*)"  

ここで、次のように実行すると、ドリブン テストでは、色が"Black"として指定されている、データのみを実行します。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Color__Black__"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_color__black__"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_COLOR__BLACK__"></span>TE.exe 例\\CSharp.DataDriven.Example.dll 例\\CPP します。DataDriven.Example.dll リンク:"@Name='\*単純\*' と@Data:Color= '黒'"  

"Color"同様<strong>@Data: &lt;DataDrivenParameterName&gt;=&lt;DataDrivenParameterValue&gt;</strong>に基づいて特定のデータを実行しますデータ ドリブン パラメーター値を指定します。 上記の場合で実行されます WEX::TestExecution::Examples::SimpleDataDrivenExample::DataDrivenTest\#1 とかかえるします。Examples.CSharpDataDrivenSimpleExample.DataDrivenTest\#1

注意してください、**テスト インデックス**で上記の list プロパティ。 選択上記もインデックスを基にします。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Index_1_"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_index_1_"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_INDEX_1_"></span>TE.exe Examples\\CSharp.DataDriven.Example.dll Examples\\CPP.DataDriven.Example.dll /select:"@Name='\*Simple\*' And @Data:Index=1"  

上記は、同じ 2 つのテストを実行@Data:Color= '黒' を選択します。 警備員とインデックスの選択に追加するも **@Data:Index &gt; lowerGuardValue と@Data:index &lt; upperGuardValue**

データ ドリブン TAEF とテストの基本を理解している場合は、同じ例では、次のクラスと共にに従います。[行レベルのメタデータのオーバーライド](metadata-overriding-data-driven-test-example.md)、[配列パラメーター型を指定する](array-support-data-driven-test-example.md)します。









