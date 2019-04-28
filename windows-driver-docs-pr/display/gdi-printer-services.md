---
title: GDI プリンター サービス
description: GDI プリンター サービス
ms.assetid: b63c9822-f737-42fb-a831-31d16b3495c9
keywords:
- GDI WDK Windows 2000 の表示、プリンターのサービス
- グラフィックス ドライバー WDK Windows 2000 の表示、プリンターのサービス
- 描画 WDK GDI やプリンター サービス
- プリンターは、WDK GDI をサービスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d604ec0aea2afee21c48d75005344dd68775fec7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374638"
---
# <a name="gdi-printer-services"></a>GDI プリンター サービス


## <span id="ddk_gdi_printer_services_gg"></span><span id="DDK_GDI_PRINTER_SERVICES_GG"></span>


GDI は、さまざまなプリンター ドライバー作成者に関心のあるサービスを提供します。 次の表には、これらのサービスが一覧表示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564850" data-raw-source="[&lt;strong&gt;EngEnumForms&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564850)"><strong>EngEnumForms</strong></a></p></td>
<td align="left"><p>指定したプリンターでサポートされている形式を列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564938" data-raw-source="[&lt;strong&gt;EngGetForm&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564938)"><strong>EngGetForm</strong></a></p></td>
<td align="left"><p>指定されたフォーム FORM_INFO_1 の詳細を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564945" data-raw-source="[&lt;strong&gt;EngGetPrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564945)"><strong>EngGetPrinter</strong></a></p></td>
<td align="left"><p>指定したプリンターに関する情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564948" data-raw-source="[&lt;strong&gt;EngGetPrinterData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564948)"><strong>EngGetPrinterData</strong></a></p></td>
<td align="left"><p>指定したプリンターの構成データを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564951" data-raw-source="[&lt;strong&gt;EngGetPrinterDataFileName&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564951)"><strong>EngGetPrinterDataFileName</strong></a></p></td>
<td align="left"><p>プリンターのデータ ファイルの文字列名を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564954" data-raw-source="[&lt;strong&gt;EngGetPrinterDriver&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564954)"><strong>EngGetPrinterDriver</strong></a></p></td>
<td align="left"><p>指定したプリンターのドライバーのデータを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564972" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564972)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>使われていません。 このテーブルのエントリを参照してください。 <strong>EngMapFontFileFD</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564973" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564973)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>必要に応じて、フォント ファイルをシステム メモリにマップし、ファイルでフォント データの基本の場所へのポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564975" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564975)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p>バンドの画面として指定されたプリンターの画面をマークします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565020" data-raw-source="[&lt;strong&gt;EngSetPrinterData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565020)"><strong>EngSetPrinterData</strong></a></p></td>
<td align="left"><p>使われていません。 指定したプリンターの構成データを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565441" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565441)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>使われていません。 このテーブルのエントリを参照してください。 <strong>EngUnmapFontFileFD</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565445" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565445)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>システム メモリから指定したフォント ファイルのマッピングを解除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565467" data-raw-source="[&lt;strong&gt;EngWritePrinter&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565467)"><strong>EngWritePrinter</strong></a></p></td>
<td align="left"><p>プリンター グラフィックス プリンター ハードウェアにデータ ストリームを送信する Dll を使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 





