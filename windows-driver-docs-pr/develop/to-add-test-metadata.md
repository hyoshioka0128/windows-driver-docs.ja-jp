---
ms.assetid: 8BADC31C-6446-41FA-82F3-F46D66954481
title: テスト メタデータを追加する方法
description: Windows Driver Kit (WDK) と Test Authoring and Execution Framework (TAEF) を使って、Windows 8 用のテスト コンテンツを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d28281ed52474270cdd340d9bd9cf7e03db7e4a2
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364208"
---
# <a name="how-to-add-test-metadata"></a>テスト メタデータを追加する方法

Windows 8 の Windows Driver Kit (WDK) では、テスト コンテンツの作成に [Test Authoring and Execution Framework (TAEF)](https://docs.microsoft.com/windows-hardware/drivers/taef/index) が使われます。 TAEF テストは、複数のメソッドを含むダイナミック リンク ライブラリ (DLL) として実装されたオブジェクトで、各メソッドは特定のテスト シナリオにマップされています。 TAEF オブジェクトは、関連するメソッドを組み合わせてテストのグループを作ります。 各テストに対して、テストについて説明する一連のメタデータがあります。 テストの移植性とカプセル化を向上させるため、TAEF はテストのメタデータをテスト オブジェクト自体と共に格納します。 ドライバー テスト テンプレートを使って独自のドライバー テストを作った場合、ドライバー テストを利用可能にして Visual Studio を使って展開できるように、このメタデータを追加する必要があります。

### <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>前提条件

-   ドライバー テスト テンプレートのいずれかを使って作ったドライバー テストのソース コード。 詳しくは、「[ドライバー テスト テンプレートを使ってドライバー テストを作成する方法](how-to-write-a-driver-test-.md)」をご覧ください。

### <a name="span-idto_add_test_metadata_attributesspanspan-idto_add_test_metadata_attributesspanspan-idto_add_test_metadata_attributesspanto-add-test-metadata-attributes"></a><span id="To_add_test_metadata_attributes"></span><span id="to_add_test_metadata_attributes"></span><span id="TO_ADD_TEST_METADATA_ATTRIBUTES"></span>テスト メタデータ属性を追加するには

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
        TEST_METHOD_PROPERTY(L"Kits.Drivers", L"TRUE")
        TEST_METHOD_PROPERTY(L"Kits.Parameter", L"DQ")
        TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Description", L"A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678")
        TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Default", L"INF::OriginalInfFileName='%InfFileName%'")  
        TEST_METHOD_PROPERTY(L"RebootPossible", L"true")
        // TODO: Required properties to be customized to match your test requirements
        TEST_METHOD_PROPERTY(L"Description", L"Plug and Play Surprise Remove Generated Template")
        TEST_METHOD_PROPERTY(L"Kits.DisplayName", L"My Plug and Play Surprise Remove Test") 
        TEST_METHOD_PROPERTY(L"Kits.Category", L"My Test Category")
        // Optional properties for driver tests
        TEST_METHOD_PROPERTY(L"Kits.Drivers.ResultFile", L"TestTextLog.log")
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
        [TestProperty("Kits.Drivers", "TRUE")]
        [TestProperty("Kits.Parameter", "DQ")]
        [TestProperty("Kits.Parameter.DQ.Description", "A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678")]
        [TestProperty("Kits.Parameter.DQ.Default", "INF::OriginalInfFileName='%InfFileName%'")]
        // TODO: Required properties to be customized to match your test requirements.
        [TestProperty("Description", "Plug and Play Surprise Remove Generated Template")]
        [TestProperty("Kits.DisplayName", "My Plug and Play Surprise Remove Test")]
        [TestProperty("Kits.Category", "My Test Category")]
        [TestProperty("RebootPossible", "true")]
        // Optional properties (see Windows Driver Kit documentation for additional optional properties):
        [TestProperty("Kits.Drivers.ResultFile", "TestTextLog.log")]</code></pre></td>
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
        &lt;method name="PlugAndPlaySurpriseRemoveTest"&gt;
        &lt;!-- Required properties for ERT--&gt;
        &lt;TestMethodProperty name="Kits.Drivers" value="TRUE"/&gt;
        &lt;TestMethodProperty name="Kits.Parameter" value="DQ"/&gt;
        &lt;TestMethodProperty name="Kits.Parameter.DQ.Description" value="A WDTF SDEL query that is used to identify the target device(s) - https://go.microsoft.com/fwlink/p/?linkid=232678"/&gt;
        &lt;TestMethodProperty name="Kits.Parameter.DQ.Default" value="INF::OriginalInfFileName='%InfFileName%'"/&gt;
        &lt;TestMethodProperty name="RebootPossible" value="true" /&gt;
        &lt;!-- TODO: Properties to be customized to match your test requirements --&gt;
        &lt;TestMethodProperty name="Description" value="Plug and Play Surprise Remove Generated Template"/&gt;
        &lt;TestMethodProperty name="Kits.DisplayName" value="My Plug and Play Surprise Remove Test"/&gt;
        &lt;TestMethodProperty name="Kits.Category" value="My Test Category"/&gt;
        &lt;!-- Optional properties for ERT--&gt;
        &lt;TestMethodProperty name="Kits.Drivers.ResultFile" value="TestTextLog.log"/&gt;
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
      &lt; TestProperty name="Description" value= "This test cycles the system through various sleep states and performs IO on devices before and after each sleep state cycle"/&gt;
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
      
     TEST_METHOD_PROPERTY(L"Description", L"Plug and Play Surprise Remove Generated Template")</code></pre></td>
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
      
     &lt; TestProperty name="Kits.DisplayName" value="Sleep with IO Before and After"/&gt;</code></pre></td>
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

      TEST_METHOD_PROPERTY(L"Kits.DisplayName", L"My Plug and Play Surprise Remove Test") </code></pre></td>
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

    &lt;ModuleProperty name="Kits.Parameter" value="TM"/&gt;</code></pre></td>
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

    TEST_METHOD_PROPERTY(L"Kits.Parameter", L"DQ")</code></pre></td>
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
      
    &lt; TestProperty name="Kits.Parameter.TM.Description" value="Test mode parameter: Logo or Simple"/&gt; </code></pre></td>
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

    TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Description", L"A WDTF SDEL query that is used to identify the target device(s)")</code></pre></td>
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

    &lt; TestProperty name="Kits.Parameter.TM.Default" value="Logo"/&gt;</code></pre></td>
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

     TEST_METHOD_PROPERTY(L"Kits.Parameter.DQ.Default", L"INF::OriginalInfFileName='%InfFileName%'")  </code></pre></td>
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
      
    &lt; TestProperty name="Kits.Drivers" value=""/&gt;</code></pre></td>
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

     TEST_METHOD_PROPERTY(L"Kits.Drivers", L"TRUE")</code></pre></td>
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
      
    &lt; TestProperty name="Kits.Category" value="Logo\Device Fundamentals"/&gt;</code></pre></td>
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

    TEST_METHOD_PROPERTY(L"Kits.Category", L"My Test Category")</code></pre></td>
    </tr>
    </tbody>
    </table>

    <span id="Deploymentitem"></span><span id="deploymentitem"></span><span id="DEPLOYMENTITEM"></span>**Deploymentitem**  
    テストの依存関係としてファイルやフォルダーを識別します。 テストの実行に必要な任意のリソースが含まれる場合があります。 このメタデータの使用について詳しくは、「[項目メタデータの展開](https://docs.microsoft.com/windows-hardware/drivers/taef/deploymentitem-metadata)」をご覧ください。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ドライバー テスト テンプレートを使ってドライバー テストを作成する方法](how-to-write-a-driver-test-.md)
 

 






