---
ms.assetid: 8BADC31C-6446-41FA-82F3-F46D66954481
title: テスト メタデータを追加する方法
description: Windows Driver Kit (WDK) と Test Authoring and Execution Framework (TAEF) を使って、Windows 8 用のテスト コンテンツを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b419ea4377228394c78b29925dc500be8d63878e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518330"
---
# <a name="how-to-add-test-metadata"></a>テスト メタデータを追加する方法

Windows 8 の Windows Driver Kit (WDK) では、テスト コンテンツの作成に [Test Authoring and Execution Framework (TAEF)](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439725) が使われます。 TAEF テストは、複数のメソッドを含むダイナミック リンク ライブラリ (DLL) として実装されたオブジェクトで、各メソッドは特定のテスト シナリオにマップされています。 TAEF オブジェクトは、関連するメソッドを組み合わせてテストのグループを作ります。 各テストに対して、テストについて説明する一連のメタデータがあります。 テストの移植性とカプセル化を向上させるため、TAEF はテストのメタデータをテスト オブジェクト自体と共に格納します。 ドライバー テスト テンプレートを使って独自のドライバー テストを作った場合、ドライバー テストを利用可能にして Visual Studio を使って展開できるように、このメタデータを追加する必要があります。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

-   ドライバー テスト テンプレートのいずれかを使って作ったドライバー テストのソース コード。 詳しくは、「[ドライバー テスト テンプレートを使ってドライバー テストを作成する方法](how-to-write-a-driver-test-.md)」をご覧ください。

### <a name="span-idtoaddtestmetadataattributesspanspan-idtoaddtestmetadataattributesspanspan-idtoaddtestmetadataattributesspanto-add-test-metadata-attributes"></a><span id="To_add_test_metadata_attributes"></span><span id="to_add_test_metadata_attributes"></span><span id="TO_ADD_TEST_METADATA_ATTRIBUTES"></span>テスト メタデータ属性を追加するには

1.  必要なテスト プロパティ メタデータをテストのソース ファイルに追加します。
2.  たとえば、ドライバー テスト テンプレートを使って独自の SurpriseRemove テストを作った場合、次のメタデータが追加されます。 テストの説明、表示名、カテゴリ、結果ファイルの属性を編集します。

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>// Declare the test class method DoSurpriseRemove - the main test method within this class
        BEGIN_TEST_METHOD(DoSurpriseRemove)
        // Required properties for driver tests
        TEST_METHOD_PROPERTY(L&quot;Kits.Drivers&quot;, L&quot;TRUE&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.Parameter&quot;, L&quot;DQ&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Description&quot;, L&quot;A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Default&quot;, L&quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;)  
        TEST_METHOD_PROPERTY(L&quot;RebootPossible&quot;, L&quot;true&quot;)
        // TODO: Required properties to be customized to match your test requirements
        TEST_METHOD_PROPERTY(L&quot;Description&quot;, L&quot;Plug and Play Surprise Remove Generated Template&quot;)
        TEST_METHOD_PROPERTY(L&quot;Kits.DisplayName&quot;, L&quot;My Plug and Play Surprise Remove Test&quot;) 
        TEST_METHOD_PROPERTY(L&quot;Kits.Category&quot;, L&quot;My Test Category&quot;)
        // Optional properties for driver tests
        TEST_METHOD_PROPERTY(L&quot;Kits.Drivers.ResultFile&quot;, L&quot;TestTextLog.log&quot;)
        // TODO: (see Windows Driver Kit documentation for additional optional properties)
        END_TEST_METHOD()</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="CSharp"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C#</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>//
        // DoSurpriseRemove is a test method as identified by the [TestMethod] tag. 
        // More methods can be added by following this basic pattern.
        // The name of the function defines the name of the test.
        //
        [TestMethod]
        // Required properties (see Windows Driver Kit documentation for more information):
        [TestProperty(&quot;Kits.Drivers&quot;, &quot;TRUE&quot;)]
        [TestProperty(&quot;Kits.Parameter&quot;, &quot;DQ&quot;)]
        [TestProperty(&quot;Kits.Parameter.DQ.Description&quot;, &quot;A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678&quot;)]
        [TestProperty(&quot;Kits.Parameter.DQ.Default&quot;, &quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;)]
        // TODO: Required properties to be customized to match your test requirements.
        [TestProperty(&quot;Description&quot;, &quot;Plug and Play Surprise Remove Generated Template&quot;)]
        [TestProperty(&quot;Kits.DisplayName&quot;, &quot;My Plug and Play Surprise Remove Test&quot;)]
        [TestProperty(&quot;Kits.Category&quot;, &quot;My Test Category&quot;)]
        [TestProperty(&quot;RebootPossible&quot;, &quot;true&quot;)]
        // Optional properties (see Windows Driver Kit documentation for additional optional properties):
        [TestProperty(&quot;Kits.Drivers.ResultFile&quot;, &quot;TestTextLog.log&quot;)]</code></pre></td>
    </tr>
    </tbody>
    </table>

    Windows スクリプト コンポーネント (.wsc)

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>&lt;!-- Define a test method with metadata: --&gt;
        &lt;method name=&quot;PlugAndPlaySurpriseRemoveTest&quot;&gt;
        &lt;!-- Required properties for ERT--&gt;
        &lt;TestMethodProperty name=&quot;Kits.Drivers&quot; value=&quot;TRUE&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Parameter&quot; value=&quot;DQ&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Parameter.DQ.Description&quot; value=&quot;A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Parameter.DQ.Default&quot; value=&quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;/&gt;
        &lt;TestMethodProperty name=&quot;RebootPossible&quot; value=&quot;true&quot; /&gt;
        &lt;!-- TODO: Properties to be customized to match your test requirements --&gt;
        &lt;TestMethodProperty name=&quot;Description&quot; value=&quot;Plug and Play Surprise Remove Generated Template&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.DisplayName&quot; value=&quot;My Plug and Play Surprise Remove Test&quot;/&gt;
        &lt;TestMethodProperty name=&quot;Kits.Category&quot; value=&quot;My Test Category&quot;/&gt;
        &lt;!-- Optional properties for ERT--&gt;
        &lt;TestMethodProperty name=&quot;Kits.Drivers.ResultFile&quot; value=&quot;TestTextLog.log&quot;/&gt;
        &lt;!-- (see Windows Driver Kit documentation for additional optional properties) --&gt;
        &lt;/method&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

