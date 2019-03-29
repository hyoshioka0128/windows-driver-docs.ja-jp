---
title: PCD ソース ファイル形式
description: PCD ソース ファイル形式
ms.assetid: 8651d6ca-7cd7-4c07-aa66-2766dd2222e0
keywords:
- プロッター ドライバー WDK の印刷、ミニドライバー
- MSPlot WDK の印刷、ミニドライバー
- ミニドライバー WDK MSPlot
- PCD ファイル WDK MSPlot
- .pcd ですファイル
- WDK MSPlot キーワード
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c0bd65790530946f0874ef3a197175b81aad2c7
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57463958"
---
# <a name="pcd-source-file-format"></a>PCD ソース ファイル形式





すべてプロッターのデバイスの特性は、次の形式を使用して指定します。

*keyword* { *value* }

場所*キーワード*は PCD ソースのいずれかのファイルのキーワードと*値*が引用符で囲まれた文字列または数値の値。 たとえば、次のステートメントでは、プロッターで色をサポートしているを指定します。

```cpp
ColorCap {1}
```

キーワードは、次の表で説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>Keyword</th>
<th>値の定義</th>
<th>既定値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BezierCap</strong></p></td>
<td><p>1 = デバイス サポート HPGL2 ベジエ曲線の拡張機能。</p>
<p>0 = サポートはありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ColorCap</strong></p></td>
<td><p>1 = デバイスの色</p>
<p>0 = モノクロ デバイス</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>COLORINFO</strong></p></td>
<td><p>30 の内容を表す値の DWORD のサイズ、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff539441" data-raw-source="[&lt;strong&gt;COLORINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539441)"> <strong>COLORINFO</strong> </a>構造体。</p></td>
<td><p></p>
{ {6810,3050,0}、//xr、年、年{2260,6550,0}、//xg yg、Yg {1810,500,0}、//xb、yb、Yb {2000,2450,0}、//クロスカントリー yc、Yc {5210,2100,0}、//xm ym、Ym {4750,5100,0}、//xy、yy、Yy {3324,3474,10000}、//-xw オプション、yw、Yw 10000,10000,10000、//RGB ガンマ 1422,952、//M/CY/C 787,495、/C/分/324,248 の Y/分//M/Y/Y, C}</td>
</tr>
<tr class="even">
<td><p><strong>DeviceMargin</strong></p></td>
<td><p>4 つの DWORD のサイズの値、左、上、右、1/1000 回 mm 単位で、下部にある紙の余白を表します。</p></td>
<td><p></p>
{5000, 5000, 5000, 36000}</td>
</tr>
<tr class="odd">
<td><p><strong>デバイス名</strong></p></td>
<td><p>表示可能なデバイス名 (31 最大文字。) を表す文字列を引用符で囲まれました。</p></td>
<td><p>「HPGL/2 プロッター」</p></td>
</tr>
<tr class="even">
<td><p><strong>DevicePelsDPI</strong></p></td>
<td><p>1 つの DWORD のサイズを表す値、デバイスの有効な DPI。 詳細については、次を参照してください。、 <strong>upDevicePelsDPI</strong>のメンバー <a href="https://msdn.microsoft.com/library/windows/hardware/ff566484" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566484)"> <strong>GDIINFO</strong></a>します。</p></td>
<td><p>既定値は 0、値を計算する GDI の原因です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DeviceSize</strong></p></td>
<td><p>2 つの DWORD のサイズ値が最大の用紙を表すサイズで<em>x</em>と<em>y</em> 1/1000 回 mm 単位の座標。</p>
<p>A <em>y</em> 25400 (1 インチ) の値未満では、デバイスは、変数の用紙の長さを受け取ることを示します。</p></td>
<td><p></p>
{215900, 279400}</td>
</tr>
<tr class="even">
<td><p><strong>FormInfo</strong></p></td>
<td><p>プロッターでサポートされている各フォームのフォームの説明です。 詳細については、次を参照してください。、<strong>フォーム説明</strong>次の表に続くセクション。</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p><strong>HTPatternSize</strong></p></td>
<td><p>標準のハーフトーン パターンを識別する HT_PATSIZE_ プレフィックス付き定数のいずれか。</p></td>
<td><p>0 xffffffff</p></td>
</tr>
<tr class="even">
<td><p><strong>InitString</strong></p></td>
<td><p>ドライバーからプリンターに送信されたコマンドを表す C 言語文字列を引用符で囲まれた<a href="https://msdn.microsoft.com/library/windows/hardware/ff556298" data-raw-source="[&lt;strong&gt;DrvStartPage&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556298)"> <strong>DrvStartPage</strong> </a>関数。</p></td>
<td><p>NULL 文字列です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxCopies</strong></p></td>
<td><p>デバイスをレンダリングするページごとのコピーの最大数。</p></td>
<td><p>1</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxPens</strong></p></td>
<td><p>ペン (32 max) の数</p></td>
<td><p>8</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxPolygonPts</strong></p></td>
<td><p>多角形に線を付けるか、入力を定義するポイントの最大数。</p></td>
<td><p>128</p></td>
</tr>
<tr class="even">
<td><p><strong>MaxQuality</strong></p></td>
<td><p>品質レベル (4 max) の数</p></td>
<td><p>4</p></td>
</tr>
<tr class="odd">
<td><p><strong>MaxScale</strong></p></td>
<td><p>スケールの最大サイズ。 0 ~ 10000 です (100 では 100%)</p></td>
<td><p>100</p></td>
</tr>
<tr class="even">
<td><p><strong>NoBitmapFont</strong></p></td>
<td><p>1 = デバイスがビットマップ フォントをサポートしていません。</p>
<p>0 = ビットマップ フォントがサポートされています。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaperTrayCap</strong></p></td>
<td><p>1 = デバイスが用紙トレイのソース。</p>
<p>0 = サポートはありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>PaperTraySize</strong></p></td>
<td><p>2 つの DWORD のサイズの値、用紙トレイの幅と高さを 1/1000 回 mm 単位を表します。</p></td>
<td><p></p>
{-1, -1}</td>
</tr>
<tr class="odd">
<td><p><strong>PlotDPI</strong></p></td>
<td><p>2 つの DWORD のサイズ値が表すペン プロッターの<em>x</em>と<em>y</em>インチあたりのドットでの解決。</p></td>
<td><p></p>
{1016, 1016}</td>
</tr>
<tr class="even">
<td><p><strong>PlotPenData</strong></p></td>
<td><p>各ペンのペン説明します。 詳細については、次を参照してください。、<strong>ペン説明</strong>次の表に続くセクション。</p></td>
<td><p>なし。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PushPopPal</strong></p></td>
<td><p>1 = ドライバーする必要がありますプッシュ/ポップ パレット右から左へと HPGL2 切り替える場合。</p>
<p>0 = プッシュ/ポップは必要ありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterByteAlign</strong></p></td>
<td><p>1 = デバイスのすべてのラスター データを受け取る必要がありますバイト揃えの x 座標。</p>
<p>0 = バイト アラインメントは必要ありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RasterCap</strong></p></td>
<td><p>1 = ラスター デバイス</p>
<p>0 = ペン デバイス</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterDPI</strong></p></td>
<td><p>DWORD のサイズの 2 つの値を表す<em>x</em>と<em>y</em>解像度、ドット/インチにします。</p>
<p>ラスターのプロッター ラスター解像度になります。</p>
<p>ペン プロッターの場合は、これは、GDI がアプリケーションに提供する理想的な解決策です。</p></td>
<td><p></p>
{300, 300}</td>
</tr>
<tr class="odd">
<td><p><strong>RollFeedCap</strong></p></td>
<td><p>1 = デバイスがロールの給紙方法。</p>
<p>0 = サポートはありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>ROPLevel</strong></p></td>
<td><p>ROP_LEVEL_0 = いいえ RasterOp サポートします。</p>
<p>ROP_LEVEL_1 Rop1 サポートを = です。</p>
<p>ROP_LEVEL_2 Rop2 サポートを = です。</p>
<p>ROP_LEVEL_3 Rop3 サポートを = です。</p></td>
<td><p>ROP_LEVEL_0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoEncode5</strong></p></td>
<td><p>1 = HP ラスター転送言語 (RTL) 5 モノクロの圧縮モードがサポートされています。</p>
<p>0 = サポートはありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLMonoFixPal</strong></p></td>
<td><p>RTL モノクロ パレットの場合のみです。</p>
<p>0 = White が、1 = 黒</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>RTLMonoNoCID</strong></p></td>
<td><p>1 = RTL Mono のモードでは、CID のコマンドは必要ありません。</p>
<p>0 = RTL Mono のモードでは、CID コマンドが必要です。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>RTLNoDPIxy</strong></p></td>
<td><p>1 = RTL DPI X、Y の移動のコマンドはサポートされていません。</p>
<p>0 = これらのコマンドがサポートされています。</p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><strong>TransparentCap</strong></p></td>
<td><p>1 = デバイスの透過的なモードをサポートしています。</p>
<p>0 = サポートはありません。</p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><strong>WindingFillCap</strong></p></td>
<td><p>1 = の塗りつぶしにワインディング デバイスをサポートします。</p>
<p>0 = サポートはありません。</p></td>
<td><p>0</p></td>
</tr>
</tbody>
</table>

 

