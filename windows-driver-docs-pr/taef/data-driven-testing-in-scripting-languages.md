---
title: スクリプト言語でデータ ドリブン テスト
description: スクリプト言語でデータ ドリブン テスト
ms.assetid: CF60C594-8877-4f09-AF82-9F4CA27123C7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 782808f9c7d86008e84b524312ddbfcd1024658a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559146"
---
# <a name="span-idtaefdata-driventestinginscriptinglanguagesspandata-driven-testing-in-scripting-languages"></a><span id="taef.data-driven_testing_in_scripting_languages"></span>スクリプト言語でデータ ドリブン テスト


このセクションを理解するためにする方法を理解しておく必要がありますあります[スクリプト言語でのテストの作成](authoring-tests-in-scripting-languages.md)です。 このセクションの詳細を説明しません、[さまざまな TAEF データ ドリブン テスト アプローチ](data-driven-testing.md)します。 簡単な概要、さまざまな TAEF データ ドリブン テスト構成を確認してください。

-   [テーブル ベースのデータ ドリブン テスト](table-data-source.md)
-   [WMI ベースのデータ ドリブン テスト](wmi-data-source.md)
-   [PICT ベースのデータ ドリブン テスト](pict-data-source.md)
-   [軽量データ ドリブン テスト](light-weight-data-driven-testing.md)

上記のいずれかのデータ ソースを 1 つ以上のことでデータ ソースの組み合わせを保持することもできます。 参照してください[複数のデータ ソースを指定する](multiple-datasources.md)詳細についてはします。

## <a name="span-idspecifyingthedatasourceinscriptinglanguagespanspan-idspecifyingthedatasourceinscriptinglanguagespanspan-idspecifyingthedatasourceinscriptinglanguagespanspecifying-the-data-source-in-scripting-language"></a><span id="Specifying_the_data_source_in_scripting_language"></span><span id="specifying_the_data_source_in_scripting_language"></span><span id="SPECIFYING_THE_DATA_SOURCE_IN_SCRIPTING_LANGUAGE"></span>スクリプト言語でデータ ソースを指定します。


データ ドリブン TAEF でテストを指定することができます、 **DataSource**クラスまたはテスト レベル。 データ ドリブンのクラスでは、データはクラスし、クラスのメソッドのセットアップ、クリーンアップ、およびすべてのテスト メソッドをテストに使用できます。 **DataSource**パラメーターは、データがから取得するかを示す情報。 この値にはデータ ドリブン テストのテーブル ベースの場合は、データが配置されている XML ファイルに XML ファイルと、TableId への相対パスが含まれています。 詳細については、上に示したリンクを参照してください。

次の例は、指定する方法を示します、 **DataSource**プロパティ。

