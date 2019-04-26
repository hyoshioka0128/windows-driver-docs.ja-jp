---
title: メタデータ オーバーライド データ ドリブン テストの例
description: メタデータ オーバーライド データ ドリブン テストの例
ms.assetid: F39A556F-1816-4272-ABDE-62164AE09685
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef422f67aeca894b264e45d4013127bbaefa4b82
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355506"
---
# <a name="metadata-overriding-data-driven-test-example"></a>メタデータ オーバーライド データ ドリブン テストの例


このセクションでは、データ ドリブンの例を使用してテストの高度な機能について説明します。 最初にする場合があります、基礎をカバーは引き続き、する場合、[単純なデータ駆動型の例です。](simple-data-driven-test-example.md)

参照されている例:

-   MetadataOverridingDataDrivenExample

-   DataDrivenMetadataOverridingExample

説明したものには、このセクションで取り上げる例と比較すると、[単純なデータ駆動型の例](simple-data-driven-test-example.md) ページで、テストでさまざまなレベルのプロパティが、唯一の違いは、そのメタデータが確認されます追加されています。 基本的なテストを作成する方法の概要を使用できます。

ネイティブの例では、行 5 と 10 では、次のコード例に従います。

```cpp
1   class MetadataOverridingDataDrivenExample
2   {
3      BEGIN_TEST_CLASS(MetadataOverridingDataDrivenExample)
4          ...
5          TEST_CLASS_PROPERTY(L"Priority", L"2")
6      END_TEST_CLASS()
7    
8      BEGIN_TEST_METHOD(DataDrivenTest)
9          ...
10     TEST_METHOD_PROPERTY(L"Owner", L"wex")
11     END_TEST_METHOD()
12  }
```

クラス"MetadataOverridingDataDrivenExample"で定義されているすべてのテストでは、2 の優先順位を持ちます。 ただし、テストが (クラスまたはモジュール) 上のレベルで指定されたすべてのメタデータをオーバーライドできます。 この場合、DataDrivenTest メソッドが 2 の優先順位を引き続き維持しが、「所有者」を「かかえる」を定義します。 これには、いずれかに基づく選択/選択でしたこれ以外のデータ ドリブン テストの場合、これで:"@Priority= 2" またはリンク:"@Owner= 'かかえる'"、し、その中で、テスト メソッドを実行します。 **をデータ ドリブン テストでさらにプロパティをオーバーライドできます、該当するテスト メソッドのレベルは「行」レベルのメタデータを指定することで。**

XML ファイルを見てみましょうか。

```cpp
    1  <?xml version="1.0"?>
    2  <Data>
    3    <Table Id="MetadataTable">
    4      <ParameterTypes>
    5        <ParameterType Name="Size">int</ParameterType>
    6      </ParameterTypes>
    7      <Row Priority="1">
    8        <Parameter Name="Size">4</Parameter>
    9        <Parameter Name="Color">White</Parameter>
    10      </Row>
    11      <Row Owner="C2">
    12        <Parameter Name="Size">10</Parameter>
    13        <Parameter Name="Color">Black</Parameter>
    14      </Row>
    15      <Row Priority="1" Owner="C3">
    16        <Parameter Name="Size">9</Parameter>
    17        <Parameter Name="Color">Orange</Parameter>
    18      </Row>
    19      <Row>
    20        <Parameter Name="Size">9</Parameter>
    21        <Parameter Name="Color">Blue</Parameter>
    22      </Row>
    23    </Table>
    24  </Data>
```

最初の 3 つの行では、例は、特定のデータ値のセットのメタデータを明示的に指定して、いくつかのメタデータをオーバーライドします。 ただし、データの最後のセットには、同じメタデータが含まれるメソッドとしてがあります。優先順位 = 2、所有者 = かかえるします。

選択およびこれらのテストの実行を検討する前にマネージ コードを見てをみましょう。

```cpp
1   [TestClass]
2   public class DataDrivenMetadataOverridingExample
3   {
4      [ClassInitialize]
5      [Priority(2)]
6      public static void MyClassInitialize(Object testContext)
7      {
8      }
9   
9      [TestMethod]
10     ...
11     [TestProperty("Owner", "WEX")]
12     public void DataDrivenTest()
13     {
14        ...
15     }
...
```

上に正確にネイティブの例では、プロパティが模倣されます。

ここで、オーバーライドするをよく理解しておきましょう。

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*overriding*' and @Priority=1"
```

実行します。

-   WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest\#0
-   かかえるします。Examples.DataDrivenMetadataOverridingExample.DataDrivenTest\#2

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*overriding*' and @Priority=1"
```

実行されます。

-   WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest\#0
-   WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest\#2

## <a name="span-idexerciseforthereaderspanspan-idexerciseforthereaderspanspan-idexerciseforthereaderspanexercise-for-the-reader"></a><span id="Exercise_for_the_reader"></span><span id="exercise_for_the_reader"></span><span id="EXERCISE_FOR_THE_READER"></span>リーダーの演習


演習としては、新しいメタデータ値を追加してみてください。 上記の例では、選択条件をさまざまなのみ

``` syntax
/select:"@Name='*overriding*' and @Owner='WEX'"
```

データ駆動型のインデックスを持つテストを実行\#0 と\#マネージとネイティブの両方の例では 3

``` syntax
 /select:"@Name='*overriding*' and @Priority=2"
```

データ駆動型のインデックスを持つテストを実行\#1 と\#3 も管理対象の例で、NonDataDrivenTest を実行します。

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll Examples\CSharp.DataDriven.Example.dll /name:*overriding* /listproperties
    F:\ Examples\CPP.DataDriven.Example.dll
        WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample
                Property[Priority] = 2

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#0
                    Property[Owner] = WEX
                    Property[Priority] = 1
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = White
                    Data[Size] = 4

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#1
                    Property[Owner] = C2
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = Black
                    Data[Size] = 10

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#2
                    Property[Owner] = C3
                    Property[Priority] = 1
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX::TestExecution::Examples::MetadataOverridingDataDrivenExample::DataDrivenTest#3
                    Property[Owner] = WEX
                    Property[DataSource] =  Table:MetadataOverridingDataDrivenExample.xml#MetadataTable

                    Data[Color] = Blue
                    Data[Size] = 9

    F:\ Examples\CSharp.DataDriven.Example.dll
        WEX.Examples.DataDrivenMetadataOverridingExample
                Setup: MyClassInitialize
                Property[Priority] = 2

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#0
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = WEX
                    Property[Priority] = 1

                    Data[Color] = White
                    Data[Size] = 4

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#1
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = C2

                    Data[Color] = Black
                    Data[Size] = 10

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#2
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = C3
                    Property[Priority] = 1

                    Data[Color] = Orange
                    Data[Size] = 9

            WEX.Examples.DataDrivenMetadataOverridingExample.DataDrivenTest#3
                    Property[DataSource] = Table:CSharpDataDrivenMetadataOverridingExample.xml#MetadataTable
                    Property[Owner] = WEX

                    Data[Color] = Blue
                    Data[Size] = 9

        WEX.Examples.DataDrivenMetadataOverridingExample.NonDataDrivenTest
```

 

 