### <a href="" id="ddk-pen-descriptions-gg"></a>ペンの説明

それぞれのペンの説明には、次の形式が必要です。

**PlotPenData {**<em>数のペン</em>**、** <em>色</em>**}**

場所*ペン番号*ペンのスロットの数を指定および*色*pc\_IDX\_-色の識別子のプレフィックスします。 以下に例のペンの説明。

```cpp
PlotPenData {1, PC_IDX_WHITE}
PlotPenData {2, PC_IDX_BLACK}
PlotPenData {3, PC_IDX_RED}
```

### <a href="" id="ddk-form-descriptions-gg"></a>フォームの説明

各フォームの説明には、次の形式が必要です。

**FormInfo {"**<em>説明を形成</em>**"、** <em>幅</em>**、** <em>長さ</em>**、** <em>左余白</em>**、** <em>上余白</em>**、** <em>右余白</em> **、** <em>下余白</em>**}**

場所*フォーム説明*、フォームを説明する文字列は、*幅*と*長さ*1/1000 回 mm 単位で、フォームのサイズを指定し、1/1000 回 mm の余白が指定されても単位です。 次は、3 つの例に示します。

```cpp
FormInfo {"Roll Paper 24 in",    609600,      0, 0, 0, 0, 0}
FormInfo {"ANSI A 8.5 x 11 in",  215900, 279400, 0, 0, 0, 0}
FormInfo {"ISO A4 210 x 297 mm", 210000, 297000, 0, 0, 0, 0}
```

 

 




