---
title: スクリプト言語でテストを作成する
description: スクリプト言語でテストを作成する
ms.assetid: 4F5328E4-4817-4391-BF56-EC9E7F469AA7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c40c7d17649f9cc3274d41b2b33ca766ee1c89a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373022"
---
# <a name="authoring-tests-in-scripting-languages"></a>スクリプト言語でテストを作成する


C++ だけでなく、 C#TAEF がサポートのスクリプト言語でのテストを作成します。

Microsoft COM スクリプト インターフェイスをサポートする任意のスクリプト言語を使用して、スクリプト コンポーネントを作成します。 これらのインターフェイスをサポートするスクリプト言語には、JScript、Microsoft Visual Basic Scripting Edition (VBScript)、PERLScript、PScript、Ruby、および Python が含まれます。

## <a name="span-idcurrentlimitationsofthescripttestauthoringspanspan-idcurrentlimitationsofthescripttestauthoringspanspan-idcurrentlimitationsofthescripttestauthoringspancurrent-limitations-of-the-script-test-authoring"></a><span id="Current_Limitations_of_the_Script_Test_Authoring"></span><span id="current_limitations_of_the_script_test_authoring"></span><span id="CURRENT_LIMITATIONS_OF_THE_SCRIPT_TEST_AUTHORING"></span>現在の制限事項、スクリプトのテストの作成


既定で Windows のみをサポート JScript および VBScript です。

## <a name="span-idscripttestfileformatspanspan-idscripttestfileformatspanspan-idscripttestfileformatspanscript-test-file-format"></a><span id="Script_Test_File_Format"></span><span id="script_test_file_format"></span><span id="SCRIPT_TEST_FILE_FORMAT"></span>スクリプトのテスト ファイルの形式


