---
title: シンプルなデータ ドリブン テストの例
description: シンプルなデータ ドリブン テストの例
ms.assetid: 59A897C3-C9CD-4e1c-B4BA-F81B3B3E4532
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6f8d4dad8e0921c334c6391057bd29e02be291
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402297"
---
# <a name="simple-data-driven-test-example"></a>シンプルなデータ ドリブン テストの例


ここでは、データドリブンテストの例をいくつか紹介し、各例の特定の機能について説明します。

最初の例は、SimpleDataDrivenExample という基本的なデータドリブンテストです。

マネージドの例では、次のような XML ファイルを検索します。

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

この XML ファイルは、使用するデータドリブンテストのデータパラメーターを定義します。 最上位の XML ノードは** &lt; データ &gt; **タグであり、その中に定義されている**1 つ以上の &lt; テーブル &gt; **タグを含むことができます。 **すべてのテーブルは、一意の "ID" 属性に関連付けられている必要があります。** テスト関数は、テーブル ID 値を使用して、XML ファイルで使用される特定のテーブルを識別します。

&lt;Table タグ内 &gt; には、省略可能な** &lt; ParameterTypes &gt; **セクションがあります。 ここでは、 ** &lt; ParameterTypes &gt; ** tags を使用して、特定のパラメーターのデータ型を明示的に指定できます。 上の例では、パラメーター "Size" の型が "Int32" で、パラメーター "Color" が文字列であることを明示的に指定しています。 概要: **ParameterTypes セクションは省略可能です。既定では、パラメーターの型情報が指定されていない場合は、文字列として保存されます。**

マネージとネイティブの例を比較した場合、2つの違いは** &lt; ParameterTypes &gt; **ブロックだけであることがわかります。 ネイティブ XML ファイルはネイティブの整数型 "int" のサイズを指定し、既定の型 WEX:: Common:: String を使用して、指定しない色の型にします。 便宜上、次の例では、ネイティブの例の XML ファイルを示します。

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

**ネイティブ**コードと**マネージ**コードでサポートされているパラメーターの型は、「[テーブルデータソースのパラメーターの型](parameter-types-in-table-data-sources.md)」に記載されています。

他のデータ型を指定した場合、テストでは警告がスローされ、それが文字列であると見なされます。

XML ファイルを引き続き使用すると、 &lt; 両方の &gt; xml ファイルの ParameterTypes ブロックの後に、同一の** &lt; 行 &gt; **セットが作成されます。これらはそれぞれ、マネージとネイティブの両方の例の1つのデータセットに対応しています。 このケースでは、4つの行ブロックによって定義された4つのデータセットがあり &lt; &gt; 、それぞれが** &lt; パラメーター &gt; **タグを使用してパラメーターの値を指定しています。

ここでは、データソースファイルのさまざまな部分の基本的な基本について説明します。 次に、上記の XML ファイルで指定した値を取得する方法を見てみましょう。

## <a name="span-idauthoring_test_to_be_a_data_driven_testspanspan-idauthoring_test_to_be_a_data_driven_testspanspan-idauthoring_test_to_be_a_data_driven_testspanauthoring-test-to-be-a-data-driven-test"></a><span id="Authoring_test_to_be_a_data_driven_test"></span><span id="authoring_test_to_be_a_data_driven_test"></span><span id="AUTHORING_TEST_TO_BE_A_DATA_DRIVEN_TEST"></span>データドリブンテストの作成テスト


データを指定したので、このデータを使用するコードまたはテストメソッドを XML ファイルで関連付ける方法が必要になります。 これを行うには、 **"DataSource"** メタデータを指定して、マネージとネイティブの両方の例を使用します。 DataSource メタデータには、次の3つの部分があります。

1.  ' Table: '-データソースを XML テーブルとして識別します。
2.  ' DataDrivenTests.xml '-XML テーブルを含むファイルです。
3.  ' \# Table2 '-' ' 区切り記号 ' の後にある ' \# table2 ' 値は、使用する XML ドキュメント内の特定のテーブルを識別します。 1つの XML テーブルデータソースには、複数のテーブルを含めることができます。 TAEF は、指定された値と一致する ' Id ' 属性を持つテーブル要素の XML ファイルを検索します。

