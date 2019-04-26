---
title: PICT データ ソース
description: PICT データ ソース
ms.assetid: 75D3E086-C277-410d-B474-742A47ABB6AC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb421c98d19598f40c31d140e2039b6271636666
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355470"
---
# <a name="pict-data-source"></a>PICT データ ソース


TAEF の基本的な実行に精通していることを確認してください作成者テストが、このセクションに進む前に使用する方法。

## <a name="span-idpictbackgroundandreferencesspanspan-idpictbackgroundandreferencesspanspan-idpictbackgroundandreferencesspanpict-background-and-references"></a><span id="PICT_Background_and_References"></span><span id="pict_background_and_references"></span><span id="PICT_BACKGROUND_AND_REFERENCES"></span>PICT 背景と参照


PICT ペアワイズ独立した組み合わせのテストの略です。 **PICT 各、パラメーターのバリエーションを個別に指定することができます。** たとえば、API をテストする場合は、2 つのパラメーターに依存します。ファイル名と FileExtension では、考えられる、使用可能なバリエーションをファイル名と FileExtensions を個別に渡すようになります。

-   ファイル名: a、z12390、Realllyreallyreallylonglonglonglonglonglonglonglonglonglong、normallength
-   FileExtension: txt、png、bat、doc、exe、bmp、wav

ここで、ことを確認できます、**ブルート フォースの組み合わせの拡張**、上記 (4 X 7 = 28) の**策略を簡単に取得できます**の一覧に追加する詳細のバリエーションについて考えるとき。 このようなテスト ケース シナリオで**PICT は入力パラメーターより包括的な組み合わせのカバレッジを取得するパラメーターの結果のコンパクトなセットを生成することによって、多くの価値を追加する可能性があります。**

## <a name="span-idpictsupportintaefspanspan-idpictsupportintaefspanspan-idpictsupportintaefspanpict-support-in-taef"></a><span id="PICT_Support_in_TAEF"></span><span id="pict_support_in_taef"></span><span id="PICT_SUPPORT_IN_TAEF"></span>PICT TAEF サポート


TAEF は、PICT ベースのテスト用の組み込みのサポートを提供します。

これを活用するには、通常どおりに pict.exe の入力モデル ファイルを記述します。 参照してください、\*上記の例のフォルダー内の .txt ファイル。 PICT で期待どおりに、モデル ファイルのため最初などのコマンド プロンプトでテストすることを実行する場合に便利な場合があります。

``` syntax
pict.exe <model file> [/e:<seed file>]
```

Pict.exe は TAEF の最新リリースの共有のバイナリの残りの部分で使用できます。

1 つが完了したら PICT のモデル ファイル (およびシード ファイル) を作成し、それを確認に対して pict.exe コマンド プロンプトで、今すぐマークできます TAEF PICT ドリブン テストしていることを把握できるように、テストします。 慣れている場合は、テーブル ベースの TAEF で使用できるデータ ドリブン テスト、見つかりますこれとよく似ています。

ネイティブ コードの場合:

```cpp
1     class PictExample
2     {
3         TEST_CLASS(PictExample)
4
5         BEGIN_TEST_METHOD(SimpleTest)
6             TEST_METHOD_PROPERTY(L"DataSource", L"pict:PictExample.txt")
7         END_TEST_METHOD()
8
9         BEGIN_TEST_METHOD(TestWithSeed)
10            TEST_METHOD_PROPERTY(L"DataSource", L"pict:TestWithSeed.txt")
11            TEST_METHOD_PROPERTY(L"Pict:SeedingFile", L"TestWithSeed.sed")
12            TEST_METHOD_PROPERTY(L"Pict:Timeout", L"00:01:30")
13        END_TEST_METHOD()
14
15        BEGIN_TEST_METHOD(TestWithFunction)
16            TEST_METHOD_PROPERTY(L"DataSource", L"pict:TestWithFunction.txt")
17        END_TEST_METHOD()
18    };
```

マネージ コードの場合:

