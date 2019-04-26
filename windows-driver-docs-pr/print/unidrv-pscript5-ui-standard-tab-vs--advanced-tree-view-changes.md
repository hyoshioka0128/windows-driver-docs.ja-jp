---
title: Unidrv/PScript5 UI 標準タブと高度なツリー ビュー変更の違い
description: Unidrv/PScript5 UI 標準タブと
ms.assetid: 07374e07-f0ca-4e97-8e5f-e5fe54d14af4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ab8047427c0a4ac56ea048916b22f694d280941
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346590"
---
# <a name="unidrvpscript5-ui-standard-tab-vs-advanced-tree-view-changes"></a>Unidrv/PScript5 UI 標準タブと高度なツリー ビュー変更の違い


した UniDrive/PScript5 ユーザー インターフェイス (UI) では、次のパブリック印刷スキーマ機能がサポートされています。

JobPageOrder

PageOrientation (PS のみ)

PageDeviceFontSubstitution

PageOutputQuality

JobNUpAllDocumentsContiguously または DocumentNUp

GPD を使用してあるカスタム GPD または PPD 機能または前の印刷スキーマ機能にマップされているオプションと、標準の印刷スキーマ オプション場合**PrintSchemaKeywordMap**キーワードまたは PPD の**MSPrintSchemaKeywordMap**キーワード、Unidrv/PScript5 ドライバー UI 機能を示します標準 タブで、GPD ファイルで機能が"XPSDrv以外のモードで実行されているUnidrvまたはPScript5のドライバの出現する同じ方法で。\*ConcealFromUI でしょうか。" "TRUE"に設定します。

(GPD または PPD のカスタム機能からマップされます) がこれらの印刷スキーマ機能が表示されている場合に汎用的な"プリンター"の機能グループではなく Unidrv/Pscript5 ドライバー UI の標準的なタブに、**詳細**ツリー ビュー、標準の UI表示名と COMPSTUI のアイコンが表示されます。 任意の表示名またはアイコン GPD または PPD ファイルで指定されたこれらの機能が無視されます。

