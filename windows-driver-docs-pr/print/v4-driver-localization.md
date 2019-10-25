---
title: V4 プリンター ドライバー ローカライズ
description: Windows 8 は、標準のローカライズされた表示文字列を提供して、プリンター拡張機能と UWP デバイスアプリの開発をサポートしています。
ms.assetid: 5C587AF2-C51E-4728-A214-7FC1F8A6E445
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d4d5c24d481953c0e07ddc209d2986cf5a5117
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844195"
---
# <a name="v4-printer-driver-localization"></a>V4 プリンター ドライバー ローカライズ


Windows 8 は、標準のローカライズされた表示文字列を提供して、プリンター拡張機能と UWP デバイスアプリの開発をサポートしています。

これらの標準のローカライズされた表示文字列は、新しい[**Iprintschemacapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)オブジェクトを通じて提供され、一部の機能とそれに関連する標準オプションをサポートします。 次の表に、Windows 8 で標準表示文字列を使用してローカライズできる機能を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>標準オプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>入力ビン</td>
<td>ジョブ/ドキュメント/PageInputBin</td>
</tr>
<tr class="even">
<td>メディアの種類</td>
<td>PageMediaType</td>
</tr>
<tr class="odd">
<td>インプリメント</td>
<td>JobDuplexAllDocumentsContiguously</td>
</tr>
<tr class="even">
<td>Collation</td>
<td>DocumentCollate</td>
</tr>
<tr class="odd">
<td>出力の色</td>
<td>PageOutputColor</td>
</tr>
<tr class="even">
<td>Orientation</td>
<td>PageOrientation</td>
</tr>
<tr class="odd">
<td>N-up</td>
<td>Jobnupallドキュメント連続</td>
</tr>
<tr class="even">
<td>パンチ穴あけ</td>
<td><ul>
<li><p>JobHolePunch</p></li>
<li><p>DocumentHolePunch</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>テナント</td>
<td><ul>
<li><p>Jobのすべてのドキュメント</p></li>
<li><p>ドキュメントホチキス止め</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Binding</td>
<td><ul>
<li><p>JobBindAllDocuments</p></li>
<li><p>DocumentBinding</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>出力品質</td>
<td>PageOutputQuality</td>
</tr>
<tr class="even">
<td>メディアサイズ</td>
<td>PageMediaSize</td>
</tr>
</tbody>
</table>

 

また、これらの文字列は、ドライバーが機能またはオプションのリソース DLL を使用して表示名を指定していない場合に、XML 形式の PrintCapabilities で使用できます。 ドライバーがリソース DLL を使用して表示名を指定した場合は、以前のバージョンの Windows で使用されていた従来の COMPSTUI ベースの印刷設定の UI だけでなく、XML でも提供されます。

さまざまなユーザーインターフェイスと Api で、表示名は異なります。 次の3つのフローチャートを使用して、特定のシナリオで想定されるローカリゼーション動作の概要を確認します。

次のフローチャートは、UWP アプリと、オブジェクトの[**IPrintSchemaFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemafeature)および[**Iprintschemaoption**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemaoption)ファミリで予想されるローカライズ動作を示しています。

![Windows アプリ、iprintschemafeature、または iprintschemaoption のローカライズ動作のフローチャート](images/locstringmodern.png)

次のフローチャートは、 **PrintCapabilities** XML ドキュメントで想定されるローカライズ動作を示しています。

![printcapabilities xml ドキュメントのローカライズ動作のフローチャート](images/locstringpcap.png)

次のフローチャートは、標準の Compstui ベースの印刷設定ダイアログで想定されるローカリゼーション動作を示しています。

![compstui ベースのダイアログのローカライズ動作のフローチャート ](images/locstringcomp.png)

Microsoft のローカライズされた表示名を使用するには、次の表の手順に従って、GPD または PPD 構成ファイルを適切に編集します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>ファイルの種類</th>
<th>手順</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>GPD</td>
<td><ul>
<li><p>GPD 機能またはオプションの <strong><em>名</strong> エントリを指定します。</p></li>
<li><p><strong></em>rcNameID</strong>エントリを指定しないでください。</p></li>
<li>次の機能やオプションについては、標準機能として指定されていない限り、PrintSchemaKeywordMap</strong><em><strong>を指定して、対応する印刷スキーマで定義されている機能またはオプションに GPD の機能またはオプションをマップする必要もあります。 <a href="standard-features.md" data-raw-source="[Standard Features](standard-features.md)"></a>. <strong></em>PrintSchemaKeywordMap</strong>を使用して機能をマップする方法を示す例については、「 <a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">GPD/PPD ベースの機能の説明の変更</a>」を参照してください。
o JobHolePunch、DocumentHolePunch o Job、DocumentStaple o JobBindAllDocuments、Documentstaple o PageOutputQuality o PageMediaType</li>
<li><p><strong><em>PrintSchemaKeywordMap</strong> をオプションの値に対して使用しないでください。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>PPD</td>
<td><ul>
<li><p><strong></em>PrintSchemaKeywordMap</strong>を使用して、対応する印刷スキーマで定義されている機能またはオプションに、PPD の機能またはオプションをマップします。 <strong><em>PrintSchemaKeywordMap</strong> を使用して機能をマップする方法を示す例については、「 <a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">GPD/PPD ベースの機能の説明の変更</a>」を参照してください。</p></li>
<li><p>PrintSchemaKeywordMap の場合、オプションの値には<strong></em></strong>を使用しないでください。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**PPD ベースのドライバーのローカライズ**

PPD ベースのドライバーでは、リソース Dll はサポートされません。 そのため、複数の PPD ファイルを指定する必要がある場合があります。 Microsoft では、PPD 構成ファイルを使用する v4 印刷ドライバーで、このトピックで説明されている方法を使用して、ロケールごとに1つの PPD ファイルを含めることをお勧めします。

## <a name="related-topics"></a>関連トピック
[**IPrintSchemaCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemacapabilities)  
[**IPrintSchemaFeature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemafeature)  
[**IPrintSchemaOption**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printerextension/nn-printerextension-iprintschemaoption)  
[GPD/PPD ベースの機能の説明の変更](gpd-ppd-based-feature-description-changes.md)  
[標準機能](standard-features.md)  



