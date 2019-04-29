---
title: ランタイム パラメーター
description: ランタイム パラメーター
ms.assetid: 5CE5D2C3-F967-4318-B799-38CE8E8B15A6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed22b05a45fc5e440ba36f9ef99b9ef375335d52
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324729"
---
# <a name="runtime-parameters"></a>ランタイム パラメーター


TAEF は、テストを実行するランタイム パラメーターを渡すための機能を提供します。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用状況


テストにパラメーターを渡す、te.exe には、このパラメーターを指定して、次の形式でコマンド ライン パラメーターとして。

``` syntax
Te.exe /p:ParameterName1=ParameterValue1  /p:ParameterName2=ParameterValue2
```

パラメーターの値にスペースが含まれている場合は、引用符で囲むと、パラメーター名とパラメーターの値を配置します。

``` syntax
Te.exe /p:"ParameterName3=The quick brown fox jumps over the lazy dog"
```

## <a name="span-idbuilt-inparametersspanspan-idbuilt-inparametersspanspan-idbuilt-inparametersspanbuilt-in-parameters"></a><span id="Built-in_Parameters"></span><span id="built-in_parameters"></span><span id="BUILT-IN_PARAMETERS"></span>組み込みのパラメーター


TAEF では、次のランタイム パラメーターの組み込みサポートがあります。

-   TestDeploymentDir:テスト バイナリ ディレクトリ。
-   TestName:現在実行されているテストの名前。
-   FullTestName:バリエーションの 1 つの修飾子を含むテストの完全名。 これは、TAEF が StartGroup と EndGroup ログだけでの名前です。
-   TestResult:このクリーンアップ関数のスコープ内で実行されたテストの集計の最悪の場合の結果。 ェャォェォラォキォ遶順番は。渡されると、スキップ、NotRun ブロック、失敗しました。 たとえば、クラス内の少なくとも 1 つのテストがブロックされたテストの失敗がない場合は、結果は「ブロックされます」(クリーンアップ関数でのみ使用できます)。

## <a name="span-idaccessingruntimeparametersfromtestsspanspan-idaccessingruntimeparametersfromtestsspanspan-idaccessingruntimeparametersfromtestsspanaccessing-runtime-parameters-from-tests"></a><span id="Accessing_Runtime_Parameters_from_Tests"></span><span id="accessing_runtime_parameters_from_tests"></span><span id="ACCESSING_RUNTIME_PARAMETERS_FROM_TESTS"></span>テストの実行時パラメーターへのアクセス


### <a name="span-idnativetestsspanspan-idnativetestsspanspan-idnativetestsspannative-tests"></a><span id="Native_Tests"></span><span id="native_tests"></span><span id="NATIVE_TESTS"></span>ネイティブのテスト

ランタイム パラメーターの設定、クリーンアップ、およびテスト メソッドで利用できます。 RuntimeParameters::TryGetValue API を使用すると、それらを取得します。

```cpp
String value;
VERIFY_SUCCEEDED(RuntimeParameters::TryGetValue(L"ParameterName3", value));
```

注:テストからランタイム パラメーターを要求するためには、Te.Common.lib ライブラリをリンクする必要があります。

### <a name="span-idmanagedtestsspanspan-idmanagedtestsspanspan-idmanagedtestsspanmanaged-tests"></a><span id="Managed_Tests"></span><span id="managed_tests"></span><span id="MANAGED_TESTS"></span>管理対象のテスト

ランタイム パラメーターは、セットアップとテスト メソッドで使用できます。 を取得するには、クラスの TestContext プロパティを使用します。

例 (クラスまたはアセンブリのセットアップ):

```cpp
[ClassInitialize]

public static void ClassSetup(TestContext context)
{
    String parameterName3  = context.Properties["ParameterName3"];

}
```

同様に、テスト: から

```cpp
[TestMethod]

public void VerifyRuntimeParametersTest()
{
    String parameterName3  = m_testContext.Properties["ParameterName3"].ToString());
}

// Note, that to work with runtime parameters, as well as with your tests,  you need to add
// definition of test context property to your class

private TestContext m_testContext;

public TestContext TestContext
{
    get { return m_testContext; }
    set { m_testContext = value; }
}
```

### <a name="span-idscripttestsspanspan-idscripttestsspanspan-idscripttestsspanscript-tests"></a><span id="Script_Tests"></span><span id="script_tests"></span><span id="SCRIPT_TESTS"></span>スクリプトのテスト

ランタイム パラメーターは、セットアップ、整理およびテスト メソッドで使用できます。 ランタイム パラメーターを取得するには、定義して Te.Common から RuntimeParameters オブジェクトをインスタンス化します。

```cpp
<object id="RuntimeParameters" progid="Te.Common.RuntimeParameters" />
```

RuntimeParameters オブジェクトがインスタンス化されると、RuntimeParameters.Contains を使用することができます ("&lt;ランタイム パラメーター名&gt;") ランタイム パラメーターが指定し、テストに使用可能な場合にクエリするメソッド。 RuntimeParameters.GetValue を使用できますし、true を返す場合 ("&lt;ランタイム パラメーター名&gt;") を取得します。 RuntimeParameters.GetValue(...) がランタイム パラメーターが使用できない場合にスローされることに注意してください。 次の例では、VBScript の例です。

```cpp
       <script language="VBScript">
            <![CDATA[
                Function TestOne()
                    dim param
                    param = "No runtime param"
                    If RuntimeParameters.Contains("param") Then
                         param = RuntimeParameters.GetValue("param")
                    End If
                    Log.Comment("Param is " + param)

                    dim testDir
                    If RuntimeParameters.Contains("testDir") Then
                        testDir = RuntimeParameters.GetValue("TestDir")
                    End If
                    Log.Comment("The test harness is running in " + testDir)
                End Function
            ]] >
        </script>
```

 

 