ここでも、上記の側面についてのコードを簡単に見ていきましょう。

### <a name="span-idnative_codespanspan-idnative_codespanspan-idnative_codespannative-code"></a><span id="Native_code"></span><span id="native_code"></span><span id="NATIVE_CODE"></span>ネイティブコード

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

### <a name="span-idmanaged_codespanspan-idmanaged_codespanspan-idmanaged_codespanmanaged-code"></a><span id="Managed_code"></span><span id="managed_code"></span><span id="MANAGED_CODE"></span>マネージコード

```cpp
    1 [TestMethod]
    2 [DataSource("Table:CSharpDataDrivenSimpleExample.xml#SimpleTable")]
    3 public void DataDrivenTest()
    4 {
    5  ...
    6 }
```

"DataSource" は、Microsoft.visualstudio.testtools.uitest.extension.silverlight.dll テストの既知のプロパティです。

上記に加えて、マネージコードでのデータドリブンテストには追加の手順が必要になります。 また、"TestContext" というプライベートプロパティを定義する必要もあり <https://msdn2.microsoft.com/library/ms404699(VS.80).aspx> ます ()。 このプロパティに対してパブリック assessors を定義することもできます。 内部 TAEF は、この TestContext プロパティを設定して、データにアクセスできるようにします。 コードの次の部分を簡単に見てみましょう。

```cpp
    1 public TestContext TestContext
    2 {
    3     get;
    4     set;
    5 }
```

## <a name="span-idretrieving_data_in_the_test_methodspanspan-idretrieving_data_in_the_test_methodspanspan-idretrieving_data_in_the_test_methodspanretrieving-data-in-the-test-method"></a><span id="Retrieving_data_in_the_Test_method"></span><span id="retrieving_data_in_the_test_method"></span><span id="RETRIEVING_DATA_IN_THE_TEST_METHOD"></span>テストメソッドでのデータの取得


取得 Api はマネージコードとネイティブコードで異なります。 まず、**ネイティブ取得 API**について説明します。

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

4、11、および17行目に特に注意を払ってください。 これらの行の前に、取得するデータを保存するローカル変数を定義します。 ここで型を取得することが重要です。 "Size" は XML ファイルの "int" 型に定義されているため、この型を取得するには int 型のローカル変数を定義する必要があります。 取得 API は、最初のパラメーターとして文字列値として取得するパラメーターの名前を受け取ります。 2番目のパラメーターは、参照渡しで渡され、TAEF コードによって設定されるローカル変数です。

この取得 API は**TestData**で定義され、すべての taef テストに含まれる WexTestClass ヘッダーに含まれています。

**マネージコード**内のデータを取得するには、定義した TestContext プロパティを使用します。 次のコードを見てみましょう (または例)。

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

VSTS を使い慣れている場合は、上記の例が似ていることがわかります。 DataRow を使用し、取得しようとしているパラメーターの名前として列名を指定します。

例を見ると、同じクラスに非データドリブンテストも存在します。 言い換える**と、DataDriven と NonDataDriven のテストを同じテストクラスで組み合わせるという柔軟性があります。**

## <a name="span-idrunning_simpledatadrivenexample_with_taefspanspan-idrunning_simpledatadrivenexample_with_taefspanspan-idrunning_simpledatadrivenexample_with_taefspanrunning-simpledatadrivenexample-with-taef"></a><span id="Running_SimpleDataDrivenExample_with_TAEF"></span><span id="running_simpledatadrivenexample_with_taef"></span><span id="RUNNING_SIMPLEDATADRIVENEXAMPLE_WITH_TAEF"></span>TAEF での SimpleDataDrivenExample の実行


**データドリブンテストを作成**する方法、および Taef で DataDrivenTests を実行するためのヒントとテクニックから始める前に、 **Taef でテストを実行**する方法を把握しておく必要があります。 TAEF での**選択**の動作に関するメモリを更新すると便利な場合があります。

