---
title: GDI フォント サービスおよびテキスト サービス
description: GDI フォント サービスおよびテキスト サービス
ms.assetid: c315f3ec-ddee-42d9-8bfb-7bb2e0d1d4b2
keywords:
- WDK GDI フォント
- フォント、GDI WDK Windows 2000 の表示
- グラフィックス ドライバー WDK Windows 2000 の表示、フォント
- WDK の GDI やフォントの描画
- GDI WDK Windows 2000 の表示、テキスト出力
- グラフィックス ドライバー WDK Windows 2000 の表示、テキスト出力
- WDK GDI の描画、テキスト出力
- テキスト出力 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 795bd946590741eef79f6007e88cf4b4a8ea92df
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372946"
---
# <a name="gdi-font-and-text-services"></a>GDI フォント サービスおよびテキスト サービス


## <span id="ddk_gdi_font_and_text_services_gg"></span><span id="DDK_GDI_FONT_AND_TEXT_SERVICES_GG"></span>


GDI は、フォントの管理とテキストの出力のサポートを提供します。 [ **FONTOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565974)構造および関連する関数は、フォントの特定のインスタンスに、ドライバーのアクセス権を付与します。 テキスト出力をサポートするために、ドライバーがへのアクセスを持つ、 [ **STROBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff569738)構造および関連する関数。 次の表には、FONTOBJ と STROBJ 関連の関数が一覧表示します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564192" data-raw-source="[&lt;strong&gt;EngComputeGlyphSet&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564192)"><strong>EngComputeGlyphSet</strong></a></p></td>
<td align="left"><p>デバイスでサポートされている設定、グリフを計算します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564877" data-raw-source="[&lt;strong&gt;EngFntCacheAlloc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564877)"><strong>EngFntCacheAlloc</strong></a></p></td>
<td align="left"><p>キャッシュされたフォント ファイルのメモリを割り当てます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564882" data-raw-source="[&lt;strong&gt;EngFntCacheFault&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564882)"><strong>EngFntCacheFault</strong></a></p></td>
<td align="left"><p>フォント ドライバーからの読み取りまたはフォント データのキャッシュへの書き込み中にエラーが発生した場合は、フォント エンジンにエラーを報告します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564887" data-raw-source="[&lt;strong&gt;EngFntCacheLookUp&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564887)"><strong>EngFntCacheLookUp</strong></a></p></td>
<td align="left"><p>キャッシュされたフォント ファイルのデータへのポインターを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564917" data-raw-source="[&lt;strong&gt;EngGetCurrentCodePage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564917)"><strong>EngGetCurrentCodePage</strong></a></p></td>
<td align="left"><p>システムの既定の OEM および ANSI コード ページを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564956" data-raw-source="[&lt;strong&gt;EngGetType1FontList&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564956)"><strong>EngGetType1FontList</strong></a></p></td>
<td align="left"><p>ローカルとリモートの両方にインストールされている PostScript Type 1 フォントの一覧を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565034" data-raw-source="[&lt;strong&gt;EngTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565034)"><strong>EngTextOut</strong></a></p></td>
<td align="left"><p>これは、GDI シミュレーション、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"> <strong>DrvTextOut</strong> </a>関数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565977" data-raw-source="[&lt;strong&gt;FONTOBJ_cGetAllGlyphHandles&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565977)"><strong>FONTOBJ_cGetAllGlyphHandles</strong></a></p></td>
<td align="left"><p>GDI フォントのすべてのグリフのハンドルを取得するドライバーを使用します。 ドライバーでは、このサービスを使用して、全体のフォントをダウンロードします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565982" data-raw-source="[&lt;strong&gt;FONTOBJ_cGetGlyphs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565982)"><strong>FONTOBJ_cGetGlyphs</strong></a></p></td>
<td align="left"><p>フォントのコンシューマーのグリフのハンドルをグリフが関連付けられているデータへのポインターに変換します。 次の呼び出しまでこれらのポインターは有効な<strong>FONTOBJ_cGetGlyphs</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565989" data-raw-source="[&lt;strong&gt;FONTOBJ_pfdg&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565989)"><strong>FONTOBJ_pfdg</strong></a></p></td>
<td align="left"><p>ポインターを取得、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff565625" data-raw-source="[&lt;strong&gt;FD_GLYPHSET&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565625)"> <strong>FD_GLYPHSET</strong> </a>指定したフォントに関連付けられている構造体。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565990" data-raw-source="[&lt;strong&gt;FONTOBJ_pifi&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565990)"><strong>FONTOBJ_pifi</strong></a></p></td>
<td align="left"><p>ポインターを取得、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff567418" data-raw-source="[&lt;strong&gt;IFIMETRICS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567418)"> <strong>IFIMETRICS</strong> </a>関連付けられているフォントを記述する構造体。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565993" data-raw-source="[&lt;strong&gt;FONTOBJ_pjOpenTypeTablePointer&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565993)"><strong>FONTOBJ_pjOpenTypeTablePointer</strong></a></p></td>
<td align="left"><p>OpenType のテーブルのビューへのポインターを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565996" data-raw-source="[&lt;strong&gt;FONTOBJ_pQueryGlyphAttrs&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565996)"><strong>FONTOBJ_pQueryGlyphAttrs</strong></a></p></td>
<td align="left"><p>フォントのグリフについての情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566001" data-raw-source="[&lt;strong&gt;FONTOBJ_pvTrueTypeFontFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566001)"><strong>FONTOBJ_pvTrueTypeFontFile</strong></a></p></td>
<td align="left"><p>TrueType、OpenType、または Type1 のフォント ファイルのビューへのポインターを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566003" data-raw-source="[&lt;strong&gt;FONTOBJ_pwszFontFilePaths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566003)"><strong>FONTOBJ_pwszFontFilePaths</strong></a></p></td>
<td align="left"><p>フォントに関連付けられているファイルのパスを取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566008" data-raw-source="[&lt;strong&gt;FONTOBJ_pxoGetXform&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566008)"><strong>FONTOBJ_pxoGetXform</strong></a></p></td>
<td align="left"><p>関連付けられているフォント変換 Notional からデバイスを取得します。 この変換は、ドライバーによって提供されるフォントを実現するためのドライバーに必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566013" data-raw-source="[&lt;strong&gt;FONTOBJ_vGetInfo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566013)"><strong>FONTOBJ_vGetInfo</strong></a></p></td>
<td align="left"><p>関連付けられているフォントを記述する情報を返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569739" data-raw-source="[&lt;strong&gt;STROBJ_bEnum&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569739)"><strong>STROBJ_bEnum</strong></a></p></td>
<td align="left"><p>グリフの id と指定した STROBJ 内の位置を列挙します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569740" data-raw-source="[&lt;strong&gt;STROBJ_bEnumPositionsOnly&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569740)"><strong>STROBJ_bEnumPositionsOnly</strong></a></p></td>
<td align="left"><p>グリフの id と、指定した文字列の位置を列挙しますが、キャッシュされたグリフ ビットマップを作成できません。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569741" data-raw-source="[&lt;strong&gt;STROBJ_bGetAdvanceWidths&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569741)"><strong>STROBJ_bGetAdvanceWidths</strong></a></p></td>
<td align="left"><p>指定した文字列を構成するグリフの可能性の高い幅を指定するベクトルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569742" data-raw-source="[&lt;strong&gt;STROBJ_dwGetCodePage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569742)"><strong>STROBJ_dwGetCodePage</strong></a></p></td>
<td align="left"><p>指定した STROBJ に関連付けられているコード ページを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569743" data-raw-source="[&lt;strong&gt;STROBJ_fxBreakExtra&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569743)"><strong>STROBJ_fxBreakExtra</strong></a></p></td>
<td align="left"><p>両端揃えテキストを表示または印刷時に文字列の場合は、各空白文字に追加する余分なスペースの量を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569745" data-raw-source="[&lt;strong&gt;STROBJ_vEnumStart&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569745)"><strong>STROBJ_vEnumStart</strong></a></p></td>
<td align="left"><p>列挙体の再起動、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff566824" data-raw-source="[&lt;strong&gt;GLYPHPOS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566824)"> <strong>GLYPHPOS</strong> </a>指定 STROBJ の配列。 この関数は、後続の列挙体の前に、ドライバーによって呼び出す必要があります。</p></td>
</tr>
</tbody>
</table>

 

 

 