```cpp
1   <?xml version="1.0" ?>
2   <?component error="true" debug="true"?>
3   <package>
4       <component id="VBSampleTests">
5           <object id="Log" progid="WEX.Logger.Log" />
6           <object id="TestData" progid="Te.Common.TestData" />
7
8           <public>
9               <method name="TestOne">
10                  <TestMethodProperty name="DataSource" value="WMI:SELECT Label, Caption FROM Win32_Volume"/>
11              </method>
12
13              <method name="TestTwo">
14                  <TestMethodProperty name="DataSource" value="Table:ScriptExampleTable.xml#MyTable;WMI:SELECT Label, Caption FROM Win32_Volume"/>
15              </method>
16          </public>
17
18          <script language="VBScript">
19              <![CDATA[
20                  Function TestOne()
21                      dim caption
22                      caption = "NoCaption"
23                      Log.Comment("Caption is " + caption)
24
25                      If TestData.Contains("Caption") Then
26                      caption = TestData.GetValue("Caption")
27                      End If
28                      Log.Comment("Caption is " + caption)
29                  End Function
30
31                  Function TestTwo()
32                      Log.Comment("Calling TestTwo")
33                      dim caption
34                      caption = "NoCaption"
35                      Log.Comment("Caption is " + caption)
36
37                      If TestData.Contains("Caption") Then
38                      caption = TestData.GetValue("Caption")
39                      End If
40                      Log.Comment("Caption is " + caption)
41
42                      dim size
43                      If TestData.Contains("Size") Then
44                      size = TestData.GetValue("Size")
45                      End If
46                      Log.Comment("Size is " + CStr(size))
47
48                      dim transparency
49                      If TestData.Contains("Transparency") Then
50                      transparency = TestData.GetValue("Transparency")
51                      End If
52                      Log.Comment("Transparency is " + CStr(transparency))
53                  End Function
54              ]] >
55          </script>
56      </component>
57
58      <component id="JScriptSampleTests">
59          <object id="Log" progid="WEX.Logger.Log" />
60          <object id="TestData" progid="Te.Common.TestData" />
61
62          <TestClassProperty name="DataSource" value="Table:ScriptExampleTable.xml#MyTable"/>
63
64          <public>
65              <method name="ClassSetup" type="TestClassSetup"/>
66              <method name="ClassCleanup" type="TestClassCleanup"/>
67              <method name="MethodSetup"  type="TestMethodSetup"/>
68              <method name="MethodCleanup" type="TestMethodCleanup"/>
69
70              <method name="TestOne"/>
71              <method name="TestTwo">
72                  <TestMethodProperty name="DataSource" value="WMI:SELECT Label, Caption FROM Win32_Volume"/>
73              </method>
74          </public>
75
76          <script language="JScript">
77              <![CDATA[
78                  function ClassSetup()
79                  {
80                      Log.Comment("Calling class setup");
81                      var size;
82                      if(TestData.Contains("Size"))
83                      {
84                          size = TestData.GetValue("Size");
85                      }
86                      Log.Comment("Size is " + size);
87  
88                      var transparency;
89                      if(TestData.Contains("Transparency"))
90                      {
91                          transparency = TestData.GetValue("Transparency");
92                      }
93                      Log.Comment("Transparency is " + transparency);
94                  }
95
96                  function ClassCleanup()
97                  {
98                      Log.Comment("Calling class cleanup");
99                      return true;
100                 }
101
102                 function MethodSetup()
103                 {
104                     Log.Comment("Calling method setup");
105                     var size;
106                     if(TestData.Contains("Size"))
107                     {
108                         size = TestData.GetValue("Size");
109                     }
110                     Log.Comment("Size is " + size);
111
112                     var transparency;
113                     if(TestData.Contains("Transparency"))
114                     {
115                         transparency = TestData.GetValue("Transparency");
116                     }
117                     Log.Comment("Transparency is " + transparency);
118                     return true;
119                 }
120
121                 function MethodCleanup()
122                 {
123                     Log.Comment("Calling method cleanup");
124                     return true;
125                 }
126
127                 function TestOne()
128                 {
129                     Log.Comment("Calling TestOne");
130                     var size;
131                     if(TestData.Contains("Size"))
132                     {
133                         size = TestData.GetValue("Size");
134                     }
135                     Log.Comment("Size is " + size);
136
137                     var transparency;
138                     if(TestData.Contains("Transparency"))
139                     {
140                         transparency = TestData.GetValue("Transparency");
141                     }
142                     Log.Comment("Transparency is " + transparency);
143                 }
144
145                 function TestTwo()
146                 {
147                     Log.Comment("Calling TestTwo");
148                     var caption = "NoCaption";
149                     Log.Comment("Initial caption: " + caption);
150
151                     if(TestData.Contains("Caption"))
152                     {
153                         caption = TestData.GetValue("Caption");
154                     }
155                     Log.Comment("Caption is " + caption);
156
157                     var size;
158                     if(TestData.Contains("Size"))
159                     {
160                         size = TestData.GetValue("Size");
161                     }
162                     Log.Comment("Size is " + size);
163
164                     var transparency;
165                     if(TestData.Contains("Transparency"))
166                     {
167                         transparency = TestData.GetValue("Transparency");
168                     }
169                     Log.Comment("Transparency is " + transparency);
170                 }
171             ]] >
172         </script>
173     </component>
174 </package>
```

上記の例では 6 ~ 60 行宣言およびインスタンス化、 **TestData**データ ドリブン テストのデータへのアクセスを許可するオブジェクト。

**&lt;TestMethodProperty&gt;** と**&lt;TestClassProperty&gt;** タグは、定義する線**DataSource**テストまたはクラス。 VBSampleTests **TestOne**が、 [WMI クエリ](wmi-data-source.md)としてその**DataSource**。 パラメーター**ラベル**と**キャプション**利用**TestOne の**セットアップ、クリーンアップ、およびテスト メソッド。 同じクラスで**TestTwo**が[複数のデータソース](multiple-datasources.md)定義します。 1 つは、[テーブル ベースのデータ ソース](table-data-source.md)、2 番目のベースと同じ WMI **DataSource**として**TestOne**します。