これらの標準的な印刷機能の一貫性のある Unidrv/PScript5 ドライバー UI を表示するには、XPSDrv モードで実行されている Unidrv/PScript5 ドライバーには、次の動作が持っています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>印刷スキーマにマップする機能</th>
<th>XPSDrv 動作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JobPageOrder</p></td>
<td><p>GPD または PPD ファイルは、印刷スキーマの"JobPageOrder"キーワードを持つ特徴を定義します機能がある、"標準"正確に 2 つのオプションと"リバース"スキーマのキーワードを印刷し場合でその機能が示すように、<strong>ページの順序</strong>内の領域。標準<strong>レイアウト</strong>タブ。ジェネリック"プリンター"の機能グループ内にある、GPD または PPD 機能が示すように、それ以外の場合、<strong>詳細</strong>ツリー ビューの UI。</p>
<p>機能が表示されている場合、<strong>ページの順序</strong>標準で領域<strong>レイアウト</strong>タブ、true を次に示します。</p>
<ul>
<li><p>ドライバーの GPD ファイルが指定されていない場合は、"<em>OutputOrderReversed?。TRUE"またはその PPD ファイルが指定されていない"DefaultOutputOrder:逆"、戻る UI のオプションを前面として GPD/PPD"Standard"オプションが表示されるし、フロント UI オプションに戻ると GPD/PPD「リバース」オプションが表示されます。</p></li>
<li><p>ドライバーの GPD ファイルで指定する場合"</em>OutputOrderReversed?。TRUE"またはその PPD ファイルで指定"DefaultOutputOrder:"、Reverse フロント UI のオプションをバックエンドとして GPD/PPD"Standard"オプションが表示され、戻る UI オプションを前面として GPD/PPD「リバース」オプションが表示されます。</p></li>
</ul>
<p>次のスクリーン ショットは、[印刷設定] ダイアログ ボックスのページの順序領域を示しています。</p>
<img src="images/xpsdrv-printingpreferences1.png" alt="Screen shot of the Page Order area on the Printing Preferences dialog box" /></td>
</tr>
<tr class="even">
<td><p>PageOrientation</p>
<p>(PS のみ)</p></td>
<td><p>印刷スキーマの"PageOrientation"キーワードを使用して、機能と機能 PPD が定義されている場合は「縦」、「横長」および"ReversePortrait"印刷スキーマのキーワードと正確に 3 つのオプションまたは「Landscape」と「Portrait」と正確に 2 つのオプションのいずれか印刷スキーマのキーワード、その機能に表示されます、<strong>向き</strong>標準で領域<strong>レイアウト</strong>タブ。</p>
<p>ジェネリック"プリンター"の機能グループ内にある PPD 機能が示すように、それ以外の場合、<strong>ツリー ビューを高度な</strong>UI。</p>
<p>次のスクリーン ショットでは、[印刷設定] ダイアログ ボックスの向き領域を示しています。</p>
<img src="images/xpsdrv-printingpreferences2.png" alt="Screen shot of the Orientation area on the Printing Preferences dialog box" />
<p>次のスクリーン ショットは、[印刷設定] ダイアログ ボックス (横 (回転) オプション) を使用せず、向き領域を示しています。</p>
<img src="images/xpsdrv-printingpreferences3.png" alt="Screen shot of the Orientation area (without the Rotated Landscape option) on the Printing Preferences dialog box" /></td>
</tr>
<tr class="odd">
<td><p>PageDeviceFont 置換</p></td>
<td><p>機能の印刷スキーマ キーワードに示した GPD または PPD は印刷スキーマの"PageDeviceFontSubstitution"キーワードを持つ特徴を定義し、機能、"On"と"Off"に正確に 2 つのオプションがある場合、 <strong>TrueType フォント</strong>の一覧<strong>高度な</strong> タブの「グラフィック」グループ。 "On"オプションを示した<strong>デバイス フォントと代替</strong>、として"Off"オプションが表示されると<strong>ソフト フォントとしてダウンロード</strong>します。</p>
<p>ジェネリック"プリンター"の機能グループ内にある、GPD または PPD 機能が示すように、それ以外の場合、<strong>ツリー ビューを高度な</strong>UI。</p>
<p>高度なオプション ダイアログ ボックスの次のスクリーン ショットは、デバイス フォント オプションを選択して、代替を示します。</p>
<img src="images/xpsdrv-printingpreferences4.png" alt="Screen shot of the Advanced Options dialog box with Substitute with Device font selected" /></td>
</tr>
<tr class="even">
<td><p>PageOutput 品質</p></td>
<td><p>GPD または PPD 印刷スキーマの"PageOutputQuality"キーワードを持つ特徴を定義します機能が"下書き"、"Normal"、および"高"には 3 つのオプションを印刷スキーマのキーワードである場合は、その機能に示した、<strong>品質設定</strong>。標準の領域<strong>用紙/品質</strong>タブ。として「下書き」オプションが表示される、<strong>ドラフト</strong>オプションとして、"Normal"オプションが表示されます、<strong>優れた</strong>としてオプション、および「高」のオプションが表示されます、<strong>ベスト</strong>オプション。</p>
<p>ジェネリック"プリンター"の機能グループ内にある、GPD または PPD 機能が示すように、それ以外の場合、<strong>ツリー ビューを高度な</strong>UI。</p>
<p>印刷設定 ダイアログ ボックスの次のスクリーン ショットは lustrates 品質設定領域です。</p>
<img src="images/xpsdrv-printingpreferences5.png" alt="Screen shot of the Quality Settings area on the Printing Preferences dialog box" /></td>
</tr>
<tr class="odd">
<td><p>JobNUpAllDocumentsContiguously または DocumentNUp</p></td>
<td><p>機能が正確に 6 つのオプションが GPD いて GPD または PPD ("DocumentNUp"機能は"JobNUpAllDocumentsContiguously"機能が存在しない場合にのみ使用されます)、"JobNUpAllDocumentsContiguously"または"DocumentNUp"印刷スキーマのキーワードを持つ特徴を定義しますまたは。PPD キーワード名は数値の文字列 (つまり、「1」、「2」、「4」、「6」、「9」、および「16」)、機能を示した、<strong>シートごとのページ</strong>標準でリスト<strong>レイアウト</strong>タブ。</p>
<p>ジェネリック"プリンター"の機能グループ内にある、GPD または PPD 機能が示すように、それ以外の場合、<strong>ツリー ビューを高度な</strong>UI。</p>
<img src="images/xpsdrv-printingpreferences6.png" alt="Screen shot of the Pages per Sheet option on the Printing Preferences dialog box" /></td>
</tr>
</tbody>
</table>

 

任意の他のカスタム GPD または PPD 機能いたとしてもいない、またはパブリックの印刷スキーマ機能にマッピングされている場合は常に表示されるジェネリック"プリンター"の機能グループ内にある、**ツリー ビューを高度な**UI。

 

 




