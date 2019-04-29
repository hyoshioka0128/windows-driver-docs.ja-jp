---
title: ダウンロードしたフォントの属性
description: ダウンロードしたフォントの属性
ms.assetid: 335413d0-cf0a-4dd9-b1a4-345945c63395
keywords:
- ダウンロードしたフォント属性 WDK Unidrv
- フォントの WDK Unidrv 属性します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b12c310b3089961b40335a729b68e24f5d279b0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331194"
---
# <a name="attributes-for-downloaded-fonts"></a>ダウンロードしたフォントの属性





次の表は、ダウンロードしたフォントのプリンターのサポートを記述する属性を一覧表示します。

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
<td><p><strong><em>DLSymbolSet</strong></p></td>
<td><p>TrueType フォントをダウンロードするときに使用される設定のシンボルを表す定数。 PC-8 またはローマ 8 のいずれかを指定できます。</p></td>
<td><p>任意。 グリフの範囲がで指定された制限内で隣接するいると見なされます指定しない場合、*<strong>MinGlyphID</strong>と *<strong>MaxGlyphID</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>FontFormat</strong></p></td>
<td><p></p>
サポートされているダウンロードの種類を示す定数値。 次のいずれかを指定する必要があります。HPPCL HPPCL_RES HPPCL_OUTLINE OEM_CALLBACK</td>
<td><p>ために必要なかどうかは、プリンターがフォントをダウンロードできます。 OEM_CALLBACK が指定されている場合は、フォントのコールバック関数を指定する必要があります。 これらのコールバックの詳細については、次を参照してください。<a href="customizing-microsoft-s-printer-drivers.md" data-raw-source="[Customizing Microsoft's Printer Drivers](customizing-microsoft-s-printer-drivers.md)">をカスタマイズする Microsoft のプリンター ドライバー</a>します。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MaxFontID</strong></p></td>
<td><p>ソフト フォントの最大の識別子を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 65535 です。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MaxGlyphID</strong></p></td>
<td><p>ダウンロードしたフォントのグリフの最大の識別子を表す数値。</p></td>
<td><p>任意。 指定されていない場合、 <em> <strong>DLSymbolSet</strong>が指定されていない、既定値は 255 です。 場合は無視されます *<strong>DLSymbolSet</strong>を指定します。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>MaxNumDownFonts</strong></p></td>
<td><p>プリンターのメモリに一度に 1 つ格納できるソフト フォントの最大数を表す数値。</p></td>
<td><p>任意。 指定しない場合、Unidrv では、ソフト フォントの無制限の数を格納することが前提としています。</p></td>
</tr>
<tr class="even">
<td><p><strong><em>MinFontID</strong></p></td>
<td><p>ソフト フォントの最小の識別子を表す数値。</p></td>
<td><p>任意。 指定しない場合、既定値は 1 つ。</p></td>
</tr>
<tr class="odd">
<td><p><strong></em>MinGlyphID</strong></p></td>
<td><p>ダウンロードしたフォントのグリフの最小の識別子を表す数値。</p></td>
<td><p>任意。 指定されていない場合、 <em> <strong>DLSymbolSet</strong>が指定されていない、既定値は 32 です。 場合は無視されます *<strong>DLSymbolSet</strong>を指定します。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>TextHalftoneThreshold</strong></p></td>
<td><p>Unidrv が TrueType フォントのテキストのハーフトーンを実行するかどうかを決定する数値。 ドライバーの解像度が Unidrv ハーフトーン テキストは、この属性で指定された値以上である場合。</p></td>
<td><p>任意。 既定値には 600 です。</p></td>
</tr>
</tbody>
</table>

 

例については、次を参照してください。、[サンプル GPD ファイル](sample-gpd-files.md)します。

 

 