TAEF の各パラメーター セットの組み合わせの展開の生成、 **DataSource**プロパティ。 1 つのパラメーター セットは、各テスト メソッドの呼び出し使用できます。 WMI クエリが結果の 4 つのセットを返す場合 (Win32\_ボリューム) ベースのテーブルの 3 つの行があると**DataSource**、 **TestOne**各 Win32 で 1 回の 4 回の実行は\_WMI クエリによって返されるボリューム。 その一方で、 **TestTwo** 12 (4 X 3) を実行します。 Win32 の組み合わせごとの時間\_ボリューム データとテーブルを指定する行。 データも、関連付けられたセットアップとクリーンアップ メソッドを使用できます。

JScriptSampleTests では、データ ドリブンのクラスの例を確認できます。 例では、指定されているので**DataSource**クラス レベルでは、データがすべてのテスト メソッドのほか、テストとクラス レベルに使用可能なセットアップおよび後処理用のメソッド。 **TestTwo**からデータをデータに基づくクラス内でデータ ドリブン テストには、 **DataSource**でクラス レベルだけでなく、テストからレベルは提供されて**TestTwo**.

## <a name="span-iddatatypesavailableforscripttestsspanspan-iddatatypesavailableforscripttestsspanspan-iddatatypesavailableforscripttestsspandata-types-available-for-script-tests"></a><span id="Data_types_available_for_script_tests"></span><span id="data_types_available_for_script_tests"></span><span id="DATA_TYPES_AVAILABLE_FOR_SCRIPT_TESTS"></span>スクリプトのテストに使用できるデータ型


次のパラメーター型のスクリプト言語を利用できます。 これらは、ベース テーブルのデータ ドリブン テストに指定できる型です。 既定のパラメーターの型は*文字列*または*BSTR* (を表す*VT\_BSTR*)。

セクション[テーブル パラメーターの型は、データ ソースをベース](parameter-types-in-table-data-sources.md)スクリプト言語でのテストを作成する際に (ネイティブおよびマネージ コード) で使用可能なパラメーターの型を表示する方法を示します。

## <a name="span-idexecutingdata-drivenscriptsspanspan-idexecutingdata-drivenscriptsspanspan-idexecutingdata-drivenscriptsspanexecuting-data-driven-scripts"></a><span id="Executing_data-driven_scripts"></span><span id="executing_data-driven_scripts"></span><span id="EXECUTING_DATA-DRIVEN_SCRIPTS"></span>データ ドリブンのスクリプトの実行


**/Listproperties**メタデータだけでなく、テストの各呼び出しに使用されるデータもオプションが一覧表示します。 (を実行している、 **/listproperties**リーダーに全体の dll にオプションを演習として残しておきます)。次の例の呼び出しを選択する**TestOne** VBSampleTests を使用してから、[選択クエリ](selection.md)言語。

``` syntax
f:\spartadev.binaries.x86chk\WexTest\CuE\TestExecution>te Examples\DataDrivenTest.wsc /listproperties /name:VBSampleTests::TestOne*

Test Authoring and Execution Framework v.R10 Build 6.1.6939.0 For x86

        f:\spartadev.binaries.x86chk\WexTest\CuE\TestExecution\Examples\DataDrivenTest.wsc
            VBSampleTests
                VBSampleTests::TestOne#0
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = C:\
                        Data[Label] =

                VBSampleTests::TestOne#1
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = D:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#2
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = F:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#3
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = E:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#4
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = G:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#5
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = H:\
                        Data[Label] = New Volume

                VBSampleTests::TestOne#6
                        Property[DataSource] = WMI:SELECT Label, Caption FROM Win32_Volume

                        Data[Caption] = K:\
                        Data[Label] =
```

**/Listproperties**オプションは、TAEF にテスト メソッドが呼び出されることを示しています。 **VBSampleTests::TestOne** 7 時間 - 各 Win32 に対して 1 回\_ボリューム。 呼び出しごとの TAEF 追加暗黙*インデックス*各呼び出しを区別するためにテスト メソッドにします。 データとメタデータは、テスト メソッドの呼び出しごとの利用もわかります。

情報を使用して、 **/listproperties**オプション、データ値に基づく選択クエリを適用するまたはよりを取得するインデックス値がテストを実行する呼び出しを制御します。 次の例は、キャプションのある呼び出しのみを実行する方法を示しています**e:\\**:。

``` syntax
te Examples\DataDrivenTest.wsc /select:"@Name='VBSampleTests::TestOne*' and @Data:Caption='E:\'"
```

次のコマンドは、同じテストを選択するのに、インデックスを使用します。

``` syntax
te Examples\DataDrivenTest.wsc /select:"@Name='VBSampleTests::TestOne*' and @Data:Index=3"
```

PICT ベースおよびライトがスクリプトのテストでのデータ ドリブン テストの重みが左を使用して、リーダーを演習として。

 

 





