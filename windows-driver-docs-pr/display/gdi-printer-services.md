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
ms.openlocfilehash: 0a454dca896140f004e12ba6627e124b84053259
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354730"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engenumforms" data-raw-source="[&lt;strong&gt;EngEnumForms&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engenumforms)"><strong>EngEnumForms</strong></a></p></td>
<td align="left"><p>指定したプリンターでサポートされている形式を列挙します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetform" data-raw-source="[&lt;strong&gt;EngGetForm&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetform)"><strong>EngGetForm</strong></a></p></td>
<td align="left"><p>指定されたフォーム FORM_INFO_1 の詳細を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinter" data-raw-source="[&lt;strong&gt;EngGetPrinter&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinter)"><strong>EngGetPrinter</strong></a></p></td>
<td align="left"><p>指定したプリンターに関する情報を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdata" data-raw-source="[&lt;strong&gt;EngGetPrinterData&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdata)"><strong>EngGetPrinterData</strong></a></p></td>
<td align="left"><p>指定したプリンターの構成データを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdatafilename" data-raw-source="[&lt;strong&gt;EngGetPrinterDataFileName&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdatafilename)"><strong>EngGetPrinterDataFileName</strong></a></p></td>
<td align="left"><p>プリンターのデータ ファイルの文字列名を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdriver" data-raw-source="[&lt;strong&gt;EngGetPrinterDriver&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enggetprinterdriver)"><strong>EngGetPrinterDriver</strong></a></p></td>
<td align="left"><p>指定したプリンターのドライバーのデータを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfile" data-raw-source="[&lt;strong&gt;EngMapFontFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfile)"><strong>EngMapFontFile</strong></a></p></td>
<td align="left"><p>使われていません。 このテーブルのエントリを参照してください。 <strong>EngMapFontFileFD</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfilefd" data-raw-source="[&lt;strong&gt;EngMapFontFileFD&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmapfontfilefd)"><strong>EngMapFontFileFD</strong></a></p></td>
<td align="left"><p>必要に応じて、フォント ファイルをシステム メモリにマップし、ファイルでフォント データの基本の場所へのポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface" data-raw-source="[&lt;strong&gt;EngMarkBandingSurface&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engmarkbandingsurface)"><strong>EngMarkBandingSurface</strong></a></p></td>
<td align="left"><p>バンドの画面として指定されたプリンターの画面をマークします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetprinterdata" data-raw-source="[&lt;strong&gt;EngSetPrinterData&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engsetprinterdata)"><strong>EngSetPrinterData</strong></a></p></td>
<td align="left"><p>使われていません。 指定したプリンターの構成データを設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfile" data-raw-source="[&lt;strong&gt;EngUnmapFontFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfile)"><strong>EngUnmapFontFile</strong></a></p></td>
<td align="left"><p>使われていません。 このテーブルのエントリを参照してください。 <strong>EngUnmapFontFileFD</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfilefd" data-raw-source="[&lt;strong&gt;EngUnmapFontFileFD&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engunmapfontfilefd)"><strong>EngUnmapFontFileFD</strong></a></p></td>
<td align="left"><p>システム メモリから指定したフォント ファイルのマッピングを解除します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter" data-raw-source="[&lt;strong&gt;EngWritePrinter&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engwriteprinter)"><strong>EngWritePrinter</strong></a></p></td>
<td align="left"><p>プリンター グラフィックス プリンター ハードウェアにデータ ストリームを送信する Dll を使用します。</p></td>
</tr>
</tbody>
</table>

 

 

 





