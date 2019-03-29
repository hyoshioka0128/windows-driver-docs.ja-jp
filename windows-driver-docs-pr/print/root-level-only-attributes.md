---
title: ルート レベル専用属性
description: ルート レベル専用属性
ms.assetid: 1b3d74b9-4cf4-4303-92ae-b93b3f9b7f7c
keywords:
- ルート レベルのみ属性 WDK Unidrv
- 一般的なプリンター WDK Unidrv、ルート レベルのみの属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6550ee4d1503c1130ed287b710dfb82dbf7868a7
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464036"
---
# <a name="root-level-only-attributes"></a>ルート レベル専用属性





ルート レベルのみの属性は[一般的な属性](general-attributes.md)リソース ファイル、ヘルプ ファイル、または追加のインクルード GPD ファイルの名前としてこのようなドライバー固有の特性をと共に、ドライバーの仕様を記述します。マスター ユニット、バージョン番号、および文字のコード ページ。

ルート レベルのみの追加の属性は、プリンターの名前、種類、コピーの最大容量、およびフォント カートリッジのスロットの数として、このようなデバイスに固有の特性を指定します。

これらの属性は属性と呼ばれるルート レベルのみのルート レベルで GPD ファイルから常に配置する必要がありますので (つまり、かっこ内にありません)。

