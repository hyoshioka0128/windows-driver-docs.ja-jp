---
title: XpsAnalyzer のルール
description: XpsAnalyzer のルール
ms.assetid: 4f617665-4cc4-475d-ae66-abc2f00309fd
keywords:
- XpsAnalyzer WDK、ルール
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e486d3a6ed9605bb24cc9e64e574760fc764769
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75208895"
---
# <a name="xpsanalyzer-rules"></a>XpsAnalyzer のルール

次の表では、XpsAnalysis ツールが XPS ファイルを分析するために使用する規則について説明します。 これらのルールは、XML Paper Specification (XPS) 1.0 仕様に基づいています。 この仕様の詳細については、「 [XML Paper specification](https://download.microsoft.com/download/1/6/a/16acc601-1b7a-42ad-8d4e-4f0aa156ec3e/XPS_1_0.exe)」をダウンロードしてください。

## <a name="open-packaging-conventions-opc-rules"></a>Open パッケージング規則 (OPC) の規則

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
<td align="left"><p>XPS パッケージが OPC 仕様に準拠していない場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ForeignContentType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 仕様の一部ではないコンテンツの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ForeignRelationshipType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS 1.0 仕様の一部ではないリレーションシップの種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LargePartCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>サイズが指定した量を超えているパーツの数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxFileSizeInBytes</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のパーツセットの最大サイズ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxPartRelationships</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージの一部に対するリレーションシップの最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PackageRelationshipCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のリレーションシップの合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PartCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>OPC ファイル内のパーツの合計数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>TotalPartRelationships</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>パーツリレーションシップの合計数。</p></td>
</tr>
</tbody>
</table>

## <a name="xps-trunk-rules"></a>XPS トランクルール

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
<td align="left"><p>XPS パッケージが XPS 1.0 仕様 (トランクレベル) に準拠していない場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedDocumentCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のドキュメントの合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCoreProperties</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>Xps パッケージに XPS Core プロパティ部分が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDiscardControl</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに DiscardControl の部分が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasDocumentPrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにドキュメントレベルの PrintTicket が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasDocumentStructure</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに DocumentStructure 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasJobPrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに DocumentSequence レベルの PrintTicket が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasMoreThanOneSignatureBlockResourceInADocument</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに複数の署名ブロックリソースを持つドキュメントが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PackageThumbnailType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージレベルのサムネイルのイメージの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureBlockRequestCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の署名の合計数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="xps-page-rules"></a>XPS ページルール

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
<td align="left"><p>XPS パッケージの既定以外の BleedBox のディメンション。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のブラシ要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の Canvas 要素の合計数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CanvasLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Canvas 要素の言語。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CanvasOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Canvas OpacityMask 要素のブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ContentBoxDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージの既定以外の ContentBox のディメンションです。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CorruptedXpsPage</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージが XPS 1.0 仕様 (ページレベル) に準拠していない場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FixedPageCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のページ要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FontType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージで見つかったフォントの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の Geometry 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureClosedFilledPatternRule</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigure の型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureMaxSegmentCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>GeometryFigures 内の SegmentCount 要素の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureMaxSegmentDataCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>GeometryFigures 内の SegmentDataCount 要素の最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFigureSegmentStrokePattern</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigures 要素のストロークパターン。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GeometryFigureSegmentType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>GeometryFigure 要素のセグメントの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GeometryFillRule</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ジオメトリの FillRule。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsBidiLevel</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>グリフの BidiLevel。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のグリフ要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsFillBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフの塗りつぶしのブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフの言語。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GlyphsOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフ OpacityMask のブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GlyphsStyleSimulations</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グリフの文字の数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルの ClipGeometry を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート ClipGeometry を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにハイパーリンクターゲットを持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Name プロパティを持つ Canvas 要素が含まれている場合は True です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 1 の Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度が0の Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル OpacityMaskBrush を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに remote OpacityMaskBrush を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに remote System.windows.media.matrixtransform> を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithAccessibilityLongDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに AccessibilityLongDescription を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasCanvasWithAccessibilityShortDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに AccessibilityShortDescription を持つ Canvas 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasCanvasWithUseAliasedEdgeMode</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Use松沢 Asededgemode = True を持つ Canvas 要素が含まれている場合は true です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasColorProfile</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに ColorProfile が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryFigureWithMultipleSegmentTypes</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに複数のセグメントの種類を持つ GeometryFigure 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryFigureWithNonDefaultStartPoint</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに、既定以外の StartPoint (0.0、0.0) を持つ GeometryFigure 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGeometryTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> の geometry が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGeometryTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート System.windows.media.matrixtransform> を持つジオメトリが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルの ClipGeometry を持つグリフが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート ClipGeometry を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsDeviceFontName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに DeviceFontName を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFillBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル FillBrush を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsFillBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート FillBrush を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsFontFaceIndex</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに FontFaceIndex を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsHyperlinkTarget</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにハイパーリンクターゲットを持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Name プロパティを持つ Glyphs 要素が含まれている場合は True です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度 = 1 のグリフ要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度が0のグリフ要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル OpacityMaskBrush を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに remote OpacityMaskBrush を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに remote System.windows.media.matrixtransform> を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasGlyphsUnicodeString</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに UnicodeString を持つ Glyphs 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasGlyphsWithSideways</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>IsSideways プロパティが有効になっている Glyphs 要素が XPS パッケージに含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Hasハイパーリンクのターゲット</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに、ハイパーリンクターゲットのページが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度 = 1 の ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度が0の ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> の ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート System.windows.media.matrixtransform> を含む ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Colorprofilimageを含む ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasImageBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の ViewBox (0、0、1、1) を持つ ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasImageBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外のビューポート (0、0、1、1) を持つ ImageBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 1 の System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 0 の System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> の System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート System.windows.media.matrixtransform> を含む System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに ColorProfileResource の System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultEndPoint</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージに、既定以外のエンドポイントを持つ System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の GradientStopOffset を持つ System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasLinearGradientBrushWithNonDefaultStartPoint</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージに既定以外の StartPoint を持つ System.windows.media.lineargradientbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasLocalDictionary</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル辞書を使用するページが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasNonDefaultBleedBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の BleedBox 値を持つページが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasNonDefaultContentBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の ContentBox 値を持つページが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPageName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Name 属性が設定されたページが含まれている場合は True です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPagePrintTicket</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにページレベルの PrintTicket が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathClipGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル ClipGeometry のパスが含まれている場合は True</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathClipGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモートの ClipGeometry 値を持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathFillBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル FillBrush のパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathFillBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに remote FillBrush を含むパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathGeometryLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルの Geometry プロパティを持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathGeometryRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモートジオメトリプロパティを持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Haspathハイパーリンクターゲット</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにハイパーリンクターゲット値を持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathName</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Name プロパティを持つパスが含まれている場合は True です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityEqualsOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度 = 1 のパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに不透明度が0のパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathOpacityMaskBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル OpacityMaskBrush 値を持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathOpacityMaskBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート OpacityMaskBrush を含むパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeBrushLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルの StrokeBrush プロパティを持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathStrokeBrushRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに remote StrokeBrush プロパティを含むパスが含まれている場合は True です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathStrokeDashOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに StrokeDashOffset のパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> のあるパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート System.windows.media.matrixtransform> のあるパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithAccessibilityLongDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに AccessibilityLongDescription 値を持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithAccessibilityShortDescription</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに AccessibilityShortDescription のパスが含まれている場合は True</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithNonDefaultStrokeMiterLimit</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の StrokeMiterLimit のパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasPathWithNonDefaultStrokeThickness</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の StrokeThickness のパスが含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasPathWithSnapsToPixel</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに SnapToPixels 値を持つパスが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 1 の RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 0 の RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> の RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート System.windows.media.matrixtransform> を含む RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに ColorProfileResource の RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultCenter</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外のセンターがある RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientOrigin</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の GradientOrigin を持つ RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultGradientStopOffset</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の GradientStopOffset を持つ RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasRadialGradientBrushWithNonDefaultRadiiSizes</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の放射型の RadialGradientBrush が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasRemoteDictionary</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>RemoteDictionary を使用するページが XPS パッケージに含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 1 の System.windows.media.solidcolorbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasSolidColorBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに Opacity = 0 の System.windows.media.solidcolorbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasSolidColorBrushWithColorProfileResource</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに ColorProfileResource の System.windows.media.solidcolorbrush> が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasStoryFragment</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに StoryFragment パーツが含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushOpacityEqualsToOne</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに、不透明度が1の VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushOpacityEqualsToZero</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに、不透明度が0の VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushTransformLocal</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカル System.windows.media.matrixtransform> を持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushTransformRemote</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモート System.windows.media.matrixtransform> を持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalCanvas</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルキャンバスを持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithLocalGlyphs</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルグリフを持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithLocalPath</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにローカルパスを持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithNonDefaultViewBox</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに既定以外の ViewBox (0、0、1、1) を持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithNonDefaultViewPort</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに、既定以外のビューポート (0、0、1、1) を持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemoteCanvas</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモートキャンバスを持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasVisualBrushWithRemoteGlyphs</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモートグリフを持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasVisualBrushWithRemotePath</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージにリモートパスを持つ VisualBrush 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の ImageBrush 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ImageBrushTileMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ImageBrush 要素の System.windows.media.tilemode> 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ImageBrushType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ImageBrush 要素のイメージの種類の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>System.windows.media.lineargradientbrush> 要素の ColorInterpolationMode 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>System.windows.media.lineargradientbrush> 要素の色の種類の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>System.windows.media.lineargradientbrush> 要素のコンテキストカラーチャネル数の値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinearGradientBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の System.windows.media.lineargradientbrush> 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LinearGradientBrushSpreadMethod</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>System.windows.media.lineargradientbrush> 要素の SpreadMethod 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LinkTargetsCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の LinkTargets 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>LocalDictionaryContent</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>このローカルディクショナリで見つかった共有可能オブジェクトの型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsFontRenderingEMSize</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Glyphs 要素の最大 FontRenderingEmSize。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsIndicesInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>グリフ要素内のインデックスの最大サイズ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGlyphsMappingsInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>グリフ要素内のマッピングの最大サイズ。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGlyphsProhibitedCaretStopCountInAGlyphs</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>グリフ要素の ProhibitedCaretStopCount の最大サイズ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxGradientStopsInALinearGradientBrush</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>System.windows.media.lineargradientbrush> 要素内の GradientStops の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxGradientStopsInARadialGradientBrush</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>RadialGradientBrush 要素内の GradientStops の最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxStrokeDashesInAPath</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>パス要素内の StrokeDashes の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageDimension</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>XPS パッケージ内のページの幅と高さ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PageLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ページの言語。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PageThumbnailType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>ページレベルのサムネイルの画像の種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のパス要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathFillBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パスの塗りつぶしのブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathLanguage</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス要素の言語の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathOpacityMaskBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス OpacityMask のブラシの種類。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeBrush</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パスストロークプロパティのブラシの種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeDashCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス要素の StrokeDashCap 型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeEndLineCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス要素の StrokeEndLineCap 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PathStrokeLineJoin</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス要素の StrokeLineJoin 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PathStrokeStartLineCap</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>パス要素の StrokeStartLineCap 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushColorInterpolationMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 要素の ColorInterpolationMode 値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 要素の色の種類の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 要素のコンテキストカラーチャネルカウント。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の RadialGradientBrush 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RadialGradientBrushEllipseOrCircle</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>グラデーションブラシが楕円または円であるかどうかを定義します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>RadialGradientBrushSpreadMethod</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>RadialGradientBrush 要素の SpreadMethod 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RemoteDictionaryContent</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>このリモートディクショナリで見つかった共有可能なオブジェクトの型。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushColorType</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>System.windows.media.solidcolorbrush> 要素の色の種類。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SolidColorBrushContextColorChannelCount</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>System.windows.media.solidcolorbrush> 要素のコンテキストカラーチャネルカウント。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SolidColorBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の System.windows.media.solidcolorbrush> 要素の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualBrushCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内の VisualBrush 要素の合計数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>VisualBrushTileMode</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>VisualBrush 要素の System.windows.media.tilemode> 値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>VisualCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のビジュアルの合計数。</p></td>
</tr>
</tbody>
</table>

## <a name="digital-signature-rules"></a>デジタル署名規則

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
<td align="left"><p>XPS パッケージに破損したデジタル署名が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureCount</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>XPS パッケージ内のデジタル署名の合計数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignaturePolicy</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Signature 要素の XPS 署名ポリシー値。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HasInvalidXpsSignature</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに無効な XPS 署名要素が含まれている場合は True。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XpsSignatureStatus</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>署名が無効な場合の signature 要素の署名状態値。 言い換えると、このルールは、HasInvalidXpsSignature が True の場合にのみ有効になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCertificatesInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Signature 要素で見つかった証明書の最大数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HasXpsSignatureWithEmptyID</p></td>
<td align="left"><p>bool</p></td>
<td align="left"><p>XPS パッケージに空の ID を持つ XPS Signature 要素が含まれている場合は True。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SignatureTimeFormat</p></td>
<td align="left"><p>string</p></td>
<td align="left"><p>Signature 要素の署名時刻形式の値。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MaxNumberOfCustomObjectsInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Signature 要素で見つかったカスタムオブジェクトの最大数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>MaxNumberOfCustomReferencesInASignature</p></td>
<td align="left"><p>long</p></td>
<td align="left"><p>Signature 要素で見つかったカスタム参照の最大数。</p></td>
</tr>
</tbody>
</table>

## <a name="miscellaneous-rules"></a>その他のルール

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
<td align="left"><p>XPS パッケージに描画以外のページが含まれている場合は True。</p></td>
</tr>
</tbody>
</table>