```cpp
1     [TestClass]
2     public class CSharpPictExample
3     {
4         [TestMethod]
5         [DataSource("pict:ConstraintsTest.txt")]
6         [TestProperty("Pict:SeedingFile", "ConstraintsTest.seed")]
7         public void ConstraintsTest()
8         {
9             ...
10        }
11
12        [TestMethod]
13        [DataSource("pict:SumofSquareRoots.txt")]
14        public void SumOfSquareRoots()
15        {
16            ...
17        }
18
19        public TestContext TestContext
20        {
21            get { return m_testContext; }
22            set { m_testContext = value; }
23        }
24
25        private TestContext m_testContext;
26    }
```

上記の例に示すように、データ ソースとしてモデル ファイルの名前を指定する必要があります。 **モデル ファイルの名前を付ける必要があります"pict:"** し、これをテスト メソッドのデータ ソースとして指定します。 管理対象のテストが発生した場合と同じように、他のデータ ドリブン テストで TAEF、する必要があります提供 TestContext プロパティを取得し、セット メソッドと、クラスにプライベートの同じインスタンスがあります。

PICT にコマンド オプションを渡す場合は、この目的のメタデータを使用することができます。 Pict.exe のコマンド オプションを TAEF メタデータにマップするのにには、次の表を使用します。


