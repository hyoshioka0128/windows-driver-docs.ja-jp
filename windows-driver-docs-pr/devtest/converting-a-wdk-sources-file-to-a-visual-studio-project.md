---
title: WDK ソース ファイルから Visual Studio プロジェクトへの変換
description: Nmake2msBuild を使用して、WDK のソース ファイルを Visual Studio プロジェクトに変換します。
ms.assetid: 6030317B-5068-40FD-8C9A-0B7A48C82B31
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15a989a7f5b46dfec63e58e02c5429c6edbc08dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343060"
---
# <a name="converting-a-wdk-sources-file-to-a-visual-studio-project"></a>WDK ソース ファイルから Visual Studio プロジェクトへの変換


**注**Nmake2MsBuild ツールは、Windows 10、バージョン 1511 以降、WDK から削除されました。

 

Build.exe を使用して作成されたほとんどの Windows 7 の WDK プロジェクトでは、使用することができます、 [Nmake2MsBuild](nmake2msbuild.md)ユーティリティ、またはプロジェクト ファイルを生成する、Visual Studio 内での自動変換プロセス (します。VcxProj)。 ほとんどの場合、Visual Studio のプロジェクト ファイルに密接に対応元*ソース*ファイルの Visual Studio で、または MSBuild コマンドから、プロジェクトを正常にビルドできるようにします。 いくつかのビルド ターゲット、変換ツールを使用するルール ベースのマッピングをカスタマイズする必要があります。 このトピックでは、変換ユーティリティのしくみし、独自のルール マッピングを作成して拡張する方法について説明します。

## <a name="span-idthenmake2msbuildconversionprocessspanspan-idthenmake2msbuildconversionprocessspanspan-idthenmake2msbuildconversionprocessspanthe-nmake2msbuild-conversion-process"></a><span id="The_Nmake2MsBuild_conversion_process"></span><span id="the_nmake2msbuild_conversion_process"></span><span id="THE_NMAKE2MSBUILD_CONVERSION_PROCESS"></span>Nmake2MsBuild 変換プロセス


[Nmake2MsBuild](nmake2msbuild.md)ツールの実行の内容のルール ベースのマッピングを*ソース*Visual Studio C のプロジェクト ファイルの内容をファイル (します。VcxProj)。 変換を各ビルド マクロ、MSBuild で使用され、ビルド時にインストルメント化されるプロパティ ファイル (.props) に対応する変換ルールがある場合します。 MSBuild の環境でのプロパティ、アイテム、およびこれらのアイテムのメタデータは、ビルド システムによって使用されます。 内の各マクロ、*ソース*ファイルは、MSBuild プロパティ、項目、または、規則によって指定された項目メタデータにマップします。 既定では、ルールが存在しない場合は、A を B 値を持つという名前のマクロに変換がプロパティ A B. 値(Nmake の) 構文でのマッピングでは、初期の変換の手順を*makefile.inc*または*ソース*ファイルに関連付けられているプロパティ ファイル (.props) MSBuild 構文にします。 各マクロ (nmake の) ファイルでは、プロパティ ファイル (.props) のプロパティに変換されます。 ビルド時に、これらのプロパティが評価され、特定のプロパティの評価値をさまざまな他のプロパティ、項目または変換規則によって指定されたメタデータにマップします。

