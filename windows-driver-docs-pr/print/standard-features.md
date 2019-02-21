---
title: 標準的な機能
description: 標準的な機能
ms.assetid: 5cd90992-5ab8-4cb3-89b0-19e58e55b652
keywords:
- WDK Unidrv、標準的なプリンターの機能
- WDK Unidrv の標準機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fd594419c0b56da317510885aa600983e84469c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557422"
---
# <a name="standard-features"></a>標準的な機能





標準的な機能は[プリンターの機能](printer-features.md)ほとんどのプリンターで一般提供されています。 GPD 言語によって認識される定義済みの名前によって識別されます。 (これらの名前を表す文字列のリソース識別子は、Microsoft Windows Driver Kit で提供される、stdnames.gpd に含まれる\[WDK\])。いくつかの標準的な機能は、必要なすべてのプリンターに指定する必要があります。 他のユーザーは、省略可能です。

次の表では、すべてアルファベット順に、標準的な機能の一覧表示し、各機能が標準オプションまたはカスタマイズされたオプションを受け入れるかどうかを示します。 印刷スキーマ キーワードを含める機能は、印刷スキーマ キーワードに自動的にマップされている GPD 機能です。 マップすることも GPD 機能印刷スキーマのキーワードを手動で PrintSchemaKeywordMap 属性を使用しています。 印刷スキーマは、Microsoft Windows SDK に記載されています。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>機能名</th>
<th>既定の印刷スキーマ機能のキーワード</th>
<th>説明</th>
<th>標準のオプション</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>部単位印刷します。</strong></p></td>
<td><p><strong>示さ</strong></p></td>
<td><p>ページの照合順序</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションを指定することはできません。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv は、ページの照合順序をサポートしていません。</p></td>
</tr>
<tr class="even">
<td><p><strong>返さ</strong></p></td>
<td><p><strong>PageOutputColor</strong></p></td>
<td><p>カラー印刷モード</p></td>
<td><p>なし。 すべてのオプションをカスタマイズします。 参照してください<a href="option-attributes-for-the-colormode-feature.md" data-raw-source="[Option Attributes for the ColorMode Feature](option-attributes-for-the-colormode-feature.md)">返さ機能のオプション属性</a>します。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv 単一平面、ピクセルあたり 1 ビットの形式で画像を表示します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>Duplex</strong></p></td>
<td><p><strong>JobDuplexAllDocumentsContiguously</strong></p></td>
<td><p>両面印刷</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションを指定することはできません。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv のみ片面印刷を実行します。</p></td>
</tr>
<tr class="even">
<td><p><strong>ハーフトーン</strong></p></td>
<td><p>既定のキーワードがありません。 PrintSchemaKeywordMap 属性を使用して、印刷スキーマ機能のキーワードを割り当てます。</p></td>
<td><p>ハーフトーン機能</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションが許可されます。</p>
<p>参照してください<a href="option-attributes-for-the-halftone-feature.md" data-raw-source="[Option Attributes for the Halftone Feature](option-attributes-for-the-halftone-feature.md)">ハーフトーン機能のオプション属性</a>します。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv は GDI でサポートされているハーフトーン メソッドを選択します。</p>
<p>参照してください<a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv のハーフトーン</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InputBin</strong></p></td>
<td><p><strong>JobInputBin</strong></p></td>
<td><p>入力ビンのタイプ</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションが許可されます。</p>
<p>参照してください<a href="option-attributes-for-the-inputbin-feature.md" data-raw-source="[Option Attributes for the InputBin Feature](option-attributes-for-the-inputbin-feature.md)">InputBin 機能のオプション属性</a>します。</p></td>
<td><p>必須。</p>
<p>カスタマイズされた入力トレイの名前は 24 文字である必要がありますまたはそれ以下。</p></td>
</tr>
<tr class="even">
<td><p><strong>メディアの種類</strong></p></td>
<td><p><strong>PageMediaType</strong></p></td>
<td><p>印刷メディアの種類</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションが許可されます。</p></td>
<td><p>(省略可能)。 プリンターを指定しない場合&#39;s の既定のメディアは常に使用します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>メモリ</strong></p></td>
<td><p>既定のキーワードがありません。 PrintSchemaKeywordMap 属性を使用して、印刷スキーマ機能のキーワードを割り当てます。</p></td>
<td><p>プリンター メモリの構成</p></td>
<td><p>すべてのオプションをカスタマイズします。 参照してください<a href="option-attributes-for-the-memory-feature.md" data-raw-source="[Option Attributes for the Memory Feature](option-attributes-for-the-memory-feature.md)">メモリ機能のオプション属性</a>します。</p></td>
<td><p>(省略可能)。 指定した場合、Unidrv はメモリ使用量を追跡しようとします。</p>
<p>既定 * FeatureType は PRINTER_PROPERTY します。</p></td>
</tr>
<tr class="even">
<td><p><strong>印刷の向き</strong></p></td>
<td><p><strong>PageOrientation</strong></p></td>
<td><p>用紙の向き</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションを指定することはできません。</p></td>
<td><p>(省略可能)。 指定しない場合、既定の方向は縦にします。</p>
<p>Windows 7 では、 <strong>MxdcGetPDEVAdjustment</strong>関数には、横置きに回転の新しいパラメーター。 詳細については、次を参照してください。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557558" data-raw-source="[&lt;strong&gt;MxdcXDCGetPDEVAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557558)"> <strong>MxdcXDCGetPDEVAdjustment</strong></a>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputBin</strong></p></td>
<td><p><strong>JobOutputBin</strong></p></td>
<td><p>出力ビンのタイプ</p></td>
<td><p>なし。 すべてのオプションをカスタマイズします。</p>
<p>参照してください<a href="option-attributes-for-the-outputbin-feature.md" data-raw-source="[Option Attributes for the OutputBin Feature](option-attributes-for-the-outputbin-feature.md)">OutputBin 機能のオプション属性</a>します。</p></td>
<td><p>(省略可能)。 指定しない場合、Unidrv しようとしません、出力トレイを選択します。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageProtect</strong></p></td>
<td><p><strong>JobPageProtection</strong></p></td>
<td><p>現在の印刷ページの保護を実現にします。</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションを指定することはできません。</p></td>
<td><p>(省略可能)。 指定しない場合、既定値は OFF です。 Unidrv は、十分なプリンターのメモリがある場合にのみページ保護をできます。 既定 * FeatureType は PRINTER_PROPERTY します。 参照してください * PageProtectMem します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>用紙サイズ</strong></p></td>
<td><p><strong>PageMediaSize</strong></p></td>
<td><p>用紙サイズ</p></td>
<td><p>参照してください<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>します。</p>
<p>カスタマイズされたオプションが許可されます。</p>
<p>参照してください<a href="option-attributes-for-the-papersize-feature.md" data-raw-source="[Option Attributes for the PaperSize Feature](option-attributes-for-the-papersize-feature.md)">PaperSize 機能のオプション属性</a>します。</p></td>
<td><p>必須。 少なくとも 1 つのオプションを指定する必要があります。 CUSTOMSIZE オプションにより、ユーザーがプリンター用紙サイズを指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESDLL</strong></p></td>
<td><p>この機能は、印刷スキーマ キーワードにマップすることはできません。</p></td>
<td><p>リソース Dll</p></td>
<td><p>すべてのオプションをカスタマイズします。</p>
<p>参照してください<a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">リソース Dll を使用して、ミニドライバーで</a>します。</p></td>
<td><p>(省略可能)。 参照してください * ResourceDLL します。</p></td>
</tr>
<tr class="odd">
<td><p><strong>解決方法</strong></p></td>
<td><p><strong>PageResolution</strong></p></td>
<td><p>印刷の解像度</p></td>
<td><p>すべてのオプションをカスタマイズします。 参照してください<a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">解決の機能のオプション属性</a>します。</p></td>
<td><p>必須。 少なくとも 1 つのオプションを指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>ホチキス止め</strong></p></td>
<td><p><strong>JobStapleAllDocuments</strong></p></td>
<td><p>ホチキス止めの機能</p></td>
<td><p>すべてのオプションをカスタマイズします。</p></td>
<td><p>(省略可能)。 指定した場合、ディレクトリ サービスは、プリンターがホチキス止めをサポートを示します。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

## <a name="related-topics"></a>関連トピック
[サンプル GPD ファイル](sample-gpd-files.md)  
[V4 プリンター ドライバーのローカライズ](v4-driver-localization.md)  



