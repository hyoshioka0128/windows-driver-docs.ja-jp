---
title: Unidrv/PScript5 ドライバーの既定の DEVMODE セットアップ動作変更
description: Unidrv/PScript5 ドライバーの既定の DEVMODE セットアップ動作変更
ms.assetid: 9760d527-0205-477b-bc16-d6aa65b1eaf7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41780d5fd3b6640f209e476b7ba31d3cb55324e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380014"
---
# <a name="unidrvpscript5-driver-default-devmode-setup-behavior-changes"></a>Unidrv/PScript5 ドライバーの既定の DEVMODE セットアップ動作変更


XPSDrv モードで実行されている Unidrv/PScript5 ドライバーでは、既定の DEVMODE セットアップ動作の変更、次のドライバーを作成します。

(次の表に"PS のみ"方法動作の変更は PScript5 ドライバーに固有です。 "Unidrv のみ"の意味、動作の変更は、Unidrv ドライバーに固有です。 これらのフレーズの両方が表示されない場合、動作の変更に適用 Unidrv と PScript5 ドライバー)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>影響を受ける既定の DEVMODE フィールド</th>
<th>XPSDrv 以外の動作</th>
<th>XPSDrv 動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_ORIENTATION</p>
<p><strong>dmOrientation</strong></p></td>
<td><p>常に DM_ORIENTATION フラグを設定するためにハードコーディング<strong>dmFields</strong>、設定と<strong>dmOrientation</strong> DMORIENT_PORTRAIT を = です。</p></td>
<td><p>(Unidrv のみ)DM_ORIENTATION フラグを設定のみ<strong>dmFields</strong> GPD ファイルが「方向」GPD をサポートしているかどうかは機能します。 <strong>dmOrientation</strong> GPD「方向」のセットが基づく GPD ファイルで指定されている機能の既定のオプション。</p>
<p>(PS のみ)DM_ORIENTATION フラグを設定のみ<strong>dmFields</strong> PPD ファイルは、印刷スキーマの"PageOrientation"キーワードを使用して機能をサポートしている場合。</p>
<p><strong>dmOrientation</strong>に設定されている<strong>DMORIENT_LANDSCAPE</strong>かどうか、その機能は「横 ()」または"ReverseLandscape"印刷スキーマのキーワードを使用して既定のオプション。 それ以外の場合、 <strong>dmOrientation</strong>に設定されている<strong>DMORIENT_PORTRAIT</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_SCALE</p></td>
<td><p>(Unidrv のみ)決して DM_SCALE フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p>
<p>(PS のみ)常に DM_SCALE フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p></td>
<td><p>DM_SCALE フラグを設定のみ<strong>dmFields</strong> GPD または PPD 印刷スキーマの"PageScaling"キーワードを使用して機能をサポートしている場合。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_TTOPTION</p>
<p><strong>dmTTOption</strong></p></td>
<td><p>常に、dmFields DM_TTOPTION フラグを設定し、設定 dmTTOption ハードコーディング DMTT_SUBDEV を = です。</p></td>
<td><p>DM_TTOPTION フラグを設定し、設定 GPD または PPD 印刷スキーマの"PageDeviceFontSubstitution"キーワードを使用して機能をサポートしています機能印刷スキーマの"オン"のキーワードを使用して既定のオプションがある場合は、 <strong>dmTTOption</strong>  =  。<strong>DMTT_SUBDEV</strong>します。</p>
<p>それ以外の場合、GPD または PPD"PageTrueTypeFontMode"機能をサポートしている場合は、スキーマのキーワードと、次のいずれかに印刷します。</p>
<ul>
<li><p>機能に印刷スキーマの"DownloadAsOutlineFont"キーワードを使用して既定のオプションがある場合は、DM_TTOPTION フラグを設定し、設定<strong>dmTTOption</strong> = <strong>DMTT_DOWNLOAD_OUTLINE</strong>します。</p></li>
<li><p>機能に印刷スキーマの"RenderAsBitmap"キーワードを使用して既定のオプションがある場合は、DM_TTOPTION フラグを設定し、設定<strong>dmTTOption</strong> = <strong>DMTT_BITMAP</strong>;</p></li>
<li><p>機能に「自動」、"DownloadAsRasterFont"または"DownloadAsNativeTrueTypeFont"印刷スキーマのキーワードを使用して既定のオプションがある場合は、DM_TTOPTION フラグを設定し、設定<strong>dmTTOption</strong> = <strong>DMTT_ダウンロード</strong>します。</p></li>
</ul>
<p>DM_TTOPTION フラグをクリアする場合は、 <strong>dmFields</strong>プリンターがまたはダウンロードする TrueType フォントの置き換えをサポートしていることを指定していないためです。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_NUP</p></td>
<td><p>常に DM_NUP フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p></td>
<td><p>DM_NUP フラグを設定のみ<strong>dmFields</strong> GPD または PPD にキーワードを使用して"JobNUpAllDocumentsContiguously または"DocumentNUp"印刷スキーマ機能がサポートしているかどうか。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_COLOR</p></td>
<td><p>常に DM_COLOR フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p></td>
<td><p>DM_COLOR フラグを設定のみ<strong>dmFields</strong> GPD または PPD のプリンターがカラー プリンターが指定されている場合。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_PRINTQUALITY、DM_YRESOLUTION</p></td>
<td><p>(Unidrv のみ)常に DM_PRINTQUALITY フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p>
<p>(PS のみ)常にで DM_PRINTQUALITY と DM_YRESOLUTION フラグを設定するハード コーディングされた<strong>dmFields</strong>します。</p></td>
<td><p>のみで DM_PRINTQUALITY と DM_YRESOLUTION フラグを設定<strong>dmFields</strong> GPD または PPD「解決」GPD または PPD 機能をサポートする場合。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_COLLATE</p>
<p><strong>dmCollate</strong></p></td>
<td><p>常に DM_COLLATE フラグを設定するためにハードコーディング<strong>dmFields</strong>、設定と<strong>dmCollate</strong> DMCOLLATE_TRUE を = です。</p></td>
<td><p>DM_COLLATE フラグを設定のみ<strong>dmFields</strong> GPD または PPD"Collate"GPD または PPD 機能をサポートする場合。 <strong>dmCollate</strong>セット"Collate"GPD または GPD または PPD. で指定されている PPD 機能の既定のオプションに基づく</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_ICMMETHOD、DM_ICMINTENT</p></td>
<td><p>(Unidrv のみ)常にで DM_ICMMETHOD と DM_ICMINTENT フラグを設定するハード コーディングされた<strong>dmFields</strong>します。</p>
<p>(PS のみ)PPD では、プリンターがカラー プリンターを指定する場合は、DM_ICMMETHOD と DM_ICMINTENT フラグを設定<strong>dmFields</strong>します。</p></td>
<td><p>DM_ICMMETHOD または DM_ICMINTENT フラグを設定しないでください<strong>dmFields</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_DITHERTYPE</p></td>
<td><p>(Unidrv のみ)常に DM_DITHERTYPE フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p></td>
<td><p>(Unidrv のみ)DM_DITHERTYPE フラグを設定しない<strong>dmFields</strong>します。</p></td>
</tr>
</tbody>
</table>

 

 

 




