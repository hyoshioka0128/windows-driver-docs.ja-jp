---
title: DeploymentItem メタデータ
description: DeploymentItem メタデータ
ms.assetid: 7F18CD71-F000-4231-9093-82980EB7584D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9d9095f3189b89baf69ab6e1ca428cc6d0c7359
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74863208"
---
# <a name="deploymentitem-metadata"></a>DeploymentItem メタデータ


**DeploymentItem**メタデータは、テストの実行中にテストによって使用されるファイルとフォルダーのファイルとフォルダーの依存関係を識別します。これにより、taef は、これらを識別して適切にコピーできます (たとえば、[クロスコンピューターの実行シナリオ](cross-machine-execution.md)では、 **DeploymentItem**プロパティで識別されるファイルが指定のテストコンピューターに配置されます)

Taef DeploymentItem の実装は、 [VSTS の同様の機能](https://docs.microsoft.com/dotnet/api/microsoft.visualstudio.testtools.unittesting.deploymentitemattribute?redirectedfrom=MSDN&view=mstest-net-1.2.0)によく似ています。

DeploymentItem メタデータは、アセンブリ、クラス、またはテストレベルで適用できます。 DeploymentItem メタデータによって指定された項目は、対応 (アセンブリ、テストクラス、またはテスト) のセットアップの実行時に配置されます。 DeploymentItem metadata が依存関係 (ファイルなど) を指定し、その依存関係が既に転送先に存在する場合、TAEF は CRC 比較を行い、変更された場合にのみファイルをコピーします。 DeploymentItem metadata が依存関係を指定し、依存関係が見つからない場合、テストに失敗するエラーがログに記録されます (または、それに応じて、すべてのテストクラスまたはアセンブリテストが失敗します)。 TAEF は、アセンブリ、クラス、またはテストごとに1回だけファイルを配置します。つまり、データドリブンの場合、アセンブリ、クラス、またはテストの展開のたびに配置が行われません。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>文


<span id="General_Usage_"></span><span id="general_usage_"></span><span id="GENERAL_USAGE_"></span>一般使用   

<span id="_DeploymentItem__FileOrFolderToDeploy____DestinationFolder___"></span><span id="_deploymentitem__fileorfoldertodeploy____destinationfolder___"></span><span id="_DEPLOYMENTITEM__FILEORFOLDERTODEPLOY____DESTINATIONFOLDER___"></span>\[DeploymentItem ("FileOrFolderToDeploy", "DestinationFolder")\]  
場所

<span id="FileOrFolderToDeploy"></span><span id="fileorfoldertodeploy"></span><span id="FILEORFOLDERTODEPLOY"></span>FileOrFolderToDeploy  
は、test dll が格納されているディレクトリを基準としたファイルまたはフォルダーのパスです。 **Fileorfoldertodeploy**がフォルダーの場合、そのすべての内容がコピーされます。ただし、フォルダー自体は作成されません。 **Fileorfoldertodeploy**の下にフォルダーの階層がある場合、taef は、ディレクトリ階層を維持しながら、これらのすべてのディレクトリを再帰的にコピーします。

<span id="DestinationFolder"></span><span id="destinationfolder"></span><span id="DESTINATIONFOLDER"></span>DestinationFolder  
は、テスト dll が配置されているディレクトリを基準としたフォルダーパスで、配置項目のコピー先となる場所です。 **Destinationfolder**パスは. を使用して指定できます。 notation (例\\MyFiles)。

テスト dll があるフォルダーに配置するだけの場合は、 **Destinationfolder**を省略できます。

```cpp
[DeploymentItem("FileOrFolderToDeploy")]
```

プロパティの複数の部分がサポートされています。 次に、例を示します。

```cpp
[TestClass]
[DeploymentItem("file1.xml")]
[DeploymentItem("file2.xml")]
[DeploymentItem("file3.xml")]
public class UnitTest1
{
    ...
}
```

## <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>例


<span id="_deploymentitem__file1.xml___"></span><span id="_DEPLOYMENTITEM__FILE1.XML___"></span>\[DeploymentItem ("file1 .xml")\]  
依存関係としてテスト dll の横に配置されるタグ file1 .xml。 このメタデータは、テスト dll の隣にあるフォルダーにある file1 という名前の項目をテスト用 dll ディレクトリに配置すると解釈される可能性があります。 この構成は、コンピューター間のシナリオでのみ有効です。

<span id="_deploymentitem__file2.xml____datafiles___"></span><span id="_DEPLOYMENTITEM__FILE2.XML____DATAFILES___"></span>\[DeploymentItem ("file2", "データファイル")\]  
テスト dll の隣にある file2 という名前の項目を、テスト dll ディレクトリに作成されたデータファイルサブディレクトリに配置します。

<span id="_DeploymentItem__C___MyDataFiles__MyDataFiles2_____"></span><span id="_deploymentitem__c___mydatafiles__mydatafiles2_____"></span><span id="_DEPLOYMENTITEM__C___MYDATAFILES__MYDATAFILES2_____"></span>\[DeploymentItem ("C:\\\\MyDataFiles ファイル\\\\MyDataFiles2\\\\")\]  
C:\\\\MyDataFiles ファイル\\\\MyDataFiles2\\\\ directory 内にあるすべての項目とディレクトリを展開します。 この構成では、配置ディレクトリの下に MyDataFiles ファイル\\MyDataFiles2 ディレクトリは作成されません。 MyDataFiles ファイル内のすべてのファイルとディレクトリが、テスト dll ディレクトリに配置されます。 MyDataFiles ファイル\\MyDataFiles2 directory 構造全体をコピーするには、MyDataFiles ファイル\\MyDataFiles2 を出力ディレクトリとして指定する必要があります。

<span id="_deploymentitem___mydir__myfile.txt___"></span><span id="_DEPLOYMENTITEM___MYDIR__MYFILE.TXT___"></span>\[DeploymentItem ("% myDir%\\Myfile.txt")\]  
% MyDir% が解決されるディレクトリにそのファイルが存在する場合は、ファイルを展開します。 TAEF が環境変数を解決できない場合は、エラーがスローされます。

## <a name="span-idmanaged_testsspanspan-idmanaged_testsspanspan-idmanaged_testsspanmanaged-tests"></a><span id="Managed_Tests"></span><span id="managed_tests"></span><span id="MANAGED_TESTS"></span>マネージドテスト


**DeploymentItem** (別名 DeploymentItemAttribute) 属性は、テストメソッド (\[の\] 属性によって修飾)、テストクラス (\[TestClass\] 属性によって修飾)、またはテストアセンブリに適用できます。 ただし、VSTS はアセンブリレベルでこのプロパティをサポートしていないため、アセンブリレベルでこのプロパティを適用するには、アセンブリのセットアップに適用する必要があります (AssemblyInitialize 属性によって修飾されます)。

```cpp
[AssemblyInitialize]
[DeploymentItem("file1.xml")]
[DeploymentItem("file2.xml")]
[DeploymentItem("file3.xml")]
public  static AssemblySetup(TestContext testContext)
{
    ...
}
```

## <a name="span-idnative_testsspanspan-idnative_testsspanspan-idnative_testsspannative-tests"></a><span id="Native_Tests"></span><span id="native_tests"></span><span id="NATIVE_TESTS"></span>ネイティブテスト


ネイティブテストの場合、プロパティの形式はマネージコードの形式に似ています。 ただし、ネイティブプロパティには1つの値しかないため、項目のパスと省略可能な変換先は、プロパティ値で **'&gt;'** 文字で区切られて指定されます。

```cpp
BEGIN_TEST_CLASS(TestClassExample)
    TEST_CLASS_PROPERTY(L"DeploymentItem", L"C:\\Dependencies\\>Dependencies")
END_TEST_CLASS()
```

## <a name="span-idscript_testsspanspan-idscript_testsspanspan-idscript_testsspanscript-tests"></a><span id="Script_Tests"></span><span id="script_tests"></span><span id="SCRIPT_TESTS"></span>テストのスクリプトを作成


スクリプトテストの場合、プロパティの形式はネイティブテストの場合と同じです。

```cpp
<method name="TestOne">
    <TestMethodProperty name="DeploymentItem" value="C:\\Dependencies\\>Dependencies"/>
</method>
```









