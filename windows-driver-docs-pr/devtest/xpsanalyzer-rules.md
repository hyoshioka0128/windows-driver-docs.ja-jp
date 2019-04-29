---
title: XpsAnalyzer のルール
description: XpsAnalyzer のルール
ms.assetid: 4f617665-4cc4-475d-ae66-abc2f00309fd
keywords:
- XpsAnalyzer WDK、規則
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: e77be3f40a0009e029c281a22c0be556928b848f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387252"
---
# <a name="xpsanalyzer-rules"></a>XpsAnalyzer のルール

次の表では、XpsAnalysis ツールが XPS ファイルを分析に使用する規則について説明します。 これらの規則は、XML Paper Specification (XPS) 1.0 仕様に基づいています。 この仕様の詳細については doiwnload、 [XML Paper Specification](http://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)します。

## <a name="open-packaging-conventions-opc-rules"></a>規則 (OPC) のパッケージを開く

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルール名</th>
<th align="left">データ型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CompressionOption</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージの圧縮オプションの値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CorruptedOpc</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージは、OPC 仕様に準拠していない場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ForeignContentType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 仕様の一部でないコンテンツの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ForeignRelationshipType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 1.0 仕様の一部でないリレーションシップの種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LargePartCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>サイズが、指定した時間を超えています区画の数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxFileSizeInBytes</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のパーツのセットの最大サイズ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxPartRelationships</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージの一部のリレーションシップの最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PackageRelationshipCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のリレーションシップの合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PartCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>OPC ファイル内の部分の合計数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TotalPartRelationships</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>パーツのリレーションシップの合計数。</p></td>
</tr>
</tbody>
</table>

## <a name="xps-trunk-rules"></a>XPS トランク ルール

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルール名</th>
<th align="left">データ型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CorruptedXpsTrunk</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージが XPS 1.0 仕様 (トランク レベル) に準拠していない場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedDocumentCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージのドキュメントの合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCoreProperties</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、XPS コア プロパティ パーツが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDiscardControl</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、DiscardControl パーツが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasDocumentPrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ドキュメント レベルの PrintTicket が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDocumentStructure</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ドキュメント構造の要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasJobPrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、DocumentSequence レベル PrintTicket が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasMoreThanOneSignatureBlockResourceInADocument</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに署名ブロックの 1 つ以上のリソースを持つドキュメントが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PackageThumbnailType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージ レベルのサムネイルの画像の種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureBlockRequestCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージの署名の合計数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="xps-page-rules"></a>XPS ページ規則

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルール名</th>
<th align="left">データ型</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BleedBoxDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージに既定以外の裁ち落としサイズのディメンションです。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の要素をブラシの合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の Canvas 要素の合計数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CanvasLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Canvas 要素の言語です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>キャンバス OpacityMask 要素のブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ContentBoxDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージの既定以外の ContentBox ディメンション。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CorruptedXpsPage</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージが XPS 1.0 仕様 (ページ レベル) に準拠していない場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedPageCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のページ要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FontType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージにフォントの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のジオメトリ要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureClosedFilledPatternRule</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigure の型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureMaxSegmentCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>GeometryFigures SegmentCount 要素の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureMaxSegmentDataCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>GeometryFigures SegmentDataCount 要素の最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureSegmentStrokePattern</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigures 要素の線のパターン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureSegmentType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigure 要素のセグメントの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFillRule</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ジオメトリの FillRule します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsBidiLevel</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>グリフの BidiLevel します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の要素のグリフの合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsFillBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフの塗りつぶしのブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフの言語です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフ OpacityMask のブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsStyleSimulations</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフは。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル ClipGeometry で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート ClipGeometry で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、HyperlinkTarget で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、名前のプロパティを使用してキャンバス要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、不透明度の Canvas 要素が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、不透明度の Canvas 要素が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル OpacityMaskBrush で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート OpacityMaskBrush で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithAccessibilityLongDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、AccessibilityLongDescription で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasWithAccessibilityShortDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、AccessibilityShortDescription で Canvas 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithUseAliasedEdgeMode</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = True の場合、XPS パッケージには、UseAliasedEdgeMode で Canvas 要素が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasColorProfile</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>ColorProfile が XPS パッケージに含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryFigureWithMultipleSegmentTypes</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、複数のセグメントの種類と GeometryFigure 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryFigureWithNonDefaultStartPoint</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定値は非 StartPoint (0.0, 0.0) GeometryFigure 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform でジオメトリが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform でジオメトリが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル ClipGeometry グリフが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート ClipGeometry と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsDeviceFontName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、DeviceFontName と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFillBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル FillBrush と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsFillBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート FillBrush と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFontFaceIndex</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、FontFaceIndex と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、HyperlinkTarget と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、Name プロパティと Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、不透明度と Glyphs 要素が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、不透明度と Glyphs 要素が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル OpacityMaskBrush と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート OpacityMaskBrush と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform と Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsUnicodeString</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ユニコードと Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsWithSideways</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージでは、有効になっている IsSideways プロパティと Glyphs 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ハイパーリンクのターゲットを含むページが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、ImageBrush 不透明度が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、ImageBrush 不透明度が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform を使用した、ImageBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform を使用した、ImageBrush が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>ImageBrush で ColorProfileResource が XPS パッケージに含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ImageBrush で既定以外の ViewBox (0, 0、1, 1) が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外のビューポート (0, 0、1, 1) を使用した ImageBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合は、LinearGradientBrush 不透明度が XPS パッケージに含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合は、LinearGradientBrush 不透明度が XPS パッケージに含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform で LinearGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform で LinearGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、LinearGradientBrush ColorProfileResource とが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultEndPoint</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージには、LinearGradientBrush を既定以外のエンドポイントが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の GradientStopOffset で LinearGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultStartPoint</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージには、既定以外の開始点と、LinearGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLocalDictionary</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカルのディクショナリを使用するページが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasNonDefaultBleedBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の裁ち落としサイズ値を含むページが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasNonDefaultContentBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の ContentBox 値を含むページが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPageName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、名前属性が設定されたページが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPagePrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ページ レベル PrintTicket が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル ClipGeometry でパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート ClipGeometry 値を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathFillBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル FillBrush でパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathFillBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート FillBrush でパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル Geometry プロパティを使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモートの Geometry プロパティを使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、HyperlinkTarget 値を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、Name プロパティを使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、不透明度を使用したパスが含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、不透明度を使用したパスが含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル OpacityMaskBrush 値を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート、OpacityMaskBrush とパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル StrokeBrush プロパティを使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathStrokeBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート StrokeBrush プロパティを使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeDashOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、StrokeDashOffset でパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithAccessibilityLongDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、AccessibilityLongDescription 値を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithAccessibilityShortDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、AccessibilityShortDescription でパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithNonDefaultStrokeMiterLimit</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の StrokeMiterLimit でパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithNonDefaultStrokeThickness</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、StrokeThickness が既定以外のパスが含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithSnapsToPixel</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、SnapToPixels 値を使用したパスが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、不透明度 RadialGradientBrush が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、不透明度 RadialGradientBrush が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform で RadialGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform で RadialGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>RadialGradientBrush ColorProfileResource でが XPS パッケージに含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultCenter</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外のセンター RadialGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientOrigin</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の GradientOrigin で RadialGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の GradientStopOffset で RadialGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultRadiiSizes</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の RadiiSizes で RadialGradientBrush が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRemoteDictionary</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、RemoteDictionary を使用するページが含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、不透明度 SolidColorBrush が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、不透明度 SolidColorBrush が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>ColorProfileResource された SolidColorBrush が XPS パッケージに含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasStoryFragment</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、1 つの部分が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 1 の場合、XPS パッケージには、不透明度 VisualBrush 要素が含まれています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>True = 0 の場合、XPS パッケージには、不透明度 VisualBrush 要素が含まれています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル MatrixTransform で VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート MatrixTransform で VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalCanvas</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカルのキャンバスで VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithLocalGlyphs</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカルのグリフで VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalPath</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、ローカル パスで VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外の ViewBox (0, 0、1, 1) と VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、既定以外のビューポート (0, 0、1, 1) と VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemoteCanvas</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモートのキャンバスで VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithRemoteGlyphs</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモートのグリフで VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemotePath</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、リモート パスを持つ VisualBrush 要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の ImageBrush 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ImageBrushTileMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ImageBrush の要素の TileMode 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ImageBrush の要素のイメージの種類の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>LinearGradientBrush 要素の ColorInterpolationMode 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>LinearGradientBrush 要素の色の種類の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>LinearGradientBrush 要素のコンテキストのカラー チャネルの数の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージに LinearGradientBrush 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushSpreadMethod</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>LinearGradientBrush 要素の SpreadMethod 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinkTargetsCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の LinkTargets 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LocalDictionaryContent</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>このローカル ディクショナリで見つかった共有可能なオブジェクトの型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsFontRenderingEMSize</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Glyphs 要素の最大 FontRenderingEmSize します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsIndicesInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Glyphs 要素のインデックスの最大サイズ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsMappingsInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Glyphs 要素のマッピングの最大サイズ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsProhibitedCaretStopCountInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Glyphs 要素の ProhibitedCaretStopCount の最大サイズ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGradientStopsInALinearGradientBrush</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>LinearGradientBrush 要素で GradientStops の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGradientStopsInARadialGradientBrush</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>RadialGradientBrush 要素で GradientStops の最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxStrokeDashesInAPath</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>パス要素で StrokeDashes の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>幅と、XPS パッケージ内のページの高さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PageLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ページの言語です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageThumbnailType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ページ レベルのサムネイルの画像の種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージのパス要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathFillBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ブラシの種類のパスを入力します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 要素の言語の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス OpacityMask のブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パスの線のプロパティのブラシの種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeDashCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 要素の StrokeDashCap 型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeEndLineCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 要素の StrokeEndLineCap 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeLineJoin</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 要素の StrokeLineJoin 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeStartLineCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Path 要素の StrokeStartLineCap 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush の要素の ColorInterpolationMode 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush の要素の色の種類の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 要素のコンテキストの色チャネルの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の RadialGradientBrush 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushEllipseOrCircle</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グラデーション ブラシが楕円または円がかどうかを定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushSpreadMethod</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush の要素の SpreadMethod 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RemoteDictionaryContent</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>このリモート辞書にある共有可能なオブジェクトの型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>SolidColorBrush 要素の色の種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SolidColorBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>SolidColorBrush 要素のコンテキストの色チャネルの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージでの SolidColorBrush 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージに VisualBrush 要素の合計数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VisualBrushTileMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>VisualBrush の要素の TileMode 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のビジュアルの合計数。</p></td>
</tr>
</tbody>
</table>

## <a name="digital-signature-rules"></a>デジタル署名の規則

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルール名</th>
<th align="left">データの種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CorruptedDigitalSignature</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、破損したデジタル署名が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージのデジタル署名の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignaturePolicy</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Signature 要素の XPS Signature ポリシーの値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasInvalidXpsSignature</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、無効な XPS 署名要素が含まれている場合は true。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignatureStatus</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>署名が有効の場合、署名要素の署名の状態値。 つまり、このルールは HasInvalidXpsSignature が True の場合のみ有効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCertificatesInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>証明書の署名要素の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasXpsSignatureWithEmptyID</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、空の ID を持つ XPS 署名要素が含まれている場合は true。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureTimeFormat</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Signature 要素の時刻形式の署名値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxNumberOfCustomObjectsInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Signature 要素内で見つかったカスタム オブジェクトの最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCustomReferencesInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Signature 要素内に含まれるカスタム参照の最大数。</p></td>
</tr>
</tbody>
</table>

## <a name="miscellaneous-rules"></a>その他の規則

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ルール名</th>
<th align="left">データの種類</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CorruptedPageRendering</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージには、レンダリングを可能なページが含まれている場合は true。</p></td>
</tr>
</tbody>
</table>
