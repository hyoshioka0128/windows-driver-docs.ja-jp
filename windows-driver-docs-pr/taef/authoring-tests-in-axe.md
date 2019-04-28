---
title: AXE でテストを作成する
description: AXE でテストを作成する
ms.assetid: B042FE1B-98E4-48ae-BE2C-15C71EC6640A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 336bf4b0eff08ceda7b978660bcd2bf5dab9141b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372743"
---
# <a name="authoring-tests-in-axe"></a>AXE でテストを作成する


TAEF 評価の実行エンジン (アックス) で実行されるテストの作成をサポートしています。

TAEF でアックス サポートには、TAEF アックス評価マニフェストを実行するができます。 主に、XML ベースのアックス評価マニフェストに、コマンド ライン Exe として記述のレガシー テストをラップする設計います。 この方法でこれらのレガシー テストでは、管理されているネイティブ、TAEF にテストを書き直すか、スクリプトをテストすることがなく TAEF で実行可能ファイルになります。

## <a name="span-idaxetestslayoutspanspan-idaxetestslayoutspanspan-idaxetestslayoutspanaxe-tests-layout"></a><span id="AXE_Tests_Layout"></span><span id="axe_tests_layout"></span><span id="AXE_TESTS_LAYOUT"></span>アックス テスト レイアウト


通常 TAEF テスト ファイルは、複数のテスト クラスとテストに含めることができます、TAEF アックス テスト (アックスの評価マニフェストで定義されているテスト) では、マニフェストは、1 つの実行可能ファイルをラップするため、1 つのテストのみを含めることができます。 したがって、TAEF アックス テスト ファイルでテストを表示するときに常に表示されます (つまり、アックス評価マニフェストを表示している)、テスト ファイルには、1 つのテスト クラスと 1 つのテストが含まれています。

``` syntax
te Examples\AXE.Basic.Examples.manifest /list
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
            Basic
                Basic::Basic

```

また、アックス テストでは、セットアップやクリーンアップ メソッドはサポートされません。

## <a name="span-idauthoringaxetestsspanspan-idauthoringaxetestsspanspan-idauthoringaxetestsspanauthoring-axe-tests"></a><span id="Authoring_AXE_Tests"></span><span id="authoring_axe_tests"></span><span id="AUTHORING_AXE_TESTS"></span>アックス テストを作成


アックスをテストする場合は、TAEF はアックス評価のマニフェスト ファイルの形式を使用します。

## <a name="span-idminimalaxetestfilespanspan-idminimalaxetestfilespanspan-idminimalaxetestfilespanminimal-axe-test-file"></a><span id="Minimal_AXE_Test_File"></span><span id="minimal_axe_test_file"></span><span id="MINIMAL_AXE_TEST_FILE"></span>最小限のアックス テスト ファイル


アックス評価マニフェスト スキーマは、高度なシナリオの複雑な評価の非常に多くの説明をサポートするために設計されています。 ただし、マニフェストこともできます非常に単純なごく少数の必須ノードがあります。 次の例では、最小限のマニフェストを含むすべての必須のタグを示します。

```cpp
1<?xml version="1.0" encoding="utf-8"?>
2<AxeAssessmentManifest xmlns="http://www.microsoft.com/axe/assessment/manifest">
3  <VersionedId>
4    <Guid>{ABCBFDE6-D731-4030-9049-E7CAAB6A6EEE}</Guid>
5    <Version>
6      <Major>1</Major>
7      <Minor>0</Minor>
8      <Build>0</Build>
9      <Revision>0</Revision>
10    </Version>
11  </VersionedId>
12  <MinimumAxeVersionRequired>
13    <Version>
14      <Major>1</Major>
15      <Minor>0</Minor>
16      <Build>1</Build>
17      <Revision>0</Revision>
18    </Version>
19  </MinimumAxeVersionRequired>
20  <Description>
21    <ProgrammaticName>Basic</ProgrammaticName>
22    <DisplayName>Basic Examples</DisplayName>
23    <ToolTip>Sample Basic Examples Assessment Tooltip</ToolTip>
24  </Description>
25  <Meta>
26    <ExitValueMeaning> <ZeroIsSuccess/> </ExitValueMeaning>
27  </Meta>
28  <Execution>
29    <CreateProcess>
30      <ApplicationName>AssessmentSample.exe</ApplicationName>
31    </CreateProcess>
32  </Execution>
33</AxeAssessmentManifest>
```

