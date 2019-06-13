---
ms.assetid: 18A9ACEF-51F8-4BC0-B305-F58287AD321C
title: ドライバー プロジェクトの Stampinf プロパティ
description: Stampinf ツール用のプロパティを設定します。 ドライバーをビルドするときに、Stampinf を使って共通の INF ファイル ディレクティブと INX ファイル ディレクティブを更新できます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6632940446faca6eca437376214f902fad7dbf2
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63378445"
---
# <a name="stampinf-properties-for-driver-projects"></a>ドライバー プロジェクトの Stampinf プロパティ

[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786) ツール用のプロパティを設定します。 ドライバーをビルドするときに、Stampinf を使って共通の INF ファイル ディレクティブと INX ファイル ディレクティブを更新できます。

## <a name="span-idsettingstampinfpropertiesfordriverprojectsspanspan-idsettingstampinfpropertiesfordriverprojectsspanspan-idsettingstampinfpropertiesfordriverprojectsspansetting-stampinf-properties-for-driver-projects"></a><span id="Setting_Stampinf_properties_for_driver_projects"></span><span id="setting_stampinf_properties_for_driver_projects"></span><span id="SETTING_STAMPINF_PROPERTIES_FOR_DRIVER_PROJECTS"></span>ドライバー プロジェクトの Stampinf プロパティの設定


1.  ドライバー プロジェクトのプロパティ ページを開きます。 **ソリューション エクスプローラー**でドライバー プロジェクトを右クリックして、 **[プロパティ]** をクリックします。
2.  ドライバー プロジェクトのプロパティ ページで、 **[構成プロパティ]** 、 **[Stampinf]** (Stampinf) の順にクリックします。
3.  プロジェクトのプロパティを設定します。