たとえば、ユーザー\_C\_フラグ マクロで、*ソース*ファイルは、ビルド時にコンパイラ (cl.exe) に渡されるコマンド ライン パラメーターを指定するために使用します。 MSBuild の環境では、ClCompile 項目のリストには、コンパイルされるソース コード ファイルが含まれています。 ClCompile 項目のリストがコンパイラによって使用される、 [CL タスク](https://msdn.microsoft.com/library/ee862477.aspx)します。 AdditionalOptions のメタデータを一覧内の各項目を決定、追加のコンパイラ (cl.exe) に渡されるフラグ。 ユーザーの値ではそのため、\_C\_フラグ マクロは、ClCompile の種類のアイテムの AdditionalOptions 項目メタデータにマップする必要があります。 初期の変換の手順では、ユーザー\_C\_フラグ マクロは、ソース ファイルでは、MSBuild プロパティの場合も名前付きユーザーに変換\_C\_フラグで生成されたファイルと呼ばれる*sources.props*. ユーザーの評価値のマッピング\_C\_次の例に示すように、ビルド時に AdditionalOptions メタデータへのフラグ プロパティに発生します。

```
  <!-- Contains rules to map compiler and linker switches -->
  <ItemDefinitionGroup>
    <ClCompile>
      ...
      <AdditionalOptions>%(AdditionalOptions) $(User_C_Flags)</AdditonalOptions>
      ...
    </ClCompile>
  </ItemDefinitionGroup>
```

前の例に示すように、マッピングは PostToolsetRules.props ファイルです。 例のマッピングでは、MSBuild の ItemDefinitionGroup を使用してその $ を指定 (ユーザー\_C\_フラグ) 型 ClCompile AdditonalOptions メタデータ内のすべての項目に追加する必要があります。 プロパティを見つけることができます、c: での変換処理で使用されるファイル\\Program Files (x86)\\Windows キット\\8.0\\bin\\変換ディレクトリ。

標準の MSBuild 構文を使用してすべての変換規則は指定します。

## <a name="span-iddefaultconversionrulesfilespanspan-iddefaultconversionrulesfilespanspan-iddefaultconversionrulesfilespandefault-conversion-rules-file"></a><span id="Default_conversion_rules_file"></span><span id="default_conversion_rules_file"></span><span id="DEFAULT_CONVERSION_RULES_FILE"></span>既定の変換ルール ファイル


変換に使用される既定の規則は、PostToolsetRules.props ファイルで指定されます。 PostToolsetRules.props ファイルとその他の変換プロパティ ファイルで見つかります、c:\\Program Files (x86)\\Windows キット\\8.0\\bin\\変換ディレクトリ。 PostToolsetRules.props ファイルは、プロジェクトの変換の新しい規則を作成するための参照として使用できます。

## <a name="span-idcreatingcustomconversionrulesspanspan-idcreatingcustomconversionrulesspanspan-idcreatingcustomconversionrulesspancreating-custom-conversion-rules"></a><span id="Creating_custom_conversion_rules"></span><span id="creating_custom_conversion_rules"></span><span id="CREATING_CUSTOM_CONVERSION_RULES"></span>カスタムの変換ルールを作成します。


既定の規則ファイル PostToolsetRules.props は常に、変換時に使用しますが、独自のカスタム ルール ファイルを作成することもできます。 カスタム ルール ファイルは、プロジェクトがビルドする以前のビルド環境に固有可能性のあるビルド マクロの追加の変換規則を説明します。

Microsoft から提供される規則は、マクロや Windows 7 の WDK で定義されているターゲットを使用するプロジェクトの変換をサポートするだけです。 たとえば、ルールのみをサポートこれらのマクロとに表示されるターゲット*makefile.new*します。 以前のビルド環境で追加または変更の機能を利用するすべてのプロジェクトの変換は automatic には保証されません。 一般的な規則としては、変換の規則ファイルは、既存のプロジェクトで、ソースまたはプロジェクトに関連付けられている .inc ファイルまたは WDK でインストールされているその他のファイルの変更を加えなければ Windows 7 の WDK の新規インストールがビルドされない場合は必要があります。

カスタム ルール ファイルは、標準の MSBuild 構文と既定の規則ファイルを使用する設計パターンに従う必要があります。 既定の規則はすべてを開発するため十分なガイドラインと例を提供する必要がありますが、最も複雑な変換規則です。

ファイルをインポートする順序をします。VcxProj ファイル、およびインストルメント化すると、ルールが重要と保持する必要があります。 Microsoft 提供の PostToolsetRules.props 後すぐに、プロジェクトにユーザーが開発したルール ファイルをインポートすることをお勧めします。

```
  <Import Project="$(PostToolsetRules)" />
  <!-- Import PostToolsetRules to map nmake properties/macros to msbuild properties/items/metadata -->
```

## <a name="span-idconversiontoollimitationsspanspan-idconversiontoollimitationsspanspan-idconversiontoollimitationsspanconversion-tool-limitations"></a><span id="Conversion_tool_limitations"></span><span id="conversion_tool_limitations"></span><span id="CONVERSION_TOOL_LIMITATIONS"></span>変換ツールの制限事項


NMake2MsBuild ユーティリティは、カスタム ターゲットの変換または BinPlace などのいくつかのビルドの重要なターゲットの変換をサポートしていません。 BinPlace 自体は、MSBuild.exe の環境が自動変換されませんでサポートされます。 NMake2MsBuild ユーティリティでは、Visual Studio のプロパティ ページで、変換後のプロジェクトのすべての設定を表示する機能は提供されません。

## <a name="span-idnmakesyntaxandbehaviornotsupportedbynmake2msbuildspanspan-idnmakesyntaxandbehaviornotsupportedbynmake2msbuildspanspan-idnmakesyntaxandbehaviornotsupportedbynmake2msbuildspannmake-syntax-and-behavior-not-supported-by-nmake2msbuild"></a><span id="NMake_syntax_and_behavior_not_supported_by_Nmake2Msbuild"></span><span id="nmake_syntax_and_behavior_not_supported_by_nmake2msbuild"></span><span id="NMAKE_SYNTAX_AND_BEHAVIOR_NOT_SUPPORTED_BY_NMAKE2MSBUILD"></span>NMake の構文と動作 Nmake2Msbuild でサポートされていません


-   マクロの展開は、省略可能なディレクトリを定義する推論のルールで参照します。

    ```
    INPUT_DIR= c:\MyDirectory
    .FromExt{$(INPUT_DIR)}.ToExt:
         cmd.exe /c echo  something 
    ```

    D を変更するには、上記しなければなりません。

    ```
    .FromExt{ c:\MyDirectory}.ToExt:
         cmd.exe /c echo  something 
    ```

-   NMAKE のインライン ファイルやマクロの置き換えはサポートされていません。

    NMAKE のインライン ファイル:参照してください**インライン ファイルのテキストを作成します。**

    マクロの置き換え:参照してください**マクロでの代入**

    インライン ファイルやマクロの置き換えはサポートされていないために、t が勝利した次のターゲットが正しく変換されます。

    ```
    fsdkmsg.mc : ..\..\wrapper\fsdkmsgbase.src
           copy ..\..\wrapper\fsdkmsgbase.src
        @type <<$(ECHO_RSP)
    $(ECHO_MSG_P) /EP $**
    <<$(BUILD_NOKEEP)
        @$(C_PREPROCESSOR_NAME) @<<$(CL_RSP) /Tc$** > $@
    $(CPPXX: =
    )
    <<$(BUILD_NOKEEP)   
    ```

-   **!エラー**ステートメントは変換されません。 S 対応する外部の MSBuild を使用する MSBuild ターゲットはありませんもします。
-   1 対 1 で NTTARGETFILE のターゲット定義と一致する必要があります\*ターゲットを呼び出すマクロ。次の操作はサポートされていません。

    ```
    Sources File:
    OBJ_NAME=Something
    NTTARGETFILES=$(_OBJ_DIR)\$(TARGET_DIRECTORY)\$(OBJ_NAME).obj
    Makefile.inc:
    obj\$(TARGET_DIRECTORY)\Something.obj : $(_OBJ_DIR)\$(TARGET_DIRECTORY)\$(Foo).obj
      
    ```

-   ターゲットの定義と NTTARGETFILES の両方が一致する必要があります。どちらも、$(OBJ\_NAME).obj を使用する必要がありますまたは*Somename*。 obj. $ でしょうか。 $&lt;ターゲット内のトークンは常にすべての依存関係を展開します。

    参照してください**ファイル名マクロ**詳細についてはします。

-   $? 現在のターゲットより後のタイムスタンプを持つすべての依存関係を展開します。  変換後のプロジェクトのタイムスタンプは無視され、すべての依存関係にこれが評価されます。 True の場合も同様 $&lt;

## <a name="span-idlimitationsofconvertedprojectsspanspan-idlimitationsofconvertedprojectsspanspan-idlimitationsofconvertedprojectsspanlimitations-of-converted-projects"></a><span id="Limitations_of_Converted_Projects"></span><span id="limitations_of_converted_projects"></span><span id="LIMITATIONS_OF_CONVERTED_PROJECTS"></span>変換後のプロジェクトの制限事項


元のソース ファイルは、条件付きで異なる一連のファイルをコンパイルし、IDE 内のファイルの名前を変更/削除/追加によって変換されたプロジェクトを変更すると、プロジェクトは更新されたファイルの一覧でのみ動作します。 別のファイルが不要になった条件付きでコンパイルします。

変換後のプロジェクトは、VS をサポートしていません。ファイルをフィルター処理します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Nmake2MsBuild](nmake2msbuild.md)

[既にあるソース ファイルからのドライバーの作成](https://msdn.microsoft.com/windows-drivers/develop/creating_a_driver_from_existing_source_files)

 

 