スクリプト言語のテストでは、TAEF を少し変更した使用[Windows スクリプト コンポーネント](https://docs.microsoft.com/previous-versions/07zhfkh8(v=vs.85))ファイル形式。 次の例では、VBScript や JScript のテスト クラスが含まれたテスト ファイルを示します。

```cpp
1   <?xml version="1.0" ?>
2
3   <!-- Debugging helpers -->
4   <!-- error    Set this to true to display detailed error messages for syntax or run-time errors in the script component.-->
5   <!-- debug    Set this to true to enable debugging. If this debugging is not enabled, you cannot launch the script debugger for a script -->
6   <?component error="true" debug="true"?>
7
8   <package>
9       <!-- Test module metadata -->
10      <ModuleProperty name="Owner" value="Someone"/>
11
12      <!-- Define a test class -->
13      <component id="VBSampleTests">
14          <!-- define and instantiate a logger -->
15          <object id="Log" progid="WEX.Logger.Log" />
16  
17          <!-- include a reference to the logger so you could use the constants defined in logger library -->
18          <reference guid="e65ef678-a232-42a7-8a36-63108d719f31" version="1.0"/>
19
20          <!-- Test class metadata -->
21          <TestClassProperty name="DocumentationUrl" value="http://shelltestkb/"/>
22
23          <public>
24              <!-- Define a test method with metadata -->
25              <method name="TestOne">
26                  <!-- Test method metadata -->
27                  <TestMethodProperty name="Priority" value="1"/>
28              </method>
29  
30              <!-- Define a test method without metadata -->
31              <method name="TestTwo"/>
32         </public>
33
34          <script language="VBScript">
35              <![CDATA[
36                  Function TestOne()
37                      Log.Comment("Calling TestOne")
38                  End Function
39
40                  Function TestTwo()
41                      Log.Comment("Calling TestTwo")
42                  End Function
43              ]] >
44          </script>
45      </component>
46
47      <!-- Define another test class -->
48      <component id="JScriptSampleTests">
49          <object id="Log" progid="WEX.Logger.Log" />
50
51          <!-- need reference to use logger constants -->
52          <reference guid="e65ef678-a232-42a7-8a36-63108d719f31" version="1.0"/>
53
54          <public>
55              <!-- Test setup and cleanup methods are declared using corresponding type = '' attributes -->
56              <method name="ClassSetup" type="TestClassSetup"/>
57              <method name="ClassCleanup" type="TestClassCleanup"/>
58              <method name="MethodSetup"  type="TestMethodSetup"/>
59              <method name="MethodCleanup" type="TestMethodCleanup"/>
60
61              <method name="TestOne"/>
62              <method name="TestTwo"/>
63          </public>
64
65          <!-- Setup and Cleanup methods return false on failure -->
66          <script language="JScript">
67              <![CDATA[
68                  function ClassSetup()
69                  {
70                      Log.Comment("Calling class setup");
71                      return true;
72                  }
73
74                  function ClassCleanup()
75                  {
76                      Log.Comment("Calling class cleanup");
77                      return true;
78                  }
79
80                  function MethodSetup()
81                  {
82                      Log.Comment("Calling method setup");
83                      return true;
84                  }
85
86                  function MethodCleanup()
87                  {
88                      Log.Comment("Calling method cleanup");
89                      return true;
90                  }
91
92                  function TestOne()
93                  {
94                      Log.Comment("Calling TestOne");
95  
96                      // For the purpose of demonstration, declare the test failed
97                      Log.Result(TestResult_Failed);
98                  }
99
100                 function TestTwo()
101                 {
102                     Log.Comment("Calling TestTwo");
103                 }
104             ]] >
105         </script>
106     </component>
107 </package>
```

この例では、XML ファイルですし、通常の XML ヘッダーで開始します。

```cpp
<?xml version="1.0" ?>
```

属性を設定して、ファイルのデバッグの設定を構成する**エラー**と**デバッグ**:

```cpp
<?component error="true" debug="true"?>
```

-   設定**エラー**に*true*スクリプト コンポーネントでの構文または実行時のエラーの詳細なエラー メッセージを表示します。
-   設定**デバッグ**に*true*デバッグを有効にします。 デバッグが有効でない場合は、スクリプトのスクリプト デバッガーを起動することはできません (などで、**デバッグ**JScript コード内でキーワード)。

**&lt;パッケージ&gt;** 要素で囲みますテストのクラス定義を **.wsc**ファイル。 この要素の後は、追加することでモジュール レベルのメタデータを挿入できます**ModuleProperty**要素。

```cpp
<ModuleProperty name = "Owner" value = "Someone"/>
```

**ModuleProperty**要素を含める必要があります、**名前**と**値**属性。

**コンポーネント**要素の開始スクリプトのテスト クラスの宣言。 この要素が、 **id**クラス名に設定されている属性。

後に、**コンポーネント**要素を使用してクラス レベルのメタデータを挿入することができます、 **TestClassProperty**要素。 同様、 **ModuleProperty**要素が必要、**名前**と**値**属性。

この時点では、オブジェクトを作成し、オブジェクトへの参照を定義することができますも。 参照してください[その他のコンポーネント セクション](https://docs.microsoft.com/previous-versions/ye6w00x4(v=vs.85))詳細についてはします。 15、18、49、および XML の例では 52 行参照を初期化する方法を表示する、**かかえるします。Logger.Log**オブジェクト。

**&lt;パブリック&gt;** 要素で、テスト スクリプト モジュールのテスト メソッドの宣言を囲みます。 テスト メソッドの名前を指定することによってテスト メソッドを宣言する、**名前**の属性を **&lt;メソッド&gt;** 要素。 内のテスト メソッドのプロパティを追加することも、 **&lt;メソッド&gt;** 要素。 他のレベルでプロパティと同様に、必要はありません。 ただし、これを追加する場合があります、**名前**と**値**属性。

**&lt;スクリプト&gt;** 要素は、テスト スクリプト言語を識別し、テスト メソッドの実装を囲みます。

**&lt;!\[CDATA\[ \] \] &gt;** セクションに、テストの実際の実装にはスクリプト言語で記述されたコードが含まれます。 宣言されているテスト メソッドを実装するこのセクションで、 **&lt;パブリック&gt; &lt;/public&gt;** セクション。

 

 