3.  次の表で、テストのプロパティの属性について説明します。 これらの例を、テストのメタデータを編集または追加するときのガイダンスとして使ってください。

    <span id="Description"></span><span id="description"></span><span id="DESCRIPTION"></span>**Description**  
    テストの実行内容の短い説明です。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      &lt; TestProperty name=&quot;Description&quot; value= &quot;This test cycles the system through various sleep states and performs IO on devices before and after each sleep state cycle&quot;/&gt;
    </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]
      
     TEST_METHOD_PROPERTY(L&quot;Description&quot;, L&quot;Plug and Play Surprise Remove Generated Template&quot;)</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="DisplayName"></span><span id="displayname"></span><span id="DISPLAYNAME"></span>**DisplayName**  
    [Driver Test] (ドライバー テスト) に表示されるテストの名前です。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      
     &lt; TestProperty name=&quot;Kits.DisplayName&quot; value=&quot;Sleep with IO Before and After&quot;/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [C++]

      TEST_METHOD_PROPERTY(L&quot;Kits.DisplayName&quot;, L&quot;My Plug and Play Surprise Remove Test&quot;) </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter"></span><span id="kits.parameter"></span><span id="KITS.PARAMETER"></span>**Kits.Parameter**  
    メソッド呼び出しの標準的なパラメーターです。 1 つのテストに複数のパラメーターを含めることができます。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 

    &lt;ModuleProperty name=&quot;Kits.Parameter&quot; value=&quot;TM&quot;/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]

    TEST_METHOD_PROPERTY(L&quot;Kits.Parameter&quot;, L&quot;DQ&quot;)</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter._ParameterName_.Description"></span><span id="kits.parameter._parametername_.description"></span><span id="KITS.PARAMETER._PARAMETERNAME_.DESCRIPTION"></span>**Kits.Parameter.***&lt;パラメーター名&gt;***.Description**  
    パラメーターの説明です。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      
    &lt; TestProperty name=&quot;Kits.Parameter.TM.Description&quot; value=&quot;Test mode parameter: Logo or Simple&quot;/&gt; </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> 
    [C++]

    TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Description&quot;, L&quot;A WDTF SDEL query that is used to identify the target device(s)&quot;)</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Parameter._ParameterName_.Default"></span><span id="kits.parameter._parametername_.default"></span><span id="KITS.PARAMETER._PARAMETERNAME_.DEFAULT"></span>**Kits.Parameter.***&lt;パラメーター名&gt;***.Default**  
    パラメーターの既定値です。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 

    &lt; TestProperty name=&quot;Kits.Parameter.TM.Default&quot; value=&quot;Logo&quot;/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]

     TEST_METHOD_PROPERTY(L&quot;Kits.Parameter.DQ.Default&quot;, L&quot;INF::OriginalInfFileName=&#39;%InfFileName%&#39;&quot;)  </code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Drivers"></span><span id="kits.drivers"></span><span id="KITS.DRIVERS"></span>**Kits.Drivers**  
    このテストが WDK に含まれることを示す属性です。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[Script] 
      
    &lt; TestProperty name=&quot;Kits.Drivers&quot; value=&quot;&quot;/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>[C++]

     TEST_METHOD_PROPERTY(L&quot;Kits.Drivers&quot;, L&quot;TRUE&quot;)</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Kits.Category"></span><span id="kits.category"></span><span id="KITS.CATEGORY"></span>**Kits.Category**  
    テストのカテゴリを説明します。

    <span codelanguage=""></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [Script] 
      
    &lt; TestProperty name=&quot;Kits.Category&quot; value=&quot;Logo\Device Fundamentals&quot;/&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span codelanguage="ManagedCPlusPlus"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">C++</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code> [C++]

    TEST_METHOD_PROPERTY(L&quot;Kits.Category&quot;, L&quot;My Test Category&quot;)</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Deploymentitem"></span><span id="deploymentitem"></span><span id="DEPLOYMENTITEM"></span>**Deploymentitem**  
    テストの依存関係としてファイルやフォルダーを識別します。 テストの実行に必要な任意のリソースが含まれる場合があります。 このメタデータの使用について詳しくは、「[項目メタデータの展開](https://msdn.microsoft.com/Library/Windows/Hardware/Hh439604)」をご覧ください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバー テスト テンプレートを使ってドライバー テストを作成する方法](how-to-write-a-driver-test-.md)
 

 