次の表は、ルート レベルのみの属性を一覧表示します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名</th>
<th>AttributeParameter</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>コード ページ</strong></p></td>
<td><p>Microsoft Windows SDK のドキュメントで説明されている数値の値を持つ Windows コード ページ識別子。</p></td>
<td><p>任意。 指定されていない場合は、Unicode が使用されます。 コード ページは表示されているすべての文字列に適用されます。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>FontCartSlots</strong></p></td>
<td><p>プリンターによって提供されるフォント カートリッジのスロットの数を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 0 です。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>GPDFileName</strong></p></td>
<td><p>(パス) を使用せず、GPD ファイル名を表すテキスト文字列を引用符で囲みます。</p></td>
<td><p>任意。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>GPDFileVersion</strong></p></td>
<td><p>現在の GPD ファイル バージョンを表すテキスト文字列を引用符で囲みます。 推奨される形式は<em>MajorVersion</em>.<em>MinorVersion</em>、「1.0」など。</p></td>
<td><p>任意。 指定した場合は、ダイアログ ボックスの詳細について Unidrv にこの文字列が表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>GPDSpecVersion</strong></p></td>
<td><p>現在の GPD 仕様のバージョンを表すテキスト文字列を引用符で囲みます。 必要な形式は<em>MajorVersion</em>.<em>MinorVersion</em>、「1.0」など。</p></td>
<td><p>必須。 コメントの前に、GPD ファイルの最初のエントリがあります。</p>
<p>この値は、Windows 2000 の場合は「1.0」である必要があります。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>HelpFile</strong></p></td>
<td><p>.Hlp 拡張子を持つ、カスタマイズされたヘルプ ファイルの名前を含む引用符で囲まれた文字列です。</p></td>
<td><p>任意。 含まれる場合、追加のトピックも Unidrv のヘルプ ファイル内の既存のトピックを上書きできます。 ヘルプ ファイルのインデックスがで指定された<em>機能とオプションのオンライン ヘルプの属性。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>含まれます</strong></p></td>
<td><p>追加の GPD ファイルの名前を含む文字列を引用符で囲みます。</p></td>
<td><p>使われていません。 このエントリとして再定義されましたが、<a href="preprocessor-directives.md" data-raw-source="[preprocessor directive](preprocessor-directives.md)">プリプロセッサ ディレクティブ</a>します。</p></td>
</tr>
<tr class="even">
<td><p><em><strong>InstalledOptionName</strong></p></td>
<td><p>表示される文字列を引用符で囲まれた、インストール可能な機能またはオプションにインストールされます。 通常、この文字列が「インストール」が、任意の適切な文字列を指定することができます。</p></td>
<td><p>場合は必須です<em>インストール可能ですか? は<strong>TRUE</strong> 、機能またはオプションの (を参照してください<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">機能属性</a>)、場合 *<strong>rcInstalledOptionNameID</strong>が指定されていません。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>MasterUnits</strong></p></td>
<td><p>プリンターを表すペア<a href="master-units.md" data-raw-source="[master units](master-units.md)">ユニットをマスター</a>します。</p></td>
<td><p>必須。 可能性のある丸めエラーを減らすためには、指定した解像度単位のフォント メトリック データの同じ値を使用<em> <strong>MasterUnits</strong>します。 (Unidrv フォント メトリックを参照してください<a href="customized-font-management.md" data-raw-source="[Customized Font Management](customized-font-management.md)">フォントの管理をカスタマイズ</a>。)。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MaxCopies</strong></p></td>
<td><p>コピーの最大数を表す数値がプリンターでサポートします。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 です。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>ModelName</strong></p></td>
<td><p>モデル名のプリンターを表すテキスト文字列を引用符で囲みます。</p></td>
<td><p>必要な場合 *<strong>rcModelNameID</strong>が指定されていません。 文字列は、セットアップ.inf で名前と一致する必要があります。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>NotInstalledOptionName</strong></p></td>
<td><p>表示される文字列を引用符で囲まれた、インストール可能な機能またはオプションにはインストールされません。 通常、この文字列は、「インストールしない」が、いずれかの適切な文字列を指定することができます。</p></td>
<td><p>場合は必須です<em><strong>インストール可能ですか?</strong>は<strong>TRUE</strong>機能やオプション (を参照してください<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">機能属性</a>)、場合 *<strong>rcNotInstalledOptionNameID</strong>が指定されていません。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>性格</strong></p></td>
<td><p>プリンターのプリンターで使用される言語を表す文字列を引用符で囲みます。</p></td>
<td><p>任意。 指定した場合は、ディレクトリ サービスによって、文字列が表示されます。 参照してください<em>rcPersonalityID します。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrinterType</strong></p></td>
<td><p>ページ、シリアル、またはおよび/DEV/TTY</p></td>
<td><p>必須。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>printRate</strong></p></td>
<td><p>モノクロ印刷速度を表す数値。 ユニットがで指定された *<strong>PrintRateUnit</strong>します。</p></td>
<td><p>任意。 指定しない場合、既定値は 0 です。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>PrintRatePPM</strong></p></td>
<td><p>1 分あたりのページで、印刷速度を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 0 です。</p></td>
</tr>
<tr class="odd">
<td><p><em><strong>PrintRateUnit</strong></p></td>
<td><p></p>
PPM ページ/分 CPS - 文字 1 秒あたりの線/分 IPM、LPM インチ/分。(IPM がプロッター)</td>
<td><p>必要な場合 *<strong>PrintRate</strong>を指定します。 指定された単位は、プリンターの種類と一致する必要があります。 たとえば、ページのプリンターの PPM を指定してください。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcInstalledOptionNameID</strong></p></td>
<td><p>インストール可能な機能またはオプションを示すために表示される文字列リソースのリソース ID がインストールされます。 通常、この文字列が「インストール」が、任意の適切な文字列を指定することができます。</p></td>
<td><p>場合は必須です<em>インストール可能ですか? は<strong>TRUE</strong> 、機能またはオプションの (を参照してください<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">機能属性</a>)、場合 *<strong>InstalledOptionName</strong>が指定されていません。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcNotInstalledOptionNameID</strong></p></td>
<td><p>インストール可能な機能またはオプションを示すために表示される文字列リソースのリソース ID がインストールされていません。 通常、この文字列は、「インストールしない」が、いずれかの適切な文字列を指定することができます。</p></td>
<td><p>場合は必須です<em><strong>インストール可能ですか?</strong>は<strong>TRUE</strong>機能やオプション (を参照してください<a href="feature-attributes.md" data-raw-source="[Feature Attributes](feature-attributes.md)">機能属性</a>)、場合 *<strong>NotInstalledOptionName</strong>が指定されていません。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>rcPersonalityID</strong></p></td>
<td><p>プリンターのプリンターで使用される言語を表す文字列リソースのリソース ID。</p></td>
<td><p>任意。 指定した場合は、ディレクトリ サービスによって、文字列が表示されます。 参照してください<em>パーソナリティします。</p></td>
</tr>
<tr class="odd">
<td><p></em><strong>rcPrinterIconID</strong></p></td>
<td><p>プリンターに関連付けられているアイコンを表す RC_ICON リソースのリソース ID。</p></td>
<td><p>任意。 指定しない場合、既定のプリンターのアイコンが表示されます。 RC_ICON のすべてのリソース Id で、1 から始まる連続する番号付きことをお勧めします。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>ResourceDLL</strong></p></td>
<td><p>リソース DLL のパス情報がない場合、名前を含む文字列を引用符で囲みます。</p></td>
<td><p>任意。 参照してください<a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">リソース Dll を使用して、ミニドライバーで</a>します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

Windows Vista の新しいルート レベルのみの属性については、次を参照してください。 [Root-Level-Only GPD 属性を Windows Vista の新しい](new-root-level-only-gpd-attributes-for-windows-vista.md)と[Root-Level-Only PPD 属性を Windows Vista の新しい](new-root-level-only-ppd-attributes-for-windows-vista.md)します。

 

 




