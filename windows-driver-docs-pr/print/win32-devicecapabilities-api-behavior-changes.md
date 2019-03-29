---
title: Win32 DeviceCapabilities API 動作変更
description: Win32 DeviceCapabilities API 動作変更
ms.assetid: 44745e33-2bd8-4200-be29-b3ddb0e30de4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9631053a57ee794600b353d06f4bcbce48bcbe52
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463903"
---
# <a name="win32-devicecapabilities-api-behavior-changes"></a>Win32 DeviceCapabilities API 動作変更


XPSDrv モードで実行されている Unidrv/PScript5 ドライバーでは、Microsoft Win32 では、次の変更を作成**DeviceCapabilities**関数。

GPD/PPD 機能またはオプションがマップされている場合、印刷スキーマ キーワードに GPD を使用して**PrintSchemaKeywordMap**または PPD の**MSPrintSchemaKeywordMap**キーワード、GPD または PPD、スキーマのキーワードの印刷をサポートしています。

(次の表に"PS のみ"方法動作の変更は PScript5 ドライバーに固有です。 "Unidrv のみ"の意味、動作の変更は、Unidrv ドライバーに固有です。 これらのフレーズの両方が表示されない場合、動作の変更に適用 Unidrv と PScript5 ドライバー)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>XPSDrv 以外の動作</th>
<th>XPSDrv 動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>DC_COPIES</p></td>
<td><p>(Unidrv のみ)EMF を有効にすると、 <strong>DeviceCapabilitiesreturns</strong>が 9999 の最大値または GPD のファイルをハード コーディングされた値の指定した * MaxCopies 値。</p>
<p>EMF を無効にすると、 <strong>DeviceCapabilities</strong> GPD を返します * MaxCopies 値。</p>
<p>(PS のみ)<strong>DeviceCapabilities</strong> 9999 のハード コーディングされた値を返します。</p></td>
<td><p>(Unidrv のみ)<strong>DeviceCapabilities</strong> GPD を返します * MaxCopies 値。</p>
<p>(PS のみ)<strong>DeviceCapabilities</strong> PPD ファイルを返します * MSXPSMaxCopies 値または PPD ファイルに値が指定されていない場合は 1 です。</p></td>
</tr>
<tr class="even">
<td><p>DC_TRUETYPE</p></td>
<td><p>Unidrv の場合、* FontFormat GPD キーワードを指定すると、 <strong>DeviceCapabilities</strong>を返します (DCTT_BITMAP |DCTT_DOWNLOAD)。それ以外の場合、 <strong>DeviceCapabilities</strong> DCTT_BITMAP を返します。</p>
<p>PS の<strong>DeviceCapabilities</strong>は常に返します (DCTT_DOWNLOAD |DCTT_SUBDEV)。</p></td>
<td><p>GPD または PPD 印刷スキーマの"PageDeviceFontSubstitution"キーワードを使用して機能をサポートする場合、DCTT_SUBDEV フラグは、戻り値で設定されます。</p>
<p>GPD または PPD 印刷スキーマの"PageTrueTypeFontMode"キーワードを使用して機能をサポートする場合、次の処理が発生します。</p>
<ul>
<li><p>機能は、印刷スキーマの"DownloadAsOutlineFont"キーワードを使用してオプションをサポートする場合、DCTT_DOWNLOAD と DCTT_DOWNLOAD_OUTLINE フラグは、戻り値に設定されます。</p></li>
<li><p>機能は、「自動」、"DownloadAsRasterFont"または"DownloadAsNativeTrueTypeFont"印刷スキーマのキーワードを使用してオプションをサポートする場合 DCTT_DOWNLOAD フラグは、戻り値に設定されます。</p></li>
<li><p>機能は、印刷スキーマの"RenderAsBitmap"キーワードを使用してオプションをサポートする場合 DCTT_BITMAP フラグは、戻り値で設定されます。</p></li>
</ul>
<p>場合、DCTT_ いずれ<em>Xxx</em>フラグが設定されている<strong>DeviceCapabilities</strong> 0 を返します。</p></td>
</tr>
<tr class="odd">
<td><p>DC_ORIENTATION</p></td>
<td><p>(PS のみ)<strong>DeviceCapabilities</strong> 90 または 270 PPD のに基づいて返します * LandscapeOrientation 値とハード コードされた横 (回転) 印刷の向きの設定のオプション、入力の DEVMODE 構造体。</p></td>
<td><p>(PS のみ)既定の戻り値は、0 で、横方向がないことを意味します。</p>
<p>PPD 印刷スキーマの"PageOrientation"キーワードを使用して機能をサポートする場合、次の処理が発生します。</p>
<ul>
<li><p>機能は、印刷スキーマの「ランドス ケープ」キーワードを使ってオプションをサポートしている場合<strong>DeviceCapabilities</strong> 90 を返します。</p></li>
<li><p>機能は、印刷スキーマの"ReverseLandscape"キーワードを使ってオプションをサポートしている場合<strong>DeviceCapabilities</strong> 270 を返します。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>DC_COLLATE</p></td>
<td><p>EMF を有効にすると、 <strong>DeviceCapabilities</strong>ハードコーディングしていますが、(つまり照合がサポートされていること) 1 を返します。</p>
<p>EMF を無効にすると、 <strong>DeviceCapabilities</strong> GPD または PPD はサポートされている機能として Collate を指定する場合と、部単位印刷 GPD または PPD 機能は任意のデバイス設定の機能によって制約されない場合は 1 を返します。 それ以外の場合、 <strong>DeviceCapabilities</strong> 0 を返します。</p></td>
<td><p>動作は無効になっている EMF のドライバーが XPSDrv 以外の場合と同様です。</p></td>
</tr>
<tr class="odd">
<td><p>DC_NUP</p></td>
<td><p><strong>DeviceCapabilities</strong>を 1、2、4、6、9、または 16 ups のサポートを示すためにハード コーディングされた値を返します。</p></td>
<td><p>GPD または PPD、印刷スキーマの"DocumentNUp"キーワード ("DocumentNUp"機能のみを使用"JobNUpAllDocumentsContiguously"機能が存在しない場合)、数値とオプション GPD/PPD キーワードの名前を指定したオプションがその機能のための機能を定義している場合数 (つまり、1、2、6、およびなど)、数値の数はシート値ごとのサポートされているページのいずれかとして報告されます。</p>
<p>それ以外の場合、XPSDrv 後処理がサポートされていないことが報告されます。</p></td>
</tr>
<tr class="even">
<td><p>DC_PERSONALITY</p></td>
<td><p>Unidrv で定義されている文字列を返します * パーソナリティまたは * rcPersonalityID GPD キーワード。</p>
<p>PS"PostScript"を常に返します。</p></td>
<td><p>動作を維持同じ XPSDrv 以外のドライバーの場合とします。</p></td>
</tr>
<tr class="odd">
<td><p>DC_MEDIAREADY</p></td>
<td><p>用紙トレイの割り当てのテーブルが作成されることがある場合<strong>DeviceCapabilities</strong>が割り当てられている、トレイの表に記載されている一意のフォームの名前を返します。</p>
<p>用紙トレイ割り当てテーブルが作成されていない場合<strong>DeviceCapabilities</strong>メトリック システム以外の既定のロケール、メトリック システムの既定のロケールの"A4"GPD または PPD 定義、既定の用紙サイズ、プリンターでない場合は、「文字」を返します「文字」と"A4"をサポートします。</p></td>
<td><p>動作は、作成された用紙トレイ割り当てテーブルを持たない XPSDrv 以外の場合と同じです。</p></td>
</tr>
<tr class="even">
<td><p>DC_STAPLE</p></td>
<td><p>(PS のみ)PPD は o't では、1 つ「ホチキス止め」機能があります。 PPD 機能を次のいずれかの PPD で定義され、デバイスがホチキス止めをサポートできるかどうかを判断するデバイスの設定によって制約されないかどうか、PScript5 ドライバーを確認します。</p>
<ul>
<li><p>"StapleLocation"</p></li>
<li><p>"StapleX"、"StapleY"</p></li>
<li><p>"StapleWhen"</p></li>
<li><p>"StapleOrientation"</p></li>
</ul></td>
<td><p>(PS のみ)PPD"JobStapleAllDocuments"または"DocumentStaple"印刷スキーマのキーワードを使って機能をサポートしている場合<strong>DeviceCapabilities</strong>をホチキス止めをサポートしているかを示す 1 を返します。 それ以外の場合、 <strong>DeviceCapabilities</strong> 0 を返します。</p></td>
</tr>
</tbody>
</table>

 

 

 




