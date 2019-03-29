---
title: すべての機能のオプション属性
description: すべての機能のオプション属性
ms.assetid: 0d269fdf-f4a1-431a-9f07-044289b9f0fa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca8ce8bb8392726042b2727072d6e8d7ab2e9526
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349205"
---
# <a name="option-attributes-for-all-features"></a>すべての機能のオプション属性





次の表にリストをアルファベット順で、[オプション属性](option-attributes.md)すべての利用可能な機能し、そのパラメーターについて説明します。

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
<td><p><em><strong>コマンド</strong></p></td>
<td><p>A <strong>CmdSelect</strong> <a href="option-selection-command.md" data-raw-source="[option selection command](option-selection-command.md)">オプションの選択コマンド</a>オプションを選択するには、プリンターに送信する必要がありますコマンド文字列を指定します。</p></td>
<td><p>必須。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>DisabledFeatures</strong></p></td>
<td><p>オプションが選択されている場合に無効にする機能を識別する、機能名の文字列の一覧です。</p>
<p>現在、双方向、および collate の各機能がサポートされています。 FeatureType PRINTER_PROPERTY に設定する機能では、このオプションの属性を使用する必要があります。</p></td>
<td><p>任意。</p>
<p>表示されている機能を使用できない<em><strong>インストール可能ですか?</strong>に設定<strong>TRUE</strong>します。 詳細については、次を参照してください。<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>します。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>オンライン ヘルプ</strong></p></td>
<td><p>指定されたヘルプ ファイルにインデックスを表す数値の値、 <em> <strong>HelpFile</strong><a href="root-level-only-attributes.md" data-raw-source="[root-level-only attribute](root-level-only-attributes.md)">属性のルート レベルのみ</a>します。</p></td>
<td><p>(また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p>
<p>インデックス値は、0 または-1 にすることはできません。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>インストール可能な場合でしょうか。</strong></p></td>
<td><p><strong>TRUE</strong>または<strong>FALSE</strong>かを示す、オプションはインストールが可能かどうか。 (<strong>FALSE</strong>常にインストールされていることを意味します)。</p>
<p>詳細については、次を参照してください。<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>します。</p></td>
<td><p>任意。 指定されていない場合、既定値は<strong>FALSE</strong>します。 (また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>InstallableFeatureName</strong></p></td>
<td><p>インストール可能なオプションが実際にインストールされているかどうかをユーザーに要求に表示されるテキスト文字列。</p>
<p>詳細については、次を参照してください。<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>します。</p></td>
<td><p>必要な場合 *<strong>インストール可能でしょうか。</strong>は<strong>TRUE</strong>と *<strong>rcInstallableFeatureNameID</strong>が指定されていません。 (また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>名前</strong></p></td>
<td><p>プリンターのプロパティ シートのオプションの表示名として使用するテキスト文字列。</p></td>
<td><p>任意。 指定しない場合<em> <strong>rcNameID</strong>指定する必要があります。 (また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>オプション Id</strong></p></td>
<td><p>プリンターに Unidrv を格納する一意のオプションの識別子を表す数値<a href="https://msdn.microsoft.com/library/windows/hardware/ff552837" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff552837)"> <strong>DEVMODEW</strong> </a>構造体。 用紙サイズ、InputSlot、ハーフトーン、およびメディアの種類の機能でのみ使用します。 DEVMODE 構造体の値が格納されている<strong>dmPaperSize</strong>、 <strong>dmDefaultSource</strong>、 <strong>dmDitherType</strong>、または<strong>dmMediaType</strong>メンバーそれぞれします。</p></td>
<td><p>任意。 指定しない場合、Unidrv が識別子の値を割り当てます (&gt;256)。 Unidrv によって割り当てられた識別子と競合を回避するために、指定した値は 512 より大きくなければなりません。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>rcIconID</strong></p></td>
<td><p>オプションに関連付けられているアイコン リソースのリソース ID。</p></td>
<td><p>任意。 指定しない場合、Unidrv はプリンターのプロパティ シートのオプションのアイコンが表示されません。 (また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcInstallableFeatureNameID</strong></p></td>
<td><p>インストール可能なオプションが実際にインストールされているかどうかをユーザーに要求に表示されるテキスト文字列のリソース ID。</p>
<p>詳細については、次を参照してください。<a href="handling-installable-features-and-options.md" data-raw-source="[Handling Installable Features and Options](handling-installable-features-and-options.md)">インストール可能な機能の処理とオプション</a>します。</p></td>
<td><p>場合は必須<em><strong>インストール可能ですか?</strong>は<strong>TRUE</strong>と *<strong>InstallableFeatureName</strong>が指定されていません。 (また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcNameID</strong></p></td>
<td><p>オプション名を表す文字列リソースのリソース ID。</p></td>
<td><p>任意。 指定しない場合 *<strong>名前</strong>指定する必要があります。 (また、<a href="feature-attributes.md" data-raw-source="[feature attribute](feature-attributes.md)">機能属性</a>)。</p>
<p><a href="standard-options.md" data-raw-source="[standard options](standard-options.md)">標準オプション</a>PaperSize 機能のみの定義済みオプション名の文字列を使用する Unidrv が原因 RCID_DMPAPER_SYSTEM_NAME にこの属性を設定します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




