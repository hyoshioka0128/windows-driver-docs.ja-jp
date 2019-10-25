---
title: 標準機能
description: 標準機能
ms.assetid: 5cd90992-5ab8-4cb3-89b0-19e58e55b652
keywords:
- プリンター機能 WDK Unidrv、standard
- 標準機能 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 505c569736987d30f3b77dea4492dc54efde189b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840399"
---
# <a name="standard-features"></a>標準機能





標準機能は、ほとんどのプリンターで一般的に提供されている[プリンター機能](printer-features.md)です。 これらは、GPD 言語で認識される定義済みの名前で識別されます。 (この名前を表す文字列のリソース識別子は、stdnames に含まれています。 gpd には、Microsoft Windows Driver Kit \[WDK\]が付属しています)。一部の標準機能は必須であり、すべてのプリンターに対して指定する必要があります。 他のオプションは省略可能です。

次の表は、すべての標準機能をアルファベット順に示したもので、各機能が標準オプションまたはカスタマイズされたオプションを受け入れるかどうかを示しています。 Print Schema キーワードを含む機能は、印刷スキーマキーワードに自動的にマップされる GPD の機能です。 PrintSchemaKeywordMap 属性を使用して、スキーマキーワードを手動で印刷するように GPD 機能をマップすることもできます。 印刷スキーマは、Microsoft Windows SDK に記載されています。

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
<th>既定の印刷スキーマ機能キーワード</th>
<th>説明</th>
<th>標準オプション</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>照合</strong></p></td>
<td><p><strong>DocumentCollate</strong></p></td>
<td><p>ページの照合順序</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションは使用できません。</p></td>
<td><p>省略可能。 指定しない場合、Unidrv はページの照合順序をサポートしません。</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorMode</strong></p></td>
<td><p><strong>PageOutputColor</strong></p></td>
<td><p>カラー印刷モード</p></td>
<td><p>なし。 すべてのオプションはカスタマイズされています。 また<a href="option-attributes-for-the-colormode-feature.md" data-raw-source="[Option Attributes for the ColorMode Feature](option-attributes-for-the-colormode-feature.md)">、ColorMode 機能のオプション属性</a>も参照してください。</p></td>
<td><p>省略可能。 指定されていない場合、Unidrv はイメージをシングルプレーン1ビット/ピクセル形式でレンダリングします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>通信</strong></p></td>
<td><p><strong>JobDuplexAllDocumentsContiguously</strong></p></td>
<td><p>両面印刷</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションは使用できません。</p></td>
<td><p>省略可能。 指定しない場合、Unidrv は片面印刷だけを実行します。</p></td>
</tr>
<tr class="even">
<td><p><strong>スクリーン</strong></p></td>
<td><p>既定のキーワードがありません。 PrintSchemaKeywordMap 属性を使用して、印刷スキーマ機能キーワードを割り当てます。</p></td>
<td><p>ハーフトーン機能</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションが許可されます。</p>
<p>また<a href="option-attributes-for-the-halftone-feature.md" data-raw-source="[Option Attributes for the Halftone Feature](option-attributes-for-the-halftone-feature.md)">、ハーフトーン機能のオプション属性</a>も参照してください。</p></td>
<td><p>省略可能。 指定しない場合、Unidrv は GDI がサポートするハーフトーン方式を選択します。</p>
<p>「 <a href="halftoning-with-unidrv.md" data-raw-source="[Halftoning with Unidrv](halftoning-with-unidrv.md)">Unidrv によるハーフトーン</a>」も参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>InputBin</strong></p></td>
<td><p><strong>JobInputBin</strong></p></td>
<td><p>入力ビンの種類</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションが許可されます。</p>
<p><a href="option-attributes-for-the-inputbin-feature.md" data-raw-source="[Option Attributes for the InputBin Feature](option-attributes-for-the-inputbin-feature.md)">InputBin 機能のオプション属性</a>も参照してください。</p></td>
<td><p>必須。</p>
<p>カスタマイズした入力ビン名は24文字以下でなければなりません。</p></td>
</tr>
<tr class="even">
<td><p><strong>MediaType</strong></p></td>
<td><p><strong>PageMediaType</strong></p></td>
<td><p>印刷メディアの種類</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションが許可されます。</p></td>
<td><p>省略可能。 指定しない場合、プリンターの既定のメディアが常に使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><strong>メモリ</strong></p></td>
<td><p>既定のキーワードがありません。 PrintSchemaKeywordMap 属性を使用して、印刷スキーマ機能キーワードを割り当てます。</p></td>
<td><p>プリンターのメモリ構成</p></td>
<td><p>すべてのオプションはカスタマイズされています。 <a href="option-attributes-for-the-memory-feature.md" data-raw-source="[Option Attributes for the Memory Feature](option-attributes-for-the-memory-feature.md)">メモリ機能のオプション属性</a>も参照してください。</p></td>
<td><p>省略可能。 指定した場合、Unidrv はメモリ使用量を追跡し続けます。</p>
<p>既定の * FeatureType 値は PRINTER_PROPERTY です。</p></td>
</tr>
<tr class="even">
<td><p><strong>細かく</strong></p></td>
<td><p><strong>PageOrientation</strong></p></td>
<td><p>用紙の向き</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションは使用できません。</p></td>
<td><p>省略可能。 指定しない場合、既定の向きは [縦] です。</p>
<p>Windows 7 の場合、 <strong>Mxdcgetpdevadjustment</strong>関数には、横方向の回転用の新しいパラメーターがあります。 詳細については、「 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment" data-raw-source="[&lt;strong&gt;MxdcXDCGetPDEVAdjustment&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/mxdc/nf-mxdc-mxdcgetpdevadjustment)"><strong>MxdcXDCGetPDEVAdjustment</strong></a>」を参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>OutputBin</strong></p></td>
<td><p><strong>JobOutputBin</strong></p></td>
<td><p>出力ビンの種類</p></td>
<td><p>なし。 すべてのオプションはカスタマイズされています。</p>
<p>また<a href="option-attributes-for-the-outputbin-feature.md" data-raw-source="[Option Attributes for the OutputBin Feature](option-attributes-for-the-outputbin-feature.md)">、OutputBin 機能のオプション属性</a>も参照してください。</p></td>
<td><p>省略可能。 指定しない場合、Unidrv は出力ビンを選択しようとしません。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageProtect</strong></p></td>
<td><p><strong>JobPageProtection</strong></p></td>
<td><p>現在の印刷ページの保護を有効にします</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションは使用できません。</p></td>
<td><p>省略可能。 指定しない場合、既定値は OFF です。 Unidrv は、十分なプリンターメモリがある場合にのみページ保護を有効にします。 既定の * FeatureType 値は PRINTER_PROPERTY です。 「* PageProtectMem」も参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperSize</strong></p></td>
<td><p><strong>PageMediaSize</strong></p></td>
<td><p>用紙サイズ</p></td>
<td><p>「<a href="standard-options.md" data-raw-source="[Standard Options](standard-options.md)">標準オプション</a>」を参照してください。</p>
<p>カスタマイズされたオプションが許可されます。</p>
<p>また<a href="option-attributes-for-the-papersize-feature.md" data-raw-source="[Option Attributes for the PaperSize Feature](option-attributes-for-the-papersize-feature.md)">、PaperSize 機能のオプション属性</a>も参照してください。</p></td>
<td><p>必須。 少なくとも1つのオプションを指定する必要があります。 CUSTOMSIZE オプションを使用すると、プリンターユーザーは用紙サイズを指定できます。</p></td>
</tr>
<tr class="even">
<td><p><strong>RESDLL</strong></p></td>
<td><p>この機能を Print Schema キーワードにマップすることはできません。</p></td>
<td><p>リソース Dll</p></td>
<td><p>すべてのオプションはカスタマイズされています。</p>
<p>「<a href="using-resource-dlls-in-a-minidriver.md" data-raw-source="[Using Resource DLLs in a Minidriver](using-resource-dlls-in-a-minidriver.md)">ミニドライバーでのリソース dll の使用</a>」を参照してください。</p></td>
<td><p>省略可能。 「* ResourceDLL」も参照してください。</p></td>
</tr>
<tr class="odd">
<td><p><strong>解決策</strong></p></td>
<td><p><strong>PageResolution 方法</strong></p></td>
<td><p>印刷の解像度</p></td>
<td><p>すべてのオプションはカスタマイズされています。 また<a href="option-attributes-for-the-resolution-feature.md" data-raw-source="[Option Attributes for the Resolution Feature](option-attributes-for-the-resolution-feature.md)">、解決機能のオプション属性</a>も参照してください。</p></td>
<td><p>必須。 少なくとも1つのオプションを指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><strong>テナント</strong></p></td>
<td><p><strong>Jobのすべてのドキュメント</strong></p></td>
<td><p>ホチキス止め機能</p></td>
<td><p>すべてのオプションはカスタマイズされています。</p></td>
<td><p>省略可能。 指定されている場合、ディレクトリサービスは、プリンターがホチキス止めをサポートしていることを示します。</p></td>
</tr>
</tbody>
</table>

 

例については、[サンプルの GPD ファイル](sample-gpd-files.md)を参照してください。

## <a name="related-topics"></a>関連トピック
[GPD ファイルのサンプル](sample-gpd-files.md)  
[V4 プリンタードライバーのローカライズ](v4-driver-localization.md)  



