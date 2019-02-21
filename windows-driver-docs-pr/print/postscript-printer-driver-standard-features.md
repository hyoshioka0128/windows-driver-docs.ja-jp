---
title: PostScript プリンターの標準機能
description: PostScript プリンターの標準的な機能は、ほとんどの PostScript プリンターによって提供される、一般的なものです。
ms.assetid: F904B8DD-7790-44FA-8C20-BCC3720B3528
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075b940e4adef181f2abf875bb4501d39116ea10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531620"
---
# <a name="postscript-printer-standard-features"></a>PostScript プリンターの標準機能


PostScript プリンターの標準的な機能は、ほとんどの PostScript プリンターによって提供される、一般的なものです。

標準的な機能は PPD 言語認識すると、定義済みの名前によって識別され、次の表は、機能名と PPD ファイルで使用される標準キーワードの間のマッピングを示します。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>機能名</th>
<th>既定の印刷スキーマ機能のキーワード</th>
<th>説明</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>部単位印刷します。</p>
<ul>
<li><p>true</p></li>
<li><p>false</p></li>
</ul></td>
<td>示さ</td>
<td><p>ページの照合順序</p>
<ul>
<li><p>部単位で印刷</p></li>
<li><p>丁合いなし</p></li>
</ul></td>
<td><p>省略可能</p>
<p>指定しない場合、照合順序がサポートされていません。</p></td>
</tr>
<tr class="even">
<td>JCLResolution</td>
<td>PageResolution</td>
<td>ページ解像度</td>
<td>解決の機能 (JCLResolution または解決) の少なくとも 1 つの種類が必要です。 少なくとも 1 つのオプションを指定する必要があります。</td>
</tr>
<tr class="odd">
<td><p>Duplex</p>
<ul>
<li><p>DuplexTumble</p></li>
<li><p>DuplexNoTumble</p></li>
<li><p>他のオプション</p></li>
</ul></td>
<td>JobDuplexAllDocumentsContiguously</td>
<td><p>両面印刷</p>
<ul>
<li><p>TwoSidedShortEdge</p></li>
<li><p>TwoSidedLongEdge</p></li>
<li><p>OneSided</p></li>
</ul></td>
<td><p>省略可能</p>
<p>指定しない場合、両面印刷を指定すると、1 つだけがサポートされています。</p></td>
</tr>
<tr class="even">
<td>InputSlot</td>
<td>JobInputBin</td>
<td>入力ビンのタイプ</td>
<td><p>必須</p>
<p>カスタマイズされた入力トレイの名前は 24 文字である必要がありますまたはそれ以下。</p></td>
</tr>
<tr class="odd">
<td>MediaType</td>
<td>PageMediatype</td>
<td>印刷メディアの種類</td>
<td><p>省略可能</p>
<p>指定しない場合、プリンターの既定のメディアが使用されます。</p></td>
</tr>
<tr class="even">
<td>OutputBin</td>
<td>JobOutputBin</td>
<td>出力ビンのタイプ</td>
<td><p>省略可能</p>
<p>指定しない場合、印刷システムしようとしません、出力トレイを選択します。</p></td>
</tr>
<tr class="odd">
<td>PageSize</td>
<td>PageMediaSize</td>
<td>用紙サイズ</td>
<td><p>必須</p>
<p>少なくとも 1 つのオプションを指定する必要があります。</p></td>
</tr>
<tr class="even">
<td>ホチキス止め</td>
<td>JobStapleAllDocuments</td>
<td>ホチキス止めの種類</td>
<td>省略可能</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[Pscript ミニドライバー](pscript-minidrivers.md)  
[標準のオプション](standard-options.md)  