アックス評価ファイルは、XML ファイルをテストします。 そのため、通常の XML ヘッダーで始まる (**行 1**)。

**2 行目**アックス マニフェストとして XML ファイルを識別します。

**行 3. ~ 10.** id とバージョン、テストを一意に識別するために使用できる、テストを提供します。

**12-19 行**アックスこのマニフェストを解釈して、テストを実行するために必要な最小限のバージョンを指定します。

**20 ~ 24 行**人間が判読できる名前と短いツールヒントの説明は、テストを提供します。 テストのプロパティを表示すると、テスト クラスの名前と、テスト名に対応することに注意してください、 **ProgrammaticName**要素の値。

``` syntax
D:\enddev2.binaries.amd64chk\WexTest\CuE\TestExecution>te Examples\AXE.Basic.Examples.manifest /list
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
            Basic
                Basic::Basic

```

人間が判読できる名前が割り当てられている、 **DisplayName**プロパティ。 この割り当ては、内部 TAEF アーキテクチャと設計のためです。

``` syntax
Te Examples\AXE.Basic.Examples.manifest /listproperties
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64


        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.Basic.Examples.manifest
                Property[TaefTestType] =  AxeAssessment

            Basic
                Basic::Basic
                        Property[DisplayName] =  Basic Examples
                        Property[ProgrammaticName] =  Basic
                        Property[RunAs] =  Elevated
                        Property[ToolTip] =  Sample Basic Examples Assessment Tooltip

```

この評価は、単純なをラップし、既存 EXE という名前のテスト**AssessmentSample.exe**します。 **AssessmentSample.exe**一般的な規則を使用して、0 は成功と失敗の 0 以外の値のプロセス終了コードを返します。

**25 ~ 27 行**アックスと TAEF を指示して、テストが成功したことと、その他の値がエラーを意味する終了値は 0 がということです。

最後に、 **28 ~ 32 行**アックス Win32 API の値を使用して実行するよう指示**AssessmentSample.exe**します。

## <a name="span-idusingmetadatainaxetestfilespanspan-idusingmetadatainaxetestfilespanspan-idusingmetadatainaxetestfilespanusing-metadata-in-axe-test-file"></a><span id="Using_Metadata_in_AXE_Test_File"></span><span id="using_metadata_in_axe_test_file"></span><span id="USING_METADATA_IN_AXE_TEST_FILE"></span>アックス テスト ファイルのメタデータを使用します。


TAEF テストと同様 TAEF アックス テストにメタデータを適用することもできます。 次のような例を検討してください。

```cpp
1<?xml version="1.0" encoding="utf-8"?>
2<AxeAssessmentManifest xmlns="http://www.microsoft.com/axe/assessment/manifest">
3  <VersionedId>
4    <Guid>{F310F3F6-F786-4118-8A18-BC020C7D2521}</Guid>
5    <Version>
6      <Major>1</Major>
7      <Minor>0</Minor>
8      <Build>0</Build>
9      <Revision>0</Revision>
10    </Version>
11  </VersionedId>
12  <MinimumAxeVersionRequired>
13    <Version>
14      <Major>1</Major>
15      <Minor>0</Minor>
16      <Build>1</Build>
17      <Revision>0</Revision>
18    </Version>
19  </MinimumAxeVersionRequired>
20  <Description>
21    <ProgrammaticName>CustomMetadataExamples</ProgrammaticName>
22    <DisplayName>Custom Metadata Examples</DisplayName>
23    <ToolTip>Sample Custom Metadata Examples Assessment Tooltip</ToolTip>
24  </Description>
25  <Properties>
26    <Owner>Someone</Owner>
27    <Priority>1</Priority>
28    <Parallel>false</Parallel>
29  </Properties>
30  <Meta>
31    <ExitValueMeaning> <ZeroIsSuccess/> </ExitValueMeaning>
32  </Meta>
33  <Execution>
34    <CreateProcess>
35      <ApplicationName>AssessmentSample.exe</ApplicationName>
36    </CreateProcess>
37  </Execution>
38</AxeAssessmentManifest>
```

