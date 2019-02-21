---
title: 既定の DEVMODE のセットアップ動作の変更を Unidrv/PScript5 ドライバー
description: 既定の DEVMODE のセットアップ動作の変更を Unidrv/PScript5 ドライバー
ms.assetid: 9760d527-0205-477b-bc16-d6aa65b1eaf7
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea91b2c247f40713a937bcf35958bef0ad55b6df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528044"
---
# <a name="unidrvpscript5-driver-default-devmode-setup-behavior-changes"></a>既定の DEVMODE のセットアップ動作の変更を Unidrv/PScript5 ドライバー


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
<td><p>(Unidrv のみ)DM_ORIENTATION フラグを設定のみ<strong>dmFields</strong> GPD ファイルがサポートしている場合、&quot;向き&quot;GPD 機能。 <strong>dmOrientation</strong>に基づいて設定されている、&quot;向き&quot;GPD 機能&#39;GPD ファイルで指定されている秒の既定のオプション。</p>
<p>(PS のみ)DM_ORIENTATION フラグを設定のみ<strong>dmFields</strong> PPD ファイルの機能をサポートしている場合、 &quot;PageOrientation&quot;印刷スキーマのキーワード。</p>
<p><strong>dmOrientation</strong>に設定されている<strong>DMORIENT_LANDSCAPE</strong>機能で、既定のオプションがある場合、&quot;ランドス ケープ&quot;または&quot;ReverseLandscape&quot;印刷スキーマキーワード。 それ以外の場合、 <strong>dmOrientation</strong>に設定されている<strong>DMORIENT_PORTRAIT</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_SCALE</p></td>
<td><p>(Unidrv のみ)決して DM_SCALE フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p>
<p>(PS のみ)常に DM_SCALE フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p></td>
<td><p>DM_SCALE フラグを設定のみ<strong>dmFields</strong> GPD または PPD の機能をサポートしている場合、 &quot;PageScaling&quot;印刷スキーマのキーワード。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_TTOPTION</p>
<p><strong>dmTTOption</strong></p></td>
<td><p>常に、dmFields DM_TTOPTION フラグを設定し、設定 dmTTOption ハードコーディング DMTT_SUBDEV を = です。</p></td>
<td><p>GPD または PPD の機能をサポートしている場合、 &quot;PageDeviceFontSubstitution&quot;印刷スキーマのキーワードと機能が既定のオプションで、&quot;で&quot;印刷スキーマのキーワード、DM_TTOPTION フラグを設定し、の設定<strong>dmTTOption</strong> = <strong>DMTT_SUBDEV</strong>します。</p>
<p>それ以外の場合、GPD または PPD の機能をサポートしている場合、 &quot;PageTrueTypeFontMode&quot;印刷スキーマのキーワードと、次のいずれか。</p>
<ul>
<li><p>機能の既定のオプションがある場合、 &quot;DownloadAsOutlineFont&quot; DM_TTOPTION フラグを設定して、設定し、印刷スキーマ キーワード<strong>dmTTOption</strong> = <strong>DMTT_DOWNLOAD_OUTLINE</strong>.</p></li>
<li><p>機能の既定のオプションがある場合、 &quot;RenderAsBitmap&quot; DM_TTOPTION フラグを設定して、設定し、印刷スキーマ キーワード<strong>dmTTOption</strong> = <strong>DMTT_BITMAP</strong>;</p></li>
<li><p>機能の既定のオプションがある場合&quot;自動&quot;、 &quot;DownloadAsRasterFont&quot;、または&quot;DownloadAsNativeTrueTypeFont&quot;印刷スキーマのキーワードが DM_TTOPTION フラグを設定し、設定と<strong>dmTTOption</strong> = <strong>DMTT_DOWNLOAD</strong>します。</p></li>
</ul>
<p>DM_TTOPTION フラグをクリアする場合は、 <strong>dmFields</strong>プリンターがまたはダウンロードする TrueType フォントの置き換えをサポートしていることを指定していないためです。</p></td>
</tr>
<tr class="even">
<td><p><strong>dmFields</strong>:</p>
<p>DM_NUP</p></td>
<td><p>常に DM_NUP フラグを設定するためにハードコーディング<strong>dmFields</strong>します。</p></td>
<td><p>DM_NUP フラグを設定のみ<strong>dmFields</strong> GPD または PPD の機能をサポートしている場合、 &quot;JobNUpAllDocumentsContiguously または&quot;DocumentNUp&quot;印刷スキーマのキーワード。</p></td>
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
<td><p>のみで DM_PRINTQUALITY と DM_YRESOLUTION フラグを設定<strong>dmFields</strong> GPD または PPD がサポートしている場合、&quot;解決&quot;GPD または PPD 機能。</p></td>
</tr>
<tr class="odd">
<td><p><strong>dmFields</strong>:</p>
<p>DM_COLLATE</p>
<p><strong>dmCollate</strong></p></td>
<td><p>常に DM_COLLATE フラグを設定するためにハードコーディング<strong>dmFields</strong>、設定と<strong>dmCollate</strong> DMCOLLATE_TRUE を = です。</p></td>
<td><p>DM_COLLATE フラグを設定のみ<strong>dmFields</strong> GPD または PPD がサポートしている場合、 &quot;Collate&quot; GPD または PPD 機能。 <strong>dmCollate</strong>に基づいて設定されている、 &quot;Collate&quot; GPD または PPD 機能&#39;GPD または PPD. で指定されている秒の既定のオプション</p></td>
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

 

 

 