このプロパティ ページをプロジェクトに追加して、ビルド プロセス中に Stampinf を実行できるようにする方法については、「[WDK と Visual Studio のビルド環境](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454286)」と「[Stampinf タスク](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)」をご覧ください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Stampinf のオプション</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="Enable_Architecture"></span><span id="enable_architecture"></span><span id="ENABLE_ARCHITECTURE"></span><strong>Enable Architecture (アーキテクチャを有効にする)</strong></p></td>
<td align="left"><p>INX ファイルで使われている $ARCH$ 変数の置換を有効にします。 有効にした場合は、<strong>[Architecture (アーキテクチャ)]</strong> に指定した値が使われます。 <strong>[いいえ]</strong> を指定した場合は、$ARCH$ 変数が削除されます。 たとえば、"Standard.NT$ARCH$" は "Standard.NT" になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Architecture"></span><span id="architecture"></span><span id="ARCHITECTURE"></span><strong>Architecture (アーキテクチャ)</strong></p></td>
<td align="left"><p>INX ファイルで使われている $ARCH$ 変数を置き換える "<em>アーキテクチャ</em>" 文字列を指定します。 既定値は $(InfArch) で、Visual Studio で現在アクティブな構成を選択するマクロです。 指定できる値は <strong>x86</strong>、<strong>x64</strong> です。 この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-a [</strong><em>architecture</em><strong>]</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_VersionStamp"></span><span id="enable_versionstamp"></span><span id="ENABLE_VERSIONSTAMP"></span><strong>Enable VersionStamp (VersionStamp を有効にする)</strong></p></td>
<td align="left"><p>バージョンのタイム スタンプを有効にします。 有効にした場合、<strong>[Driver Version Number (ドライバーのバージョン番号)]</strong> を空にすることはできません。 <strong>[Driver Version Number]</strong> (ドライバーのバージョン番号) は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394)"><strong>INF DriverVer ディレクティブ</strong></a>に書き込まれるバージョン番号の時刻を指定します。 有効にしない場合は、<strong>[Driver Version Number]</strong> (ドライバーのバージョン番号) の下にある、このオプションの既定の動作の説明をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Driver_Version_Number"></span><span id="driver_version_number"></span><span id="DRIVER_VERSION_NUMBER"></span><strong>Driver Version Number (ドライバーのバージョン番号)</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394)"><strong>INF DriverVer ディレクティブ</strong></a>に書き込まれるバージョン番号の時刻を指定します。 時刻の書式は <em>hours.minutes.seconds.milliseconds</em> です (例: 11.30.20.15)。 このオプションはドライバーのバージョン番号を増やす方法として便利であり、開発時に重宝します。 この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-v [</strong> <em>time</em> <strong>| <em>]</strong> を指定するのと同じです。</p>
<p>現在の時刻を使うには、このパラメーターと共にアスタリスク (</em>) を指定します。</p>
<p><em>既定の動作:</em></p>
<p><strong>[Driver Version Number (ドライバーのバージョン番号)]</strong> を指定しない場合、または <strong>[Enable VersionStamp (VersionStamp を有効にする)]</strong> が <strong>[いいえ]</strong> か指定されていない場合、Stampinf は次のバージョン番号値のいずれかを使います。</p>
<ul>
<li><p>STAMPINF_VERSION 環境変数が設定されていると、Stampinf はこの環境変数で指定されているバージョン番号値を使います。</p></li>
<li><p>STAMPINF_VERSION 環境変数が指定されていないと、Stampinf は ntverp.h ファイルからバージョン番号を抽出します。</p></li>
</ul>
<div class="alert">
<strong>注</strong>  既定では、STAMPINF_VERSION 環境変数は、システム環境変数として設定しない限り、ドライバーをビルドするときに設定されません。 この環境変数を Visual Studio のビルド環境で指定するには、「<a href="https://msdn.microsoft.com/Library/Windows/Hardware/ms171459" data-raw-source="[How to: Use Environment Variables in a Build](https://msdn.microsoft.com/Library/Windows/Hardware/ms171459)">ビルドで環境変数を使用する方法</a>」をご覧ください。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_DateStamp"></span><span id="enable_datestamp"></span><span id="ENABLE_DATESTAMP"></span><strong>Enable DateStamp (DateStamp を有効にする)</strong></p></td>
<td align="left"><p>日付スタンプを有効にします。 有効にした場合、<strong>[Driver Version Directive Date (ドライバー バージョン ディレクティブ日付)]</strong> を空にすることはできません。 有効にしない場合は、<strong>[Driver Version Directive Date] (ドライバー バージョン ディレクティブ日付)</strong> の下にある、このオプションの既定の動作の説明をご覧ください。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Driver_Version_Directive_Date"></span><span id="driver_version_directive_date"></span><span id="DRIVER_VERSION_DIRECTIVE_DATE"></span><strong>Driver Version Directive Date (ドライバー バージョン ディレクティブ日付)</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394)"><strong>INF DriverVer ディレクティブ</strong></a>に書き込まれる日付を指定します。 日付の書式は <em>month</em>/<em>date</em>/<em>year</em> です (例: <strong>10/20/2011</strong>)。</p>
<p>現在の日付を使うには、このパラメーターと共にアスタリスク (<strong><em></strong>) を指定します。</p>
<p><em>既定の動作:</em></p>
<p><strong>[Driver Version Directive Date (ドライバー バージョン ディレクティブ日付)]</strong> パラメーターを指定しない場合、または <strong>[Enable DateStamp (DateStamp を有効にする)]</strong> が <strong>[いいえ]</strong> か指定されていない場合、Stampinf は次の日付値のいずれかを使います。</p>
<ul>
<li><p>STAMPINF_DATE 環境変数が設定されていると、Stampinf はこの環境変数で指定されている日付値を使います。</p></li>
<li><p>STAMPINF_DATE 環境変数が指定されていないと、Stampinf は現在の日付を使います。</p></li>
</ul>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-d [</strong><em>date</em><strong>|</em>]</strong> を指定するのと同じです。</p>
<div class="alert">
<strong>注</strong>  既定では、STAMPINF_DATE 環境変数は、システム環境変数として設定しない限り、ドライバーをビルドするときに設定されません。 この環境変数を Visual Studio のビルド環境で指定するには、「<a href="https://msdn.microsoft.com/Library/Windows/Hardware/ms171459" data-raw-source="[How to: Use Environment Variables in a Build](https://msdn.microsoft.com/Library/Windows/Hardware/ms171459)">ビルドで環境変数を使用する方法</a>」をご覧ください。
</div>
<div>
 
