---
title: 標準変数
description: 標準変数
ms.assetid: d3f85c0f-7387-4301-8b1e-904471aed4b0
keywords:
- GPD ファイル エントリ WDK Unidrv、標準的な変数
- 変数 WDK GPD ファイル
- 標準的な変数 WDK GPD ファイル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d19d4fd97a53252283a725f635876d166a8607
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375186"
---
# <a name="standard-variables"></a>標準変数





GPD 言語を使用して、コマンド文字列内で参照できる標準的な変数のセットを定義する、[コマンド文字列の形式](command-string-format.md)します。 Unidrv ドライバーは、これらの変数に値を割り当てます。 GPD ファイルのポイントのビューから、変数は読み取り専用です。

すべての標準的な変数は、DWORD の整数として格納されます。

次[プリンター コマンド](printer-commands.md)エントリをラスター データ ブロックの準備ができたら、HP LaserJet 4 P に送信されるコマンド文字列を指定します。

```cpp
*Command: CmdSendBlockData: "<1B>*b" %d{NumOfDataBytes} "W"
```

次の表には、すべてのアルファベット順で、標準的な変数が含まれます。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>標準的な変数名</th>
<th>値</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>BlueValue</strong></p></td>
<td><p>現在の色の青のコンポーネント。</p></td>
<td><p>CmdDefinePaletteEntry コマンド文字列で使用するため無効です。 (また<strong>GreenValue</strong>、 <strong>RedValue</strong>)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CurrentFontID</strong></p></td>
<td><p>現在の id 番号は、ソフト フォントをダウンロードします。</p></td>
<td><p>現在の印刷ジョブには、ダウンロードしたソフト フォントが含まれている場合は有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CurrentPaletteIndex</strong></p></td>
<td><p>カラー パレットに現在のインデックス。</p></td>
<td><p>CmdSelectPaletteEntry コマンド文字列で使用するため無効です。 (また<strong>GreenValue</strong>、 <strong>RedValue</strong>)。</p></td>
</tr>
<tr class="even">
<td><p><strong>CursorOriginX</strong></p></td>
<td><p>マスターの単位でのカーソルの原点の x 座標。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>CursorOriginY</strong></p></td>
<td><p>マスターの単位でのカーソルの原点の Y 座標。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestX</strong></p></td>
<td><p>カーソルの原点のマスター ユニット内のカーソルの変換先の x 座標。</p></td>
<td><p>CmdXMoveAbsolute コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestXRel</strong></p></td>
<td><p>マスター単位、現在のカーソルでのカーソルの変換先の X 座標を配置します。</p></td>
<td><p>CmdXMoveRelLeft と CmdXMoveRelRight コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>DestY</strong></p></td>
<td><p>カーソルの原点のマスター ユニット内のカーソルの変換先の Y 座標。</p></td>
<td><p>CmdYMoveAbsolute コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestYRel</strong></p></td>
<td><p>マスター単位、現在のカーソル位置でのカーソルの変換先の Y 座標します。</p></td>
<td><p>CmdYMoveRelUp と CmdYMoveRelDown コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontBold</strong></p></td>
<td><p>現在のフォントが太字の場合は、いずれかに設定、または 0 のそれ以外の場合。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontHeight</strong></p></td>
<td><p>マスター ユニットは、現在のフォントの高さ。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontItalic</strong></p></td>
<td><p>現在のフォントが斜体、またはそれ以外の場合 0 の場合は、いずれかに設定します。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>FontMaxWidth</strong></p></td>
<td><p>フォントのすべてのグリフの最大文字数のインクリメントに設定します。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontStrikeThru</strong></p></td>
<td><p>現在のフォントまたは 0 それ以外の場合の取り消しが有効な場合は、いずれかに設定します。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>引く</strong></p></td>
<td><p>現在のフォントが下線付きの場合は、1 または 0 に設定します。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="even">
<td><p><strong>FontWidth</strong></p></td>
<td><p>現在のフォントのマスターの単位の幅。</p></td>
<td><p>フォントが指定されている場合に有効にします。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GraphicsXRes</strong></p></td>
<td><p>DPI では、画像の水平方向の解像度現在します。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>GraphicsYRes</strong></p></td>
<td><p>DPI でのグラフィックスの現在の垂直解像度します。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GrayPercentage</strong></p></td>
<td><p>灰色の灰色の塗りつぶしに使用するレベル (割合)。</p></td>
<td><p>CmdRectGrayFill コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>GreenValue</strong></p></td>
<td><p>現在の色の緑のコンポーネント。</p></td>
<td><p>CmdDefinePaletteEntry コマンド文字列で使用するため無効です。 (また<strong>BlueValue</strong>、 <strong>RedValue</strong>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>LinefeedSpacing</strong></p></td>
<td><p>マスター単位、改行を表す、垂直方向の領域の量。</p></td>
<td><p>CmdSetLineSpacing コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NextFontID</strong></p></td>
<td><p>次の論理的なフォントをダウンロードするの識別番号。</p></td>
<td><p>CmdSetFontID コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NextGlyph</strong></p></td>
<td><p>[次へ] をダウンロードするグリフの 2 バイト コード。</p></td>
<td><p>CmdSetCharCode コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>NumOfCopies</strong></p></td>
<td><p>ユーザーによって要求されたコピーの数。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>NumOfDataBytes</strong></p></td>
<td><p>ラスター データの転送の準備のバイト数。</p></td>
<td><p>CmdSend 任意で使用できる有効な<em>XXX</em>データ コマンドの文字列。</p>
<p>データが圧縮されている場合、値は、圧縮後のバイト数です。</p></td>
</tr>
<tr class="even">
<td><p><strong>PageNumber</strong></p></td>
<td><p>現在印刷中のページの数。 注、これは必ずしも対応しません、アプリケーションのページの番号が何回ではなく<a href="https://msdn.microsoft.com/library/windows/hardware/ff556281" data-raw-source="[&lt;em&gt;DrvSendPage&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556281)"> <em>DrvSendPage</em> </a>が呼び出されました。</p>
<p>この値がによって初期化<a href="https://msdn.microsoft.com/library/windows/hardware/ff556296" data-raw-source="[&lt;strong&gt;DrvStartDoc&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556296)"> <strong>DrvStartDoc</strong> </a>によって増加されると<strong>DrvSendPage</strong>。</p>
<p>たとえば、n-up 場合 = 4 が選択されている<strong>PageNumber</strong>ドキュメントの 5 番目のページが印刷されている場合にのみは、2 に上がります。</p>
<p>(前) に、ドキュメントを逆の順序で印刷される場合、別の例として、 <strong>PageNumber</strong>標準変数は、1 ページとして印刷する最初のページを場合でも、これは、ドキュメントの最後のページに報告されます。</p>
<p>この動作が正しく自動二重化機能をサポートするために必要です。</p>
<p>OEM が使用する必要があります<strong>PageNumber</strong>または背面に現在のページが前面かどうかを確認するだけです。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PaletteIndexToProgram</strong></p></td>
<td><p>プログラムには、次のエントリのカラー パレット内のインデックスします。</p></td>
<td><p>CmdDefinePaletteEntry コマンド文字列で使用するため無効です。 (また<strong>RedValue</strong>、 <strong>GreenValue</strong>、 <strong>BlueValue</strong>、 <strong>CurrentPaletteIndex</strong>)。</p></td>
</tr>
<tr class="even">
<td><p><strong>PatternBrushID</strong></p></td>
<td><p>ダウンロードしたパターンのブラシの識別番号。</p></td>
<td><p>CmdDownloadPattern と CmdSelectPattern コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PatternBrushSize</strong></p></td>
<td><p>現在のブラシのパターンのバイト単位のサイズ。</p></td>
<td><p>CmdDownloadPattern コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>PatternBrushType</strong></p></td>
<td><p></p>
現在のブラシのパターンの種類。 値になります。2:網掛けパターン 3:クロス ハッチ パターン 4:ユーザー定義のパターン</td>
<td><p>CmdDownloadPattern と CmdSelectPattern コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PhysPaperLength</strong></p></td>
<td><p>縦モードの長さを y マスター単位には、現在使用されているホワイト ペーパー。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>PhysPaperWidth</strong></p></td>
<td><p>マスター単位、現在使用されているホワイト ペーパーで縦向きモードの幅。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>PrintDirInCCDegrees</strong></p></td>
<td><p>度数で測定、反時計回りに回転の量。</p></td>
<td><p>ドライバー CmdSetSimpleRotation または CmdSetAnyRotation のいずれかのコマンド文字列を送信するときに有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>RasterDataHeightInPixels</strong></p></td>
<td><p>現在のデータによって表されるイメージのピクセル単位の高さ。</p></td>
<td><p>CmdSend 任意で使用できる有効な<em>XXX</em>データ コマンド文字列、および CmdSetSrcBmpHeight にコマンド文字列。 圧縮では、この値は変更されません。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RasterDataWidthInBytes</strong></p></td>
<td><p>スキャン ラインに含まれるバイト数。</p></td>
<td><p>CmdSend 任意で使用できる有効な<em>XXX</em>データ コマンド文字列、および CmdSetSrcBmpWidth にコマンド文字列。 圧縮では、この値は変更されません。</p></td>
</tr>
<tr class="even">
<td><p><strong>RectXSize</strong></p></td>
<td><p>X マスター単位での四角形の幅。</p></td>
<td><p>CmdSetRectWidth コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="odd">
<td><p><strong>RectYSize</strong></p></td>
<td><p>Y マスター単位での四角形の長さ。</p></td>
<td><p>CmdSetRectHeight コマンド文字列で使用するため無効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>RedValue</strong></p></td>
<td><p>現在の色の赤のコンポーネント。</p></td>
<td><p>CmdDefinePaletteEntry コマンド文字列で使用するため無効です。 (また<strong>GreenValue</strong>、 <strong>BlueValue</strong>)。</p></td>
</tr>
<tr class="odd">
<td><p><strong>TextXRes</strong></p></td>
<td><p>DPI でのテキストの水平方向の解像度現在します。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
<tr class="even">
<td><p><strong>TextYRes</strong></p></td>
<td><p>DPI でのテキストの垂直方向の解像度現在します。</p></td>
<td><p>印刷ジョブが進行中のときに有効です。</p></td>
</tr>
</tbody>
</table>

 

 

 




