---
title: アレイ サポート データ ドリブン テストの例
description: アレイ サポート データ ドリブン テストの例
ms.assetid: ECCDE395-C887-4485-8C8F-312EFCFD16A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80891fa370f9e172e713001cd3582ba7886965e3
ms.sourcegitcommit: 1d531bf9d02653fdf9ad728126d68b8acb86182e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/29/2020
ms.locfileid: "87402291"
---
# <a name="array-support-data-driven-test-example"></a>アレイ サポート データ ドリブン テストの例


このセクションでは、例によるデータドリブンテストの高度な機能について説明します。 まだ基本について説明している場合は、[単純なデータドリブンの例](data-driven-testing.md)から始めることをお勧めします。

参照される例:

-   ArraySupportDataDrivenExample

-   CSharpDataDrivenArraySupportExample

前のセクションでは、データドリブンテストの作成と実行の基本について説明しました。 次の一覧では、TAEF データドリブンテストの意味での**配列**の意味について説明します。

-   **配列は可変長で、1つのパラメーターとして扱われる要素の同種の型セットです。**
-   **配列型を指定するには、ParameterTypes ブロックでパラメーターの型を明示的に指定し、Array = "true" 属性を追加する必要があります。**

サポートされているパラメーターの型は、「[テーブルデータソースのパラメーターの型](parameter-types-in-table-data-sources.md)」に記載されています。

その他のデータ型が指定されている場合、テストでは警告がスローされ、それが文字列であると見なされます。 配列の場合、データ型は文字列型であると見なされ \[ \] ます。

次の例は、パラメーターが基本型の1つの配列であることを指定する方法を示しています。 配列の場合、既定の型は許可されないことに注意してください。型を明示的に指定し、パラメーターの**配列**属性を true に設定する必要があります。

```cpp
1  <?xml version="1.0"?>
2  <Data>
3    <Table Id="ArraySupportTable">
4      <ParameterTypes>
5        <ParameterType Name="Size" Array="true">int</ParameterType>
6        <ParameterType Name="Color" Array="true">String</ParameterType>
7      </ParameterTypes>
8      <Row>
9        <Parameter Name="Size">4</Parameter>
10       <Parameter Name="Color">White</Parameter>
11     </Row>
12     <Row>
13       <Parameter Name="Size">
14         <Value>4</Value>
15         <Value>6</Value>
16         <Value>8</Value>
17       </Parameter>
18       <Parameter Name="Color">
19         <Value>Red</Value>
20         <Value>Green</Value>
21         <Value>Blue</Value>
22       </Parameter>
23     </Row>
24     <Row>
25       <Parameter Name="Size">
26         <Value>9</Value>
27         <Value>12</Value>
28         <Value>16</Value>
29       </Parameter>
30       <Parameter Name="Color">Orange</Parameter>
31     </Row>
32     <Row>
33       <Parameter Name="Size">9</Parameter>
34       <Parameter Name="Color">
35         <Value>White</Value>
36         <Value>Black</Value>
37       </Parameter>
38     </Row>
39   </Table>
40 </Data>
```

上の例の**値**タグと**配列**属性を確認します。 まず、**サイズ**と**色**の両方のパラメーターに対して型を明示的に指定し、**配列**の属性を**true**に設定して、これらのパラメーターが配列であることを指定する必要があります。 次に、[ ** &lt; 値 &gt; &lt; ] に値を指定します。/値 &gt; **タグ。 &lt; &gt; 特定の行のパラメーターに対して、配列内の任意の数の値を指定するために必要な数の値タグを持つことができます。

上記の XML 例では、9、10、30、および33行に注意してください。 これらのエントリは、1つの値を持つ配列要素です。 つまり、 **1 つの値を持つ配列要素をパラメータータグに直接指定し、追加の Value タグを追加することはでき &lt; &gt; &lt; &gt; ません。** また、**行のパラメーターには値が1つしかない場合でも、1つの要素の配列として扱われ、それ以外の場合は取得できません。**

次に、取得 Api を見てみましょう。

## <a name="span-idnative_retrievalspanspan-idnative_retrievalspanspan-idnative_retrievalspannative-retrieval"></a><span id="Native_Retrieval"></span><span id="native_retrieval"></span><span id="NATIVE_RETRIEVAL"></span>ネイティブ検索


配列要素は、 **wex:: testexecution:: testdataarray &lt; &gt; **テンプレートクラスを使用して、ネイティブコードで取得できます。 詳細については、公開されているヘッダー TestData を参照してください。 **Testdataarray**クラスは、配列要素の有効期間を管理し、配列内の特定の値を取得するのに便利な api を提供します。

```cpp
1  namespace WEX { namespace TestExecution
2  {
3      template <typename T>
4      class TECOMMON_API TestDataArray sealed
5      {
6         ...
7      public:
8          TestDataArray();
9          ~TestDataArray();
10         const size_t GetSize() const;
11         T& operator[](size_t index);
12
13     private:
14        ...
15     };
16 } /* namespace TestExecution */ } /* namespace WEX */
```

