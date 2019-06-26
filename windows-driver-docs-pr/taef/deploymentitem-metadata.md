---
title: DeploymentItem メタデータ
description: DeploymentItem メタデータ
ms.assetid: 7F18CD71-F000-4231-9093-82980EB7584D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80be6a1d97a4670de74360db4fa351a21b4e611
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373029"
---
# <a name="deploymentitem-metadata"></a>DeploymentItem メタデータ


**DeploymentItem**メタデータ ファイルと Taef は、これらを識別し、適切にコピーすることができるように、テストの実行中に、テストで使用されるフォルダーのファイルとフォルダーの依存関係を識別します (など、で[クロス マシン実行シナリオ](cross-machine-execution.md)、Taef はで識別されるファイルは展開**DeploymentItem**プロパティを指定されたテスト マシン)。

Taef DeploymentItem 実装に非常に似ています、[と同等の VSTS 機能](https://docs.microsoft.com/en-US/dotnet/api/microsoft.visualstudio.testtools.unittesting.deploymentitemattribute?redirectedfrom=MSDN&view=mstest-net-1.2.0)します。

アセンブリ、クラス、またはテスト レベルのいずれかに DeploymentItem メタデータを適用できます。 DeploymentItem メタデータで指定された項目は、送信者 (アセンブリ、テスト クラスまたはテスト) のセットアップの実行時間によってデプロイされます。 DeploymentItem メタデータ依存関係 (たとえば、ファイル) を指定する、転送先にその依存関係が既に存在する場合は、TAEF CRC 比較がし、変更された場合にのみ、ファイルをコピーします。 エラーが記録されます DeploymentItem メタデータは、依存関係と依存関係を検出することはできませんを指定する場合、テストが失敗する (またはクラスやアセンブリのテストをそれに応じてテストすべて)。 アセンブリ、クラス、またはテスト - あたり、展開、クラス、すべてのアセンブリに行われるまたはしませんこれらは、データ駆動型の場合は、展開をテストしたら TAEF はファイルのみ配置します。

## <a name="span-idsyntaxspanspan-idsyntaxspanspan-idsyntaxspansyntax"></a><span id="Syntax"></span><span id="syntax"></span><span id="SYNTAX"></span>構文


<span id="General_Usage_"></span><span id="general_usage_"></span><span id="GENERAL_USAGE_"></span>一般的な使用法   

<span id="_DeploymentItem__FileOrFolderToDeploy____DestinationFolder___"></span><span id="_deploymentitem__fileorfoldertodeploy____destinationfolder___"></span><span id="_DEPLOYMENTITEM__FILEORFOLDERTODEPLOY____DESTINATIONFOLDER___"></span>\[DeploymentItem("FileOrFolderToDeploy", "DestinationFolder")\]  
パラメーターの説明

<span id="FileOrFolderToDeploy"></span><span id="fileorfoldertodeploy"></span><span id="FILEORFOLDERTODEPLOY"></span>FileOrFolderToDeploy  
ファイルまたはフォルダー パスをテスト dll がディレクトリに対して相対的です。 場合**FileOrFolderToDeploy**フォルダーですべての内容がコピーされます。 ただし、フォルダー自体が作成されません。 フォルダーの階層がある場合**FileOrFolderToDeploy**Taef はコピーすべてこれらのディレクトリを再帰的に、ディレクトリの階層を維持します。

<span id="DestinationFolder"></span><span id="destinationfolder"></span><span id="DESTINATIONFOLDER"></span>DestinationFolder  
ディレクトリに対する相対フォルダー パスでテスト dll は、および配置項目がコピーされます。 **DestinationFolder**を使用してパスを指定できます. (たとえば、.. の表記\\MyFiles)。

テスト dll が、フォルダーを展開する場合**DestinationFolder**は省略できます。

```cpp
[DeploymentItem("FileOrFolderToDeploy")]
```

複数のプロパティがサポートされています。 次に、例を示します。

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


<span id="_deploymentitem__file1.xml___"></span><span id="_DEPLOYMENTITEM__FILE1.XML___"></span>\[DeploymentItem("file1.xml")\]  
依存関係としてテスト dll の横にある file1.xml をタグ付けします。 このメタデータは、システムが、テスト dll は、テスト dll ディレクトリの横にあるフォルダーにあるという名前の項目の file1.xml をデプロイとして解釈できます。 この構成では、クロス マシンのシナリオに役立ちますのみです。

<span id="_deploymentitem__file2.xml____datafiles___"></span><span id="_DEPLOYMENTITEM__FILE2.XML____DATAFILES___"></span>\[DeploymentItem("file2.xml", "DataFiles")\]  
テスト dll ディレクトリに作成されたデータ ファイルのサブディレクトリに、テスト dll の横にあるという名前の項目の file2.xml をデプロイします。

<span id="_DeploymentItem__C___MyDataFiles__MyDataFiles2_____"></span><span id="_deploymentitem__c___mydatafiles__mydatafiles2_____"></span><span id="_DEPLOYMENTITEM__C___MYDATAFILES__MYDATAFILES2_____"></span>\[DeploymentItem("C:\\\\MyDataFiles\\\\MyDataFiles2\\\\")\]  
すべての項目とディレクトリを c: ドライブ内で見つかったデプロイ\\\\MyDataFiles\\\\MyDataFiles2\\ \\ディレクトリ。 この構成は、MyDataFiles を作成していない\\配置ディレクトリの下にある MyDataFiles2 ディレクトリ。 すべてのファイルと MyDataFiles 内のディレクトリはテスト dll ディレクトリに配置されます。 全体の MyDataFiles をコピーする\\MyDataFiles2 ディレクトリ構造、MyDataFiles を指定する必要があります\\MyDataFiles2 出力ディレクトリとします。

<span id="_deploymentitem___mydir__myfile.txt___"></span><span id="_DEPLOYMENTITEM___MYDIR__MYFILE.TXT___"></span>\[DeploymentItem("%myDir%\\myFile.txt")\]  
どの %mydir% 解決されるディレクトリにそのファイルが存在する場合は、ファイル myFile.txt をデプロイします。 TAEF で環境変数を解決することがない場合、エラーをスローします。

## <a name="span-idmanagedtestsspanspan-idmanagedtestsspanspan-idmanagedtestsspanmanaged-tests"></a><span id="Managed_Tests"></span><span id="managed_tests"></span><span id="MANAGED_TESTS"></span>管理対象のテスト


**DeploymentItem** (DeploymentItemAttribute とも呼ばれます) のテスト メソッドに属性を適用できます (によって修飾された\[TestMethod\]属性)、テスト クラス (で修飾\[TestClass\]属性) またはアセンブリをテストします。 ただし、VSTS がアセンブリ レベルでこのプロパティをサポートされていないため、アセンブリ レベルでこのプロパティを適用する必要があるアセンブリのセットアップ (AssemblyInitialize 属性で修飾された) に適用します。

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

## <a name="span-idnativetestsspanspan-idnativetestsspanspan-idnativetestsspannative-tests"></a><span id="Native_Tests"></span><span id="native_tests"></span><span id="NATIVE_TESTS"></span>ネイティブのテスト


ネイティブのテストでは、プロパティの形式は、マネージ コードの形式に似ています。 ただし、ネイティブのプロパティは、1 つの値のみがある、ため、項目のパスと省略可能な宛先がで指定された区切りで、プロパティの値を **'&gt;'** 文字。

```cpp
BEGIN_TEST_CLASS(TestClassExample)
    TEST_CLASS_PROPERTY(L"DeploymentItem", L"C:\\Dependencies\\>Dependencies")
END_TEST_CLASS()
```

## <a name="span-idscripttestsspanspan-idscripttestsspanspan-idscripttestsspanscript-tests"></a><span id="Script_Tests"></span><span id="script_tests"></span><span id="SCRIPT_TESTS"></span>スクリプトのテスト


スクリプトをテストする場合はプロパティの形式がネイティブのテストの場合と同様です。

```cpp
<method name="TestOne">
    <TestMethodProperty name="DeploymentItem" value="C:\\Dependencies\\>Dependencies"/>
</method>
```









