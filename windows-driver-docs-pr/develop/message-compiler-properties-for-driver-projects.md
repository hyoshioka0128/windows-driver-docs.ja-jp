---
ms.assetid: 388C0D27-F3B9-4EF0-A03C-B58F38F2EFD6
title: ドライバー プロジェクトのメッセージ コンパイラ プロパティ
description: Message Compiler (MC.exe) ツール用のプロパティを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5cbea73bb79d260dc703c226a5898c2784ecf5
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364258"
---
# <a name="message-compiler-properties-for-driver-projects"></a>ドライバー プロジェクトのメッセージ コンパイラ プロパティ

[  **Message Compiler (MC.exe)** ](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-) ツール用のプロパティを設定します。 コンパイラは、プロジェクトに追加できるメッセージ リソース ファイルを生成します。

たとえば、[Windows イベント トレーシング (ETW)](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-) カーネル モード API を使ってカーネル モード ドライバーにイベント トレーシングを追加している場合、メッセージ コンパイラを使って、イベント プロバイダー、イベント属性、チャネル、イベントの定義を含むヘッダー ファイルを作ることができます。 ソース コードには、このヘッダー ファイルをインクルードする必要があります。 メッセージ コンパイラでは、プロジェクト ファイルに追加するリソース コンパイラ スクリプト (\*.rc) が作成されます。

## <a name="span-idsetting_message_compiler_properties_for_driver_projectsspanspan-idsetting_message_compiler_properties_for_driver_projectsspanspan-idsetting_message_compiler_properties_for_driver_projectsspansetting-message-compiler-properties-for-driver-projects"></a><span id="Setting_Message_Compiler_properties_for_driver_projects"></span><span id="setting_message_compiler_properties_for_driver_projects"></span><span id="SETTING_MESSAGE_COMPILER_PROPERTIES_FOR_DRIVER_PROJECTS"></span>ドライバー プロジェクト用のメッセージ コンパイラ プロパティの設定


1.  ドライバー プロジェクトのプロパティ ページを開きます。 **ソリューション エクスプローラー**でドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで、 **[構成プロパティ]** 、 **[Message Compiler]** (メッセージ コンパイラ) の順にクリックします。
3.  プロジェクトのプロパティを設定します。

