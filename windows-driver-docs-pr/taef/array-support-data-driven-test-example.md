---
title: 配列のサポート データ ドリブン テストの例
description: 配列のサポート データ ドリブン テストの例
ms.assetid: ECCDE395-C887-4485-8C8F-312EFCFD16A2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 362c60743ed9db0252e7e42da1f871ba1e530af9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553692"
---
# <a name="array-support-data-driven-test-example"></a>配列のサポート データ ドリブン テストの例


このセクションでは、データ ドリブンの例を使用してテストの高度な機能について説明します。 最初にする場合があります、基礎をカバーは引き続き、する場合、[単純なデータ駆動型の例](data-driven-testing.md)します。

参照されている例:

-   ArraySupportDataDrivenExample

-   CSharpDataDrivenArraySupportExample

前のセクションでは、「データ ドリブン テストの作成と実行の基本です。 次の一覧の意味を説明する**配列**TAEF データ ドリブン テストという意味で。

-   **配列は、可変長の 1 つのパラメーターとして扱われる要素の同種の型のセットです。**
-   **配列型を指定するには、明示的にも存在しないブロックで、パラメーターの型を指定し、配列を追加する必要があります"true"属性を = です。**

サポートされているパラメーターの型が表示されている[ここ](parameter-types-in-table-data-sources.md)します。

他のデータ型が指定されている場合、テストは警告をスローしは文字列であると判断します。 配列の場合、データ型と思われる文字列型である\[\]します。

次の例では、パラメーターが、基本的な型の 1 つの配列であることを指定する方法を示します。 既定の型は許可されません - 配列の場合は明示的にする必要がありますは注意して、型を指定し、設定、**配列**属性にパラメーターを true にします。

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

確認、**値**タグと**配列**上記の例での属性。 まず、する必要があります明示的に指定する型の両方、**サイズ**と**色**パラメーターし、これらのパラメーターを設定して、配列は、**配列**属性を**true**します。 内の値を指定し、 **&lt;値&gt;.&lt;/Value&gt;** タグ。 多くは&lt;値&gt;タグのように、特定の行のパラメーターの配列内の値の任意の数を指定する必要があります。

行 9、10、30、および上記の XML の例で 33 に注意してください。 これらのエントリは、1 つの値を持つ配列の要素です。 つまり、**で直接 1 つの値を持つ配列要素を指定することがあります、&lt;パラメーター&gt;タグを追加せず&lt;値&gt;タグ。** また、**は 1 つの要素の配列として扱われますが、それ以外の場合を取得できません行にパラメーターが 1 つだけの値を持つ場合でもです。**

ここで、検索 Api を見てみましょう。

## <a name="span-idnativeretrievalspanspan-idnativeretrievalspanspan-idnativeretrievalspannative-retrieval"></a><span id="Native_Retrieval"></span><span id="native_retrieval"></span><span id="NATIVE_RETRIEVAL"></span>ネイティブの取得


使用してネイティブ コードで配列の要素を取得できます、 **WEX::TestExecution::TestDataArray&lt; &gt;** テンプレート クラス。 詳細については、パブリッシュされたヘッダー TestData.h を参照してください。 **TestDataArray**クラスが配列の要素の有効期間を管理し、配列内の特定の値を取得する便利な Api を提供します。

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

呼び出すことによって、配列の長さを取得する**GetSize**演算子を使用して、特定の要素を取得することができますと**\[ \]**。

次の例では、コードでこれらの関数を使用する方法を示します。 ネイティブの例では、cpp ファイルを考慮してください。

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

最初に、配列型のローカル TestDataArray を定義します。 この場合、**サイズ**int 型の配列と**色**WEX::Common::String 型の配列です。 配列を取得する API は、任意の変数を取得する 1 つに似ています。 呼び出す**TestData::TryGetValue**、パラメーターを取得するように指示**サイズ**、値をローカル変数に格納および**サイズ**します。

**非配列を取得しようが配列にパラメーターを指定することに注意してくださいでは、エラーが発生し、テストは失敗します。同様に、配列では、1 つの要素のみが持つ場合でも、非配列変数に配列を取得しようとすると、エラーが発生します。**

配列パラメーターがまったく指定 XML の行にしない場合、パラメーターを取得しようとするは失敗します。 たとえば、行の検索などの場合。

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

注意パラメーター**サイズ**行では、配列が指定されていません。 取得しようとした場合**サイズ**コードから API の呼び出しは失敗のリターン コードを返します。 既定値は配列を定義するのにには、これを使用できます。

空のパラメーターのタグを指定することで、空の配列を指定する一方で**サイズ**次のようにします。

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

取得を試行する場合は、この**サイズ**は成功が、配列のサイズは 0 になります。

## <a name="span-idmanagedretrievalspanspan-idmanagedretrievalspanspan-idmanagedretrievalspanmanaged-retrieval"></a><span id="Managed_Retrieval"></span><span id="managed_retrieval"></span><span id="MANAGED_RETRIEVAL"></span>管理対象の取得


管理対象の取得が以前とほぼ同じまま - 適切な配列型のローカル変数に値を取得することを確認する必要があるだけです。 管理対象の次の例を検討してください。

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

パラメーターが型のオブジェクトを返しますのすべてを取得しようとすると、XML 行で配列パラメーターが指定されていない場合、ネイティブの取得に似ています**System.DBNull**します。 たとえば、行の検索などの場合。

```cpp
       <Row>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

注意パラメーター**サイズ**行では、配列が指定されていません。 取得しようとした場合**サイズ**API 呼び出し、コードから型のオブジェクトが返されます**DBNull**します。 取得してそのコンテキストからオブジェクトに最初に対象のオブジェクトの種類を比較した後に適切な手順を実行することがあります、テーブルのような値があれば、 **typeof(System.DBNull)** またはとしている型exepecting にします。

その一方で、空のパラメーターのタグを指定することで空の配列を指定することがあります**サイズ**次のようにします。

```cpp
       <Row>
         <Parameter Name="Size"></Parameter>
         <Parameter Name="Color">
           <Value>White</Value>
           <Value>Black</Value>
         </Parameter>
       </Row>
```

この場合は、取得を試行**サイズ**succeessfully 型の空の配列を返します**System.Int32\[\]** します。

## <a name="span-idexecutionspanspan-idexecutionspanspan-idexecutionspanexecution"></a><span id="Execution"></span><span id="execution"></span><span id="EXECUTION"></span>実行


データ駆動型の配列をサポートしているテストの実行は、同じ、他のデータ ドリブン テストを実行するからです。 違いののみ重要な点は **"equals"ではなく"contains"を意味する配列のデータ パラメーターの場合、選択条件の変更の sematics します。**

つまりをすべてのデータ ドリブン テストを選択することを想定している、**色**配列に値が含まれています**ホワイト**します。 これを行うには、次のコマンドを実行します。

``` syntax
TE.exe Examples\CSharp.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

``` syntax
TE.exe Examples\CPP.DataDriven.Example.dll /select:"@Name='*Array* And @Data:Color='White'"
```

このコマンドは、データ駆動型のインデックスを持つテストを実行\#0 と\#上記のケースの両方で 3。

テストのみを選択、たとえばより複雑なクエリを作成することができます、**色**配列に含まれる**白い**と**色**が配列に含まれています**黒**、データ駆動型のインデックスを持つテストのみを選択する\#3。 演習として記述し、これを実行してくださいは自分でクエリします。

 

 





