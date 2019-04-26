---
title: 複数のデータソース
description: 複数のデータソース
ms.assetid: FD0B252F-1D70-4840-986F-94FF80D42246
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd2518c0b91964ed13e57d4ff3a1d7c410b27f08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355500"
---
# <a name="multiple-datasources"></a>複数のデータソース


複数のデータ ソースは、1 つまたは複数のデータ ソースの組み合わせの拡張を探している場合に便利です ([テーブル ベースのデータ ソース](table-data-source.md)、 [PICT ベース DataSource](pict-data-source.md)、または[WMI ベースのデータ ソース](wmi-data-source.md)).

この機能を効率的に使用するようにテスト デザインを作成することが最重要視です。 例の目的に沿ったを見てみましょうこれは、理由。 たとえば、複数のデータ ソースの一部として指定する 2 つのテーブル ベースのデータ ソース、1 つの WMI ベースのデータ ソースと 1 つ PICT ベースのデータ ソース。 説明のためと、最初のテーブルが 4 行、2 つ目が 5 行、WMI クエリを返します 2 つの結果と PICT データソースが 6 のペアの組み合わせを生成します。 これらのパラメーターのセットの組み合わせの展開と TAEF を上げます。 つまり、該当するテスト メソッドが呼び出されます (4 X 5 X 2 X 6 =) **240**回です。 パラメーターのさまざまな組み合わせをテスト メソッドの呼び出しの数を増やすと、テスト カバレッジが限りに減少の結果が生成する可能性があります。 これにより、複数のデータ ソースを使用して、他の方法を検討して慎重にテストを設計します。 次に、いくつかの点を検討することがあります。

-   値が複数のテーブルを追加することを確認します。 別にすることを必要としない場合がまとまったら、効率のよい組み合わせのパラメーターの自分で。
-   複数のテーブルではなく、制約を持つ PICT モデル ファイルを使用することができるかどうかを確認します。
-   複数のテストにテスト_ケースをリファクタリングで値があるし、サブのテストを作成する新しく各に複数のデータ ソースからのサブセットを関連付けることを確認します。

## <a name="span-idspecifymultipledatasourcesspanspan-idspecifymultipledatasourcesspanspan-idspecifymultipledatasourcesspanspecify-multiple-datasources"></a><span id="Specify_multiple_DataSources"></span><span id="specify_multiple_datasources"></span><span id="SPECIFY_MULTIPLE_DATASOURCES"></span>複数のデータ ソースを指定します。


ここで重要な点は、データ ソースを指定する方法を示します。 ネイティブおよびマネージ サンプルからのコード スニペットを見ていきましょう。

### <a name="span-idnativespanspan-idnativespanspan-idnativespannative"></a><span id="Native"></span><span id="native"></span><span id="NATIVE"></span>ネイティブ

```cpp
1   namespace WEX { namespace TestExecution { namespace Examples
2   {
3       class AdvancedDataDrivenTests
4       {
5           TEST_METHOD_SETUP(DataDrivenSetup);
6           TEST_METHOD_CLEANUP(DataDrivenCleanup);
7
8           TEST_CLASS(AdvancedDataDrivenTests)
9
10          BEGIN_TEST_METHOD(SecondTable)
11              TEST_METHOD_PROPERTY(L"DataSource", L"Table:AdvancedDataDrivenTests.xml#Table2;Table:CppTestLevelDataSource.xml#NestedTable")
12          END_TEST_METHOD()
13
14          BEGIN_TEST_METHOD(FirstTable)
15              TEST_METHOD_PROPERTY(L"DataSource", L"Table:AdvancedDataDrivenTests.xml#Table1;"
16                  L"PICT:PictDataSource.txt;" L"WMI:SELECT Location FROM Win32_StartupCommand")
17          END_TEST_METHOD()
18      };
19  } /* namespace Examples */ } /* namespace TestExecution */ } /* namespace WEX */
```

11、15、および上記の例では 16 に行を参照してください。 一般に、セミコロンでデータ ソースを指定するために従うパターンでは、各データ ソースの仕様の一覧が区切られます。 マネージ コードも非常に似ています、仕様になります。