**行の 25 ~ 29** TAEF 標準およびカスタム メタデータを適用する方法を示しますアックス テストにします。 で、 **AxeAssessmentManifest** XML ノードが、**プロパティ**ノード。 1 つのレベルの XML タグの下、**プロパティ**ノードは、メタデータ (プロパティ) として認識されます。 すべての 1 つのレベル XML タグの下**プロパティ**プロパティの名前と値は、プロパティの値として解釈されます、テキストとして解釈されます。 上記の例では、**所有者**はプロパティ名として解釈されます、**だれかが**プロパティの値として。 これらの要素にテキストがない XML タグは要素の値が空の文字列として解釈されます (たとえば、  **&lt;SimpleTagWithNoText/&gt;**)。 複数レベルの XML タグの下**プロパティ**(例では、複数レベルのようなタグでは無視されます

```cpp
<VerifyOSVersion>
    <Major>6</Major>
    <Minor>0</Minor>
    <Build>0</Build>
</VerifyOSVersion>
```

無視されます)。 使用する他の TAEF テストと同様に、 **/listProperties** TAEF メタデータを表示するオプション。

``` syntax
te Examples\AXE.CustomMetadata.Examples.manifest /listProperties
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64

        D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\Examples\AXE.CustomMetadata.Examples.manifest
                Property[TaefTestType] =  AxeAssessment

            CustomMetadataExamples
                CustomMetadataExamples::CustomMetadataExamples
                        Property[DisplayName] =  Custom Metadata Examples
                        Property[Owner] =  Someone
                        Property[Parallel] =  false
                        Property[Priority] =  1
                        Property[ProgrammaticName] =  CustomMetadataExamples
                        Property[RunAs] =  Elevated
                        Property[ToolTip] =  Sample Custom Metadata Examples Assessment Tooltip


```

## <a name="span-idaxetestsmetadatasupportlimitationsspanspan-idaxetestsmetadatasupportlimitationsspanspan-idaxetestsmetadatasupportlimitationsspanaxe-tests-metadata-support-limitations"></a><span id="AXE_Tests_Metadata_Support_Limitations"></span><span id="axe_tests_metadata_support_limitations"></span><span id="AXE_TESTS_METADATA_SUPPORT_LIMITATIONS"></span>アックスは、メタデータ サポートの制限をテストします。


注:TAEF 標準的なテストのすべてのメタデータは、TAEF アックス テストで使用できます。

-   すべてのメタデータは、プロセスが実行される、このような環境を変更することを目的とした**ActivationContext**と**ThreadingModel**、アックス テストでは動作しません。 アックスでは、テストを実行する TAEF のプロセスを使用しませんが、アックス テスト ファイル (アックス評価マニフェスト) で指定されている実行可能プログラムを実行、新しいプロセスを作成します。 同じ理由から、データ ドリブン TAEF テスト (**DataSource**プロパティ) アックス TAEF のテストを使用したか、機能しません。
-   同様に、TAEF アックス テスト ファイルでのみ、1 つのテスト、に関して他のテストのテストの動作を変更する TAEF メタデータをカプセル化できますのでなど**ExecutionGroup**も動作しません。
-   アックス アーキテクチャにより、アックスは、昇格されたプロセスにのみ実行できます。 そのため、上記の TAEF アックス テストのプロパティから学習したようにすべて TAEF アックスのテストが**プロパティ\[RunAs\]管理者特権での =** 適用します。

## <a name="span-idaxetestfilewithruntimeparametersspanspan-idaxetestfilewithruntimeparametersspanspan-idaxetestfilewithruntimeparametersspanaxe-test-file-with-runtime-parameters"></a><span id="AXE_Test_File_with_Runtime_Parameters"></span><span id="axe_test_file_with_runtime_parameters"></span><span id="AXE_TEST_FILE_WITH_RUNTIME_PARAMETERS"></span>ランタイム パラメーターを持つアックス テスト ファイル


TAEF アックス テストでは、ランタイム パラメーターもサポートします。 アックス テストでは、TAEF のランタイム パラメーターを使用するには、実行可能プログラムに渡されるパラメーター名をアックスのテスト ファイルで定義する必要があります。

