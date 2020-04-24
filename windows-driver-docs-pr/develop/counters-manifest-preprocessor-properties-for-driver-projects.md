---
ms.assetid: 216E5337-0B05-4560-92AF-0D7AB90EAEEB
title: ドライバー プロジェクトのカウンター マニフェスト プリプロセッサ プロパティ
description: カウンター マニフェストの解析と検証を行う CTRPP ツールのプロパティを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f33684b24b51557b594f9153c82048a3e396cae3
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67370819"
---
# <a name="counters-manifest-preprocessor-properties-for-driver-projects"></a>ドライバー プロジェクトのカウンター マニフェスト プリプロセッサ プロパティ

カウンター マニフェストの解析と検証を行う [CTRPP](https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp) ツールのプロパティを設定します。 パフォーマンス カウンターの操作について詳しくは、「[パフォーマンス カウンター](https://docs.microsoft.com/windows/desktop/PerfCtrs/performance-counters-portal)」をご覧ください。 カーネル モード Windows ドライバーでのパフォーマンス カウンターの使用方法については、「[カーネル モードのパフォーマンスの監視](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-mode-performance-monitoring)」をご覧ください。

## <a name="span-idsetting_the_counters_manifest_preprocessor_properties_for_driver_projectsspanspan-idsetting_the_counters_manifest_preprocessor_properties_for_driver_projectsspanspan-idsetting_the_counters_manifest_preprocessor_properties_for_driver_projectsspansetting-the-counters-manifest-preprocessor-properties-for-driver-projects"></a><span id="Setting_the_Counters_Manifest_Preprocessor_properties_for_driver_projects"></span><span id="setting_the_counters_manifest_preprocessor_properties_for_driver_projects"></span><span id="SETTING_THE_COUNTERS_MANIFEST_PREPROCESSOR_PROPERTIES_FOR_DRIVER_PROJECTS"></span>ドライバー プロジェクトのカウンター マニフェスト プリプロセッサ プロパティの設定


1.  ドライバー プロジェクトのプロパティ ページを開きます。 **ソリューション エクスプローラー**でドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで、 **[構成プロパティ]** をクリックし、 **[Counters Manifest Preprocessor Properties]** (カウンター マニフェスト プリプロセッサ プロパティ) をクリックします。
3.  プロジェクトのプロパティを設定します。

このプロパティ ページをプロジェクトに追加して、ビルド プロセス中に CTRPP ツールを実行できるようにする方法については、「[WDK と Visual Studio のビルド環境](https://docs.microsoft.com/windows-hardware/drivers/devtest/wdk-and-visual-studio-build-environment)」と「[Ctrpp タスク](https://docs.microsoft.com/windows-hardware/drivers/devtest/ctrpp-task)」をご覧ください。

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
<td align="left"><p><span id="Add_Prefix"></span><span id="add_prefix"></span><span id="ADD_PREFIX"></span>プレフィックスの追加</p></td>
<td align="left"><p>生成されたヘッダー ファイルで定義されているグローバル変数および関数に使うプレフィックスを指定します (<strong>-prefix</strong> コマンド オプションと同じ)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Additional_Options"></span><span id="additional_options"></span><span id="ADDITIONAL_OPTIONS"></span>追加オプション</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp" data-raw-source="[&lt;strong&gt;CTRPP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp)"><strong>CTRPP</strong></a> ツールへの追加オプションを指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Backward_Compatibility"></span><span id="backward_compatibility"></span><span id="BACKWARD_COMPATIBILITY"></span>下位互換性</p></td>
<td align="left"><p>Windows 7 より前のバージョンの Windows とバイナリ レベルで互換性のあるコードを生成します (<strong>-backcompat</strong> コマンド オプションと同じ)。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Legacy"></span><span id="enable_legacy"></span><span id="ENABLE_LEGACY"></span>Enable Legacy (レガシを有効にする)</p></td>
<td align="left"><p>Windows Vista のコード テンプレートを使うコード生成に戻します。 このオプションを指定すると、<a href="https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp" data-raw-source="[&lt;strong&gt;CTRPP&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp)"><strong>CTRPP</strong></a> によって 4 つの出力ファイル (2 つのヘッダー ファイル (.h、_r.h)、1 つのリソース ファイル (.rc)、1 つのソース コード ファイル (c)) が生成されます。 (<strong>-legacy</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_header_file_for_containing_counter_names_and_GUIDs"></span><span id="generate_header_file_for_containing_counter_names_and_guids"></span><span id="GENERATE_HEADER_FILE_FOR_CONTAINING_COUNTER_NAMES_AND_GUIDS"></span>Generate header file for containing counter names and GUIDs (カウンター名と GUID を格納するためのヘッダー ファイルを生成する)</p></td>
<td align="left"><p>マニフェスト内の各カウンター セットのカウンター セットの名前と GUID にシンボルを割り当てるヘッダー ファイルを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_header_file_for_provider"></span><span id="generate_header_file_for_provider"></span><span id="GENERATE_HEADER_FILE_FOR_PROVIDER"></span>Generate header file for provider (プロバイダーのヘッダー ファイルを生成する)</p></td>
<td align="left"><p>ツールによって生成されるヘッダー ファイルの名前を指定します。 パスを指定しない場合、ファイルは現在のフォルダーに生成されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_Memory_Routines"></span><span id="generate_memory_routines"></span><span id="GENERATE_MEMORY_ROUTINES"></span>Generate Memory Routines (メモリ ルーチンを生成する)</p></td>
<td align="left"><p>メモリ割り当て/フリー ルーチン テンプレートを生成します。 (<strong>-MemoryRoutines</strong>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_Notification_Callback"></span><span id="generate_notification_callback"></span><span id="GENERATE_NOTIFICATION_CALLBACK"></span>Generate Notification Callback (通知コールバックを生成する)</p></td>
<td align="left"><p>カスタマイズされた通知コールバック テンプレートを生成します。 (<strong>-NotificationCallback</strong> )</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generate_resource_file"></span><span id="generate_resource_file"></span><span id="GENERATE_RESOURCE_FILE"></span>Generate resource file (リソース ファイルを生成する)</p></td>
<td align="left"><p>ツールによって生成されるリソース ファイルの名前を指定します。 パスを指定しない場合、ファイルは現在のフォルダーに生成されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Generate_Summary_Global_File"></span><span id="generate_summary_global_file"></span><span id="GENERATE_SUMMARY_GLOBAL_FILE"></span>Generate Summary Global File (要約グローバル ファイルを生成する)</p></td>
<td align="left"><p>プロバイダーごとにバイナリ カウンター ファイルを生成します。 (<strong>-summary</strong> <em>path</em>)</p>
<p>要約グローバル ファイル GenSumResource.BIN を生成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Generated_Counter_Files_Path"></span><span id="generated_counter_files_path"></span><span id="GENERATED_COUNTER_FILES_PATH"></span>Generated Counter Files Path (生成されるカウンター ファイルのパス)</p></td>
<td align="left"><p>バイナリ カウンター ファイルを生成するパスを指定します。 (<strong>-sumPath</strong> <em>path</em>)</p>
<p>パスを指定しない場合、現在のディレクトリが使われます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Header_File_Name_For_Counter"></span><span id="header_file_name_for_counter"></span><span id="HEADER_FILE_NAME_FOR_COUNTER"></span>Header File Name For Counter (カウンターのヘッダー ファイル名)</p></td>
<td align="left"><p>カウンター名と ID を格納するためのヘッダー ファイルを生成します。 (<strong>-ch</strong> <em>filename</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Header_FileName_For_Provider"></span><span id="header_filename_for_provider"></span><span id="HEADER_FILENAME_FOR_PROVIDER"></span>Header FileName For Provider (プロバイダーのヘッダー ファイル名)</p></td>
<td align="left"><p>プロバイダーのヘッダー ファイルを生成します。 既定の名前を置き換えます。 (<strong>-o</strong> <em>filename</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Resource_File_Name"></span><span id="resource_file_name"></span><span id="RESOURCE_FILE_NAME"></span>Resource File Name (リソース ファイル名)</p></td>
<td align="left"><p>リソース ファイルの名前を指定します。 これは既定の名前を置き換えます。 (<strong>-rc</strong> <em>filename</em>)</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idcommentspanspan-idcommentspanspan-idcommentspancomment"></a><span id="Comment"></span><span id="comment"></span><span id="COMMENT"></span>コメント


ツールが生成するファイルの既定の名前は、[**CTRPP**](https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp) ツールに渡すマニフェスト ファイルの名前に基づいて決定されます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [**CTRPP**](https://docs.microsoft.com/windows/desktop/PerfCtrs/ctrpp)
* [パフォーマンス カウンター](https://docs.microsoft.com/windows/desktop/PerfCtrs/performance-counters-portal)
* [カーネル モードのパフォーマンスの監視](https://docs.microsoft.com/windows-hardware/drivers/devtest/kernel-mode-performance-monitoring)
 

 