### <a name="span-idmanagedspanspan-idmanagedspanspan-idmanagedspanmanaged"></a><span id="Managed"></span><span id="managed"></span><span id="MANAGED"></span>管理されています。

```cpp
[TestMethod]
[DataSource(@"Table:CSharpAdvancedDataDrivenTests.xml#FirstTable;
    WMI:SELECT ProcessId FROM Win32_Service WHERE Name='Themes'")]

public void First()
{
    Log.Comment("In CSharpAdvancedDataDrivenTests.First");
    String[] shapes = m_testContext.DataRow["Shape"] as String[];
    foreach (String shape in shapes)
    {
        Console.WriteLine("The shape is " + shape);
    }

    Int32[] lengths = m_testContext.DataRow["Length"] as Int32[];
    foreach (int length in lengths)
    {
        Console.WriteLine("The length is " + length.ToString());
    }

    String description = (String)m_testContext.DataRow["Description"];
    Boolean desktopInteract = (Boolean)m_testContext.DataRow["DesktopInteract"];
    UInt32 processId = (UInt32)m_testContext.DataRow["ProcessId"];
    Log.Comment("Themes service is running on process " + processId.ToString());
    Log.Comment("Themes service description: " + description);
}
```

例では、複数の行に複数のデータ ソースを指定する方法も示します。 もちろん、(下図のように)、1 行で、データ ソースを指定した可能性がありますが、上記に示すように構成要素を使用して、読みやすさを大幅に改善できます。

## <a name="span-idspecifyingdatasourceonasinglelinespanspan-idspecifyingdatasourceonasinglelinespanspan-idspecifyingdatasourceonasinglelinespanspecifying-datasource-on-a-single-line"></a><span id="Specifying_DataSource_on_a_single_line"></span><span id="specifying_datasource_on_a_single_line"></span><span id="SPECIFYING_DATASOURCE_ON_A_SINGLE_LINE"></span>1 行にデータ ソースを指定します。


```cpp
[DataSource("Table:CSharpAdvancedDataDrivenTests.xml#FirstTable;WMI:SELECT ProcessId FROM Win32_Service WHERE Name='Themes'")]
```

再反復処理するだけです:**テスト メソッドはそれぞれが、各個々 のデータ ソースによって生成されたデータ セットの組み合わせの拡張を n 方法の 1 回実行する**します。 たとえば、上の管理対象の例で安全に想定していますが 1 つだけのテーマ サービスを実行していることと、指定されたテーブルのデータ ソースで 3 つの行があることを知ること、テスト メソッドが 3 回呼び出されます (1 X 3)。 ネイティブの例の場合、SecondTable テスト メソッドでは、いくつか 2 つのテーブル データソースを指定します。 最初のテーブルに 3 つの行が含まれていて、2 番目のテーブルには、4 行が含まれています。 そのため、テスト メソッドが呼び出される 12 回 (3 X 4)。

## <a name="span-idconstraintsthatapplywhilespecifyingmultipledatasourcesspanspan-idconstraintsthatapplywhilespecifyingmultipledatasourcesspanspan-idconstraintsthatapplywhilespecifyingmultipledatasourcesspanconstraints-that-apply-while-specifying-multiple-datasources"></a><span id="Constraints_that_apply_while_specifying_Multiple_DataSources"></span><span id="constraints_that_apply_while_specifying_multiple_datasources"></span><span id="CONSTRAINTS_THAT_APPLY_WHILE_SPECIFYING_MULTIPLE_DATASOURCES"></span>複数のデータ ソースを指定するときに適用される制約


制約は、テーブルでは、データ ソースをベースに複数のデータ ソースの仕様を指定する場合にのみに適用されます。 **データ ソースのテーブル**テーブルとして指定する必要があります:&lt;XML ファイルへのパスを reative&gt;\#&lt;TableId&gt;します。 TAEF"TableId"が別のメタデータとして提供されることを検出としても、データ ソースが 1 つのテーブル ベースのデータ ソースであり、続行ことと想定されます。

 

 





