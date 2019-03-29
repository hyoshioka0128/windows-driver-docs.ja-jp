---
title: 静的ドライバー検証ツールのコマンド (MSBuild)
description: Static Driver Verifier で使用されるコマンド
ms.assetid: F0663631-AD7B-4BFE-8E07-7BB2FFC72911
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8c956588adc855333659e8978ead5156ff09636
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574149"
---
#  <a name="static-driver-verifier-commands-msbuild"></a>静的ドライバー検証ツールのコマンド (MSBuild)


Static Driver Verifier (SDV) で実行することができます、 **Visual Studio コマンド プロンプト**ウィンドウで、Windows Driver Kit (WDK) をインストールまたは Enterprise Windows Driver Kit (EWDK) を実行しています。 ドライバーのプロジェクト ファイルまたはライブラリのプロジェクト ファイルが格納されているディレクトリに移動します。 パラメーターは、コマンドラインで任意の順序で表示できます。

**注**SDV は、WDK のインストール時に Visual Studio に統合し、"Driver"メニューを使用して、IDE からも実行します。 

```
msbuild /t:sdv /p:Inputs="Parameters" ProjectFile /p:Configuration=configuration /p:Platform=platform     
```

リリース構成を選択する必要があります (たとえば、 **/p:Configuration =「Windows 7 リリース」**)。 サポートされるリリース構成の一覧で、次を参照してください。[ドライバーをビルド](https://msdn.microsoft.com/windows-drivers/develop/building_a_driver)します。 プラットフォームは、 **Win32** x86 または**x64** (たとえば、 **/p:Platform = Win32**)。

**注**をコンピュータに、コンピューターの電源管理プランは省きますスリープ状態の分析中に確認してください。

 

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>パラメーター


### <span id="parameters"></span><span id="PARAMETERS"></span>

<span id="_scan"></span><span id="_SCAN"></span>/**scan**  
関数の役割の型宣言に対して、ドライバーのソース コードをスキャンします。 提供されているドライバーのコールバック関数を宣言してルーチンをディスパッチする方法については、次を参照してください。[を使用して関数の役割の型の宣言](using-function-role-type-declarations.md)します。 このスキャンでは、SDV は、ドライバーを確認するために必要なドライバーのエントリ ポイントを検出しようとします。 スキャンの結果を記録[Sdv map.h](sdv-map-h.md)ドライバーのプロジェクト ディレクトリで作成したファイル。

詳細については、次を参照してください。 [、ソース コードを準備する](using-static-driver-verifier-to-find-defects-in-drivers.md#preparing_your_source_code)します。

<span id="________check_Rule____Rule_..._"></span><span id="________check_rule____rule_..._"></span><span id="________CHECK_RULE____RULE_..._"></span> **/check:**<em>ルール</em> | *ルール*、.  
指定した規則と検証を開始します。 1 つ以上のルールを指定するには、各ルールをコンマで区切ります。 実行、 **/check:** コマンドし、ドライバーの Visual Studio プロジェクト ファイルを指定します (\*.vcxproj)。

*ルール*いずれかの名前を指定[ルール](static-driver-verifier-rule.md)またはワイルドカード文字を含むルール名のパターン (\*) を 1 つまたは複数の文字を表します。 ワイルドカード文字を単独で、使用する場合 (\*) すべてのルールを表します。

<span id="________check_rulelist.sdv______"></span><span id="________CHECK_RULELIST.SDV______"></span> **/check:*RuleList*.sdv**   
指定した規則の一覧ファイルの規則に検証を開始します。 このパラメーターを持つ 1 つのファイルを一覧表示できます。 ルールの一覧ファイルの各行が 1 つの規則の名前を指定できますか、ワイルドカード文字であることができます (\*)、すべての SDV のルールを表します。  実行 **/check:*RuleList*.sdv**コマンドし、ドライバーの Visual Studio プロジェクト ファイルを指定します (\*.vcxproj)。

<em>RuleList</em>**.sdv**の完全修飾パスとファイル名には、[規則の一覧ファイル](static-driver-verifier-rule-list-file.md)します。 ファイルが必要、 **.sdv**ファイル名拡張子。 ファイルがローカル ディレクトリにない限り、パスが必要です。 パスまたはファイル名にスペースが含まれる場合囲みます<em>RuleList</em> 。**sdv**引用符で囲んで指定します。

指定した場合、 **/check:** SDV、ルールを指定することがなくオプション設定、ドライバー モデルの既定のルールでが実行されます。

<span id="________lib______"></span><span id="________LIB______"></span> **/lib**   
現在のディレクトリでは、ライブラリを処理します。 SDV は、コンパイルし、外部の使用のためのライブラリをビルドする MSBuild.exe を呼び出すし、ライブラリ、ドライバーの検証に含めるために必要なファイルが生成されます。

ライブラリが必要なドライバーを検証する前に、このパラメーターを使用します。 実行、 **msbuild/t:sdv/p:Inputs =「/lib」** コマンドし、Visual Studio プロジェクト ファイルを指定します (\*.vcxproj) ライブラリ。

使用と、その効果の詳細については、 **/lib**パラメーターを参照してください[ライブラリは、Static Driver Verifier で処理](library-processing-in-static-driver-verifier.md)します。

<span id="________view______"></span><span id="________VIEW______"></span> **/view**   
Static Driver Verifier を開きます。 実行 **/ビュー**コマンドし、ドライバーの Visual Studio プロジェクト ファイルを指定します (\*.vcxproj)。

結果の検証が完了すると、すぐに利用を使用するまで使用できます、 **/clean**ドライバーのプロジェクト ディレクトリからファイルを SDV を削除するコマンド。

<span id="________clean______"></span><span id="________CLEAN______"></span> **/clean**   
SDV のファイルをディレクトリから削除します。 これらのファイル、静的ドライバー検証ツールのレポートの表示を生成するため、 **/clean**コマンドでは、検証のレポートも削除されます。

実行、 **/clean**コマンドし、Visual Studio プロジェクト ファイルを指定します (\*.vcxproj) ドライバーまたはライブラリです。 コマンドは、指定されたプロジェクトに対してのみ SDV ファイルを削除します。

実行、 **/clean**ドライバー プロジェクトの各検証する前にコマンド。

実行、 **/clean**ライブラリ ファイルがライブラリ コードが変更されたときなど、古くなったライブラリ コマンド。

A **/clean**ユーザー承認済みフラグが設定されている場合は、コマンドには、Sdv map.h ファイルは削除されません Sdv map.h ファイルで true (承認済み = true)。 SDV は、今後の認証、このファイルを使用できます。

<span id="_______________"></span> **/?**   
SDV コマンドの使用状況を表示します。 このパラメーターを使用するコマンドは、ビルド環境のウィンドウで実行する必要はありません。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>コメント

Running **msbuild /t:/sdv p:/Inputs= /?** パラメーターを指定せずには、SDV コマンドの使用状況を表示します。

A **/clean**コマンドは、SDV を使用して検証用の静的ドライバー検証ツールのレポートの表示を作成するファイルを削除します。 このコマンドを実行した後、確認のための静的ドライバー検証ツールのレポートの表示は使用できなくします。

### <a name="span-idexamplesspanspan-idexamplesspanexamples"></a><span id="examples"></span><span id="EXAMPLES"></span>例

<span id="To_run_SDV_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="to_run_sdv_using_all_rules_on_the_driver_files_in_the_local_directory_for_the_mydriver_project_"></span><span id="TO_RUN_SDV_USING_ALL_RULES_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_FOR_THE_MYDRIVER_PROJECT_"></span>SDV mydriver プロジェクト用のローカル ディレクトリにドライバー ファイルのすべてのルールを使用してを実行します。  
```
msbuild /t:sdv /p:Inputs="/check:*" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_run_SDV_using_the_CancelSpinLock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="to_run_sdv_using_the_cancelspinlock_rule_on_the_driver_files_in_the_local_directory_"></span><span id="TO_RUN_SDV_USING_THE_CANCELSPINLOCK_RULE_ON_THE_DRIVER_FILES_IN_THE_LOCAL_DIRECTORY_"></span>SDV を使用して実行する、 [CancelSpinLock](https://msdn.microsoft.com/library/windows/hardware/ff542478)ローカル ディレクトリにドライバー ファイルの規則。  
```
msbuild /t:sdv /p:Inputs="/check:CancelSpinLock" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_using_the_rule_that_is_specified_in_the_rules1.sdv_rule_list_file_in_the_d__sdv_directory_"></span><span id="TO_RUN_SDV_USING_THE_RULE_THAT_IS_SPECIFIED_IN_THE_RULES1.SDV_RULE_LIST_FILE_IN_THE_D__SDV_DIRECTORY_"></span>SDV は、d: Rules1.sdv ルール一覧のファイルで指定されている規則を使用してを実行する\\SDV ディレクトリ。  
```
msbuild /t:sdv /p:Inputs="/check:D:\SDV\Rules1.sdv" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

<span id="to_run_sdv_again__this_time_using_the__clean_option."></span><span id="TO_RUN_SDV_AGAIN__THIS_TIME_USING_THE__CLEAN_OPTION."></span>SDV をもう一度実行するには、/clean を使用して、この時間は次のオプションします。  
```
msbuild /t:sdv /p:Inputs="/clean" mydriver.VcxProj /p:Configuration="Windows 7 Release"/p:Platform=Win32
```

<span id="To_display_Static_Driver_Verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="to_display_static_driver_verifier__so_that_you_can_view_the_results_for_the_most_recent_verification_of_the_driver_in_the_local_directory_"></span><span id="TO_DISPLAY_STATIC_DRIVER_VERIFIER__SO_THAT_YOU_CAN_VIEW_THE_RESULTS_FOR_THE_MOST_RECENT_VERIFICATION_OF_THE_DRIVER_IN_THE_LOCAL_DIRECTORY_"></span>ローカル ディレクトリにドライバーの最新の検証の結果を表示できるように、Static Driver Verifier を表示。  
```
msbuild /t:sdv /p:Inputs="/view" mydriver.VcxProj /p:Configuration="Windows 7 Release" /p:Platform=Win32
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Static Driver Verifier を使用して Windows ドライバーで障害が検出するには](using-static-driver-verifier-to-find-defects-in-drivers.md)

 

 