</div></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Driver_Version_Directive_Section"></span><span id="driver_version_directive_section"></span><span id="DRIVER_VERSION_DIRECTIVE_SECTION"></span><strong>Driver Version Directive Section (ドライバー バージョン ディレクティブ セクション)</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394" data-raw-source="[&lt;strong&gt;INF DriverVer directive&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394)"><strong>INF DriverVer ディレクティブ</strong></a>を追加する INF セクションを指定します。 このディレクティブの既定の場所は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547502" data-raw-source="[&lt;strong&gt;INF Version section&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547502)"><strong>INF Version セクション</strong></a>です。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-s</strong> <em>section</em> を指定するのと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="KMDF_Version_Number"></span><span id="kmdf_version_number"></span><span id="KMDF_VERSION_NUMBER"></span><strong>KMDF Version Number (KMDF のバージョン番号)</strong></p></td>
<td align="left"><p>このドライバーが依存する KMDF のバージョンを指定します。 これは、INF ファイル内の KmdfLibraryVersion と KMDF 共同インストーラー名をカスタマイズするために使われます。 このオプションは、INF ファイル内の $KMDFVERSION$ キーワードと $KMDFCOINSTALLERVERSION$ キーワードを置き換えます。 この文字列の書式は次のようになります。</p>
<p><em>&lt;major_version&gt;</em>.<em>&lt;minor_version&gt;</em></p>
<p>たとえば、バージョン文字列として 1.5 を指定すると、1 つのキーワードに値 1.5 が使われ、もう 1 つのキーワードに 01005 が使われます。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-k</strong> <em>KMDFversion</em> を指定するのと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="UMDF_Version_Number"></span><span id="umdf_version_number"></span><span id="UMDF_VERSION_NUMBER"></span><strong>UMDF Version Number (UMDF のバージョン番号)</strong></p></td>
<td align="left"><p>このドライバーが依存する UMDF の<em>バージョン</em>を指定します。 このオプションは、INF ファイル内の UmdfLibraryVersion と UMDF 共同インストーラー名を指定するために使われます。 指定した<em>バージョン</em>は、INF ファイル内の $UMDFVERSION$ キーワードと $UMDFCOINSTALLERVERSION$ キーワードを置き換えます。 <em>バージョン</em>の文字列の書式は次のようになります。</p>
<p><em>&lt;major_version&gt;</em>.<em>&lt;minor_version&gt;</em>.<em>&lt;service_version&gt;</em></p>
<p>(<em>&lt;service_version&gt;</em> は通常は 0です)。</p>
<p>たとえば、バージョン文字列として 1.5.0 を指定すると、メジャー キーワードに値 1.5.0 が使われ、マイナー キーワードに 01005 が使われます。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-u</strong> <em>UMDFversion</em> を指定するのと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Catalog_File_Name"></span><span id="catalog_file_name"></span><span id="CATALOG_FILE_NAME"></span><strong>Catalog File Name (カタログ ファイル名)</strong></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff547502" data-raw-source="[&lt;strong&gt;INF Version section&lt;/strong&gt;](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547502)"><strong>INF Version セクション</strong></a>の <strong>CatalogFile</strong> ディレクティブに書き込まれる値を指定します。 既定では、<strong>CatalogFile</strong> ディレクティブは書き込まれません。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-c</strong> <em>catalogfile</em> を指定するのと同じです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Verbose"></span><span id="verbose"></span><span id="VERBOSE"></span><strong>Verbose (詳細)</strong></p></td>
<td align="left"><p>詳細な Stampinf 出力を示します。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-n</strong> を指定するのと同じです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Version_Header_Path"></span><span id="version_header_path"></span><span id="VERSION_HEADER_PATH"></span><strong>Version Header Path (バージョン ヘッダー パス)</strong></p></td>
<td align="left"><p>Ntverp.h ファイルの場所を指定します。 このパスは、Ntverp.h が含まれるディレクトリの完全修飾された場所を表します。</p>
<p>この設定は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786" data-raw-source="[Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)">Stampinf</a> にオプションとして <strong>-i</strong> <em>path</em> を指定するのと同じです。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [Stampinf](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786)
* [**INF DriverVer ディレクティブ**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547394)
* [**INF Version セクション**](https://msdn.microsoft.com/Library/Windows/Hardware/Ff547502)
* [WDK と Visual Studio のビルド環境](https://msdn.microsoft.com/Library/Windows/Hardware/Hh454286)
* [Stampinf タスク](https://msdn.microsoft.com/Library/Windows/Hardware/Ff552786_task)
* 「[ビルドで環境変数を使用する方法](https://msdn.microsoft.com/Library/Windows/Hardware/ms171459)」をご覧ください
 

 






