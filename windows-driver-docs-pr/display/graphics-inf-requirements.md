---
title: WDDM 1.2 でのグラフィックス INF 要件
description: Windows 8 で Windows Display Driver Model (WDDM) ドライバーでは、グラフィックス ドライバーの INF 変更が必要です。
ms.assetid: BB1E35B4-8691-4B0C-9D6C-9A7D1ADFAB55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37806f8c74e01be0133a54946e5616b64dfb6462
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349167"
---
# <a name="graphics-inf-requirements-in-wddm-12"></a>WDDM 1.2 でのグラフィックス INF 要件


Windows 8 で Windows Display Driver Model (WDDM) ドライバーでは、グラフィックス ドライバーの INF 変更が必要です。 最も注目すべき変更は、特徴のスコアです。 WDDM 1.2 ドライバーには、WDDM ドライバーを以前よりも高い特徴のスコアが必要です。 このセクションには、Windows 8 のグラフィック ドライバーのすべての関連する INF 要件がについて説明します

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">トピック</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="updated-feature-score-directive.md" data-raw-source="[Updated feature score directive in Windows 8](updated-feature-score-directive.md)">Windows 8 の機能が更新されたスコア ディレクティブ</a></p></td>
<td align="left"><p>更新された機能スコアのディレクティブは、WDDM の後に続くすべての Windows 8 ドライバーに必要なインストールに関する一般的な設定です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driver-matching-criteria.md" data-raw-source="[Driver matching criteria](driver-matching-criteria.md)">ドライバーの一致条件</a></p></td>
<td align="left"><p>このトピックでは、ドライバーの最適な一致の選択に使用される要素について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="updated-friendly-name.md" data-raw-source="[Updated friendly name for WDDM 1.2](updated-friendly-name.md)">WDDM 1.2 の更新のフレンドリ名</a></p></td>
<td align="left"><p>このトピックでは、グラフィックス INF の更新のフレンドリ名を示します。 これは、すべての Windows 8 インボックス ディスプレイ ドライバーの Inf のローカライズ可能な文字列名要件です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="sku-differentiation-directive.md" data-raw-source="[SKU differentiation directive](sku-differentiation-directive.md)">SKU の差別化ディレクティブ</a></p></td>
<td align="left"><p>Windows Server 2008 と Windows Vista SP1 では、インボックスのディスプレイ ドライバーの Inf としてドライバーを表す新しい値を含める変更された<em>クライアントのみ</em>ドライバーはサーバー Sku の Windows でインストールすることを意味します。 このディレクティブは、Windows 8 でのすべてのディスプレイ ドライバーに必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="general-unicode-requirement.md" data-raw-source="[General Unicode requirement in INF files](general-unicode-requirement.md)">INF ファイルに Unicode の一般的な要件</a></p></td>
<td align="left"><p>INF ファイルを保存して; Unicode でエンコードする必要があります。ANSI はできません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="installed-display-drivers-directive.md" data-raw-source="[Installed display drivers directive](installed-display-drivers-directive.md)">インストールされているディスプレイ ドライバー ディレクティブ</a></p></td>
<td align="left"><p>インストールされているディスプレイ ドライバーのディレクティブは、ドライバー パッケージの一部としてインストールされている UMD の適切な名前を指定するソフトウェア デバイス設定です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="copy-flags-to-support-pnp-stop-directive.md" data-raw-source="[Copy flags to support PnP stop directive](copy-flags-to-support-pnp-stop-directive.md)">PnP 停止ディレクティブをサポートするためにフラグをコピーします。</a></p></td>
<td align="left"><p>プラグ アンド プレイ (PnP) の停止ディレクティブ ファイルのセクションのフラグは、WDDM の再起動を必要としないドライバーをアップグレードをサポートする必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="driver-services-start-type-directive.md" data-raw-source="[Driver\services start type directive](driver-services-start-type-directive.md)">Driver\services は、type ディレクティブを開始します。</a></p></td>
<td align="left"><p><em>Driver\services</em>開始 type ディレクティブがすべてのディスプレイ ドライバーのサービスのインストールの設定要件。 WDDM ドライバーがプラグ アンド プレイ (PnP) およびしたがって必要がありますオンデマンド起動、場所<em>StartType</em> = 3。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="capability-override-settings-to-disable-opengl.md" data-raw-source="[Capability override settings to disable OpenGL](capability-override-settings-to-disable-opengl.md)">機能は、OpenGL を無効にする設定を上書き</a></p></td>
<td align="left"><p>すべてのボックスに表示 Inf のこのソフトウェアのデバイス設定では、既製の OpenGL ICDs で可能な相互運用性の問題にインボックス ドライバーを公開しないことが保証されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="-version--section-directives.md" data-raw-source="[[Version] section directives](-version--section-directives.md)">[バージョン] セクション ディレクティブ</a></p></td>
<td align="left"><p>このトピックで説明<em>[バージョン]</em> INF でディレクティブをセクションします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="-sourcedisknames--section-directives.md" data-raw-source="[[SourceDiskNames] section directives](-sourcedisknames--section-directives.md)">[SourceDiskNames] セクション ディレクティブ</a></p></td>
<td align="left"><p>Windows Vista 以降、インボックス Inf の使用、 <em>[SourceDisksXxx]</em>ディレクティブ。 ただし、これらのセクションの値は、何が通常された上記の独立系ハードウェア ベンダー (IHV) 実稼働のドライバー パッケージ内から変更されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="general-x64-directives.md" data-raw-source="[General x64 directives](general-x64-directives.md)">[全般] x 64 ディレクティブ</a></p></td>
<td align="left"><p>このトピックでは、64 ビット Windows で使用するための INF を適切に修飾するために必要な変更について説明します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="general-install-section-directives.md" data-raw-source="[General install section directives](general-install-section-directives.md)">一般的なインストール セクション ディレクティブ</a></p></td>
<td align="left"><p>これは、既製のまたは実稼働/出荷版バイナリ、サービス、regadd、またはしてのセクションでは通常、小売 WHQL ドライバー パッケージの一部であるすべての参照が、Windows のインボックス ドライバー パッケージに表示されません一般的なアラームです。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="-string--section-changes-for-localized-strings.md" data-raw-source="[[String] section changes for localized strings](-string--section-changes-for-localized-strings.md)">ローカライズされた文字列を [文字列] セクションの変更</a></p></td>
<td align="left"><p>この INF 要件により、作業をビルドする擬似ローカライズします。 要件を区切る文字列セクション内で、ローカライズできない文字列とローカライズ可能なです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="driver-dll-for-display-adapter-or-chipset-has-properly-formatted-file-version.md" data-raw-source="[Driver DLL for display adapter or chipset has properly formatted file version](driver-dll-for-display-adapter-or-chipset-has-properly-formatted-file-version.md)">ファイルのバージョンをディスプレイ アダプターまたはチップセット ドライバー DLL が正しく書式設定します。</a></p></td>
<td align="left"><p>このトピックでは、ディスプレイ ドライバー Dll の適切な形式について説明します。</p></td>
</tr>
</tbody>
</table>

 

 

 