このプロパティ ページを使えるのは、ソリューションにメッセージ テキスト ファイル (.mc) かマニフェスト (.man) を追加した場合のみです。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Additional_Options"></span><span id="additional_options"></span><span id="ADDITIONAL_OPTIONS"></span><strong>追加オプション</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-" data-raw-source="[&lt;strong&gt;Message Compiler (MC.exe)&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)"><strong>メッセージ コンパイラ (MC.exe)</strong></a> ツールに渡す追加オプションを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Ansi_Input_File"></span><span id="ansi_input_file"></span><span id="ANSI_INPUT_FILE"></span><strong>Ansi Input File (ANSI 入力ファイル)</strong></p></td>
<td align="left"><p>入力ファイルが ANSI コンテンツ (既定) を含むことを指定します。 (<strong>-a</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Ansi_Message_In_Bin_File"></span><span id="ansi_message_in_bin_file"></span><span id="ANSI_MESSAGE_IN_BIN_FILE"></span><strong>Ansi Message In Bin File (Bin ファイル内の ANSI メッセージ)</strong></p></td>
<td align="left"><p>出力 .bin ファイル内のメッセージが ANSI であることを指定します。 (<strong>-A</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Baseline_Path"></span><span id="baseline_path"></span><span id="BASELINE_PATH"></span><strong>Baseline Path (ベースライン パス)</strong></p></td>
<td align="left"><p>このパスは、ベースライン操作が作成した .BIN ファイルが格納されているフォルダーを指している必要があります。 (<strong>-t</strong> <em>directory</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Baseline_Resource_Path"></span><span id="baseline_resource_path"></span><span id="BASELINE_RESOURCE_PATH"></span><strong>Baseline Resource Path (ベースライン リソース パス)</strong></p></td>
<td align="left"><p>ベースライン マニフェスト ファイルが格納されているフォルダーです。 (<strong>-s</strong> <em>directory</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Debug_Output_Path"></span><span id="debug_output_path"></span><span id="DEBUG_OUTPUT_PATH"></span><strong>Debug Output Path (デバッグ出力パス)</strong></p></td>
<td align="left"><p>.dbg C インクルード ファイルを配置するパスです。 (<strong>-x</strong> <em>path</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_Callout_Macro"></span><span id="enable_callout_macro"></span><span id="ENABLE_CALLOUT_MACRO"></span><strong>Enable Callout Macro (コールアウト マクロを有効にする)</strong></p></td>
<td align="left"><p>ログへの記録時に、コールアウト マクロを追加してユーザー コードを呼び出します。 C# では使用できないため、無視されます。 (<strong>-co</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Debug_Output_Path"></span><span id="enable_debug_output_path"></span><span id="ENABLE_DEBUG_OUTPUT_PATH"></span><strong>Enable Debug Output Path (デバッグ出力パスを有効にする)</strong></p></td>
<td align="left"><p>コンパイラを有効にして <strong>[Debug Output Path (デバッグ出力パス)]</strong> プロパティで指定された .dbg C インクルード ファイルを配置します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="File_extension_for_the_generated_header"></span><span id="file_extension_for_the_generated_header"></span><span id="FILE_EXTENSION_FOR_THE_GENERATED_HEADER"></span><strong>File extension for the generated header (生成されたヘッダーのファイル拡張子)</strong></p></td>
<td align="left"><p>生成されたヘッダー ファイルの拡張子を指定します。 (<strong>-e</strong> <em>extension</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_Baseline_Resource"></span><span id="generate_baseline_resource"></span><span id="GENERATE_BASELINE_RESOURCE"></span><strong>Generate Baseline Resource (ベースライン リソースを生成する)</strong></p></td>
<td align="left"><p>インストルメンテーションのベースラインを作成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_C___managed__logging_class"></span><span id="generate_c___managed__logging_class"></span><span id="GENERATE_C___MANAGED__LOGGING_CLASS"></span><strong>Generate C# (managed) logging class (C# (マネージド) ログ記録クラスを生成する)</strong></p></td>
<td align="left"><p>マニフェストにイベントを記録するために呼び出すメソッドを含む C# (マネージ) ログ記録クラスを生成します。 (<strong>-cs</strong> <em>namespace</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_header_file_for_containing_counter_names_and_GUIDs"></span><span id="generate_header_file_for_containing_counter_names_and_guids"></span><span id="GENERATE_HEADER_FILE_FOR_CONTAINING_COUNTER_NAMES_AND_GUIDS"></span><strong>Generate header file for containing counter names and GUIDs (カウンター名と GUID を格納するためのヘッダー ファイルを生成する)</strong></p></td>
<td align="left"><p>コンパイラが生成したヘッダー ファイルを配置するフォルダーを指定するには、このオプションを使います。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_Kernel_Mode_Logging_Macros"></span><span id="generate_kernel_mode_logging_macros"></span><span id="GENERATE_KERNEL_MODE_LOGGING_MACROS"></span><strong>Generate Kernel Mode Logging Macros (カーネル モード ログ記録マクロを生成する)</strong></p></td>
<td align="left"><p>カーネル モード ログ記録マクロを生成します。 (<strong>-km</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_MOF_File"></span><span id="generate_mof_file"></span><span id="GENERATE_MOF_FILE"></span><strong>Generate MOF File (MOF ファイルを生成する)</strong></p></td>
<td align="left"><p>生成されるすべての関数とマクロに対してダウンレベルのサポートを生成します。 マニフェストから MOF ファイルが生成されます。 MOF ファイルは、<strong>-h</strong> オプション (<strong>-mof</strong>) で指定した場所に配置されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_OLE2_Header"></span><span id="generate_ole2_header"></span><span id="GENERATE_OLE2_HEADER"></span><strong>Generate OLE2 Header (OLE2 ヘッダーを生成する)</strong></p></td>
<td align="left"><p>OLE2 ヘッダー ファイルを生成します。 (<strong>-o</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_static_C___managed__logging_class"></span><span id="generate_static_c___managed__logging_class"></span><span id="GENERATE_STATIC_C___MANAGED__LOGGING_CLASS"></span><strong>Generate static C# (managed) logging class (静的な C# (マネージド) ログ記録クラスを生成する)</strong></p></td>
<td align="left"><p>マニフェストにイベントを記録するために呼び出すメソッドを含む静的な C# (マネージ) ログ記録クラスを生成します。 (<strong>-css</strong> <em>namespace</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_User_Mode_Logging_Macros"></span><span id="generate_user_mode_logging_macros"></span><span id="GENERATE_USER_MODE_LOGGING_MACROS"></span><strong>Generate User Mode Logging Macros (ユーザー モードのログ記録マクロを生成する)</strong></p></td>
<td align="left"><p>ユーザー モードのログ記録マクロを生成します。 (<strong>-um</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generated_Files_Base_Name"></span><span id="generated_files_base_name"></span><span id="GENERATED_FILES_BASE_NAME"></span><strong>Generated Files Base Name (生成されるファイルのベース名)</strong></p></td>
<td align="left"><p>生成されるすべてのファイルのベース名を指定します。 (<strong>-z</strong> <em>basename</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generated_RC_and_Binary_Message_Files_Path"></span><span id="generated_rc_and_binary_message_files_path"></span><span id="GENERATED_RC_AND_BINARY_MESSAGE_FILES_PATH"></span><strong>Generated RC and Binary Message Files Path (生成される RC ファイルとバイナリ メッセージ ファイルのパス)</strong></p></td>
<td align="left"><p>生成される RC ファイルとバイナリ メッセージ ファイルのパスを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Header_File_Path"></span><span id="header_file_path"></span><span id="HEADER_FILE_PATH"></span><strong>Header File Path (ヘッダー ファイル パス)</strong></p></td>
<td align="left"><p>生成されるヘッダー ファイルのパスを指定します。 (<strong>-h</strong> <em>path</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Maximum_Message_Length"></span><span id="maximum_message_length"></span><span id="MAXIMUM_MESSAGE_LENGTH"></span><strong>Maximum Message Length (メッセージの最大長)</strong></p></td>
<td align="left"><p>メッセージのいずれかが指定された文字数を超えた場合にコンパイラで警告が表示されるようにするには、この引数を使います。 (<strong>-m</strong> <em>length</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Prefix_Macro_Name"></span><span id="prefix_macro_name"></span><span id="PREFIX_MACRO_NAME"></span><strong>Prefix Macro Name (マクロ名のプレフィックス)</strong></p></td>
<td align="left"><p>コンパイラがログ記録マクロ名とメソッド名に使う既定のプレフィックスを上書きするには、この引数を使います。 (<strong>-p</strong> <em>prefix</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="RC_File_Path"></span><span id="rc_file_path"></span><span id="RC_FILE_PATH"></span><strong>RC File Path (RC ファイル パス)</strong></p></td>
<td align="left"><p>コンパイラが生成したリソース コンパイラ スクリプト (.rc ファイル) と .bin ファイルを配置するフォルダーです。 (<strong>-r</strong> <em>path</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Remove_Characters_From_Symbolic_Name"></span><span id="remove_characters_from_symbolic_name"></span><span id="REMOVE_CHARACTERS_FROM_SYMBOLIC_NAME"></span><strong>Remove Characters From Symbolic Name (シンボリック名から文字を削除する)</strong></p></td>
<td align="left"><p>イベントに対して指定したシンボリック名の先頭から文字を削除するには、この引数を使います。 (<strong>-P</strong> <em>prefix</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Set_Customer_Bit"></span><span id="set_customer_bit"></span><span id="SET_CUSTOMER_BIT"></span><strong>Set Customer Bit (カスタマー ビットを設定する)</strong></p></td>
<td align="left"><p>メッセージ ID 全体におけるカスタマー ビットを設定します。 (<strong>-c</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Terminate_Message_With_Null"></span><span id="terminate_message_with_null"></span><span id="TERMINATE_MESSAGE_WITH_NULL"></span><strong>Terminate Message With Null (メッセージを null で終了させる)</strong></p></td>
<td align="left"><p>メッセージ テーブル内のすべての文字列を null で終了させます。 (<strong>-n</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Unicode_Input_File"></span><span id="unicode_input_file"></span><span id="UNICODE_INPUT_FILE"></span><strong>Unicode Input File (Unicode 入力ファイル)</strong></p></td>
<td align="left"><p>入力ファイルが Unicode コンテンツを含むことを指定します。 (<strong>-u</strong>)</p>
<p>既定値は ANSI です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Unicode_Message_In_Bin_File"></span><span id="unicode_message_in_bin_file"></span><span id="UNICODE_MESSAGE_IN_BIN_FILE"></span><strong>Unicode Message In Bin File (Bin ファイル内の Unicode メッセージ)</strong></p></td>
<td align="left"><p>出力 .bin ファイル内のメッセージが Unicode であることを指定します。 (<strong>-U</strong>)</p>
<p>これは既定です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Use_Base_Name_Of_Input"></span><span id="use_base_name_of_input"></span><span id="USE_BASE_NAME_OF_INPUT"></span><strong>Use Base Name Of Input (入力のベース名を使う)</strong></p></td>
<td align="left"><p>コンパイラが出力 .bin ファイルの名前に入力ファイルのベース名を使うようにするには、この引数を使います。 (<strong>-b</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Use_Decimal_Values"></span><span id="use_decimal_values"></span><span id="USE_DECIMAL_VALUES"></span><strong>Use Decimal Values (10 進値を使う)</strong></p></td>
<td align="left"><p>ヘッダー ファイル内の Severity 定数と Facility 定数に 16 進値ではなく 10 進値を使うには、この引数を使います。 (<strong>-d</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Validate_Against_Baseline_Resource"></span><span id="validate_against_baseline_resource"></span><span id="VALIDATE_AGAINST_BASELINE_RESOURCE"></span><strong>Validate Against Baseline Resource (ベースライン リソースに照らして検証する)</strong></p></td>
<td align="left"><p>新しいバージョンのマニフェストを作るときに、<strong>-s</strong> オプションを使って作ったベースラインに照らしてそのアプリケーションの互換性を確認するには、この引数を使います。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verbose"></span><span id="verbose"></span><span id="VERBOSE"></span><strong>Verbose (詳細)</strong></p></td>
<td align="left"><p>詳しい出力を生成するには、このオプションを使います。 (<strong>-v</strong>)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [メッセージ コンパイラ (MC.exe)](https://docs.microsoft.com/windows-hardware/drivers/devtest/message-compiler-task)
* [WDK と Visual Studio のビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)メッセージ コンパイラー タスク
* [Windows イベント トレーシング (ETW)](https://docs.microsoft.com/windows-hardware/drivers/devtest/event-tracing-for-windows--etw-)
 

 






