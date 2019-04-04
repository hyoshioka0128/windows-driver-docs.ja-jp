---
title: 機能属性
description: 機能属性
ms.assetid: ae1a489e-2554-46fc-8f2e-45128b073f91
keywords:
- プリンターは、WDK Unidrv、機能を属性します。
- 機能 attribues WDK Unidrv
- プリンターは、WDK Unidrv、属性を機能します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455f08c3fbe61188ffb91691ed4a759e94b63102
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57350353"
---
# <a name="feature-attributes"></a>機能属性





プリンターの機能を指定するときに属性を使用して Unidrv を次の情報を提供します。

-   機能の表示名を表すテキスト文字列。

-   この機能に関連付けられているプリンター オプションのセット。

-   機能が常に存在するかはインストールが可能かを示すブール値。

-   種類の機能と機能をカスタマイズすると、プロパティ シートで、機能が表示されることを示す場合は、優先順位とその相対的な優先順位。

次の表では、アルファベット順で機能の属性の一覧し、そのパラメーターについて説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>属性パラメーター</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>ConcealFromUI でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示すかどうか、機能は、ユーザー インターフェイスで表示するか。</p></td>
<td><p>任意。 既定値は指定されていない場合<strong>FALSE</strong>、つまり、この機能が表示されます。</p>
<p>必要があります<strong>TRUE</strong>機能のオプションを選択したがもう 1 つの機能のオプションの設定によって制御されている場合または機能の 1 つだけのオプション (たとえば、1 つ解決策) はありませんので、ユーザーが変更できる場合のみです。</p>
<p>場合、  <strong></em>ConcealFromUI</strong>属性に設定されて<strong>TRUE</strong>、Unidrv または PrintConfig PrintCapabilities XML では、この項目の機能の要素に psk:DisplayUI 要素が追加されます。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>ConflictPriority</strong></p></td>
<td><p>1 が最も高い優先順位は、機能の優先順位を表す数値。</p></td>
<td><p>任意。 参照してください<a href="feature-conflict-priority.md" data-raw-source="[Feature Conflict Priority](feature-conflict-priority.md)">機能の競合の優先度</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>DefaultOption</strong></p></td>
<td><p>機能のオプションのいずれかの名前です。</p></td>
<td><p>任意。 指定しない場合、最初のオプションが一覧表示、<em>機能のエントリは既定値。 用紙サイズ機能は、Unidrv の既定のオプションは A4 メトリックのロケールと文字の別の場所です。 かどうか PaperSize が存在しない既定、Unidrv オプションを使用して、用紙サイズで指定されている、*<strong>DefaultOption</strong>キーワード。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>FeatureType</strong></p></td>
<td><p>DOC_PROPERTY</p>
<p>JOB_PROPERTY</p>
<p>PRINTER_PROPERTY</p>
<p>DOC_PROPERTY または JOB_PROPERTY に、機能が、ドキュメントのプロパティ シートに割り当てられたかどうか。 場合 PRINTER_PROPERTY、機能は、プリンターのプロパティ シートに割り当てられます。</p></td>
<td><p>カスタマイズされた機能に必要です。 標準的な機能の省略可能。 指定しない場合、標準的な機能の既定値は、明記されない限り DOC_PROPERTY が。</p>
<p>場合 PRINTER_PROPERTY、機能のオプションの値は、レジストリに保存されます。 DOC_PROPERTY または JOB_PROPERTY にしたかどうか、機能のオプションの値がドキュメントに保存します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>オンライン ヘルプ</strong></p></td>
<td><p>指定されたヘルプ ファイルにインデックスを表す数値の値、*<strong>HelpFile</strong> <a href="root-level-only-attributes.md" data-raw-source="[root-level-only attribute](root-level-only-attributes.md)">属性のルート レベルのみ</a>します。</p></td>
<td><p>(また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>インストール可能な場合でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>ことを示す、この機能はインストールが可能かどうか。 (<strong>FALSE</strong>常にインストールされていることを意味します)。</p>
<p>詳細については、<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>を参照してください。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 場合<strong>TRUE</strong>、インストール可能な指定された最初のものを除くすべての機能のオプションもします。 場合<strong>FALSE</strong>機能のオプションの少なくとも 1 つは常にもインストールする必要があります。 (また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>InstallableFeatureName</strong></p></td>
<td><p>インストール可能な機能が実際にインストールされているかどうかをユーザーに要求を表示するテキスト文字列。</p>
<p>詳細については、<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>を参照してください。</p></td>
<td><p>必要な場合 *<strong>インストール可能でしょうか。</strong>は<strong>TRUE</strong>と *<strong>rcInstallableFeatureNameID</strong>が指定されていません。 (また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>名</strong></p></td>
<td><p>プリンターのプロパティ シートで、機能の表示名として使用するテキスト文字列。</p></td>
<td><p>任意。 指定しない場合<em> <strong>rcNameID</strong>指定する必要があります。 (また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>オプション</strong></p></td>
<td><p>」の説明に従って、パラメーターをオプション<a href="option-entry-format.md" data-raw-source="[Option Entry Format](option-entry-format.md)">オプション エントリ形式</a>します。</p></td>
<td><p>必須。 使用して、 <strong><em>オプション</strong>機能に関連付けられている各オプションのエントリ。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>rcIconID</strong></p></td>
<td><p>この機能に関連付けられているアイコン リソースのリソース ID。</p></td>
<td><p>任意。 指定しない場合、Unidrv のプリンターのプロパティ シートで、機能のアイコンは表示されません。 (また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>rcInstallableFeatureNameID</strong></p></td>
<td><p>インストール可能な機能が実際にインストールされているかどうかをユーザーに要求を表示するテキスト文字列のリソース ID。</p>
<p>詳細については、<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>を参照してください。</p></td>
<td><p>必要な場合 *<strong>インストール可能でしょうか。</strong>は<strong>TRUE</strong>と *<strong>InstallableFeatureName</strong>が指定されていません。 (また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>rcNameID</strong></p></td>
<td><p>機能名を表す文字列リソースのリソース ID。 (ゼロは有効なリソース ID ではない)</p></td>
<td><p>任意。 指定しない場合<em><strong>名前</strong>指定する必要があります。 (また、<a href="option-attributes.md" data-raw-source="[option attribute](option-attributes.md)">オプション属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>UpdateQualityMacro でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、品質の設定を指定する条件付きステートメントで、機能が含まれているかどうか (を参照してください<a href="controlling-image-quality.md" data-raw-source="[Controlling Image Quality](controlling-image-quality.md)">画質を制御する</a>)。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 (値を強制的に<strong>TRUE</strong>品質設定を指定する条件付きステートメントに、機能が含まれます)。</p></td>
</tr>
</tbody>
</table>

 

例については、、[サンプル GPD ファイル](sample-gpd-files.md)を参照してください。

 

 