すべての可能なアックス マニフェスト パラメーター機能のすべての詳細を記述するには、このドキュメントの範囲外です。 その情報は、アックス評価ドキュメントを参照してください。 このドキュメントは、最も一般的で便利なパラメーターのアプリケーションとのみについて説明します。

次の例より複雑なアックス評価マニフェストです。

```cpp
1<?xml version="1.0" encoding="utf-8"?>
2<AxeAssessmentManifest xmlns="http://www.microsoft.com/axe/assessment/manifest">
3  <VersionedId>
4    <Guid>{B63B2FFF-EDEB-41FB-92EA-529CE4A46D20}</Guid>
5    <Version>
6      <Major>1</Major>
7      <Minor>0</Minor>
8      <Build>0</Build>
9      <Revision>0</Revision>
10    </Version>
11  </VersionedId>
12  <MinimumAxeVersionRequired>
13    <Version>
14      <Major>1</Major>
15      <Minor>0</Minor>
16      <Build>1</Build>
17      <Revision>0</Revision>
18    </Version>
19  </MinimumAxeVersionRequired>
20  <Description>
21    <ProgrammaticName>ExplicitRuntimeParameters</ProgrammaticName>
22    <DisplayName>Explicit Runtime Parameters</DisplayName>
23    <ToolTip>Sample Explicit Runtime Parameters Assessment Tooltip</ToolTip>
24  </Description>
25  <ParameterDefinitions>
26    <ParameterDefinition>
27      <Description>
28        <ProgrammaticName>SimpleParameter</ProgrammaticName>
29        <DisplayName>Simple parameter</DisplayName>
30        <ToolTip>The is an example of a simple parameter.</ToolTip>
31      </Description>
32      <Type>
33        <String></String>
34      </Type>
35      <CommandLineFormat>{0}</CommandLineFormat>
36    </ParameterDefinition>
37    <ParameterDefinition>
38      <Description>
39        <ProgrammaticName>RequiredParameterWithoutDefaultValue</ProgrammaticName>
40        <DisplayName>Required parameter without a default value.</DisplayName>
41        <ToolTip>The is an example of a required parameter Without a default value.</ToolTip>
42      </Description>
43      <Required>True</Required>
44      <Type>
45        <Int></Int>
46      </Type>
47      <CommandLineFormat>{0}</CommandLineFormat>
48    </ParameterDefinition>
49    <ParameterDefinition>
50      <Description>
51        <ProgrammaticName>RequiredParameterWithDefaultValue</ProgrammaticName>
52        <DisplayName>Required parameter with a default value</DisplayName>
53        <ToolTip>The is an example of a required parameter With a default value.</ToolTip>
54      </Description>
55      <Required></Required>
56      <DefaultValue>"%AssessmentResultsPath%"</DefaultValue>
57      <Type>
58        <String></String>
59      </Type>
60      <CommandLineFormat>/RequiredParameterWithDefaultValue={0}</CommandLineFormat>
61    </ParameterDefinition>
62  </ParameterDefinitions>
63  <Meta>
64    <ExitValueMeaning> <ZeroIsSuccess/> </ExitValueMeaning>
65  </Meta>
66  <Execution>
67    <CreateProcess>
68      <ApplicationName>AssessmentSample.exe</ApplicationName>
69    </CreateProcess>
70  </Execution>
71</AxeAssessmentManifest>
```

**25 ~ 62 行**TAEF してアックス実行可能ファイルの評価にデータを渡すために使用されるパラメーターを記述するパラメーターの定義を示します。

最も単純なパラメーター定義は、**行 26 ~ 36**します。 必須の**説明**が正確に同じセクション、**説明**前述のようには、マニフェストのセクション。 表示、**型**パラメーターのデータ型を定義するタグ。 (くださいすべてのサポートされているデータ型アックス評価のマニュアルを参照する。)

省略可能な**CommandLineFormat**セクションでは、評価のコマンドラインのため、評価のパラメーターを書式設定する方法について説明します。 この XML ノードは、有効な .NET 書式設定文字列である、空でない文字列を含める必要があります。 評価のパラメーター値をフォーマッタに渡される唯一のオブジェクトとなります。 つまり、書式指定文字列が 1 つだけの複合インデックス 0 を持つ項目を書式設定を含める必要があります。 例としては、:-入力{0}、/affinity:0 x {0, X}、または-inputfile ="{0}"。