データドリブンテストを実行するためのコマンドプロンプトは、TAEF で汎用テストを実行する場合と大きく異なります。 上記で説明した両方の例 (ネイティブとマネージ) を実行するには、次のコマンドを実行します。

<span id="TE.exe_Examples_CPP.DataDriven.Example.dll_Examples_CSharp.DataDriven.Example.dll__________________________name__Simple_"></span><span id="te.exe_examples_cpp.datadriven.example.dll_examples_csharp.datadriven.example.dll__________________________name__simple_"></span><span id="TE.EXE_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL__________________________NAME__SIMPLE_"></span>TE.exe 例 \\CPP.DataDriven.Example.dll 例 \\CSharp.DataDriven.Example.dll/Name: \* Simple\*  

'/Name ' は、名前に基づいて選択条件を追加し、関心のあるクラスのみを選択します。 クラス内から実行するテストを選択するには、まず dll のすべてのプロパティを一覧表示する必要があります。 次に、選択条件に使用するプロパティを決定できます。

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

ここでは、上記の SetsOfMetadataTest と SetsOfDataTest を無視してみましょう。 これらの詳細については、「[軽量なデータドリブンテスト](light-weight-data-driven-testing.md)」を参照してください。 さまざまなプロパティとデータパラメーターの名前と値がわかったので、それに基づいて特定のテストを選択できます。 試してみて、選択内容を確認してください。

非データドリブンテストのみを実行するには、次のように実行します。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And_not__DataSource____"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and_not__datasource____"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND_NOT__DATASOURCE____"></span>TE.exe 例 \\CSharp.DataDriven.Example.dll 例 \\CPP.DataDriven.Example.dll/select: " @Name = ' \* Simple \* ' And not ( @DataSource = \* )"  

ここで、color が "Black" と指定されているデータドリブンテストのみを実行するには、次のように実行します。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Color__Black__"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_color__black__"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_COLOR__BLACK__"></span>TE.exe 例 \\CSharp.DataDriven.Example.dll 例 \\CPP.DataDriven.Example.dll/select: " @Name = ' \* Simple \* ' And @Data:Color = ' Black '"  

"Color" を使用した場合と同様に、 <strong> @Data: &lt; datadriDataDriven &gt; = &lt; &gt; </strong>は、指定されたパラメーター値に基づいて特定のデータを実行します。 上記の例では、WEX:: TestExecution:: example:: Simpledatadriatadriventest の例::D \# 1 と WEX が実行されます。例. CSharpDataDrivenSimpleExample. DataDrivenTest \# 1

上記の listproperties の**テストインデックス**に注意してください。 インデックスに基づいて上記を選択することもできます。

<span id="TE.exe_Examples_CSharp.DataDriven.Example.dll_Examples_CPP.DataDriven.Example.dll__________________________select___Name___Simple___And__Data_Index_1_"></span><span id="te.exe_examples_csharp.datadriven.example.dll_examples_cpp.datadriven.example.dll__________________________select___name___simple___and__data_index_1_"></span><span id="TE.EXE_EXAMPLES_CSHARP.DATADRIVEN.EXAMPLE.DLL_EXAMPLES_CPP.DATADRIVEN.EXAMPLE.DLL__________________________SELECT___NAME___SIMPLE___AND__DATA_INDEX_1_"></span>TE.exe 例 \\CSharp.DataDriven.Example.dll 例 \\CPP.DataDriven.Example.dll/select: " @Name = ' \* Simple \* ' And @Data:Index = 1"  

上の例では、' Black ' が選択されているのと同じ2つのテストが実行され @Data:Color ます。 また、下** @Data:Index &gt; guシャード値と @Data:index &lt; upperGuardValue**を使用して、インデックス選択にガードを追加することもできます。

TAEF でのデータドリブンテストの基本を理解している場合は、同じ例の次のクラスに従います。[行レベルでメタデータをオーバーライド](metadata-overriding-data-driven-test-example.md)し、[配列パラメーターの型を指定](array-support-data-driven-test-example.md)します。