| pict.exe コマンドの構文 |                ネイティブ TAEF メタデータ構文                |           マネージ TAEF メタデータ構文            |
|-------------------------|-----------------------------------------------------------|---------------------------------------------------|
|          /o:3           |        TEST\_METHOD\_PROPERTY(L"Pict:Order", L"3")        |        \[TestProperty("Pict:Order", "3")\]        |
|          /d:、           |   TEST\_METHOD\_PROPERTY(L"Pict:ValueSeparator", L",")    |   \[TestProperty("Pict:ValueSeparator", ",")\]    |
|           /a:           |                                                           | テスト\_メソッド\_(L"Pict: AliasSeparator", L"プロパティ |
|          /n: ~           | TEST\_METHOD\_PROPERTY(L"Pict:NegativeValuePrefix", L"~") | \[TestProperty("Pict:NegativeValuePrefix", "~")\] |
|      /e:test.seed       | TEST\_METHOD\_PROPERTY(L"Pict:SeedingFile", L"test.seed") | \[TestProperty("Pict:SeedingFile", "test.seed")\] |
|           /r            |      テスト\_メソッド\_プロパティ (L"Pict: ランダムな"、"true"の L)      |      \[TestProperty("Pict:Random", "true")\]      |
|          /r:33          |     TEST\_METHOD\_PROPERTY(L"Pict:RandomSeed", L"33")     |     \[TestProperty("Pict:RandomSeed", "33")\]     |
|           /c            |  テスト\_メソッド\_プロパティ (L"Pict: CaseSensitive"、"true"L)   |  \[TestProperty("Pict:CaseSensitive", "true")\]   |

上記のメタデータのいずれかは、優先順位の順序でコマンド プロンプトで、データ ソースのプロパティやテスト、クラス、またはモジュール レベルのメタデータで設定できます。 コマンド プロンプトで設定するとを構文を使用します。

``` syntax
te.exe <test dll> /Pict:Order=3 /Pict:SeedingFile=test.seed
```

メタデータをデータ ソースのプロパティを設定するには、疑問符 (?)、アンパサンドで区切られたメタデータ名のセットでモデル ファイル名を追加のメタデータ値のペアします。 このメソッドを使用する場合、"Pict:"メタデータ名のプレフィックスは省略可能です。 以下に例を示します。

```cpp
TEST_METHOD_PROPERTY(L"DataSource", L"Pict:model.txt?Order=3&CaseSensitive=true&Random=true")
```

バック グラウンドで TAEF は PICT に、入力モデル ファイルとコマンド オプションを指定し、結果を取得します。 PICT では、エラーまたは警告が生成される場合、によって TAEF 警告としてこれらのログ記録わかります。 PICT を生成する結果の出力行ごとに TAEF が問題でテストを再呼び出されます。

既定値が変更されます"Pict: RandomSeed"値の設定"Pict: ランダムな"から false を true にします。 これにより、明示的に設定できます"Pict: ランダムな"を"Pict: RandomSeed"を無視する TAEF を取得する場合は false にします。

**モデル ファイルを実行し、指定したファイルの入力をシード PICT.exe の許可されている既定のタイムアウトは、5 分です。** 指定することで、CPP 上記の例で示すように、このタイムアウトをオーバーライドすることができる場合は、モデル ファイルは複雑ですし、結果を返す PICT.exe まで 5 分よりも時間が必要に、 **"Pict: Timeout"** メタデータ。 例では、1.5 分のタイムアウトは、標準を使用して指定[TAEF タイムアウト](taef-timeouts.md)形式。 その他の PICT メタデータと同様に「Pict: タイムアウト」のメタデータが継承され、そのため、クラス全体またはモジュールに対して指定できます。

値にアクセスできます、データを特定の呼び出し中にテスト メソッドとその関連付けられたセットアップおよびクリーンアップ メソッドから同じ方法で TAEF - TestData クラスを使用してネイティブ コードとの TestContext を使用してでベース テーブルのデータ ドリブン テストの場合と同様マネージ コードようになります。

ネイティブ コードの場合:

```cpp
1     void PictExample::SimpleTest()
2     {
3         String valueA;
4         if (SUCCEEDED(TestData::TryGetValue(L"A", valueA)))
5         {
6           Log::Comment(L"A retrieved was " + valueA);
7         }
8
9         String valueB;
10        if (SUCCEEDED(TestData::TryGetValue(L"B", valueB)))
11        {
12            Log::Comment(L"B retrieved was " + valueB);
13        }
14
15        String valueC;
16        if (SUCCEEDED(TestData::TryGetValue(L"C", valueC)))
17        {
18            Log::Comment(L"C retrieved was " + valueC);
19        }
20
21        unsigned int index;
22        if (SUCCEEDED(TestData::TryGetValue(L"index", index)))
23        {
24            Log::Comment(String().Format(L"At index %d", index));
25        }
26    }
```

マネージ コードの場合:

```cpp
1      [TestClass]
2      public class CSharpPictExample
3      {
4          [TestMethod]
5          [DataSource("pict:ConstraintsTest.txt")]
6          public void ConstraintsTest()
7          {
8              Log.Comment("A is " + m_testContext.DataRow["A"]);
9              Log.Comment("B is " + m_testContext.DataRow["B"]);
10             Log.Comment("C is " + m_testContext.DataRow["C"]);
11             Log.Comment("D is " + m_testContext.DataRow["D"]);
12
13             UInt32 index = (UInt32)m_testContext.DataRow["Index"];
14             Log.Comment("At index " + index.ToString());
15        }
16
17        [TestMethod]
18        [DataSource("pict:SumofSquareRoots.txt")]
19        public void SumOfSquareRoots()
20        {
21             Log.Comment("A is " + m_testContext.DataRow["A"]);
22             Log.Comment("B is " + m_testContext.DataRow["B"]);
23
24             UInt32 index = (UInt32)m_testContext.DataRow["Index"];
25             Log.Comment("At index " + index.ToString());
26        }
27
28        public TestContext TestContext
29        {
30             get { return m_testContext; }
31             set { m_testContext = value; }
32        }
33
34        private TestContext m_testContext;
35    }
```

まったく同様に、TAEF でデータ ドリブン テストに"Index"は予約されていないパラメーター名として使用する必要があります。 インデックスは、暗黙的にはテスト メソッドの呼び出しのインデックスと、テストでは、その必要がある場合は、テスト メソッドからアクセスできます。

**テストをベース PICT が発生した場合に注意しても、すべてのパラメーターのデータ型と見なされます WEX::Common::String (ネイティブ) String(managed) または VT\_BSTR(script) します。** 変換と解釈は、ユーザーに一任されます。

TAEF を使用して、PICT ベースのテストを作成したら、これでは、コマンド プロンプトから呼び出すこととすべての TAEF を提供するコマンド機能を適用: のような **/list**が生成されるすべてのテスト メソッドの一覧を取得するにはPICT データとして出力を使用して **/listproperties**メソッド名などに関連付けられているメタデータとデータ値と共に、テストの一覧を取得します。重要な**注開始する前に、その pict.exe がパスを確認します。**

以下は例です。

``` syntax
te Examples\CPP.Pict.Example.dll /list /name:*SimpleTest*
Test Authoring and Execution Framework v2.9.3k for x86
        f:\ Examples\CPP.Pict.Example.dll
            WEX::TestExecution::Examples::PictExample
                WEX::TestExecution::Examples::PictExample::SimpleTest#0
                WEX::TestExecution::Examples::PictExample::SimpleTest#1
                WEX::TestExecution::Examples::PictExample::SimpleTest#2
                WEX::TestExecution::Examples::PictExample::SimpleTest#3
                WEX::TestExecution::Examples::PictExample::SimpleTest#4
                WEX::TestExecution::Examples::PictExample::SimpleTest#5
                WEX::TestExecution::Examples::PictExample::SimpleTest#6
                WEX::TestExecution::Examples::PictExample::SimpleTest#7
                WEX::TestExecution::Examples::PictExample::SimpleTest#8
                WEX::TestExecution::Examples::PictExample::SimpleTest#9
                WEX::TestExecution::Examples::PictExample::SimpleTest#10
                WEX::TestExecution::Examples::PictExample::SimpleTest#11
                WEX::TestExecution::Examples::PictExample::SimpleTest#12
                WEX::TestExecution::Examples::PictExample::SimpleTest#13
                WEX::TestExecution::Examples::PictExample::SimpleTest#14
                WEX::TestExecution::Examples::PictExample::SimpleTest#15
                WEX::TestExecution::Examples::PictExample::SimpleTest#16
                WEX::TestExecution::Examples::PictExample::SimpleTest#17
                WEX::TestExecution::Examples::PictExample::SimpleTest#18
                WEX::TestExecution::Examples::PictExample::SimpleTest#19
                WEX::TestExecution::Examples::PictExample::SimpleTest#20
                WEX::TestExecution::Examples::PictExample::SimpleTest#21
                WEX::TestExecution::Examples::PictExample::SimpleTest#22
                WEX::TestExecution::Examples::PictExample::SimpleTest#23
```

詳細の選択条件について (選択/と/name) 選択 wiki ページを参照してください。

``` syntax
te Examples\Csharp.Pict.Example.dll /listproperties /select:"@Name='*SumofSquare*'
                    and @Data:index>10
Test Authoring and Execution Framework v2.9.3k for x86
        f:\ Examples\CSharp.Pict.Example.dll
            WEX.Examples.CSharpPictExample
                WEX.Examples.CSharpPictExample.SumOfSquareRoots#11
                        Property[DataSource] = pict:SumofSquareRoots.txt
                        Data[a] = 1
                        Data[b] = ~-1
                WEX.Examples.CSharpPictExample.SumOfSquareRoots#12
                        Property[DataSource] = pict:SumofSquareRoots.txt
                        Data[a] = 2
                        Data[b] = ~-1
```

上記の例では、インデックスを使用してを選択する方法を示します。 できますを選択するデータ値に基づきます。

``` syntax
te Examples\Csharp.Pict.Example.dll /listproperties /select:"@Name='*SumofSquare*'
                    and (@Data:A='1' and @Data:B='1')"
Test Authoring and Execution Framework v2.9.3k for x86
        f:\ Examples\CSharp.Pict.Example.dll
            WEX.Examples.CSharpPictExample
                WEX.Examples.CSharpPictExample.SumOfSquareRoots#8
                        Property[DataSource] = pict:SumofSquareRoots.txt
                        Data[a] = 1
                        Data[b] = 1
```

## <a name="span-idpictresultcachingspanspan-idpictresultcachingspanspan-idpictresultcachingspanpict-result-caching"></a><span id="PICT_Result_Caching"></span><span id="pict_result_caching"></span><span id="PICT_RESULT_CACHING"></span>PICT 結果のキャッシュ


いくつかモデル ファイルは、非常に複雑な発生してしまうし、Pict.exe によって処理に長い時間がかかります。 TAEF が Te.exe の特定の実行中に結果をキャッシュすることによって、結果の処理時間を軽減しようとするとします。 後続のテストを実行する同じ実行では、同じモデルとシード ファイルの組み合わせを参照している場合、TAEF はキャッシュされた結果を使用します。 既定では、各実行の最後にキャッシュされた結果削除します。

後続の実行でキャッシュされた結果の利用を継続するかどうか、可能性がありますを指定する、"/persistPictResults"実行中に、コマンド プロンプト オプション。 指定したときに"/persistPictResults"すべての後続の実行はキャッシュされた結果を使用して場合、モデルおよびシードのファイルが変更されていませんが、コマンドの最初の実行は pict.exe を実際に実行され、時間がかかる場合があります。 **注:指定する必要があります"/persistPictResults"その後の実行。指定しない後続の実行の実行を最後にキャッシュされた結果が削除されます。**

PICT を永続化の結果、既定では実行したいものは、キャッシュされたデータを使用して、場合は、te の一部として設定することがあります\_cmd 環境変数の下に示すように実行するたびにこれを指定する必要がなくなります。 参照してください[テストの実行](executing-tests.md)te の詳細については\_cmd.

``` syntax
set te_cmd = /persistPictResults
```

キャッシュされた結果ファイルは、Te.exe が起動されてから Te.exe へのアクセスがある場合に、% %temp% ディレクトリまたは現在の実行ディレクトリに"TAEF PICT"がという名前のフォルダーに格納されます。 結果は不整合な状態にする必要がありますのみの時間では、Ctrl + C を実行中にヒットしたかどうかです。 このような場合は、TAEF は、キャッシュされた結果を削除しようとしていますができるようにする場合は、効果にエラーが表示されます。 エラーは、キャッシュされた結果の場所を削除することを求められます。 実行に失敗すると、後続のテストで定義されていないか正しくない動作する可能性があります。

TAEF で組み込みの PICT サポート両方 PICT 機能と、テスト自動化で TAEF 機能を最大限に活用することができますようになりました。

## <a name="span-iddatasourceasaresourcespanspan-iddatasourceasaresourcespanspan-iddatasourceasaresourcespandatasource-as-a-resource"></a><span id="DataSource_as_a_Resource"></span><span id="datasource_as_a_resource"></span><span id="DATASOURCE_AS_A_RESOURCE"></span>リソースとしてデータ ソース


テスト モジュールで、リソースとして PICT モデルとシード処理のファイルを追加できます。

ネイティブ コードでこれはデータ ソースのメタデータでファイル名の代わりに、リソース名を指定することによって行われます。 以下に例を示します。

```cpp
BEGIN_TEST_METHOD(ResourceNameDataSource)
    TEST_METHOD_PROPERTY(L"DataSource", L"Pict:MyModelResourceName?SeedingFile=MySeedingResourceName")
END_TEST_METHOD()
```

"MyModelResourceName"と"MySeedingResourceName"は、.rc ファイルで定義されているリソースの名前です。 とは異なり、データ ファイルをする必要があるリソースの種類[データ ソースのテーブル](table-data-source.md)リソースの種類がデータ ソースにする必要がある\_XML。

```cpp
MyModelResourceName DATAFILE "model.txt"
MySeedingResourceName DATAFILE "seed.txt"
```

データ ソースのメタデータ値は、モデルがファイルの場合と同じです。 同様に、ネイティブ コードで行うことができます、リソース名、ファイル名と同じであります。 TAEF まずデータ ソースの名前を持つ実際のファイルの存在を検索します。 ファイルが見つからない場合は、test モジュールのリソースを参照して続行します。 リソースに格納されているデータ ソースを変更するには、再コンパイルする必要があります、ために、開発中に、データ ソース ファイルをテスト dll と同じ場所にコピーしてこの設計を利用できます (と名前付けと同じファイル名であるリソース名)。 完了したら、テスト (コピーではなく) ファイルに移動、コードのディレクトリと、リソースの埋め込みを再コンパイルします。