次のパラメーターが定義されている**行 37 ~ 48**は必須パラメーターです。 前のパラメーターからの定義内で唯一の違いは、省略可能な**必要**タグ。 このタグは、アックス アックス テストの実行時にこのパラメーターを渡すユーザーが期待していることを示します。 このパラメーターを省略した場合 (たとえば、0 の INT、文字列などの空の文字列) のパラメーターのデータ型の既定値が使用されます。

最後に、例の最後のパラメーターは省略可能な指定**DefaultValue**タグで、パラメーターの既定値について説明します。 このノードが空白の場合、パラメーターのデータ型の既定値は、既定値として使用されます。 上記の例では、"%assessmentresultspath%"、これは、評価の実行開始時にアックスによって設定される環境変数を使用します。 ここでもを参照してくださいアックス評価ドキュメント アックス環境変数をすべてサポートされています。

パラメーターは、定義の逆の順序で実行可能ファイルに渡される - パラメーター ファイルで定義されている最後は、最初に渡される実行可能ファイルです。

TAEF アックスを実行する[ランタイム パラメーター](runtime-parameters.md)ランタイム パラメーターを使用するその他の TAEF テストとしてのテスト (を使用して、 **/p**コマンド ライン オプション)。

``` syntax
te AXE.ExplicitRuntimeParameters.Examples.manifest /p:SimpleParameter=Test1 /p:RequiredParameterWithoutDefaultValue=10
Test Authoring and Execution Framework v2.7 Build 6.2.7918.0 (1320) For x64

ExplicitRuntimeParameters::ExplicitRuntimeParameters
AssessmentSample.exe is simple application for AXE assessment demo.
It just echoes the arguments passed to it to the console.

Parameters passed from the command line:
Argument[0]=AssessmentSample.exe
Argument[1]=10
Argument[2]=/RequiredParameterWithDefaultValue=C:\Results\JobResults_DEVRH_2011-0129_0250-12.394\0
Argument[3]=Test1

FileName: C:\Results\JobResults_DEVRH_2011-0129_0250-12.394\JobResults_DEVRH_2011-0129_0250-12.394.xml
Saved output file to: D:\enddev2.binaries.amd64chk\Test\CuE\TestExecution\WexLogFileOutput\
000001_~ExplicitRuntimeParameters_JobResults_DEVRH_2011-0129_0250-12.394.xml
EndGroup: ExplicitRuntimeParameters::ExplicitRuntimeParameters [Passed]

```

## <a name="span-idaxetestcrossmachineexecutionspanspan-idaxetestcrossmachineexecutionspanspan-idaxetestcrossmachineexecutionspanaxe-test-cross-machine-execution"></a><span id="AXE_Test_Cross_Machine_Execution"></span><span id="axe_test_cross_machine_execution"></span><span id="AXE_TEST_CROSS_MACHINE_EXECUTION"></span>クロス マシン実行アックス テスト


[コンピューター間の実行のシナリオで](cross-machine-execution.md)TAEF は成功したテストの実行、テストと共に配置する必要があるテストの依存関係を判断しようとしています。 場合は、アックス テスト ファイル TAEF は TAEF アックス テストの実行用のリモート コンピューターと同じフォルダー内にあるすべてのファイルをコピーします。

マシンの実行、ARM アックス テストのクロス プラットフォームが現在サポートされていません。

## <a name="span-idtaefaxesupportdependenciesspanspan-idtaefaxesupportdependenciesspanspan-idtaefaxesupportdependenciesspantaef-axe-support-dependencies"></a><span id="TAEF_AXE_Support_Dependencies"></span><span id="taef_axe_support_dependencies"></span><span id="TAEF_AXE_SUPPORT_DEPENDENCIES"></span>TAEF アックス サポートの依存関係


アックスは、Windows が付属していません。 アックス テストを実行できるようにするには、コピーする必要があります。 **axecore.dll**と**Microsoft.Assessment.dll** TAEF または TAEF アックス テスト ディレクトリにします。









