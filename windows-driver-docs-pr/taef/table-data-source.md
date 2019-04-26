---
title: テーブルのデータ ソース
description: テーブルのデータ ソース
ms.assetid: D0CC0536-5569-47ed-8DE8-B64FF3042C51
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90c098dafbaf6c14d04b30e4db95f2d99cd5b413
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341812"
---
# <a name="table-data-source"></a>テーブルのデータ ソース


基本的な実行について理解しているかどうかを確認してください[TAEF](index.md)を理解して方法[作成者テスト](authoring-tests.md)、このセクションに進む前に使用します。

基本的なテスト自動化を記述する必要があるし、TAEF を使用することができたさまざまなデータ セットで動作するコードをテスト同じシナリオについて重点的に説明を使用できます。 この目的では、TAEF は、データ ドリブン テストに「テーブルに基づく」アプローチを提供します。 データ ドリブン テストの作成に着手する方法を理解する簡単な例を見ていきましょう。

単純な非-データ駆動型のサイズと、コンソールにテーマを印刷する例を検討してください。 この演習では、データ ドリブン テストにこのテストを変換します。

```cpp
1  namespace WEX { namespace TestExecution { namespace Examples
2  {
3     void DataDrivenTests::FirstTable()
4     {
5         int size = 12;
6         Log::Comment(String().Format(L"Size retrieved was %d", size));
7     }
8
9     void DataDrivenTests::SecondTable()
10    {
11        String theme = "Aero";
12        Log::Comment(L"Theme supplied as " + theme);
13    }
14 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

## <a name="span-iddefiningthedataspanspan-iddefiningthedataspanspan-iddefiningthedataspandefining-the-data"></a><span id="Defining_the_Data"></span><span id="defining_the_data"></span><span id="DEFINING_THE_DATA"></span>データを定義します。


ここで、サイズとテーマのセットに対応する上記の関数をします。 つまり、関数が使用できるバリアント データ値をします。 これを行うには、XML ファイル DataDrivenTests.xml で 2 つのテーブルを定義します。

```cpp
1  <?xml version="1.0"?>
2  <Data>
3  <Table Id ="Table1">
4          <ParameterTypes>
5                  <ParameterType Name="Size">Int32</ParameterType>
6                  <ParameterType Name="Color">String</ParameterType>
7                  <ParameterType Name="Transparency">Boolean</ParameterType>
8          </ParameterTypes>
9          <Row Priority="1" Owner="C2">
10                 <Parameter Name="Size">12</Parameter>
11                 <Parameter Name="Color">Blue</Parameter>
12                 <Parameter Name="Transparency">True</Parameter>
13         </Row>
14         <Row Priority="2" Owner="wex">
15                 <Parameter Name="Size">4</Parameter>
16                 <Parameter Name="Color">White</Parameter>
17                 <Parameter Name="Transparency">False</Parameter>
18         </Row>
19         <Row Owner="C2">
20                 <Parameter Name="Size">9</Parameter>
21                 <Parameter Name="Color">Black</Parameter>
22                 <Parameter Name="Transparency">True</Parameter>
23         </Row>
24 </Table>
25 <Table id ="Table2">
26         <Row Description="ButtonTest" Owner="C2" Priority="1">
27                 <Parameter Name="Control">Button</Parameter>
28                 <Parameter Name="Theme">Aero</Parameter>
29         </Row>
30         <Row Description="ComboBoxTest" Priority="2">
31                 <Parameter Name="Control">ComboBox</Parameter>
32                 <Parameter Name="Theme">Classic</Parameter>
33         </Row>
34         <Row Description="ListviewTest" Owner="wex">
35                 <Parameter Name="Control">Listview</Parameter>
36                 <Parameter Name="Theme">AeroBasic</Parameter>
37         </Row>
38 </Table>
39 </Data>
```

"Table1"と"Table2"の 2 つのテーブルに定義したようになりました。 **同じ XML ファイルでは、テーブルのいくつかのテスト メソッドを定義できます。**

Table1 でも存在しない事前定義されているを整数にするには、「サイズ」の選択を確認します。 **存在しないセクションは省略可能です。** 既定では、パラメーターの型情報が指定されていない場合は、保存されますを文字列として。 これは、「Table2」すべてパラメーターの場合です。

各「行」テーブル内で定義されているは、一連のデータ (パラメーター) の値を受け入れるように、テスト関数を希望します。 9、14 ~ 19 行目では、3、FirstTable 関数はそのまま使用するデータ セットを定義します。 同様に 26、30 ~ 34 行目では、SecondTable のデータ セットを定義します。

通知行 9、14、19、26、30、および上記の例では 34 - 行に固有のメタデータを定義することができます。 今すぐメタデータについては、同じ関数のデータ セットを変更する方法があります。 データ (9 行目) の最初のセットの優先順位は 1、2 番目のセットのデータ (14 行目) の優先順位が 2 と 3 番目の関数の優先順位のデータ (19 行目) の既定値のセット。 **すべての行では、テーブルが関連付けられている関数からメタデータを継承します。同じメタデータは、行レベルでもう一度指定されている場合、関数レベルで定義されているメタデータの値が上書きされます。**

**注:XML ファイルのスキーマ定義は、サポートされている種類の定義を除く、ネイティブとマネージ コードの同じです。** 別のデータを定義する方法の例は、以下の「データ ドリブン テストの管理」セクションの最初の部分を参照してください。 ネイティブ データ ドリブン テストをネイティブ コードで使用できる型を理解しておくを続行します。

## <a name="span-idnativedatadriventestspanspan-idnativedatadriventestspanspan-idnativedatadriventestspannative-data-driven-test"></a><span id="Native_Data_driven_test"></span><span id="native_data_driven_test"></span><span id="NATIVE_DATA_DRIVEN_TEST"></span>ネイティブのデータ ドリブン テスト


定義され、使用可能な状態は、データ セットでデータ ドリブン テストとして、テスト関数を修飾し、データ セットを定義するテーブルに関連付ける手段が必要するようになりました。 これは追加のメタデータを使用して、テストを作成する際に行われます。

```cpp
1  namespace WEX { namespace TestExecution { namespace Examples
2  {
3      class DataDrivenTests
4      {
5          TEST_CLASS(DataDrivenTests);
6
7          BEGIN_TEST_METHOD(SecondTable)
8              TEST_METHOD_PROPERTY(L"DataSource", L"Table:DataDrivenTests.xml#Table2")
9              TEST_METHOD_PROPERTY(L"Priority", L"3")
10         END_TEST_METHOD()
11
12         BEGIN_TEST_METHOD(FirstTable)
13             TEST_METHOD_PROPERTY(L"Priority", L"4")
14             TEST_METHOD_PROPERTY(L"DataSource", L"Table:DataDrivenTests.xml#Table1")
15         END_TEST_METHOD()
16     };
17 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

テスト XML テーブルを関連付けるためには、テストのメソッドに 'DataSource' のメタデータを追加します。 この関連付けを TAEF は、ドライブのテストを指定したデータソースを使用します。 データ ソースの値では、次の 3 つの部分に分かれてがあります。

1.  ' テーブル:'-これは XML テーブルとしてデータ ソースを識別します。
2.  'DataDrivenTests.xml' の XML テーブルを含むファイルです。
3.  '\#Table2' - 次の'\#' 区切り、'Table2' 値が使用する XML ドキュメント内で特定のテーブルを識別します。 1 つのテーブルの XML データ ソースは、複数のテーブルを含めることができます。 TAEF は、指定した値に一致する 'Id' 属性を持つ Table 要素の XML ファイルを参照します。

上記の例"SecondTable"が"FirstTable"の前に定義されていることを確認しました可能性があります。 これは、"SecondTable"関数"FirstTable"関数で、前に実行されますが、"Table1"、"Table2"前に、"FirstTable"、"SecondTable"に対応するテーブルに対応するテーブルを定義することを意味します。 これはことを強調する**検出およびデータ ドリブン テストの実行中にテーブル定義の順序は関係ありません。**

完全なテスト メソッドに、データ ソースのマッピングでは、ソースからデータを取得する例を変更することができます。 その前に、パブリッシュされたヘッダー ファイル、TestData.h で、紹介を実行します。 関心のある部分です。

```cpp
1    class TestData
2    {
3    public:
4        template <typename T>
5        static HRESULT __stdcall TryGetValue(_In_z_ const wchar_t* pszString, T& result)
6        {
7            return Private::TestData<T>::TryGetValue(pszString, result);
8        }
9    };
```

5 行目では、関数内のデータを取得するために呼び出す API を示します。 使用可能なについて見て[パラメーターの型](parameter-types-in-table-data-sources.md)取得できるようにします。

Ok - すべての例を再書き込みに設定します。

```cpp
1  namespace WEX { namespace TestExecution { namespace Examples
2  {
3      void DataDrivenTests::FirstTable()
4      {
5          Log::Comment(L"I am in first table");
6          int size;
7          if (SUCCEEDED(TestData::TryGetValue(L"size", size)))
8          {
9              VERIFY_ARE_NOT_EQUAL(size, 0);
10             Log::Comment(String().Format(L"Size retrieved was %d", size));
11         }
12     }
13
14     void DataDrivenTests::SecondTable()
15     {
16         Log::Comment(L"I am in second table.");
17         String theme;
18         if (SUCCEEDED(TestData::TryGetValue(L"theme", theme)))
19         {
20             Log::Comment(L"Theme supplied as " + theme);
21         }
22     }
23 } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

7 ~ 18 行目は、テスト データ ドリブンを行うために変更する主な部分です。 変更の優れた処理ではありません。 データ ドリブン テストの実行中に TAEF を最大限に活用する方法についてのデータ ドリブン テストの実行を見てください。

## <a name="span-idmanageddatadriventestspanspan-idmanageddatadriventestspanspan-idmanageddatadriventestspanmanaged-data-driven-test"></a><span id="Managed_Data_driven_test"></span><span id="managed_data_driven_test"></span><span id="MANAGED_DATA_DRIVEN_TEST"></span>管理対象のデータ ドリブン テスト


四角形の座標をコンソールに印刷する例を検討してください。 これらの座標を定義する XML ファイル内のデータ セットとしてを起動します。

```cpp
1  <?xml version="1.0"?>
2  <Data>
3  <Table Id="FirstTable">
4          <ParameterTypes>
5                  <ParameterType Name="Left">Int32</ParameterType>
6                  <ParameterType Name="Right">String</ParameterType>
7                  <ParameterType Name="Top">Integer</ParameterType>
8                  <ParameterType Name="Bottom">Int32</ParameterType>
9          </ParameterTypes>
10         <Row Priority="1" Owner="C2" Description="Zero rect">
11                 <Parameter Name="Left">0</Parameter>
12                 <Parameter Name="Right">0</Parameter>
13                 <Parameter Name="Top">0</Parameter>
14                 <Parameter Name="Bottom">0</Parameter>
15         </Row>
16         <Row Priority="2" Owner="wex" Description="normal rect">
17                 <Parameter Name="Left">12</Parameter>
18                 <Parameter Name="Right">25</Parameter>
19                 <Parameter Name="Top">10</Parameter>
20                 <Parameter Name="Bottom">50</Parameter>
21         </Row>
22         <Row Owner="C2" Description="invalid rect">
23                 <Parameter Name="Left">30</Parameter>
24                 <Parameter Name="Right">15</Parameter>
25                 <Parameter Name="Top">40</Parameter>
26                 <Parameter Name="Bottom">10</Parameter>
27         </Row>
28 </Table>
29 </Data>
```

"FirstTable"上の 3 つの行で定義されているこのケースでは、テーブルのスコープ内のデータ セットを定義します。 **同じ XML ファイルでは、テーブルのいくつかのテスト メソッドを定義できます。**

FirstTable が事前も存在しないを定義し、"Int32"にするには、"Left"を呼び出すことを確認します。 **存在しないセクションは省略可能です。既定では、パラメーターの型情報が指定されていない場合は、保存されますを文字列として。**

一覧を見てサポートされている[パラメーターの型](parameter-types-in-table-data-sources.md)します。

その他の任意のデータ型を指定すると、テストは警告がスロー文字列であることだとします。

**注:型の文字列は大文字と小文字は区別されませんが、前に示したとおりスペルする必要があります。**

各「行」、テーブル内で定義されているは、一連のデータ (パラメーター) の値を受け入れるように、テスト関数を希望します。 10、16 ~ 22 行目は、データの 3 つのセットを定義する関数。

通知行 10、16、および上記の例では 22 - 行に固有のメタデータを定義することができます。 メタデータについては、同じ関数のデータ セットを変更する方法があるようになりました。 データ (10 行目) の最初のセットの優先順位は 1、2 番目のセットのデータ (16 行目) の優先順位が 2 と 3 番目の関数の優先順位のデータ (22 行目) の既定値のセット。 **すべての行では、テーブルが関連付けられている関数からメタデータを継承します。同じメタデータは、行レベルでもう一度指定されている場合、関数レベルで定義されているメタデータの値が上書きされます。**

**注:XML ファイルのスキーマ定義は、サポートされている種類の定義を除く、ネイティブとマネージ コードの同じです。** これを定義する方法の別の例は、このページの上部にある「データを定義する」セクションをご覧ください。

ここで、定義されているすべてのデータがあります。 次の例では、それにアクセスする方法を示します。

```cpp
1  namespace WEX.Examples
2  {
3      using Microsoft.VisualStudio.TestTools.UnitTesting;
4      using System;
5      using System.Collections;
6      using WEX.Logging.Interop;
7      using WEX.TestExecution;
8
9      [TestClass]
10     public class CSharpDataDrivenTests
11     {
12         [TestMethod]
15         [DataSource("Table:CSharpDataDrivenTests.xml#FirstTable")]
16         public void First()
17         {
18             Console.WriteLine("Left is " + m_testContext.DataRow["Left"].ToString());
19
20             Log.Comment("In CSharpDataDrivenTests.First");
21         }
22
23         [TestMethod]
24         public void Second()
25         {
26             Log.Comment("In CSharpDataDrivenTests.Second");
27             Verify.IsTrue(true);
28         }
29
30         public TestContext TestContext
31         {
32             get { return m_testContext; }
33             set { m_testContext = value; }
34         }
35
36         private TestContext m_testContext;
37     }
38 }
```

マネージ コードで指定されたテスト メソッドを使用して XML テーブルを関連付けることは、ネイティブ コードによく似ています'DataSource' のメタデータを適用します。 としてする前に、これはから成ります 3 つの部分。

1.  ' テーブル:' - XML テーブルとしてデータ ソースを識別するためにします。
2.  ' CSharpDataDrivenTests.xml' の XML テーブルを含むファイル。
3.  '\#FirstTable' - 次の'\#' 区切り、'FirstTable' 値が使用する XML ドキュメント内で特定のテーブルを識別します。 TAEF は、指定した値に一致する 'Id' 属性を持つ Table 要素の XML ファイルを参照します。

2 番目の関数がないデータ ドリブンに注意してください。 **データ ドリブン テストの一部のみができます。また、そのテーブルを別の XML ファイルで定義されている各テストのオプションがあります。**

プライベート TestContext プロパティ - VSTS をお勧めなどを定義する行の 36 (<https://msdn2.microsoft.com/library/ms404699(VS.80).aspx>)。 このプロパティ (30 ~ 34 行) にパブリック assessors も定義します。 内部的に TAEF はフォーカスのある対応するデータ セットの TestContext のディクショナリ プロパティを読み込みます。

TestContext は Microsoft.VisualStudio.TestTools.UnitTesting で定義されます。 上記の例では、行 3 を参照してください。 必要があります既に含めますこれ参照として、管理対象のテストの作成します。 **そのため、その他の参照をデータ ドリブン テストを作成する必要はありません。**

上記の例の行 18 では、関数でデータを取得する方法を示します。 データが m で使用できることに注意してください。\_ための testContext.DataRow します。

## <a name="span-idnameinsteadofindextoidentifyadatarowspanspan-idnameinsteadofindextoidentifyadatarowspanspan-idnameinsteadofindextoidentifyadatarowspanname-instead-of-index-to-identify-a-datarow"></a><span id="Name_instead_of_Index_to_Identify_a_DataRow"></span><span id="name_instead_of_index_to_identify_a_datarow"></span><span id="NAME_INSTEAD_OF_INDEX_TO_IDENTIFY_A_DATAROW"></span>DataRow を識別するインデックスではなく名前します。


TAEF は、データソースで任意の DataRow を識別するためにインデックスではなく意味のある 'Name' プロパティが存在することができます。 これを行うには、単に、データ ソースで行レベルで 'Name' のメタデータを追加します。 このページの最初の例は、次のようにこの機能を使用して変更できます。

```cpp
1  <?xml version="1.0"?>
2  <Data>
3  <Table id ="Table1">
4          <ParameterTypes>
5                  <ParameterType Name="Size">Int32</ParameterType>
6                  <ParameterType Name="Color">String</ParameterType>
7                  <ParameterType Name="Transparency">Boolean</ParameterType>
8          </ParameterTypes>
9          <Row Name='BlueTransparent' Priority="1" Owner="C2">
10                 <Parameter Name="Size">12</Parameter>
11                 <Parameter Name="Color">Blue</Parameter>
12                 <Parameter Name="Transparency">True</Parameter>
13         </Row>
14         <Row Priority="2" Owner="wex">
15                 <Parameter Name="Size">4</Parameter>
16                 <Parameter Name="Color">White</Parameter>
17                 <Parameter Name="Transparency">False</Parameter>
18         </Row>
19         <Row Name='BlackTransparent' Owner="C2">
20                 <Parameter Name="Size">9</Parameter>
21                 <Parameter Name="Color">Black</Parameter>
22                 <Parameter Name="Transparency">True</Parameter>
23         </Row>
24 </Table>
25 ...
39 </Data>
```

上記の例では、'BlueTransparent' correspondes をインデックス 0 に変更します。 インデックス 1 を持つ行に指定の特別な名前を持たないし、インデックス 2 を持つ行が、名前を持つ ' BlackTransparent 関連付けられています。 0 または 2 'Table1' 内のインデックスを検索する選択クエリを使用することもでき、適切な行が検出されます。 実行しているかが表示されるのではなく、dll の一覧を表示する場合。

```cpp
<qualified name of the test method>#<index>
```

代わりに表示されます。

```cpp
<qualified name of the test method>#<name property provided at Row level>
```

"Name"属性が、行レベルで提供されている場所の行。 任意の行の"Name"プロパティを指定しない場合のようなインデックス 1 の場合は既定に\# **&lt;インデックス&gt;** メソッドの修飾名にします。

行レベルの"Name"属性を提供するを使用して変更している本質的に TAEF、メソッドを呼び出すと、対応する行のデータのインスタンスの名前を解釈する方法に注意してください。

## <a name="span-iddatasourceasaruntimeparameterspanspan-iddatasourceasaruntimeparameterspanspan-iddatasourceasaruntimeparameterspandatasource-as-a-runtime-parameter"></a><span id="DataSource_as_a_Runtime_parameter"></span><span id="datasource_as_a_runtime_parameter"></span><span id="DATASOURCE_AS_A_RUNTIME_PARAMETER"></span>実行時のパラメーターとしてデータ ソース


TAEF では、ランタイム パラメーターとしてデータ ソースの指定をサポートします。 この構文は次のとおりです。

```cpp
te <test dll names> /p:<DataSource runtime name>=Table:<DataSoure XML file>#<Table Id>
```

問題のテストを作成する際に指定する必要があります、"p:&lt;DataSource ランタイム名&gt;"データ ソースとして。 実行時に一緒に完全な文字列のテーブルの id と同様に、XML ファイル名を指定する必要があることに留意してください。 TableId は、実行時に、データ ソースが指定されている場合、テスト メタデータとして提供する必要はありません。 "テーブル:"プレフィックスでは、テーブルのデータ ソースを探していることを指定します。

この設定は、リリース共有上の例は、のいずれか利用できます。

``` syntax
te Examples\CPP.RuntimeDataSource.Example.dll /p:MyDataSource=Table:RuntimeDataSourceExample.xml#SimpleTable
```

## <a name="span-iddatasourceasaresourcespanspan-iddatasourceasaresourcespanspan-iddatasourceasaresourcespandatasource-as-a-resource"></a><span id="DataSource_as_a_Resource"></span><span id="datasource_as_a_resource"></span><span id="DATASOURCE_AS_A_RESOURCE"></span>リソースとしてデータ ソース


TAEF、次に準拠している限り、test モジュールのリソースとして、データ ソースを追加することができます。

ネイティブのテストのモジュールが発生した場合は、リソース id またはリソースの名前として、データ ソースを指定することでこれを実行できます。 次のコード例に示します。

```cpp
BEGIN_TEST_METHOD(ResourceNameDataSource)
    TEST_METHOD_PROPERTY(L"DataSource", L"Table:MyResourceName#SimpleTable")
END_TEST_METHOD()
```

"MyResourceName"は、ここで ResourceDataSource.rc ファイルで定義されて、リソース名を示します。

```cpp
MyResourceName DATASOURCE_XML "ResourceDataSource.xml"
```

管理対象のテストのモジュールが発生した場合、リソースのみ指定できますが決まった方法でのように、**ソース**次に示すファイルのスニペット。

```cpp
LANGUAGE_NEUTRAL_MANAGED_RESOURCES = CSharpAdvancedDataDrivenTests.xml
```

データ ソースのメタデータの仕様はデータ ソースの XML ファイルを指定する場合と同じです。 マネージ コードの場合と同様に、XML ファイルの名前と同じ名前のリソースを作成できます。 そのため、TAEF はまずデータソースの名前を持つ実際のファイルの存在を検索することを理解しておく必要なります。 このような XML ファイルが見つからない場合のみが、手順を踏み探している特定のリソースの名前または id を持つテスト モジュールでテスト リソース。データ ソースを指定するリソースは、再コンパイルする必要があります、以降を利用するこの設計の開発中に、データ ソースの XML ファイルをテスト dll と同じ場所にコピーして (および、XML ファイル名と同じであるリソース名の名前を付ける)。 完了したら、テスト、XML をコード ディレクトリにコピーし、リソースとして再コンパイルします。 XML ファイルを実行ディレクトリから削除する、ご注意ください。 :)

## <a name="span-idexamplewalk-throughsspanspan-idexamplewalk-throughsspanspan-idexamplewalk-throughsspanexample-walk-throughs"></a><span id="Example_Walk-throughs"></span><span id="example_walk-throughs"></span><span id="EXAMPLE_WALK-THROUGHS"></span>例のチュートリアル


さまざまな側面のベース テーブルのデータ ドリブン テストを理解するには、いくつか詳細の例のチュートリアルを参照してください。

-   [単純なデータ ドリブンの例](data-driven-testing.md)
-   [行レベルのメタデータのオーバーライド](metadata-overriding-data-driven-test-example.md)
-   [配列パラメーター型を指定します。](array-support-data-driven-test-example.md)
-   [データ ドリブン クラス](data-driven-class.md)

 

 





