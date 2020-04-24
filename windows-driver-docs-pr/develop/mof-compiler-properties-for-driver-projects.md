---
ms.assetid: 4444E8A5-9624-4CA2-84D8-C83A67A2C871
title: ドライバー プロジェクトの MOF コンパイラ プロパティ
description: 管理オブジェクト フォーマット (MOF) コンパイラ (mofcomp.exe) は、MOF ファイルを解析し、MOF ファイルで定義されているクラスとクラス インスタンスを WMI リポジトリに追加します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5fe74aba3fe87b75c37285202bd714eb7e64784
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "67364252"
---
# <a name="mof-compiler-properties-for-driver-projects"></a>ドライバー プロジェクトの MOF コンパイラ プロパティ

管理オブジェクト フォーマット (MOF) コンパイラ (mofcomp.exe) は、MOF ファイルを解析し、MOF ファイルで定義されているクラスとクラス インスタンスを WMI リポジトリに追加します。 ドライバーで MOF ファイルをコンパイルするには、Mofcomp プロパティ ページを使います。 Mofcomp.exe と WMI について詳しくは、「[**mofcomp**](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)」、「[MOF ファイルのコンパイル](https://docs.microsoft.com/windows/desktop/WmiSdk/compiling-mof-files)」、「[ドライバーの MOF ファイルのコンパイル](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)」をご覧ください。

## <a name="span-idsetting_managed_object_format__mof__compiler_properties_for_driver_projectsspanspan-idsetting_managed_object_format__mof__compiler_properties_for_driver_projectsspanspan-idsetting_managed_object_format__mof__compiler_properties_for_driver_projectsspansetting-managed-object-format-mof-compiler-properties-for-driver-projects"></a><span id="Setting_Managed_Object_Format__MOF__Compiler_properties_for_driver_projects"></span><span id="setting_managed_object_format__mof__compiler_properties_for_driver_projects"></span><span id="SETTING_MANAGED_OBJECT_FORMAT__MOF__COMPILER_PROPERTIES_FOR_DRIVER_PROJECTS"></span>ドライバー プロジェクト用の管理オブジェクト フォーマット (MOF) コンパイラ プロパティの設定


1.  ドライバー プロジェクトのプロパティ ページを開きます。 **ソリューション エクスプローラー**でドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで、 **[構成プロパティ]** 、 **[Mof Compiler]** (MOF コンパイラ) の順にクリックします。
3.  プロジェクトのプロパティを設定します。

このプロパティ ページを使えるのは、ソリューションに管理オブジェクト フォーマット (MOF) ファイル (.mof) を追加した場合のみです。

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
<td align="left"><p><span id="Additional_Options"></span><span id="additional_options"></span><span id="ADDITIONAL_OPTIONS"></span><strong>Additional Options (追加オプション)</strong></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp" data-raw-source="[&lt;strong&gt;mofcomp&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)"><strong>mofcomp</strong></a> ツールに渡す追加オプションを指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Amendement"></span><span id="amendement"></span><span id="AMENDEMENT"></span><strong>Amendment (修正)</strong></p></td>
<td align="left"><p>MOF ファイルを、言語に依存しないバージョンと言語固有のバージョンに分割します。 (<strong>-AMENDMENT:</strong><em>Locale</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Authority"></span><span id="authority"></span><span id="AUTHORITY"></span><strong>Authority (機関)</strong></p></td>
<td align="left"><p>WMI へのログオン時に使う機関 (ドメイン名) として <Authority> を指定します。 (<strong>-A:</strong><em>Authority</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Auto_Recover"></span><span id="auto_recover"></span><span id="AUTO_RECOVER"></span><strong>Auto Recover (自動回復)</strong></p></td>
<td align="left"><p>指定した MOF ファイルを、リポジトリ回復時にコンパイルされるファイルの一覧に追加します。 (<strong>-autorecover</strong>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Create_Binary_Mof_File"></span><span id="create_binary_mof_file"></span><span id="CREATE_BINARY_MOF_FILE"></span><strong>Create Binary Mof File (バイナリ MOF ファイルの作成)</strong></p></td>
<td align="left"><p>WMI リポジトリに変更を加えることなく、<Filename> に指定した名前でコンパイラがバイナリ バージョンの MOF ファイルを作ることを要求します。 (<strong>-B:</strong><em>Filename</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Language_Neutral_Output"></span><span id="language_neutral_output"></span><span id="LANGUAGE_NEUTRAL_OUTPUT"></span><strong>Language Neutral Output (言語に依存しない出力)</strong></p></td>
<td align="left"><p>言語に依存しない出力の名前です。 (<strong>-MOF:</strong><em>Path</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Language_Specific_Output"></span><span id="language_specific_output"></span><span id="LANGUAGE_SPECIFIC_OUTPUT"></span><strong>Language Specific Output (言語固有の出力)</strong></p></td>
<td align="left"><p>言語固有の出力の名前です。 (<strong>-MFL:</strong><em>Path</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Mof_Class"></span><span id="mof_class"></span><span id="MOF_CLASS"></span><strong>Mof Class (MOF クラス)</strong></p></td>
<td align="left"><p>MOF クラスを作成または更新します。</p>
<p><strong>Create Only (作成のみ) (-class:createonly)</strong>: コンパイラが既存のクラスを変更しないよう要求します。 このスイッチを指定すると、MOF ファイルで指定されたクラスが既に存在する場合、コンパイル処理が終了します。</p>
<p><strong>Force Update (強制的に更新) (class:forceupdate)</strong>: 競合する子クラスが存在しても、強制的にクラスを更新します。</p>
<p><strong>Safe Update (安全な更新) (-class:safeupdate)</strong>: 子クラスが存在しても、変更によって子クラスで競合が発生しない場合に限り、クラスの更新を許可します。</p>
<p><strong>Update Only (更新のみ) (-class:updateonly)</strong>: コンパイラが新しいクラスを作らないよう要求します。</p>
<p></p>
<p>詳しくは、「<a href="https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp" data-raw-source="[&lt;strong&gt;mofcomp&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)"><strong>mofcomp</strong></a>」をご覧ください。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="NamespacePath"></span><span id="namespacepath"></span><span id="NAMESPACEPATH"></span><strong>NamespacePath</strong></p></td>
<td align="left"><p><em>namespacepath</em> として指定した名前空間に、コンパイラが MOF ファイルを読み込むことを要求します。 (<strong>-N:</strong><em>namespacepath</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Resource_Locale"></span><span id="resource_locale"></span><span id="RESOURCE_LOCALE"></span><strong>Resource Locale (リソース ロケール)</strong></p></td>
<td align="left"><p>-ER スイッチと組み合わせて使うと、MOF についてのローカライズされた説明テキストをバイナリ MOF から抽出します。 (<strong>-L:</strong><em>ResourceLocale</em>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Resource_Name"></span><span id="resource_name"></span><span id="RESOURCE_NAME"></span><strong>Resource Name (リソース名)</strong></p></td>
<td align="left"><p>指定したリソースからバイナリ MOF を抽出します。 (<strong>-ER:</strong><em>ResourceName</em>)</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Syntax_Check"></span><span id="syntax_check"></span><span id="SYNTAX_CHECK"></span><strong>Syntax Check (構文チェック)</strong></p></td>
<td align="left"><p>コンパイラが構文チェックだけを実行して適切なエラー メッセージを出力することを要求します。 その他のオプションを <strong>[Syntax Check]</strong> (構文チェック) オプションと共に使うことはできません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="WMI_Syntax_Check"></span><span id="wmi_syntax_check"></span><span id="WMI_SYNTAX_CHECK"></span><strong>WMI Syntax Check (WMI 構文チェック)</strong></p></td>
<td align="left"><p>コンパイラが WMI 構文チェック (<strong>-WMI</strong>) を実行することを要求します。 このオプションを選ぶ場合は、<strong>[Create Binary Mof File (バイナリ MOF ファイルの作成)]</strong> オプション (<strong>-B:</strong><em>Filename</em>) を選ぶ必要があります。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [MOF ファイルのコンパイル](https://docs.microsoft.com/windows/desktop/WmiSdk/compiling-mof-files)
* [ドライバーの MOF ファイルのコンパイル](https://docs.microsoft.com/windows-hardware/drivers/kernel/compiling-a-driver-s-mof-file)
* [**mofcomp**](https://docs.microsoft.com/windows/desktop/WmiSdk/mofcomp)
 

 