**GetSize**を呼び出して配列の長さを取得し、演算子を使用して特定の要素を取得でき **\[\]** ます。

次の例は、これらの関数をコードで使用する方法を示しています。 ネイティブの例の cpp ファイルを考えてみましょう。

```cpp
1  TestDataArray<int> sizes;
2  if (SUCCEEDED(TestData::TryGetValue(L"size", sizes)))
3  {
4      size_t count = sizes.GetSize();
5      for (size_t i = 0; i < count; ++i)
6      {
7          Log::Comment(String().Format(L"Size[%d] retrieved was %d", i, sizes[i]));
8      }
9  }
10
11 TestDataArray<String> colors;
12 if (SUCCEEDED(TestData::TryGetValue(L"color", colors)))
13 {
14     size_t count = colors.GetSize();
15     for (size_t i = 0; i < count; ++i)
16     {
17         Log::Comment(String().Format(L"Color[%d] retrieved was ", i) + colors[i]);
18     }
19 }
```

まず、配列型のローカル TestDataArray を定義します。 この場合、**サイズ**は int 型の配列であり、 **colors**は Wex:: Common:: String 型の配列です。 配列を取得する API は、任意の変数を取得する API に似ています。 **TestData:: TryGetValue**を呼び出し、パラメーターの**サイズ**を取得するように要求し、値をローカル変数の**サイズ**に設定します。

**配列に指定されていないパラメーターを取得しようとすると、エラーが発生してテストが失敗することに注意してください。同様に、配列に要素が1つしかない場合でも、配列を非配列変数に取得しようとすると、エラーが発生します。**

XML 行で配列パラメーターが指定されていない場合、パラメーターを取得しようとすると失敗します。 たとえば、次のような行があるとします。

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

配列であるパラメーター**サイズ**が行内に指定されていないことに注意してください。 コードから**サイズ**を取得しようとすると、失敗したリターンコードが API 呼び出しによって返されます。 これを使用すると、既定の配列値を定義できます。

一方、空の配列を指定するには、次のように**サイズ**に空のパラメータータグを指定します。

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

この場合、**サイズ**を取得しようとすると成功しますが、配列のサイズは0になります。

## <a name="span-idmanaged_retrievalspanspan-idmanaged_retrievalspanspan-idmanaged_retrievalspanmanaged-retrieval"></a><span id="Managed_Retrieval"></span><span id="managed_retrieval"></span><span id="MANAGED_RETRIEVAL"></span>マネージ検索


マネージ取得は、以前とほぼ同じですが、必ず、適切な配列型のローカル変数に値を取得する必要があります。 次の管理された例を考えてみましょう。

```cpp
1  Int32[] sizes = m_testContext.DataRow["Size"] as Int32[];
2  foreach (int size in sizes)
3  {
4          Verify.AreNotEqual(size, 0);
5          Console.WriteLine("Size is " + size.ToString());
6  }
7
8  String[] colors = m_testContext.DataRow["Color"] as String[];
9  foreach (String color in colors)
10 {
11         Console.WriteLine("Color is " + color);
12 }
```

ネイティブ検索と同様に、配列パラメーターが XML 行にまったく指定されていない場合、パラメーターを取得しようとすると、system.string**型の**オブジェクトが返されます。 たとえば、次のような行があるとします。

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

配列であるパラメーター**サイズ**が行内に指定されていないことに注意してください。 コードから**サイズ**を取得しようとすると、API 呼び出しでは、 **DBNull**型のオブジェクトが返されます。 テーブルにそのような値が含まれている場合は、まずコンテキストからオブジェクトにオブジェクトを取得し、オブジェクトの型を**typeof (system.string)** または exepecting の型と比較した後に適切な手順を実行します。

一方、空の配列を指定するには、次のように**サイズ**に空のパラメータータグを指定します。

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

この場合、**サイズ**succeessfully を取得しようとすると、 **system.string \[ \] 型の**空の配列が返されます。

## <a name="span-idexecutionspanspan-idexecutionspanspan-idexecutionspanexecution"></a><span id="Execution"></span><span id="execution"></span><span id="EXECUTION"></span>例外


配列をサポートするデータドリブンテストの実行は、他のデータドリブンテストを実行する場合と変わりありません。 唯一の重要な点は、**配列データパラメーターの場合、選択条件の sematics が変更され、"equals" ではなく "contains" という意味です。**

この意味を確認するために、**カラー**配列に**白**の値が含まれているすべてのデータドリブンテストを選択するとします。 これを行うには、次を実行します。

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

このコマンドは、上記のいずれかのケースで、インデックス0および3を使用してデータドリブンテストを実行し \# \# ます。

たとえば、**カラー**配列に**白**が含まれ、**カラー**配列に**黒**が含まれているテストのみを選択して、インデックス3のデータドリブンテストのみを選択するなど、より複雑なクエリを作成でき \# ます。 練習として、このクエリを自分で作成して実行してみてください。

 

 





