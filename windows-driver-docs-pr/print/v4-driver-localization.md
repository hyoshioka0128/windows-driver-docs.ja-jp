---
title: V4 プリンター ドライバー ローカライズ
description: Windows 8 は、プリンターの拡張機能と UWP デバイス アプリの開発をサポートする標準的なローカライズされた表示文字列を提供しています。
ms.assetid: 5C587AF2-C51E-4728-A214-7FC1F8A6E445
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31cffd917fad5cda53ba8ad4de2619720ee9bd32
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358582"
---
# <a name="v4-printer-driver-localization"></a>V4 プリンター ドライバー ローカライズ


Windows 8 は、プリンターの拡張機能と UWP デバイス アプリの開発をサポートする標準的なローカライズされた表示文字列を提供しています。

新しいを通じて提供されます。 これらの標準的なローカライズされた表示文字列[ **IPrintSchemaCapabilities** ](https://msdn.microsoft.com/library/windows/hardware/hh451256)一部の機能とその関連する標準的なオプションをサポートするオブジェクト。 次の表は、文字列の表示機能を Windows 8 は、その標準にローカライズできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>機能</th>
<th>標準のオプション</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>入力ビン</td>
<td>PageInputBin/ジョブ/ドキュメント</td>
</tr>
<tr class="even">
<td>メディアの種類</td>
<td>PageMediaType</td>
</tr>
<tr class="odd">
<td>二重化</td>
<td>JobDuplexAllDocumentsContiguously</td>
</tr>
<tr class="even">
<td>[照合順序]</td>
<td>示さ</td>
</tr>
<tr class="odd">
<td>出力の色</td>
<td>印刷</td>
</tr>
<tr class="even">
<td>方向</td>
<td>PageOrientation</td>
</tr>
<tr class="odd">
<td>N-up</td>
<td>JobNUpAllDocumentsContiguously</td>
</tr>
<tr class="even">
<td>パンチ穴あけ</td>
<td><ul>
<li><p>JobHolePunch</p></li>
<li><p>DocumentHolePunch</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>ホチキス止め</td>
<td><ul>
<li><p>JobStapleAllDocuments</p></li>
<li><p>DocumentStaple</p></li>
</ul></td>
</tr>
<tr class="even">
<td>バインディング</td>
<td><ul>
<li><p>JobBindAllDocuments</p></li>
<li><p>DocumentBinding</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>出力の品質</td>
<td>PageOutputQuality</td>
</tr>
<tr class="even">
<td>メディアのサイズ</td>
<td>PageMediaSize</td>
</tr>
</tbody>
</table>

 

さらに、ドライバーが機能またはオプションのリソース DLL を使用して表示名を指定しないことは、これらの文字列は PrintCapabilities の XML 形式で利用できます。 ドライバーがリソース DLL を使用して表示名を指定する場合は、レガシ COMPSTUI ベース印刷の設定 UI が以前のバージョンの Windows で使用されるほか、xml で提供されます。

表示名は、別のユーザー インターフェイスと Api の間で異なります。 次の 3 つのフローチャートを使用して、特定のシナリオで想定されるローカリゼーション動作の概要を参照してください。

次のフローチャート、予想されるローカリゼーションは動作を示します UWP アプリで、 [ **IPrintSchemaFeature** ](https://msdn.microsoft.com/library/windows/hardware/hh451284)と[ **IPrintSchemaOption**](https://msdn.microsoft.com/library/windows/hardware/hh451335)オブジェクトのファミリです。

![Windows アプリ、iprintschemafeature または iprintschemaoption ローカリゼーション動作のフローチャート](images/locstringmodern.png)

次のフローチャートで期待されるローカリゼーション動作を示しています。 **PrintCapabilities** XML ドキュメント。

![printcapabilities xml ドキュメントのローカライズの動作のフローチャート](images/locstringpcap.png)

次のフローチャートは、標準的な Compstui ベースの印刷設定 ダイアログで予想されるローカリゼーション動作を示します。

![compstui ベースのダイアログのローカリゼーションの動作のフローチャート ](images/locstringcomp.png)

Microsoft のローカライズされた表示名を使用するには、適切 GPD または PPD 構成ファイルを編集する次の表の指示に従います。

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
<li><p>指定、 <strong><em>名前</strong>GPD 機能またはオプションのエントリ。</p></li>
<li><p>指定しない、  <strong></em>rcNameID</strong>エントリ。</p></li>
<li>次の機能/オプションにする必要がありますを指定するも<strong> <em>PrintSchemaKeywordMap</strong> GPD 機能やオプションは、として指定されていない場合、対応する印刷スキーマで定義された機能またはオプションにマップするには<a href="standard-features.md" data-raw-source="[Standard Features](standard-features.md)">標準的な機能</a>します。 使用する方法を示す例を参照する <strong></em>PrintSchemaKeywordMap</strong>機能をマップするを参照してください。 <a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">GPD PPD ベースの機能の説明の変更</a>します。
o JobHolePunch、DocumentHolePunch o JobStapleAllDocuments、DocumentStaple o JobBindAllDocuments、DocumentBinding o PageOutputQuality o PageMediaType</li>
<li><p>N-up、ため使用しないで<strong> <em>PrintSchemaKeywordMap</strong>オプションの値にします。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>PPD</td>
<td><ul>
<li><p>使用 <strong></em>PrintSchemaKeywordMap</strong> PPD 機能やオプションを対応する印刷スキーマで定義された機能またはオプションにマップします。 使用する方法を示す例を参照する<strong> <em>PrintSchemaKeywordMap</strong>機能をマップするを参照してください。 <a href="gpd-ppd-based-feature-description-changes.md" data-raw-source="[GPD/PPD-Based Feature Description Changes](gpd-ppd-based-feature-description-changes.md)">GPD PPD ベースの機能の説明の変更</a>します。</p></li>
<li><p>N-up、ため使用しないで <strong></em>PrintSchemaKeywordMap</strong>オプションの値にします。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**ドライバーに基づく PPD のローカライズ**

PPD ベースのドライバーは、リソース Dll をサポートしていません。 その結果、複数の PPD ファイルを提供するために必要な場合があります。 PPD 構成ファイルを使用する v4 印刷ドライバーがロケールごとに 1 つ PPD ファイルにこのトピックで説明されたテクニックを使用することをお勧めします。

## <a name="related-topics"></a>関連トピック
[**IPrintSchemaCapabilities**](https://msdn.microsoft.com/library/windows/hardware/hh451256)  
[**IPrintSchemaFeature**](https://msdn.microsoft.com/library/windows/hardware/hh451284)  
[**IPrintSchemaOption**](https://msdn.microsoft.com/library/windows/hardware/hh451335)  
[GPD PPD ベースの機能の説明の変更](gpd-ppd-based-feature-description-changes.md)  
[標準的な機能](standard-features.md)  



