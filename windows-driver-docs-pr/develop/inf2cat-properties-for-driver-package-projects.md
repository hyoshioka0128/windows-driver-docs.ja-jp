---
ms.assetid: 0877831F-2FBF-402E-A01B-B153F2A18AD4
title: ドライバー パッケージ プロジェクトの Inf2Cat プロパティ
description: Inf2Cat ツール用のプロパティを設定します。 Inf2Cat ツールを使って、INF ファイルを持つ任意のドライバー パッケージ用のカタログ ファイルを作ることができます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3bd9988c392bf875e43bf5c87f094f2ef00befd9
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63344154"
---
# <a name="inf2cat-properties-for-driver-package-projects"></a>ドライバー パッケージ プロジェクトの Inf2Cat プロパティ

[  **Inf2Cat**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089) ツール用のプロパティを設定します。 **Inf2Cat** ツールを使って、INF ファイルを持つ任意のドライバー パッケージ用のカタログ ファイルを作ることができます。

## <a name="span-idsettinginf2catpropertiesfordriverpackageprojectsspanspan-idsettinginf2catpropertiesfordriverpackageprojectsspanspan-idsettinginf2catpropertiesfordriverpackageprojectsspansetting-inf2cat-properties-for-driver-package-projects"></a><span id="Setting_Inf2Cat_properties_for_driver_package_projects"></span><span id="setting_inf2cat_properties_for_driver_package_projects"></span><span id="SETTING_INF2CAT_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>ドライバー パッケージ プロジェクトの Inf2Cat プロパティの設定


1.  ドライバー パッケージのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー パッケージ プロジェクトを右クリックし、 **[プロパティ]** をクリックします。
2.  ドライバー パッケージのプロパティ ページで、 **[構成プロパティ]** 、 **[Inf2Cat]** の順にクリックします。
3.  **[Run Inf2Cat (Inf2Cat の実行)]** オプションを選びます。 このオプションは、プロジェクト内のすべての INF ファイル (.inf、.inx、.inv ファイルなど) に対して [**Inf2Cat**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089) ツールを実行します。

INF ファイルを使ってドライバー パッケージがインストールされている場合は、Inf2Cat ツールを使ってカタログ ファイルを作ります。 Inf2Cat は、パッケージ内にある、INF ファイルで参照されているファイルを検証します。 パッケージにファイルを追加するには、パッケージ プロジェクトとドライバー プロジェクトのプロパティ ページを使います。 詳しくは、「[ドライバー パッケージの作成](creating-a-driver-package.md)」をご覧ください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Run_Inf2Cat"></span><span id="run_inf2cat"></span><span id="RUN_INF2CAT"></span><strong>Run Inf2Cat (Inf2Cat の実行)</strong></p></td>
<td align="left"><p>プロジェクト内のすべての INF ファイル (.inf、.inx、.inv ファイルなど) に対して <a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> ツールを実行します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Windows_Version_List"></span><span id="windows_version_list"></span><span id="WINDOWS_VERSION_LIST"></span><strong>Windows Version List (Windows バージョンの一覧)</strong></p></td>
<td align="left"><p>.inf ファイルでサポートされている Windows のバージョンの一覧を指定します。 Windows の各バージョンはコンマで区切ります。 既定の設定は $(Inf2CatWindowsVersionList) で、アクティブなプラットフォームと構成に対してドライバーをビルドするマクロです。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/os:</strong><em>WindowsVersionList</em> を指定するのと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Include_Page_Hashes"></span><span id="include_page_hashes"></span><span id="INCLUDE_PAGE_HASHES"></span><strong>Include Page Hashes (ページ ハッシュを含む)</strong></p></td>
<td align="left"><p>ファイルにページ ハッシュを含めます。 必要に応じて、後にファイルの一覧が続きます。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/pageHashes[:</strong><em>file1</em><strong>[,</strong><em>file2</em><strong>]...]</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Add_PE_Attribute"></span><span id="add_pe_attribute"></span><span id="ADD_PE_ATTRIBUTE"></span><strong>Add PE Attribute (PE 属性の追加)</strong></p></td>
<td align="left"><p>ファイルに PE カタログ属性を追加します。 必要に応じて、後にファイルの一覧が続きます。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/pe[:</strong><em>file1</em><strong>[,</strong><em>file2</em><strong>]...]</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Add_Drm"></span><span id="add_drm"></span><span id="ADD_DRM"></span><strong>Add Drm (DRM の追加)</strong></p></td>
<td align="left"><p>ファイルに DRM レベルのカタログ属性を追加します。 必要に応じて、後にファイルの一覧が続きます。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/drm[:</strong><em>file1</em><strong>[,</strong><em>file2</em><strong>]...]</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verbose"></span><span id="verbose"></span><span id="VERBOSE"></span><strong>Verbose (詳細)</strong></p></td>
<td align="left"><p>Visual Studio の [出力] ウィンドウに、ツールの出力についての詳細情報を表示します。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/verbose</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="No_Catalog"></span><span id="no_catalog"></span><span id="NO_CATALOG"></span><strong>No Catalog (カタログなし)</strong></p></td>
<td align="left"><p>カタログ ファイルが作られないようにします。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/nocat</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Use_Local_Time"></span><span id="use_local_time"></span><span id="USE_LOCAL_TIME"></span><strong>Use Local Time (現地時刻の使用)</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer Directive&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394)"><strong>INF DriverVer ディレクティブ</strong></a>を検証するときにローカル タイム ゾーンを使用します。 既定では、UTC が使われます。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089" data-raw-source="[&lt;strong&gt;Inf2Cat&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)"><strong>Inf2Cat</strong></a> のオプション <strong>/uselocaltime</strong> を指定するのと同じです。</p></td>
</tr>
</tbody>
</table>

 

Inf2Cat ツールの使い方について詳しくは、「[Inf2Cat を使ったカタログ ファイルの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Ff553618)」をご覧ください。

プロパティ ページとプロジェクトについて詳しくは、「[WDK と Visual Studio のビルド環境](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454286)」をご覧ください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [PnP ドライバー パッケージ用のカタログ ファイルの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Ff540161)
* [**Inf2Cat**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547089)
* [ドライバー パッケージの作成](creating-a-driver-package.md)
* [ドライバーへの署名](signing-a-driver.md)
* [Inf2Cat を使ったカタログ ファイルの作成](https://msdn.microsoft.com/Library/Windows/Hardware/Ff553618)
* [WDK と Visual Studio のビルド環境](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454286)
 

 






